<script lang="ts">
    import { onMount, onDestroy } from "svelte";
    import { browser } from "$app/environment";

    type AdItem = {
        id: string | number;
        title?: string;
        description?: string;
        mediaUrl?: string;
        linkUrl?: string;
    };

    let ads: AdItem[] = [];
    let currentIndex = 0;
    let interval: number | undefined;
    let currentAd: AdItem | null = null;

    const API = import.meta.env.VITE_BACKEND_URL || "";

    function guessMediaType(url?: string) {
        if (!url) return "image";
        const ext = url.split(".").pop()?.toLowerCase();
        return ["mp4", "webm", "ogg"].includes(ext || "") ? "video" : "image";
    }

    function nextAd() {
        if (ads.length > 1) {
            currentIndex = (currentIndex + 1) % ads.length;
        }
    }

    function apiPost(path: string, body?: unknown) {
        if (!API) return;

        fetch(`${API}${path}`, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: body ? JSON.stringify(body) : undefined,
        }).catch(() => {
            // ignore network errors silently
        });
    }

    function trackImpression(id: string | number) {
        apiPost(`/ads/${id}/impression`);
    }

    function getDeviceInfo() {
        const ua = navigator.userAgent;
        let os = "Desktop";
        let deviceType: "desktop" | "mobile" | "tablet" = "desktop";

        if (/android/i.test(ua)) {
            os = "Android";
            deviceType = /tablet|iPad/i.test(ua) ? "tablet" : "mobile";
        } else if (/iPad|iPhone|iPod/i.test(ua)) {
            os = "iOS";
            deviceType = /iPad/i.test(ua) ? "tablet" : "mobile";
        } else if (/Windows NT/i.test(ua)) {
            os = "Windows";
        } else if (/Mac OS X/i.test(ua)) {
            os = "macOS";
        } else if (/Linux/i.test(ua)) {
            os = "Linux";
        }

        return { os, deviceType };
    }

    function trackClick(id: string | number) {
        const { os, deviceType } = getDeviceInfo();
        apiPost(`/ads/${id}/click`, { os, deviceType });
    }

    $: currentAd = ads[currentIndex] ?? null;

    onMount(async () => {
        if (!browser) return;

        try {
            const res = await fetch(`${API}/ads/public?placement=landing-page`);
            if (res.ok) {
                ads = await res.json();
                ads.forEach((ad) => trackImpression(ad.id));
            }
        } catch (e) {
            console.warn("AdBanner: failed to load ads", e);
        }

        if (ads.length > 1) {
            interval = window.setInterval(nextAd, 6000);
        }
    });

    onDestroy(() => {
        if (interval) {
            window.clearInterval(interval);
        }
    });
</script>

{#if currentAd}
    <div class="ad-banner-fixed">
        <div class="ad-banner-inner">
            <div class="ad-tag">Anúncio</div>
            <div class="ad-banner-content" on:click={nextAd}>
                <div class="ad-item">
                    {#if currentAd.mediaUrl}
                        <div class="ad-thumb">
                            {#if guessMediaType(currentAd.mediaUrl) === "image"}
                                <img src={currentAd.mediaUrl} alt={currentAd.title ?? "Anúncio"} crossorigin="anonymous" />
                            {:else}
                                <video
                                    src={currentAd.mediaUrl}
                                    muted
                                    loop
                                    autoplay
                                    playsinline
                                    crossorigin="anonymous"
                                />
                            {/if}
                        </div>
                    {/if}

                    <div class="ad-text">
                        <div class="ad-title">{currentAd.title || "Anúncio"}</div>
                        <div class="ad-desc">{currentAd.description}</div>
                    </div>

                    {#if currentAd.linkUrl}
                        <a
                            class="ad-cta"
                            href={currentAd.linkUrl}
                            target="_blank"
                            rel="noopener noreferrer"
                            on:click|stopPropagation={() => trackClick(currentAd.id)}
                        >
                            Saiba mais
                        </a>
                    {/if}
                </div>
            </div>

            {#if ads.length > 1}
                <div class="ad-dots">
                    {#each ads as _, i}
                        <span class:active={i === currentIndex}></span>
                    {/each}
                </div>
            {/if}
        </div>
    </div>
{/if}

<style>
    .ad-banner-fixed {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 9999;
        min-height: 72px;
        padding: 8px 16px;
        background: rgba(20, 20, 30, 0.92);
        backdrop-filter: blur(12px);
        border-top: 1px solid rgba(255, 255, 255, 0.08);
        display: flex;
        justify-content: center;
        pointer-events: auto;
    }

    .ad-banner-inner {
        max-width: 900px;
        width: 100%;
        display: flex;
        align-items: center;
        gap: 12px;
        position: relative;
    }

    .ad-tag {
        flex-shrink: 0;
        padding: 6px 10px;
        font-size: 12px;
        font-weight: 700;
        color: #fff;
        background: rgba(255, 255, 255, 0.08);
        border-radius: 999px;
        text-transform: uppercase;
        letter-spacing: 0.08em;
    }

    .ad-banner-content {
        flex: 1;
        cursor: pointer;
        min-width: 0;
    }

    .ad-item {
        display: flex;
        align-items: center;
        gap: 12px;
    }

    .ad-thumb {
        width: 56px;
        height: 56px;
        flex-shrink: 0;
        border-radius: 12px;
        overflow: hidden;
        background: #10101a;
    }

    .ad-thumb img,
    .ad-thumb video {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: block;
    }

    .ad-text {
        flex: 1;
        min-width: 0;
    }

    .ad-title {
        font-size: 13px;
        font-weight: 700;
        color: #fff;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .ad-desc {
        font-size: 11px;
        color: #94a3b8;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .ad-cta {
        flex-shrink: 0;
        padding: 6px 14px;
        font-size: 12px;
        font-weight: 600;
        color: #fff;
        background: linear-gradient(135deg, #00e676, #00bcd4);
        border-radius: 6px;
        text-decoration: none;
        white-space: nowrap;
    }

    .ad-dots {
        display: flex;
        gap: 4px;
        position: absolute;
        bottom: -4px;
        left: 50%;
        transform: translateX(-50%);
    }

    .ad-dots span {
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background: rgba(255, 255, 255, 0.2);
        transition: background 0.3s;
    }

    .ad-dots span.active {
        background: #00e676;
    }
</style>

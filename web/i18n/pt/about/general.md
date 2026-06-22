<script lang="ts">
    import { t } from "$lib/i18n/translations";
    import { contacts, docs } from "$lib/env";

    import SectionHeading from "$components/misc/SectionHeading.svelte";
</script>

<section id="summary">
<SectionHeading
    title={$t("about.heading.summary")}
    sectionId="summary"
/>

cobalt ajuda você a salvar qualquer coisa dos seus sites favoritos: vídeo, áudio, fotos ou gifs. basta colar o link e você está pronto para baixar!

sem anúncios, rastreamento, paywalls ou outras bobagens. apenas um app web prático que funciona em qualquer lugar, quando você precisar.
</section>

<section id="motivation">
<SectionHeading
    title={$t("about.heading.motivation")}
    sectionId="motivation"
/>

cobalt foi criado para benefício público, para proteger as pessoas de anúncios e malware empurrados por outros downloaders.
acreditamos que o melhor software é seguro, aberto e acessível. todos os projetos imput seguem esses princípios básicos.
</section>

<section id="privacy-efficiency">
<SectionHeading
    title={$t("about.heading.privacy_efficiency")}
    sectionId="privacy-efficiency"
/>

todas as requisições ao backend são anônimas e todas as informações sobre possíveis túneis de arquivo são criptografadas.
temos uma política estrita de zero logs e não armazenamos nem rastreamos *nada* sobre pessoas individuais.

se uma requisição exigir processamento adicional, como remux ou transcodificação, o cobalt processa a mídia diretamente no seu dispositivo. isso garante melhor eficiência e privacidade.

se o seu dispositivo não suportar processamento local, o processamento ao vivo baseado no servidor é usado em vez disso.
nesse cenário, a mídia processada é transmitida diretamente para o cliente, sem nunca ser armazenada no disco do servidor.

você pode [ativar o tunelamento forçado](/settings/privacy#tunnel) para aumentar ainda mais a privacidade.
quando ativado, o cobalt tunelará todos os arquivos baixados, não apenas aqueles que exigem isso.
inguém saberá de onde você baixa algo, nem mesmo seu provedor de internet.	udo o que verão é que você está usando uma instância cobalt.
</section>

<section id="community">
<SectionHeading
    title={$t("about.heading.community")}
    sectionId="community"
/>

cobalt é usado por inúmeros artistas, educadores e criadores de conteúdo para fazer o que amam.
estamos sempre em contato com nossa comunidade e trabalhamos juntos para tornar o cobalt ainda mais útil.
sinta-se à vontade para [participar da conversa](/about/community)!

acreditamos que o futuro da internet é aberto, por isso o cobalt é
[source first](https://sourcefirst.com/) e [fácil de auto-hospedar]({docs.instanceHosting}).

se seu amigo hospeda uma instância de processamento, basta pedir o domínio e [adicioná-lo nas configurações de instância](/settings/instances#community).

você pode ver o código fonte e contribuir [no github]({contacts.github}) a qualquer momento.
nós recebemos bem todas as contribuições e sugestões!
</section>

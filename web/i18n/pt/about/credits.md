<script lang="ts">
    import { contacts, docs, partners } from "$lib/env";
    import { t } from "$lib/i18n/translations";

    import SectionHeading from "$components/misc/SectionHeading.svelte";
    import BetaTesters from "$components/misc/BetaTesters.svelte";
</script>

<section id="imput">
<SectionHeading
    title="imput"
    sectionId="imput"
/>

cobalt é feito com amor e cuidado por [imput](https://imput.net/) ❤️

somos uma equipe pequena de duas pessoas, mas trabalhamos muito para fazer um ótimo software que beneficie a todos.
se você gosta do nosso trabalho, considere apoiar na [página de doações](/donate)!
</section>

<section id="testers">
<SectionHeading
    title={$t("about.heading.testers")}
    sectionId="testers"
/>

um grande obrigado aos nossos testadores por testarem atualizações cedo e ajudarem a garantir que estão estáveis.
eles também ajudaram a lançar o cobalt 10!
<BetaTesters />

todos os links são externos e levam aos sites pessoais ou redes sociais deles.
</section>

<section id="partners">
<SectionHeading
    title={$t("about.heading.partners")}
    sectionId="partners"
/>

uma parte da infraestrutura de processamento do cobalt
é fornecida pelo nosso parceiro de longa data, [royalehosting.net]({partners.royalehosting})!
</section>

<section id="meowbalt">
<SectionHeading
    title={$t("general.meowbalt")}
    sectionId="meowbalt"
/>

meowbalt é o mascote veloz do cobalt, um gato muito expressivo que adora internet rápida.

toda arte incrível do meowbalt que você vê no cobalt
foi feita por [GlitchyPSI](https://glitchypsi.xyz/).
ele também é o criador original do personagem.

o imput detém os direitos legais sobre o design do personagem meowbalt,
mas não sobre as obras específicas criadas pelo GlitchyPSI.

amamos o meowbalt, então precisamos definir algumas regras para protegê-lo:
- você não pode usar o design do meowbalt em qualquer forma que não seja fan art.
- você não pode usar o design ou as obras do meowbalt comercialmente.
- você não pode usar o design ou as obras do meowbalt nos seus próprios projetos.
- você não pode usar ou modificar as obras do GlitchyPSI do meowbalt em qualquer forma.

se você criar fan art do meowbalt, compartilhe em
[nosso servidor do discord](/about/community), vamos adorar ver!
</section>

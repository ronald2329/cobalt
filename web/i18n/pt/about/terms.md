<script lang="ts">
    import { t } from "$lib/i18n/translations";
    import SectionHeading from "$components/misc/SectionHeading.svelte";
</script>

<section id="general">
<SectionHeading
    title={$t("about.heading.general")}
    sectionId="general"
/>

estes termos são aplicáveis apenas ao uso da instância oficial do cobalt.
em outros casos, pode ser necessário contatar o responsável pela instância para obter informações precisas.
</section>

<section id="saving">
<SectionHeading
    title={$t("about.heading.saving")}
    sectionId="saving"
/>

a funcionalidade de salvamento simplifica o download de conteúdo da internet
e não assumimos qualquer responsabilidade pelo uso do conteúdo salvo.

os servidores de processamento operam como proxies avançados e nunca gravam conteúdo solicitado em disco.
tudo é tratado na RAM e apagado permanentemente assim que o túnel é concluído.
não temos registros de downloads e não podemos identificar ninguém.

você pode saber mais sobre como os túneis funcionam em [política de privacidade](/about/privacy).
</section>

<section id="responsibility">
<SectionHeading
    title={$t("about.heading.responsibility")}
    sectionId="responsibility"
/>

você (usuário final) é responsável pelo que faz com nossas ferramentas, como usa e distribui o conteúdo resultante.
por favor, seja cuidadoso ao usar conteúdo de terceiros e sempre credite os criadores originais.
certifique-se de não violar quaisquer termos ou licenças.

quando usado para fins educacionais, sempre cite as fontes e credite os criadores originais.

o uso justo e os créditos beneficiam a todos.
</section>

<section id="abuse">
<SectionHeading
    title={$t("about.heading.abuse")}
    sectionId="abuse"
/>

não temos como detectar automaticamente comportamentos abusivos porque o cobalt é totalmente anônimo.
contudo, você pode reportar essas atividades para nós por e-mail e faremos o possível para atender manualmente: abuse[at]imput.net

**este e-mail não se destina ao suporte de usuários; você não receberá resposta se sua preocupação não estiver relacionada a abuso.**

se você estiver enfrentando problemas, pode buscar suporte por qualquer método preferido na [página da comunidade](/about/community).
</section>

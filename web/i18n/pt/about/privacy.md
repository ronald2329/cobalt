<script lang="ts">
    import env from "$lib/env";
    import { t } from "$lib/i18n/translations";

    import SectionHeading from "$components/misc/SectionHeading.svelte";
</script>

<section id="general">
<SectionHeading
    title={$t("about.heading.general")}
    sectionId="general"
/>

a política de privacidade do cobalt é simples: não coletamos nem armazenamos nada sobre você.
o que você faz é negócio seu, não nosso ou de qualquer outra pessoa.

estes termos são aplicáveis apenas ao uso da instância oficial do cobalt.
em outros casos, pode ser necessário contatar o responsável pela instância para obter informações precisas.
</section>

<section id="local">
<SectionHeading
    title={$t("about.heading.local")}
    sectionId="local"
/>

ferramentas que usam processamento no dispositivo funcionam offline, localmente,
e nunca enviam dados processados para lugar nenhum.
elas são explicitamente marcadas assim sempre que aplicável.
</section>

<section id="saving">
<SectionHeading
    title={$t("about.heading.saving")}
    sectionId="saving"
/>

ao usar a funcionalidade de salvamento, o cobalt pode precisar fazer proxy ou remux/transcodificar arquivos.
se for esse o caso, um túnel temporário é criado para esse propósito
e informações mínimas sobre a mídia são armazenadas por 90 segundos.

em uma instância oficial e não modificada do cobalt,
**todas as informações de túnel são criptografadas com uma chave que somente o usuário final tem acesso**.

dados de túnel criptografados podem incluir:
- nome do serviço de origem.
- URLs originais da mídia.
- argumentos internos necessários para diferenciar os tipos de processamento.
- metadados mínimos do arquivo (nome gerado, título, autor, ano de criação, direitos autorais).
- informações mínimas sobre a solicitação original que podem ser usadas em caso de falha do URL durante o tunelamento.

esses dados são apagados da RAM do servidor em 90 segundos.
inguém tem acesso ao cache de dados de túnel, mesmo os donos da instância,
contanto que o código fonte do cobalt não seja modificado.

dados de mídia de túneis nunca são armazenados/cachêados em lugar nenhum.
tudo é processado ao vivo, mesmo durante remux e transcodificação.
os túneis do cobalt funcionam como um proxy anônimo.

se seu dispositivo suporta processamento local,
então as informações de túnel criptografadas incluem muito menos dados, porque retornam ao cliente em vez de ao servidor.

veja o [código relacionado no github](https://github.com/imputnet/cobalt/tree/main/api/src/stream) para saber mais sobre como funciona.
</section>

<section id="encryption">
<SectionHeading
    title={$t("about.heading.encryption")}
    sectionId="encryption"
/>

dados de túnel temporariamente armazenados são criptografados usando o padrão AES-256.
as chaves de descriptografia são incluídas apenas no link de acesso e nunca são registradas/cachêadas/armazenadas em lugar nenhum.
somente o usuário final tem acesso ao link e às chaves de criptografia.
as chaves são geradas de forma única para cada túnel solicitado.
</section>

{#if env.PLAUSIBLE_ENABLED}
<section id="plausible">
<SectionHeading
    title={$t("about.heading.plausible")}
    sectionId="plausible"
/>

usamos [plausible](https://plausible.io/) para obter uma estimativa aproximada
do número de usuários ativos do cobalt, totalmente anonimamente. nenhuma informação identificável sobre
você ou suas requisições é armazenada. todos os dados são anonimizados e agregados.

nós auto-hospedamos e gerenciamos a [instância plausible](https://{env.PLAUSIBLE_HOST}/) que o cobalt usa.

o plausible não usa cookies e é totalmente compatível com GDPR, CCPA e PECR.

se você quiser sair da análise anônima, pode fazer isso em [configurações de privacidade](/settings/privacy#analytics).
se você sair, o script plausible não será carregado.

[saiba mais sobre a dedicação do plausible à privacidade](https://plausible.io/privacy-focused-web-analytics).
</section>
{/if}

<section id="cloudflare">
<SectionHeading
    title={$t("about.heading.cloudflare")}
    sectionId="cloudflare"
/>

usamos serviços da cloudflare para:
- proteção contra ddos e abuso.
- proteção contra bots (cloudflare turnstile).
- hospedagem e deploy do app web renderizado estaticamente (cloudflare workers).

todos esses serviços são necessários para fornecer a melhor experiência para todos.

a cloudflare é a provedora mais privada e confiável para todas as soluções mencionadas que conhecemos.

a cloudflare é totalmente compatível com GDPR e HIPAA.

[saiba mais sobre a dedicação da cloudflare à privacidade](https://www.cloudflare.com/trust-hub/privacy-and-data-protection/).
</section>

# Documentacao em portugues do Brasil

Esta pasta concentra a documentacao em portugues do Brasil do OpenClaw neste
fork. Ela foi mantida com a mesma estrutura relativa da documentacao original em
ingles para facilitar comparacoes, atualizacoes futuras e revisoes com o
upstream.

## Comece por aqui

- [Guia de uso rapido](./guia-de-uso.md): resumo pratico para instalar,
  configurar e testar o OpenClaw.
- [Pagina inicial da documentacao](./index.md): visao geral oficial traduzida.
- [Primeiros passos](./start/getting-started.md): instalacao e configuracao
  inicial.
- [Onboarding](./start/wizard.md): fluxo guiado com `openclaw onboard`.
- [Configuracao do Gateway](./gateway/configuration.md): arquivo
  `~/.openclaw/openclaw.json`, tokens e opcoes principais.
- [Seguranca](./gateway/security/index.md): permissoes, tokens e boas praticas.
- [Solução de problemas](./help/troubleshooting.md): erros comuns e diagnostico.

## Organizacao

| Pasta | Conteudo |
| --- | --- |
| `automation/` | Cron, webhooks, taskflow, clawflow e automacoes. |
| `channels/` | Telegram, WhatsApp, Discord, Slack, Signal e outros canais. |
| `cli/` | Comandos da CLI `openclaw`. |
| `concepts/` | Arquitetura, memoria, agentes, contexto e recursos centrais. |
| `gateway/` | Gateway, configuracao, seguranca, acesso remoto e operacao. |
| `install/` | Instalacao local, Docker, Fly, GCP, VPS e migracoes. |
| `nodes/` | Nodes e pareamento de dispositivos. |
| `platforms/` | Plataformas como macOS, iOS, Android e Web. |
| `plugins/` | Manifestos, SDK, arquitetura e publicacao de plugins. |
| `providers/` | Provedores de modelos, busca, midia, voz e transcricao. |
| `reference/` | Referencias tecnicas e materiais de apoio. |
| `start/` | Entrada para novos usuarios. |
| `tools/` | Ferramentas disponiveis para agentes. |
| `web/` | UI de controle e superficies Web. |

Os arquivos Markdown que ficam diretamente na raiz desta pasta seguem a
organizacao da documentacao original do projeto. Eles nao foram movidos para nao
quebrar links nem dificultar sincronizacoes futuras.

## Politica para este fork

- Mantenha documentos traduzidos dentro de `docs/pt-BR/`.
- Preserve o caminho relativo do documento original sempre que possivel.
- Crie guias proprios com nomes em minusculo e `kebab-case`, como
  `guia-de-uso.md`.
- Evite misturar commits de documentacao com commits de codigo.
- Ao atualizar traducoes, prefira commits pequenos por area: `channels`,
  `providers`, `gateway`, `tools`, e assim por diante.

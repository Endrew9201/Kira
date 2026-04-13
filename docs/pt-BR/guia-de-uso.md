---
title: Guia de uso do OpenClaw em portugues do Brasil
summary: Caminho rapido para instalar, configurar e testar o OpenClaw usando a documentacao traduzida neste fork.
---

# Guia de uso do OpenClaw em português do Brasil

Este guia resume a varredura local do projeto e aponta o caminho mais curto para
começar a usar o OpenClaw sem precisar caçar respostas em centenas de arquivos.

## Estado deste checkout

- O projeto baixado aqui é uma árvore de código-fonte do OpenClaw.
- A versão declarada em `package.json` é `2026.4.10`.
- O runtime local está adequado: Node `v24.14.0`.
- O `pnpm` ainda não está instalado/ativado neste ambiente.
- `node openclaw.mjs --help` falha por falta de `dist/entry.(m)js`, ou seja: este
  checkout precisa ser construído antes de executar a CLI diretamente.
- Foram encontrados 99 manifests de plugins em `extensions/**/openclaw.plugin.json`
  e 53 skills em `skills/**/SKILL.md`.
- A documentação oficial em PT-BR foi importada para `docs/pt-BR/` com 421 páginas
  traduzidas.

## O que é o OpenClaw

O OpenClaw é um assistente pessoal de IA auto-hospedado. A ideia central é rodar
um Gateway no seu computador ou servidor e conectar esse Gateway a canais de
mensagem, modelos de IA, ferramentas locais, automações e dispositivos pareados.

Em vez de ser só um chatbot, ele pode:

- conversar pela Web UI ou por apps como Telegram, WhatsApp, Discord, Slack,
  Signal, Google Chat, Matrix, Mattermost, Microsoft Teams, Nostr, Twitch, Zalo e
  outros;
- usar modelos de provedores como OpenAI, Anthropic, Google, OpenRouter, Ollama,
  vLLM, SGLang, Groq, Mistral, DeepSeek, Qwen, NVIDIA e muitos mais;
- executar ferramentas de agente, como leitura/escrita de arquivos, comandos de
  shell, navegador controlado, busca web, geração/análise de mídia, cron, webhooks
  e gerenciamento de sessões;
- trabalhar com múltiplos agentes, workspaces isolados e roteamento por canal,
  remetente ou grupo;
- usar apps/nodes em macOS, iOS e Android para voz, Canvas, câmera, gravação de
  tela, notificações, localização e comandos de dispositivo;
- instalar plugins e skills para adicionar canais, providers, workflows e
  instruções especializadas.

## Caminho recomendado para usar agora

Se você quer usar o OpenClaw sem mexer no código-fonte, instale o pacote pronto:

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
openclaw dashboard
```

O onboarding é o caminho principal. Ele configura provedor/modelo, Gateway,
workspace, canais, daemon e skills recomendadas.

Depois rode:

```bash
openclaw health
openclaw gateway status
openclaw doctor
```

Se a UI abrir com `openclaw dashboard`, você já pode conversar com o agente pelo
navegador, mesmo antes de conectar WhatsApp/Telegram/etc.

## Caminho a partir deste código-fonte

Este checkout não está construído. Para rodar localmente:

```bash
corepack enable
corepack prepare pnpm@10.32.1 --activate
pnpm install
pnpm ui:build
pnpm build
node openclaw.mjs onboard --install-daemon
node openclaw.mjs dashboard
```

Para desenvolvimento com recarregamento automático:

```bash
pnpm gateway:watch
```

Se você só quer usar o produto, prefira a instalação global por `npm install -g`.
Se você quer alterar ou estudar o código, use o fluxo com `pnpm`.

## Primeiro canal: escolha simples

O jeito mais rápido de testar chat externo costuma ser Telegram:

1. Crie um bot no Telegram falando com `@BotFather`.
2. Salve o token.
3. Configure `channels.telegram.botToken` ou use `TELEGRAM_BOT_TOKEN`.
4. Inicie o Gateway.
5. Aprove a primeira DM, se a política estiver em pareamento.

Exemplo em `~/.openclaw/openclaw.json`:

```json5
{
  channels: {
    telegram: {
      enabled: true,
      botToken: "123:abc",
      dmPolicy: "pairing",
      groups: { "*": { requireMention: true } },
    },
  },
}
```

Comandos úteis:

```bash
openclaw gateway
openclaw pairing list telegram
openclaw pairing approve telegram <CODE>
```

Para WhatsApp:

```bash
openclaw channels login --channel whatsapp
openclaw gateway
openclaw pairing list whatsapp
openclaw pairing approve whatsapp <CODE>
```

Use WhatsApp com cuidado: é uma superfície real de mensagem. O projeto recomenda
número dedicado quando possível.

## Capacidades principais encontradas

### Canais de chat

Documentados em `docs/pt-BR/channels/`.

Incluem WhatsApp, Telegram, Discord, Slack, Signal, Google Chat, iMessage,
BlueBubbles, IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud
Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, QQ Bot, WebChat e
Voice Call via plugin.

### Modelos e provedores

Documentados em `docs/pt-BR/providers/`.

O projeto suporta muitos backends: OpenAI, Anthropic, Google/Gemini, OpenRouter,
Ollama, vLLM, SGLang, Groq, Mistral, DeepSeek, Qwen, MiniMax, Moonshot, NVIDIA,
Together, Bedrock, Hugging Face, LiteLLM, xAI, Z.AI, Runway, fal, Deepgram e
outros.

### Ferramentas do agente

Documentadas em `docs/pt-BR/tools/`.

As ferramentas embutidas incluem:

- `exec` / `process`: comandos e processos;
- `read` / `write` / `edit` / `apply_patch`: arquivos no workspace;
- `browser`: controle de Chromium;
- `web_search` / `web_fetch`: pesquisa e leitura web;
- `message`: envio de mensagens por canais;
- `image`, `image_generate`, `music_generate`, `video_generate`, `tts`;
- `cron`, `webhooks`, `gateway`;
- `sessions_*`, subagentes e roteamento multiagente;
- `nodes`: dispositivos pareados, câmera, notificações, localização e Canvas.

### Integrações com IDEs, ACP e MCP

Documentadas em `docs/pt-BR/cli/acp.md`, `docs/pt-BR/tools/acp-agents.md` e
`docs/pt-BR/cli/mcp.md`.

O comando `openclaw acp` expõe o OpenClaw como uma bridge do Agent Client Protocol
por stdio. Isso permite que IDEs ou clientes compatíveis com ACP encaminhem prompts
para uma sessão do Gateway OpenClaw. O projeto também documenta ACPX para executar
harnesses como Codex/Claude/Gemini e MCP via `openclaw mcp serve` ou integrações
de plugin.

### Automação

Documentada em `docs/pt-BR/automation/`.

O OpenClaw tem cron jobs, heartbeat, webhooks, Gmail Pub/Sub, hooks e fluxos
`clawflow`/`taskflow`. Isso permite tarefas periódicas e gatilhos externos.

### Plugins e skills

Documentados em `docs/pt-BR/plugins/` e `docs/pt-BR/tools/skills.md`.

Plugins empacotam canais, provedores, ferramentas, providers de mídia e skills.
Skills são arquivos Markdown que ensinam o agente como agir em um domínio
específico. Neste checkout há 53 skills locais, incluindo GitHub, Slack, Discord,
Obsidian, Notion, Trello, 1Password, weather, coding-agent, tmux, spotify-player,
voice-call e outras.

### Apps e nodes

Documentados em `docs/pt-BR/platforms/` e `docs/pt-BR/nodes/`.

Há suporte para app macOS, node iOS e node Android. Eles adicionam voz, Canvas,
câmera, gravação de tela, notificações, localização e comandos locais do
dispositivo.

## Configuração mínima segura

Antes de abrir acesso por canais ou expor o Gateway, rode:

```bash
openclaw security audit
openclaw doctor
```

Baseline conservadora para começar:

```json5
{
  gateway: {
    mode: "local",
    bind: "loopback",
    auth: { mode: "token", token: "troque-por-um-token-longo" },
  },
  session: {
    dmScope: "per-channel-peer",
  },
  tools: {
    profile: "messaging",
    fs: { workspaceOnly: true },
    exec: { security: "deny", ask: "always" },
    elevated: { enabled: false },
  },
}
```

Depois aumente permissão por agente ou por canal quando você entender o risco.
Não coloque `dmPolicy: "open"` com `allowFrom: ["*"]` em canais reais a menos que
você queira mesmo aceitar mensagens de qualquer pessoa.

## Comandos úteis no dia a dia

```bash
openclaw onboard --install-daemon
openclaw dashboard
openclaw health
openclaw doctor
openclaw gateway status
openclaw channels list
openclaw channels status
openclaw models list
openclaw models set <provider/model>
openclaw plugins list
openclaw skills list
openclaw message send --to <destino> --message "Olá do OpenClaw"
openclaw agent --message "Crie um plano para minha semana" --thinking high
```

## Onde ler em português

Comece por estes arquivos:

- `docs/pt-BR/index.md`
- `docs/pt-BR/start/getting-started.md`
- `docs/pt-BR/start/wizard.md`
- `docs/pt-BR/channels/index.md`
- `docs/pt-BR/tools/index.md`
- `docs/pt-BR/providers/index.md`
- `docs/pt-BR/gateway/configuration.md`
- `docs/pt-BR/gateway/security/index.md`
- `docs/pt-BR/help/troubleshooting.md`
- `docs/pt-BR/cli/index.md`

## Resumo prático

Se você quer testar hoje:

1. Instale com `npm install -g openclaw@latest`.
2. Rode `openclaw onboard --install-daemon`.
3. Abra `openclaw dashboard` e converse pelo navegador.
4. Configure Telegram se quiser o canal externo mais simples.
5. Configure WhatsApp se quiser usar no celular, preferindo um número dedicado.
6. Rode `openclaw security audit` antes de abrir acesso para outras pessoas ou
   grupos.

O OpenClaw já está bem além de um chatbot: ele é um gateway pessoal para agentes
com canais, ferramentas, automação, plugins, skills, memória, mídia e dispositivos.
O ponto de atenção neste checkout específico é que ele está sem build; para usar
imediatamente, instale o pacote publicado ou construa a partir do fonte.

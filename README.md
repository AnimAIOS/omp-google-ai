# omp-google-ai-search

Google AI Mode search tool ported from [`github:Vecchete/Opencode-Google-AI-Search-Plugin`](https://github.com/Vecchete/Opencode-Google-AI-Search-Plugin) into an [oh-my-pi (omp)](https://github.com/oh-my-pi/pi-ai) extension.

Registers the `google_ai_search_plus` tool, which searches the web using Google's AI Mode via a shared Playwright browser session (cookie/UA identity carried over from local Chrome), with abort handling, idle disposal, and markdown output.
## Install

```bash
omp plugin install github:AnimAIOS/omp-google-ai
```

Or load directly from a local path:

```bash
omp --extension /path/to/omp-google-ai/google-ai-search.ts
```

## Usage

```bash
omp --tool google_ai_search_plus print
```

or, through an agent call:

```
google_ai_search_plus({ "query": "current events in ...", "timeout": 30, "followUp": false })
```

Parameters mirror the original OpenCode plugin:

- `query` (string): Question or topic to submit to Google AI Mode.
- `timeout` (number, 5–120, default 30): Timeout in seconds.
- `followUp` (boolean, default false): Treat the query as a follow-up in the same session.

## Auth / environment

Browser identity is resolved from:

1. `GOOGLE_AI_COOKIES_PATH` (default `/home/vi/chrome-to-playwright-cookies/cookies.json`)
2. `GOOGLE_AI_UA_PATH` (default `/home/vi/chrome-to-playwright-cookies/chrome-ua.txt`)
3. `GOOGLE_AI_CHROME_PATH` (default `/opt/chromium.org/chromium-unstable/chrome`)

## Development

```bash
bun install --ignore-scripts
bun test
bun run check
```
- `google-ai-search.ts` — extension entry point (source of truth; default factory exporting `registerTool("google_ai_search_plus", …)`); `extensions/google-ai-search.ts` is its byte-identical copy for `~/.omp/agent/extensions/`
- `package.json` — plugin manifest (peerDeps on `pi-coding-agent`, deps on `playwright` + `pi-utils`)
- `tsconfig.json` — typecheck config

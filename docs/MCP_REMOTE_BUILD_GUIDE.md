# 🛰️ Guia de Builds Remotos via MCP (Model Context Protocol)

Este guia ensina como conectar qualquer computador cliente (usando Claude Desktop, Antigravity IDE, Cursor ou agentes de IA) ao **YamiTec AI Orchestrator** para disparar compilações e releases oficiais do **Yami** sem executar código pesado na máquina cliente.

---

## 🎯 Por que Builds Remotos via MCP?

1. **Desoneração da Máquina Cliente**: Notebooks ou PCs de trabalho não precisam ter compiladores pesados (Rust, Cargo, Node 22, Android NDK, Docker, Apple SDKs) instalados localmente.
2. **Ambiente Padronizado**: O Orchestrator reside na estação de trabalho / servidor oficial, garantindo builds reproduzíveis e determinísticos.
3. **Controle por Linguagem Natural**: Você pode simplesmente pedir ao seu assistente de IA: *"Gere uma nova versão do Yami para Windows e iOS"* e o agente usará as ferramentas MCP para acionar o build no Orchestrator.

---

## 🔌 1. Como Conectar o seu Outro PC ao Orchestrator

O servidor do Orchestrator expõe o protocolo MCP via **Server-Sent Events (SSE)** na rota `/mcp/sse`.

### Conexão via Rede Local (LAN)
Identifique o IP do PC onde o Orchestrator está rodando (por exemplo, `192.168.42.17`):

No arquivo de configuração do seu cliente MCP no outro computador:

#### No Claude Desktop
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "yamitec-ai-orchestrator": {
      "url": "http://192.168.42.17:8000/mcp/sse"
    }
  }
}
```

#### No Antigravity IDE / Cursor
- Adicione à configuração MCP (`.agents/mcp_config.json` ou nas configurações da IDE):

```json
{
  "mcpServers": {
    "yamitec-ai-orchestrator": {
      "url": "http://192.168.42.17:8000/mcp/sse"
    }
  }
}
```

### Conexão Externa / Remota (Cloudflare Tunnel)
Se você estiver fora de casa ou da rede local, o Orchestrator suporta exposição segura via túnel público (definido em `PUBLIC_BASE_URL` no `.env`):

```json
{
  "mcpServers": {
    "yamitec-ai-orchestrator": {
      "url": "https://treo-continually-mumbai-repairs.trycloudflare.com/mcp/sse"
    }
  }
}
```

---

## 🛠️ 2. Ferramentas MCP Disponíveis para Release

### `build_yami_release`
Dispara a esteira de compilação do Yami para a plataforma solicitada.

```json
{
  "name": "build_yami_release",
  "arguments": {
    "target": "windows",
    "version": "0.2.0",
    "use_xtool": true,
    "dry_run": false,
    "clean": false
  }
}
```

#### Parâmetros:
- `target` *(string, obrigatório)*:
  - `"windows"`: Compila o executável (.exe) e o instalador MSI via Tauri.
  - `"linux"`: Gera pacotes AppImage, .deb e .rpm.
  - `"android"`: Gera o APK do Yami Launcher e companion via Gradle.
  - `"macos"`: Compila o binário/bundle (.app) para computadores Apple.
  - `"ios"`: Compila o pacote (.ipa) para dispositivos móveis Apple.
  - `"all"`: Dispara compilação em lote para todos os alvos suportados.
- `version` *(string, opcional)*: Especifica a versão semântica do release (ex: `"0.2.1"`).
- `use_xtool` *(boolean, default: `true`)*: Quando o host não é macOS nativo, encaminha compilações de macOS e iOS para o **`xtool`**.
- `dry_run` *(boolean, default: `false`)*: Valida permissões, caminhos e toolchains sem compilar binários reais.
- `clean` *(boolean, default: `false`)*: Limpa diretórios temporários e caches antes de iniciar.

---

### `check_build_toolchains`
Consulta o status de todas as ferramentas de compilação instaladas na máquina do Orchestrator.

```json
{
  "name": "check_build_toolchains",
  "arguments": {}
}
```

#### Exemplo de Resposta:
```json
{
  "host_os": "linux",
  "host_arch": "x86_64",
  "is_osx": false,
  "node_available": true,
  "node_version": "v22.23.5",
  "rust_available": true,
  "rust_version": "rustc 1.85.0",
  "tauri_available": true,
  "android_sdk_available": true,
  "xtool_available": true,
  "xtool_path": "/usr/local/bin/xtool",
  "xtool_version": "xtool 0.1.0",
  "xtool_sdks": ["iPhoneOS18.0.sdk", "MacOSX15.0.sdk"],
  "xcode_available": false,
  "wsl_available": false
}
```

---

## 💬 3. Exemplos de Uso por Linguagem Natural

Quando o MCP estiver configurado, você pode pedir ao assistente no outro PC:

> **Usuário**: *"Verifique quais compiladores estão disponíveis no Orchestrator."*
> **Assistente**: Executa `check_build_toolchains()` e lista o status das ferramentas.

> **Usuário**: *"Gere um novo release do Yami para Windows na versão 0.2.0."*
> **Assistente**: Executa `build_yami_release(target="windows", version="0.2.0")`, aguarda o término no Orchestrator e retorna os caminhos dos instaladores gerados e seus checksums SHA256.

> **Usuário**: *"Faça um dry-run do build de iOS para conferir se o xtool está configurado corretamente."*
> **Assistente**: Executa `build_yami_release(target="ios", dry_run=true, use_xtool=true)` e exibe o relatório de validação.

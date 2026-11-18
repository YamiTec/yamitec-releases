# 🌐 Yamitec Ecosystem Hub

O **Yamitec Ecosystem Hub** é a estrutura central unificada que reúne, orquestra e distribui todos os projetos e componentes da organização Yamitec.

---

## 🏛️ Arquitetura Geral do Ecossistema

```mermaid
flowchart TD
    subgraph RemoteClients["Clientes Remotos & IDEs"]
        REMOTE["💻 Outro Computador<br/>(Claude Desktop / Antigravity / Cursor)"]
    end

    subgraph Hub["Yamitec Ecosystem Hub (Servidor Central)"]
        subgraph Core["Cérebro & Orquestração"]
            ORCH["🧠 YamiTec AI Orchestrator<br/>(FastAPI / MCP SSE / Agentes)"]
            LOCAL_AI["⚡ Ollama & Modelos Locais<br/>(DeepSeek, Qwen, Llama)"]
            ENGINE["⚙️ Yami Release Engine<br/>(Compilador Centralizado)"]
        end

        subgraph ClientApp["Aplicações do Usuário"]
            YAMI["🧑‍🚀 Yami Companion (yamitec-yami)<br/>Ilha Dinâmica Desktop & Launcher Android"]
        end

        subgraph Toolchain["Esteiras de Compilação"]
            XTOOL["🔧 xtool (Linux / Windows)<br/>Builds iOS & macOS sem Mac"]
            NATIVE["🍎 Xcode / XcodeGen<br/>(Se host for macOS nativo)"]
            TAURI["🦀 Tauri / Rust / Node<br/>(Builds Windows & Linux)"]
            GRADLE["📱 Gradle / Android SDK<br/>(Builds Android TV & Mobile)"]
        end

        subgraph Distribution["Canal Oficial de Distribuição"]
            REL["📦 yamitec-releases<br/>Instaladores, Checksums e Wiki"]
        end
    end

    REMOTE -->|Model Context Protocol (SSE /mcp/sse)| ORCH
    YAMI -->|WebSocket / REST| ORCH
    ORCH --> LOCAL_AI
    ORCH --> ENGINE

    ENGINE -->|iOS / macOS em Não-OSX| XTOOL
    ENGINE -->|macOS em Mac Nativo| NATIVE
    ENGINE -->|Windows Desktop| TAURI
    ENGINE -->|Android APK| GRADLE

    ENGINE -->|Publica Artefatos| REL
    YAMI -.->|Verifica Atualizações| REL
```

---

## 📁 Estrutura dos Repositórios no Hub

O Hub reside no diretório raiz do ecossistema e integra três projetos interdependentes:

```
D:\OLLAMA\Projetos\Yamitec\
├── YamiTec-AI-Orchestrator\    # Backend FastAPI, Agentes, MCP Server e Release Engine
├── yamitec-yami\               # Código-fonte do Companion Yami (Windows, Linux, Android, iOS/macOS)
├── yamitec-releases\           # Binários compilados, instaladores oficiais, tags e documentação
├── yamitec.code-workspace      # Workspace multi-root para VS Code e Antigravity
├── yamitec-hub.ps1             # CLI Helper unificado do ecossistema
└── README.md                   # Visão geral centralizada
```

### Detalhamento dos Componentes

1. **[`YamiTec-AI-Orchestrator`](../YamiTec-AI-Orchestrator/)**:
   - **Backend FastAPI**: Servidor robusto com suporte a múltiplos agentes de IA locais (DeepSeek, Qwen, Llama via Ollama).
   - **Servidor MCP Oficial**: Suporte a transportes stdio e **SSE (Server-Sent Events)** para conexão remota de clientes.
   - **Release Engine Centralizado**: Responsável por receber pedidos de compilação e orquestrar as ferramentas locais sem sobrecarregar máquinas clientes.

2. **[`yamitec-yami`](../yamitec-yami/)**:
   - **Desktop Companion**: Ilha interativa no topo da tela (Dynamic Island) para Windows 10/11 e distribuições Linux com suporte a Wayland/X11 e layer-shell.
   - **NotchBuddy**: Implementação Swift / SwiftUI nativa para macOS e iOS.
   - **Android Launcher**: Home screen para projetores inteligentes e Android TV (Android 11+).
   - **Voz Contínua e Integrações**: Ativação por voz contínua ("OK Yami"), integração direta com Discord, Ollama e o Orchestrator.

3. **[`yamitec-releases`](./)**:
   - Repositório oficial de publicação e versionamento.
   - Hospeda instaladores finais (`.exe`, `.msi`, `.AppImage`, `.deb`, `.rpm`, `.apk`, `.ipa`).
   - Mantém as tags móveis de versão contínua (`windows-latest`, `linux-latest`) e versões congeladas (`windows-v*`, `linux-v*`).
   - Centraliza a documentação técnica e a Wiki da organização Yamitec.

---

## 🛠️ CLI de Gerenciamento (`yamitec-hub.ps1`)

O script PowerShell [`yamitec-hub.ps1`](../yamitec-hub.ps1) permite controle centralizado de todos os projetos:

```powershell
# Verificar status git e branches em todos os repositórios
.\yamitec-hub.ps1 status

# Puxar as últimas alterações de todos os repositórios simultaneamente
.\yamitec-hub.ps1 pull

# Iniciar o servidor e contêineres do Orchestrator
.\yamitec-hub.ps1 start-orchestrator

# Exibir os endpoints e configuração de conexão MCP para outros PCs
.\yamitec-hub.ps1 mcp-info

# Inspecionar compiladores disponíveis (Rust, Node, Android SDK, xtool)
.\yamitec-hub.ps1 check-toolchains

# Disparar build do Yami (ex: windows, ios, macos, android)
.\yamitec-hub.ps1 build-yami -Target windows
.\yamitec-hub.ps1 build-yami -Target ios -DryRun
```

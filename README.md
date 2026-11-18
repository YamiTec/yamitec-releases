# Yami Releases & Distribution Hub

Instaladores oficiais, atualizações e documentação central do **Yami**, o assistente desktop e companheiro astronauta da **YamiTec**: uma ilha interativa no topo da sua tela que opera offline e se conecta ao **YamiTec AI Orchestrator**.

Este repositório centraliza as compilações oficiais, o versionamento contínuo, a Wiki pública e a documentação da esteira de distribuição do ecossistema Yamitec.

---

## ⬇️ Download

| Plataforma | Build Mais Recente | Formatos Adicionais |
|---|---|---|
| **Windows 10/11** | [`Yami-Windows-setup.exe`](https://github.com/YamiTec/yamitec-releases/releases/download/windows-latest/Yami-Windows-setup.exe) | [`Yami-Windows.msi`](https://github.com/YamiTec/yamitec-releases/releases/download/windows-latest/Yami-Windows.msi) |
| **Linux (x86_64)** | [`Yami-Linux-x86_64.AppImage`](https://github.com/YamiTec/yamitec-releases/releases/download/linux-latest/Yami-Linux-x86_64.AppImage) | `.deb` (Debian/Ubuntu) · `.rpm` (Fedora/openSUSE) |
| **Android TV / Mobile** | [`YamiLauncher-latest.apk`](https://github.com/YamiTec/yamitec-releases/releases) | APKs de celular e launcher de projetor |
| **Apple (macOS / iOS)** | Compilado via `xtool` no Orchestrator | Pacotes `.app` e `.ipa` sob demanda |

Versões específicas, changelogs e o arquivo `SHA256SUMS` estão disponíveis na [Página Oficial de Releases](https://github.com/YamiTec/yamitec-releases/releases).

---

## 📦 Como Instalar

### Windows 10 / 11
Execute o instalador baixado. Caso o Windows SmartScreen exiba aviso por ausência temporária de assinatura de código: clique em **Mais informações → Executar assim mesmo**.

### Linux
```bash
# AppImage (execução direta):
chmod +x Yami-Linux-*-x86_64.AppImage
./Yami-Linux-*-x86_64.AppImage

# Debian / Ubuntu:
sudo apt install ./Yami-Linux-*-amd64.deb

# Fedora / openSUSE:
sudo dnf install ./Yami-Linux-*-x86_64.rpm
```

> **Dica**: Em compositores com suporte a `layer-shell` (COSMIC, KDE Plasma, Hyprland, Sway), a ilha ancora nativamente no topo da tela. No GNOME, ela abre como uma janela flutuante padrão.

---

## 🏷️ Tags de Release

| Tag | Finalidade |
|---|---|
| `windows-v*`, `linux-v*`, `android-v*` | Versões estáveis imutáveis |
| `windows-latest`, `linux-latest` | Tags móveis apontando sempre para o build mais recente |

---

## 📚 Documentação Técnica da Esteira de Releases

Toda a infraestrutura de builds do ecossistema agora está documentada em detalhes:

1. **[🌐 Yamitec Ecosystem Hub](docs/ECOSYSTEM_HUB.md)**:
   - Estrutura dos projetos integrados (`YamiTec-AI-Orchestrator`, `yamitec-yami`, `yamitec-releases`).
   - Diagrama de arquitetura unificada e uso do CLI `yamitec-hub.ps1`.

2. **[🛰️ Guia de Builds Remotos via MCP](docs/MCP_REMOTE_BUILD_GUIDE.md)**:
   - Como conectar outro computador (Claude Desktop, Antigravity, Cursor) ao Orchestrator via MCP over SSE (`/mcp/sse`).
   - Como disparar compilações no servidor central por comandos em linguagem natural sem sobrecarregar a máquina cliente.

3. **[🍏 Compilação Cross-Platform com `xtool`](docs/XTOOL_CROSS_COMPILATION.md)**:
   - Como o Orchestrator compila o projeto `NotchBuddy` (SwiftUI para iOS e macOS) em ambientes Linux ou Windows (não-OSX).
   - Uso da ferramenta `xtool` (`xtool-org/xtool`) e registro de SDKs Darwin da Apple sem necessidade de um Mac físico.

---

## 📖 Wiki e Comunidade

- **Wiki Oficial (em Português)**: [Yamitec Wiki](https://github.com/YamiTec/yamitec-releases/wiki) — Guia de recursos, personalização do astronauta, segurança/privacidade e arquitetura de plugins.
- **Organização GitHub**: [GitHub YamiTec](https://github.com/YamiTec)

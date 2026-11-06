# Yami releases

Installers and updates for **Yami**, the YamiTec desktop companion: an astronaut at the top of your screen that you can talk to, that works offline and plugs into the Yamitec Orchestrator.

This repository holds only the published builds and the [wiki](https://github.com/YamiTec/yamitec-releases/wiki). It has no source code.

## Download

| Platform | Always the newest build |
|---|---|
| **Windows 10/11** | [`Yami-Windows-setup.exe`](https://github.com/YamiTec/yamitec-releases/releases/download/windows-latest/Yami-Windows-setup.exe) · [`Yami-Windows.msi`](https://github.com/YamiTec/yamitec-releases/releases/download/windows-latest/Yami-Windows.msi) |
| **Linux** | [`Yami-Linux-x86_64.AppImage`](https://github.com/YamiTec/yamitec-releases/releases/download/linux-latest/Yami-Linux-x86_64.AppImage) |

Specific versions, plus the Linux `.deb`, `.rpm` and `SHA256SUMS`, are on the [releases page](https://github.com/YamiTec/yamitec-releases/releases).

## Install

**Windows:** run the installer. It is not code-signed yet, so SmartScreen shows a warning the first time: **More info → Run anyway**.

**Linux:**

```bash
chmod +x Yami-Linux-*-x86_64.AppImage    # AppImage: then run it
sudo apt install ./Yami-Linux-*-amd64.deb    # Debian/Ubuntu
sudo dnf install ./Yami-Linux-*-x86_64.rpm   # Fedora/openSUSE
```

Check a versioned download with `sha256sum -c SHA256SUMS --ignore-missing`.

The island sits on the top edge on compositors with layer-shell (COSMIC, KDE Plasma, Hyprland, Sway…). On GNOME it opens as a regular window.

## Release tags

| Tag | What it is |
|---|---|
| `windows-v*`, `linux-v*` | One fixed version |
| `windows-latest`, `linux-latest` | Moving tags, replaced at every release with the newest build |

## Documentation

The [wiki](https://github.com/YamiTec/yamitec-releases/wiki) (in Portuguese) covers features, customization, security and privacy, architecture and how to publish.

---
project: lume
stars: 2167
description: |-
    A lightweight CLI and local API server to create, run and manage macOS and Linux virtual machines (VMs) natively on Apple Silicon.
url: https://github.com/trycua/lume
---

<div align="center">
<h1>
  <div class="image-wrapper" style="display: inline-block;">
    <picture>
      <source media="(prefers-color-scheme: dark)" alt="logo" height="150" srcset="img/logo_white.png" style="display: block; margin: auto;">
      <source media="(prefers-color-scheme: light)" alt="logo" height="150" srcset="img/logo_black.png" style="display: block; margin: auto;">
      <img alt="Shows my svg">
    </picture>
  </div>

  [![Swift 6](https://img.shields.io/badge/Swift_6-F54A2A?logo=swift&logoColor=white&labelColor=F54A2A)](#)
  [![macOS](https://img.shields.io/badge/macOS-000000?logo=apple&logoColor=F0F0F0)](#)
  [![Homebrew](https://img.shields.io/badge/Homebrew-FBB040?logo=homebrew&logoColor=fff)](#install)
  [![Discord](https://img.shields.io/badge/Discord-%235865F2.svg?&logo=discord&logoColor=white)](https://discord.com/invite/mVnXXpdE85)
  [![All Contributors](https://img.shields.io/github/all-contributors/trycua/lume?color=ee8449&style=flat-square)](#contributors)
</h1>
</div>


**lume** is a lightweight Command Line Interface and local API server to create, run and manage macOS and Linux virtual machines (VMs) with near-native performance on Apple Silicon, using Apple's `Virtualization.Framework`.

### Run prebuilt macOS images in just 1 step

<div align="center">
<img src="img/cli.png" alt="lume cli">
</div>


```bash
lume run macos-sequoia-vanilla:latest
```

For a python interface, check out [pylume](https://github.com/trycua/pylume).

## Usage

```bash
lume <command>

Commands:
  lume create <name>            Create a new macOS or Linux VM
  lume run <name>               Run a VM
  lume ls                       List all VMs
  lume get <name>               Get detailed information about a VM
  lume set <name>               Modify VM configuration
  lume stop <name>              Stop a running VM
  lume delete <name>            Delete a VM
  lume pull <image>             Pull a macOS image from container registry
  lume clone <name> <new-name>  Clone an existing VM
  lume images                   List available macOS images in local cache
  lume ipsw                     Get the latest macOS restore image URL
  lume prune                    Remove cached images
  lume serve                    Start the API server

Options:
  --help     Show help [boolean]
  --version  Show version number [boolean]

Command Options:
  create:
    --os <os>            Operating system to install (macOS or linux, default: macOS)
    --cpu <cores>        Number of CPU cores (default: 4)
    --memory <size>      Memory size, e.g., 8GB (default: 4GB)
    --disk-size <size>   Disk size, e.g., 50GB (default: 40GB)
    --display <res>      Display resolution (default: 1024x768)
    --ipsw <path>        Path to IPSW file or 'latest' for macOS VMs

  run:
    --no-display                Do not start the VNC client app
    --shared-dir <dir>          Share directory with VM (format: path[:ro|rw])
    --mount <path>              For Linux VMs only, attach a read-only disk image
    --registry <url>            Container registry URL (default: ghcr.io)
    --organization <org>        Organization to pull from (default: trycua)
    --vnc-port <port>           Port to use for the VNC server (default: 0 for auto-assign)
    --recovery-mode <boolean>   For MacOS VMs only, start VM in recovery mode (default: false)

  set:
    --cpu <cores>        New number of CPU cores (e.g., 4)
    --memory <size>      New memory size (e.g., 8192MB or 8GB)
    --disk-size <size>   New disk size (e.g., 40960MB or 40GB)
    --display <res>      New display resolution in format WIDTHxHEIGHT (e.g., 1024x768)

  delete:
    --force              Force deletion without confirmation

  pull:
    --registry <url>     Container registry URL (default: ghcr.io)
    --organization <org> Organization to pull from (default: trycua)

  serve:
    --port <port>        Port to listen on (default: 3000)
```

## Install

```bash
brew tap trycua/lume
brew install lume
```

You can also download the `lume.pkg.tar.gz` archive from the [latest release](https://github.com/trycua/lume/releases), extract it, and install the package manually.

## Prebuilt Images

Pre-built images are available in the registry [ghcr.io/trycua](https://github.com/orgs/trycua/packages). 
These images come with an SSH server pre-configured and auto-login enabled.

For the security of your VM, change the default password `lume` immediately after your first login.

| Image | Tag | Description | Size |
|-------|------------|-------------|------|
| `macos-sequoia-vanilla` | `latest`, `15.2` | macOS Sequoia 15.2 | 40GB |
| `macos-sequoia-xcode` | `latest`, `15.2` | macOS Sequoia 15.2 with Xcode command line tools | 50GB |
| `ubuntu-noble-vanilla` | `latest`, `24.04.1` | [Ubuntu Server for ARM 24.04.1 LTS](https://ubuntu.com/download/server/arm) with Ubuntu Desktop | 20GB |

For additional disk space, resize the VM disk after pulling the image using the `lume set <name> --disk-size <size>` command.

## Local API Server
  
`lume` exposes a local HTTP API server that listens on `http://localhost:3000/lume`, enabling automated management of VMs.

```bash
lume serve
```

For detailed API documentation, please refer to [API Reference](docs/API-Reference.md).

## Docs

- [API Reference](docs/API-Reference.md)
- [Development](docs/Development.md)
- [FAQ](docs/FAQ.md)

## Contributing

We welcome and greatly appreciate contributions to lume! Whether you're improving documentation, adding new features, fixing bugs, or adding new VM images, your efforts help make lume better for everyone. For detailed instructions on how to contribute, please refer to our [Contributing Guidelines](CONTRIBUTING.md).

Join our [Discord community](https://discord.com/invite/mVnXXpdE85) to discuss ideas or get assistance.

## License

lume is open-sourced under the MIT License - see the [LICENSE](LICENSE) file for details.

## Trademarks

Apple, macOS, and Apple Silicon are trademarks of Apple Inc. Ubuntu and Canonical are registered trademarks of Canonical Ltd. This project is not affiliated with, endorsed by, or sponsored by Apple Inc. or Canonical Ltd.

## Stargazers over time

[![Stargazers over time](https://starchart.cc/trycua/lume.svg?variant=adaptive)](https://starchart.cc/trycua/lume)

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/f-trycua"><img src="https://avatars.githubusercontent.com/u/195596869?v=4?s=100" width="100px;" alt="f-trycua"/><br /><sub><b>f-trycua</b></sub></a><br /><a href="#code-f-trycua" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->


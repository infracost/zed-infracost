# Infracost for Zed

A [Zed](https://zed.dev) extension that provides cloud cost estimates and FinOps policy checks for Terraform files, powered by [Infracost](https://www.infracost.io).

## Features

- Inline cloud cost estimates for Terraform resources
- FinOps policy violation detection
- Automatic installation and updates of the Infracost language server

## Installation

1. Clone this repository:
   ```sh
   git clone https://github.com/infracost/zed-infracost.git
   ```
2. Open Zed
3. Go to **Extensions** (Cmd+Shift+X)
4. Click **Install Dev Extension**
5. Select the cloned `zed-infracost` directory

The extension automatically downloads the [Infracost language server](https://github.com/infracost/infracost-ls) on first use. If `infracost-ls` is already on your PATH, it will use that instead.

## Bicep

Bicep cost estimates are off by default, because estimating a Bicep file compiles it — which requires the [Bicep CLI](https://aka.ms/bicep-install) on your `PATH` and downloads any modules the file references from their registries.

Unlike the other editor integrations, this extension has no `enableBicep` setting. Enable it by exporting the environment variable in the environment Zed is launched from:

```sh
export INFRACOST_ENABLE_BICEP=true
```

This is deliberate. The toggle must be user-level only: a repository must not be able to make Infracost run a compiler over its own contents. Zed's [project settings](https://zed.dev/docs/configuring-zed) (`.zed/settings.json`) merge over user settings and are part of the checked-out repository, and Zed has no workspace-trust equivalent to fall back on — so an extension setting read through `LspSettings::for_worktree` would be repo-controlled. The language server treats an absent `enableBicep` as "use the ambient environment", so omitting it leaves the decision with the environment you started Zed in.

Note that Zed also needs a Bicep language extension installed for `.bicep` files to be routed to any language server.

ARM JSON is estimated either way, including JSON that a Bicep build produced.

## Requirements

- [Zed](https://zed.dev) editor
- Internet connection (for the initial language server download)

## Supported Platforms

- macOS (Apple Silicon and Intel)
- Linux (ARM64 and AMD64)
- Windows (AMD64)

## Development

### Prerequisites

- [Rust](https://rustup.rs) toolchain
- WebAssembly target: `rustup target add wasm32-wasip1`

### Building

```sh
cargo build --target wasm32-wasip1 --release
```

### Linting

```sh
cargo fmt --check
cargo clippy --target wasm32-wasip1 -- -D warnings
```

## License

See [LICENSE](LICENSE) for details.

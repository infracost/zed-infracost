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

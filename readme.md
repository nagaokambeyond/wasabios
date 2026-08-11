#［作って学ぶ］OSのしくみⅠ 練習

# rust
> curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
> source "$HOME/.cargo/env"
> rustup --version

# qemu
> brew install qemu
> qemu-system-x86_64 --version

# ツールのバージョン固定 `rust-toolchain.toml`

```toml
[toolchain]
channel = "nightly-2024-01-01"
components = ["rustfmt", "rust-src"]
targets = ["x86_64-unknown-linux-gnu"]
profile = "default"
```

> rustup show active-toolchain

> rustup target list
> rustup target list | grep uefi

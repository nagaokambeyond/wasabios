# ［作って学ぶ］OSのしくみⅠ 練習

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

## ビルド

```bash
rustup show active-toolchain
rustup target list
rustup target list | grep uefi
cargo build --target x86_64-unknown-uefi
rustup target add x86_64-unknown-uefi
cargo build --target x86_64-unknown-uefi
```

## 実行→エラーになる

```bash
cargo run --target x86_64-unknown-uefi
target/x86_64-unknown-uefi/debug/wasabi.efi
```

## ファイルの属性確認

```bash
file target/x86_64-unknown-uefi/debug/wasabi.efi
```

## 実行準備

```bash
qemu-system-x86_64 --version
mkdir -p third_party/ovmf
cd third_party/ovmf
wget https://github.com/hikalium/wasabi/raw/main/third_party/ovmf/RELEASEX64_OVMF.fd
cd -
```

## UEFIの起動確認
```bash
qemu-system-x86_64 -bios third_party/ovmf/RELEASEX64_OVMF.fd
```

```bash
mkdir -p mnt/EFI/BOOT
cp target/x86_64-unknown-uefi/debug/wasabi.efi mnt/EFI/BOOT/BOOTX64.EFI

qemu-system-x86_64 -bios third_party/ovmf/RELEASEX64_OVMF.fd -drive format=raw,file=fat:rw:mnt
```

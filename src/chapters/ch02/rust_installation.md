# Cài đặt Rust

Mục tiêu: cài `rustup`, cài toolchain stable, kiểm tra môi trường, editor plugin.

## 1) Cài nhanh với rustup (Linux/macOS/WSL)
```bash
curl https://sh.rustup.rs -sSf | sh
# chọn 1) Proceed with installation (mặc định)
source $HOME/.cargo/env
````

## 2) Windows (PowerShell)

* Cài **Rustup-init.exe** từ [https://rustup.rs](https://rustup.rs)
* Chọn toolchain **stable (default)**, toolchain MSVC.
* Cài **Build Tools** (nếu được hỏi): `Visual Studio Build Tools` (MSVC, Windows 10/11 SDK).

## 3) Kiểm tra

```bash
rustc --version
cargo --version
rustup --version
```

## 4) Cập nhật / gỡ

```bash
rustup update
rustup self uninstall
```

## 5) Toolchain & targets

```bash
rustup default stable
rustup toolchain list
rustup target add x86_64-unknown-linux-gnu
```

## 6) Dự án mẫu

```bash
cargo new hello-rust
cd hello-rust
cargo run
```



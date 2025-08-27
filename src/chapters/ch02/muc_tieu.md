# Mục tiêu

Kết thúc chương này, bạn sẽ:

- Cài đặt được **Rust** (stable) và cấu hình môi trường phát triển.
- Hiểu lại các khái niệm **Ownership / Borrowing / Lifetimes** và vì sao chúng quan trọng trong **async I/O**.
- Viết và chuẩn hóa **xử lý lỗi** với `Result`, `?`, `thiserror`/`anyhow`.
- Làm chủ các công cụ **Cargo**: workspace, features, profiles (dev/release), và mẹo tối ưu build.
- Sẵn sàng cho các chương Axum: có thể đọc/hiểu signature async, errors typed, và tổ chức project lớn.

---

## Lộ trình đọc nhanh

1. [Cài đặt Rust](./rust_installation.md)  
2. [Ownership/borrow trong async I/O](./ownership_async.md)  
3. [Lỗi & kết quả: Result, anyhow/thiserror](./error_handling.md)  
4. [Cargo: workspace, feature flags, profiles](./cargo.md)

---

## Yêu cầu tối thiểu

- Hệ điều hành Linux/macOS/Windows.
- Quyền cài đặt phần mềm, có thể chạy Docker (khuyến nghị cho các chương sau).

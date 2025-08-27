# Lời mở đầu

Đây là một quyển sách được tổng hợp lại những điều cần biết nếu bạn bắt đầu triển khai Axum trong dự án của mình.

### Mục tiêu của sách

- Hiểu nền tảng: async/await, Tokio, Tower, HTTP cơ bản.

- Sử dụng Axum để thiết kế API có cấu trúc, dễ kiểm thử, dễ mở rộng.

- Kết nối cơ sở dữ liệu, xác thực (JWT/Session), upload/streaming.

- Làm observability (logging, metrics, tracing), tối ưu hiệu năng.

- Triển khai với Docker/CI, và hoàn thành dự án cuối khóa.

### Dành cho ai?

- Lập trình viên đã biết Rust cơ bản (ownership, Result, Cargo).

- Backend dev muốn thử Rust/Axum, hoặc chuyển từ Node/Go/Java.

- Sinh viên/nhóm nghiên cứu cần một lộ trình tự học có dự án mẫu.

- Mới biết Rust? Bạn vẫn theo kịp: phần đầu có “Ôn nhanh Rust cho web”.

### Yêu cầu đầu vào & môi trường

- Rust kênh stable (cài qua rustup), cargo kèm theo.

- Docker (khuyến nghị cho phần triển khai & DB).

- Một trình soạn thảo có rust-analyzer (VS Code, IntelliJ, v.v.).

- Hệ điều hành: Linux/macOS/Windows đều OK.

### Bộ công cụ hay dùng trong sách

- tokio, axum, tower, tracing, serde, thiserror/anyhow, sqlx (PostgreSQL), jsonwebtoken/argon2, redis, v.v.


# Hệ sinh thái Rust web

## 1. Tokio
- **Tokio** là runtime async phổ biến nhất trong Rust.  
- Cung cấp event loop, task scheduler, timer, I/O bất đồng bộ.  
- Thư viện mạng như `hyper`, `reqwest`, `tonic`, và cả `axum` đều chạy trên nền Tokio.

## 2. Tower
- **Tower** cung cấp abstraction *Service* và *Layer*.  
- Service = một đơn vị xử lý request → response (giống handler chuẩn hóa).  
- Layer = wrapper/middleware để bổ sung tính năng (logging, timeout, auth...).  
- Lợi ích: composable, test dễ hơn, tách biệt concern rõ ràng.

## 3. Hyper
- **Hyper** là thư viện HTTP tốc độ cao viết bằng Rust.  
- Axum dùng Hyper ở lớp thấp nhất để giao tiếp HTTP.  
- Bạn hiếm khi gọi Hyper trực tiếp, nhưng biết nền tảng sẽ giúp debug & tối ưu.

## 4. Axum
- **Axum** = framework web xây trên *Tokio + Tower + Hyper*.  
- Triết lý: tận dụng type system Rust để đảm bảo tính đúng đắn compile-time.  
- Cung cấp router, extractors, response types, middleware sẵn sàng.  
- Thiết kế “modular”: dễ kết hợp thư viện ngoài (sqlx, tracing, serde...).

---

## Tóm lại
- **Tokio**: runtime.  
- **Hyper**: HTTP.  
- **Tower**: abstraction cho middleware/service.  
- **Axum**: lớp framework thân thiện, kết nối mọi thứ lại.

→ Đây là lý do khi học Axum, bạn cũng cần hiểu sơ qua Tokio & Tower.

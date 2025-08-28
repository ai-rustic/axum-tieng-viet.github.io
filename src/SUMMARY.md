# Tóm lược

- [Lời mở đầu](./intro.md)

---

# Phần I – Khởi động & nền tảng

- [Ch1. Giới thiệu Axum & hệ sinh thái Rust web](./chapters/ch01/README.md)
  - [Mục tiêu](./chapters/ch01/muc_tieu.md)
  - [Hệ sinh thái Rust web](./chapters/ch01/he_sinh_thai.md)
  - [So sánh nhanh: Axum, Actix, Rocket, Warp](./chapters/ch01/so_sanh.md)
  
- [Ch2. Kiến thức cơ bản về Rust](./chapters/ch02/README.md)
  - [Mục tiêu](./chapters/ch02/muc_tieu.md)
  - [Cài đặt Rust](./chapters/ch02/rust_installation.md)
  - [Ownership và Borrowing](./chapters/ch02/ownership_and_borrowing.md)
  - [Structs và Enums](./chapters/ch02/structs_and_enums.md)
  - [Collections](./chapters/ch02/collections.md)
  - [Pattern Matching](./chapters/ch02/matching.md)
  - [Traits và Generics](./chapters/ch02/traits_and_generics.md)
  - [Error Handling](./chapters/ch02/error_handling.md)
  

- [Ch3. HTTP căn bản dành cho backend Rustaceans](./chapters/ch03/README.md)
  - [Mục tiêu](./chapters/ch03/muc_tieu.md)
  - [Request/Response, headers, status](./chapters/ch03/http_primer.md)
  - [JSON, form, multipart, streaming, WS/SSE](./chapters/ch03/dinh_dang_du_lieu.md)
  - [Client HTTP với reqwest](./chapters/ch03/reqwest_client.md)

- [Ch4. Tokio & Tower trong 60 phút](./chapters/ch04/README.md)
  - [Mục tiêu](./chapters/ch04/muc_tieu.md)
  - [Tokio runtime, tasks, cancellation](./chapters/ch04/tokio.md)
  - [Tower Service & Layer](./chapters/ch04/tower.md)
  - [Tự viết một logging Layer](./chapters/ch04/log_layer.md)

---

# Phần II – Axum căn bản

- [Ch5. Router & Handlers](./chapters/ch05/README.md)
  - [Mục tiêu](./chapters/ch05/muc_tieu.md)
  - [Khai báo tuyến & route nesting](./chapters/ch05/router.md)
  - [Path, Query, Json, State extractors](./chapters/ch05/extractors_co_ban.md)
  - [Mini project: TODOs in-memory](./chapters/ch05/mini_todo.md)

- [Ch6. Extractors & Responses nâng cao](./chapters/ch06/README.md)
  - [Mục tiêu](./chapters/ch06/muc_tieu.md)
  - [Typed responses, IntoResponse](./chapters/ch06/into_response.md)
  - [Custom extractors & validation sớm](./chapters/ch06/custom_extractors.md)
  - [Xử lý lỗi nhất quán toàn app](./chapters/ch06/error_strategy.md)
 
- [Ch7. Middleware trong Axum](./chapters/ch07/README.md)
  - [Mục tiêu](./chapters/ch07/muc_tieu.md)
  - [CORS, timeouts, rate limit cơ bản](./chapters/ch07/middleware_co_ban.md)
  - [Request-ID & correlation](./chapters/ch07/request_id.md)
  - [Viết & kiểm thử middleware tuỳ biến](./chapters/ch07/custom_middleware.md)

- [Ch8. State & cấu hình ứng dụng](./chapters/ch08/README.md)
  - [Mục tiêu](./chapters/ch08/muc_tieu.md)
  - [AppState & chia sẻ tài nguyên](./chapters/ch08/app_state.md)
  - [Cấu hình theo môi trường (.env, builder)](./chapters/ch08/config.md)
  - [Secrets, đường biên khởi tạo](./chapters/ch08/secrets_init.md)

- [Ch9. Testing với Axum](./chapters/ch09/README.md)
  - [Mục tiêu](./chapters/ch09/muc_tieu.md)
  - [Unit test handler & router](./chapters/ch09/unit_integration.md)
  - [Test async & mock phụ thuộc](./chapters/ch09/mocking.md)
  - [Test E2E cơ bản](./chapters/ch09/e2e.md)

---

# Phần III – Dữ liệu, xác thực & kiến trúc

- [Ch10. Kết nối cơ sở dữ liệu](./chapters/ch10/README.md)
  - [Mục tiêu](./chapters/ch10/muc_tieu.md)
  - [Chọn thư viện (SQLx/SeaORM/Diesel)](./chapters/ch10/chon_thu_vien.md)
  - [Migration, query, transaction](./chapters/ch10/migration_query_tx.md)
  - [Pagination & indexing](./chapters/ch10/pagination_index.md)

- [Ch11. Validation & serialization](./chapters/ch11/README.md)
  - [Mục tiêu](./chapters/ch11/muc_tieu.md)
  - [serde & newtype pattern](./chapters/ch11/serde_newtype.md)
  - [validator & ràng buộc dữ liệu](./chapters/ch11/validator.md)
  - [DTO vs Domain model](./chapters/ch11/dto_vs_domain.md)

- [Ch12. Xác thực & phân quyền (AuthN/AuthZ)](./chapters/ch12/README.md)
  - [Mục tiêu](./chapters/ch12/muc_tieu.md)
  - [Session, cookie an toàn, CSRF cơ bản](./chapters/ch12/session_cookie_csrf.md)
  - [JWT, refresh token, expiry](./chapters/ch12/jwt_refresh.md)
  - [RBAC/CBAC & middleware kiểm quyền](./chapters/ch12/rbac_cbax.md)

- [Ch13. Upload file, static & streaming](./chapters/ch13/README.md)
  - [Mục tiêu](./chapters/ch13/muc_tieu.md)
  - [Multipart upload & lưu trữ (disk/S3)](./chapters/ch13/multipart_storage.md)
  - [Phục vụ static & range requests](./chapters/ch13/static_range.md)
  - [Streaming response & backpressure](./chapters/ch13/streaming.md)

- [Ch14. Kiến trúc dịch vụ](./chapters/ch14/README.md)
  - [Mục tiêu](./chapters/ch14/muc_tieu.md)
  - [Tổ chức module: routes/handlers/services/repos](./chapters/ch14/to_chuc_module.md)
  - [Error boundary & dependency inversion](./chapters/ch14/error_boundary_di.md)
  - [Test theo lớp (unit/service/integration)](./chapters/ch14/test_layers.md)

---

# Phần IV – Vận hành, quan sát & mở rộng

- [Ch15. Observability (logging, metrics, tracing)](./chapters/ch15/README.md)
  - [Mục tiêu](./chapters/ch15/muc_tieu.md)
  - [tracing & structured logs](./chapters/ch15/tracing_logs.md)
  - [OpenTelemetry, Prometheus, Grafana](./chapters/ch15/otel_prom_grafana.md)
  - [Trace-ID xuyên suốt request](./chapters/ch15/correlation.md)

- [Ch16. Hiệu năng & đồng thời](./chapters/ch16/README.md)
  - [Mục tiêu](./chapters/ch16/muc_tieu.md)
  - [Keep-alive, connection limits, tuning](./chapters/ch16/tuning.md)
  - [Caching với Redis](./chapters/ch16/caching_redis.md)
  - [Load test (k6/hey) & profiling](./chapters/ch16/loadtest_profiling.md)

- [Ch17. Tác vụ nền & lịch](./chapters/ch17/README.md)
  - [Mục tiêu](./chapters/ch17/muc_tieu.md)
  - [tokio::spawn & tokio::time](./chapters/ch17/spawn_time.md)
  - [Job queues (RabbitMQ/NATS/Redis)](./chapters/ch17/job_queues.md)
  - [Workers an toàn & idempotent](./chapters/ch17/workers.md)

- [Ch18. Triển khai & CI/CD](./chapters/ch18/README.md)
  - [Mục tiêu](./chapters/ch18/muc_tieu.md)
  - [Dockerfile multi-stage & tối ưu](./chapters/ch18/dockerfile.md)
  - [Reverse proxy (Nginx/Caddy) & systemd](./chapters/ch18/reverse_proxy_systemd.md)
  - [Migrations khi deploy & secrets](./chapters/ch18/migration_secrets.md)


---

# Phần V – Phụ lục & Dự án lớn

- [Ch19. Realtime với WebSocket/SSE](./chapters/ch19/README.md)
  - [Mục tiêu](./chapters/ch19/muc_tieu.md)
  - [Kết nối, broadcast, backpressure](./chapters/ch19/ws_basics.md)
  - [Auth trên WS/SSE](./chapters/ch19/ws_auth.md)
  - [Mini chat room (demo)](./chapters/ch19/mini_chat.md)


---

# Phụ lục

- [Phụ lục A. OpenAPI & client generation](./chapters/appendix_a/README.md)
  - [Sinh spec bằng utoipa/okapi](./chapters/appendix_a/sinh_spec.md)
  - [Swagger UI & doc portal](./chapters/appendix_a/swagger_ui.md)
  - [Tạo client TypeScript](./chapters/appendix_a/client_ts.md)

- [Phụ lục B. Mẫu mã nguồn & style guide](./chapters/appendix_b/README.md)
  - [Layout thư mục & module](./chapters/appendix_b/layout.md)
  - [Linting (clippy) & fmt](./chapters/appendix_b/lints_fmt.md)
  - [Pattern khuyến nghị](./chapters/appendix_b/patterns.md)

- [Phụ lục C. Bảo mật](./chapters/appendix_c/README.md)
  - [TLS termination & reverse proxy](./chapters/appendix_c/tls.md)
  - [Headers bảo mật (CSP, HSTS…)](./chapters/appendix_c/headers.md)
  - [Rate limit & chống lạm dụng](./chapters/appendix_c/rate_limit.md)

- [Phụ lục D. Patterns & Anti-patterns](./chapters/appendix_d/README.md)
  - [Những sai lầm phổ biến](./chapters/appendix_d/anti_patterns.md)
  - [Checklist review trước khi merge](./chapters/appendix_d/checklist.md)

- [Tài liệu tham khảo](./references.md)
- [Chỉ mục](./index.md)

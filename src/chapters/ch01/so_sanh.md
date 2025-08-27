# So sánh nhanh: Axum, Actix, Rocket, Warp

Rust có nhiều framework web. Dưới đây là so sánh ngắn để bạn định vị Axum trong hệ sinh thái.

## 1. Actix Web
- **Điểm mạnh**: hiệu năng cao (actor model, hệ sinh thái phong phú).  
- **Hạn chế**: API phức tạp hơn, macro và pattern riêng khó tiếp cận với người mới.  
- **Thích hợp**: ứng dụng yêu cầu throughput cực cao, hệ sinh thái Actix sẵn.

## 2. Rocket
- **Điểm mạnh**: ergonomic, cú pháp macro dễ đọc, code “sạch đẹp”.  
- **Hạn chế**: phụ thuộc nightly (một thời gian dài), tốc độ phát triển chậm hơn.  
- **Thích hợp**: dự án nhỏ, demo, hoặc khi ưu tiên DX (developer experience).

## 3. Warp
- **Điểm mạnh**: functional style (filter combinators), rất composable.  
- **Hạn chế**: pattern lạ, khó đọc với người mới; dễ “filter hell”.  
- **Thích hợp**: ai thích functional programming, muốn pipeline rõ ràng.

## 4. Axum
- **Điểm mạnh**: dựa trên Tower, dễ hiểu, extractors typed an toàn, middleware linh hoạt.  
- **Hạn chế**: còn trẻ so với Actix, một số tính năng phải lắp ghép thư viện ngoài.  
- **Thích hợp**: sản phẩm thực tế cần cân bằng giữa hiệu năng, bảo trì, test, mở rộng.

---

## 5. Bảng so sánh nhanh

| Framework | Hiệu năng | Dễ học | DX | Middleware | Testing | Cộng đồng |
|-----------|-----------|--------|----|------------|---------|-----------|
| **Axum**  | ★★★★☆    | ★★★☆  | ★★★★ | Tower (chuẩn) | Dễ mock router | Rất tích cực |
| **Actix** | ★★★★★    | ★★★   | ★★★ | actix-* | Hỗ trợ tốt | Rất lớn |
| **Rocket**| ★★★       | ★★☆   | ★★★★ | Built-in | Ổn | Vừa |
| **Warp**  | ★★★★      | ★★★   | ★★☆ | Filters | Ổn | Vừa |

---

## 6. Kết luận
Trong cuốn sách này, ta chọn **Axum** vì:

- Dễ học & typed safety tốt.  
- Hệ sinh thái Tower chuẩn, dễ ghép thư viện ngoài.  
- Cộng đồng đang tăng trưởng nhanh.  

Tuy nhiên, nếu bạn đã có kinh nghiệm hoặc nhu cầu đặc thù, Actix, Rocket, hay Warp đều vẫn là lựa chọn hợp lệ.

# Pattern Matching

---

## Kiến thức quan trọng về Pattern Matching trong Rust dành cho học Axum

### 1. Khái niệm Pattern Matching
- Pattern Matching là một kỹ thuật mạnh mẽ giúp kiểm tra và trích xuất giá trị theo cấu trúc của kiểu dữ liệu.
- Được sử dụng thường xuyên với match, if let, while let và destructuring (phá vỡ cấu trúc).

### 2. Cú pháp cơ bản với match
```rust
let x = 5;
match x {
    1 => println!("x là 1"),
    2 | 3 | 4 => println!("x là 2, 3 hoặc 4"),
    5..=10 => println!("x thuộc đoạn 5 đến 10"),
    _ => println!("x khác các giá trị trên"),
}
```

### 3. Sử dụng với Option, Result
```rust
let value = Some(10);
match value {
    Some(v) => println!("Có giá trị: {}", v),
    None => println!("Không có giá trị"),
}

let res: Result<i32, &str> = Ok(30);
match res {
    Ok(val) => println!("Thành công: {}", val),
    Err(e) => println!("Lỗi: {}", e),
}
```

### 4. Destructuring Struct, Enum
```rust
struct Point {x: i32, y: i32}
let p = Point { x: 1, y: 2 };
let Point { x, y } = p;
println!("x: {}, y: {}", x, y);

enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
}
let msg = Message::Move { x: 10, y: 20 };
match msg {
    Message::Move { x, y } => println!("Di chuyển tới ({}, {})", x, y),
    _ => ()
}
```

### 5. if let, while let
```rust
let some_val = Some(8);
if let Some(v) = some_val {
    println!("Giá trị: {}", v);
}
```

### 6. Ứng dụng trong Axum
- Nhận dữ liệu từ Request, trích xuất dữ liệu từ body/query/path sử dụng destructuring và match để xử lý logic đa dạng, hiệu quả.
- Bắt lỗi (error handling) với match cho Result khi thao tác async (ví dụ: truy vấn DB, gọi API).
---

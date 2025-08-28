## Struct & Enum trong Rust

### 1. Struct là gì?
- Struct là kiểu dữ liệu cho phép gom nhiều giá trị có liên quan thành một kiểu mới.
- Định nghĩa struct:
```rust
struct User {
    username: String,
    email: String,
    active: bool,
}
```
- Khởi tạo và truy cập giá trị:
```rust
let user1 = User {
    username: String::from("alice"),
    email: String::from("alice@email.com"),
    active: true,
};
println!("{}", user1.username);
```
#### Tuple struct và unit-like struct
- Tuple struct giống như tuple, nhưng đặt tên:
```rust
struct Color(i32, i32, i32);
let black = Color(0, 0, 0);
```
- Unit-like struct: không có trường nào, dùng cho pattern marker.
```rust
struct Marker;
```

### 2. Enum là gì?
- Enum cho phép khai báo nhiều biến thể (variant) khác nhau của cùng một kiểu.
- Định nghĩa enum:
```rust
enum Direction {
    Left,
    Right,
    Up,
    Down,
}
```
- Sử dụng match với enum:
```rust
fn print_dir(dir: Direction) {
    match dir {
        Direction::Left => println!("Left"),
        Direction::Right => println!("Right"),
        _ => println!("Other"),
    }
}
```
#### Enum chứa dữ liệu (variant with data)
- Enum có thể chứa dữ liệu riêng cho từng biến thể:
```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
}
```
- Một số enum phổ biến trong Rust:
  - `Option<T>`: biểu diễn giá trị có hoặc không.
  - `Result<T, E>`: kết quả thành công hoặc lỗi.

### 3. Khi nào dùng struct, khi nào dùng enum?
- Dùng **struct** khi muốn gom nhóm nhiều trường dữ liệu cố định.
- Dùng **enum** khi các trường hợp logic khác nhau, có thể kèm dữ liệu hoặc không.

### 4. Lợi ích cho lập trình Rust và Axum
- Giúp biểu diễn dữ liệu linh hoạt và an toàn.
- Phối hợp với pattern matching để kiểm soát luồng logic.
- Chuẩn bị cho Axum: thường dùng struct để làm request/response, enum để xử lý các trường hợp đặc biệt hoặc trạng thái.

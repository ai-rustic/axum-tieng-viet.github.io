# Ownership và Borrowing

## 1. Khái niệm về Ownership trong Rust

Ownership là một trong những khái niệm cốt lõi của Rust, giúp quản lý bộ nhớ một cách an toàn mà không cần garbage collector.

### Quy tắc cơ bản:
- Mỗi giá trị trong Rust chỉ có **một owner** duy nhất
- Khi owner ra khỏi scope, giá trị sẽ bị **drop** (giải phóng bộ nhớ)
- Không thể có hai owner cùng sở hữu một giá trị

### Ví dụ minh họa:

```rust
fn main() {
    let s1 = String::from("Hello"); // s1 là owner của String
    
    { // Scope mới bắt đầu
        let s2 = String::from("World"); // s2 là owner
        println!("{}", s2); // "World"
    } // s2 ra khỏi scope, String "World" bị drop
    
    println!("{}", s1); // Vẫn hoạt động vì s1 còn trong scope
} // s1 ra khỏi scope, String "Hello" bị drop
```

## 2. Chuyển giao (Move) và Sao chép (Copy)

### Move Semantics:
Khi gán giá trị cho biến khác, ownership được **chuyển giao** (move):

```rust
fn main() {
    let s1 = String::from("Hello");
    let s2 = s1; // Ownership chuyển từ s1 sang s2
    
    // println!("{}", s1); // Lỗi! s1 không còn hợp lệ
    println!("{}", s2); // OK
}
```

### Copy Trait:
Các kiểu dữ liệu đơn giản được **sao chép** thay vì move:

```rust
fn main() {
    let x = 5;
    let y = x; // Copy, không phải move
    
    println!("x = {}, y = {}", x, y); // Cả hai đều hợp lệ
}
```

**Các kiểu Copy:** integers, floats, booleans, char, tuples (nếu các phần tử đều Copy)

**Các kiểu Move:** String, Vec, HashMap, structs tùy chỉnh (mặc định)

## 3. Mượn (Borrowing)

Borrowing cho phép sử dụng giá trị mà không cần sở hữu nó thông qua **references**.

### Immutable Reference (&):

```rust
fn main() {
    let s1 = String::from("Hello");
    let len = calculate_length(&s1); // Mượn s1
    
    println!("Độ dài của '{}' là {}", s1, len); // s1 vẫn hợp lệ
}

fn calculate_length(s: &String) -> usize {
    s.len() // Có thể đọc nhưng không thể thay đổi
}
```

### Mutable Reference (&mut):

```rust
fn main() {
    let mut s = String::from("Hello");
    change(&mut s); // Mượn có thể thay đổi
    
    println!("{}", s); // "Hello, world"
}

fn change(s: &mut String) {
    s.push_str(", world");
}
```

## 4. Quy tắc về Borrowing

Borrow checker của Rust thực thi các quy tắc nghiêm ngặt:

### Quy tắc chính:
1. **Tại một thời điểm**, chỉ có thể có:
   - **Một** mutable reference, HOẶC
   - **Nhiều** immutable references
2. **Không thể** đồng thời có cả mutable và immutable references
3. References phải **luôn hợp lệ**

### Ví dụ vi phạm quy tắc:

```rust
fn main() {
    let mut s = String::from("Hello");
    
    let r1 = &s;        // OK - immutable reference
    let r2 = &s;        // OK - nhiều immutable references
    let r3 = &mut s;    // LỖI! Không thể có mutable khi đã có immutable
    
    println!("{}, {}, {}", r1, r2, r3);
}
```

### Ví dụ đúng quy tắc:

```rust
fn main() {
    let mut s = String::from("Hello");
    
    {
        let r1 = &s;
        let r2 = &s;
        println!("{} and {}", r1, r2);
        // r1 và r2 ra khỏi scope
    }
    
    let r3 = &mut s; // OK - không còn immutable references
    println!("{}", r3);
}
```

## 5. Lợi ích và Ý nghĩa

### Memory Safety:
- **Không có garbage collector** nhưng vẫn an toàn bộ nhớ
- **Tự động giải phóng bộ nhớ** khi ra khỏi scope
- **Zero-cost abstractions** - không tốn thêm runtime overhead

### Ngăn chặn lỗi thường gặp:

#### Use After Free:
```rust
// Rust ngăn chặn lỗi này tại compile time
fn main() {
    let s1 = String::from("Hello");
    let s2 = s1; // s1 moved
    // println!("{}", s1); // Compile error!
}
```

#### Data Races:
```rust
// Rust ngăn chặn data race thông qua borrow checker
use std::thread;

fn main() {
    let mut data = vec![1, 2, 3];
    
    // Không thể có multiple mutable references
    // cho cùng một data trong threads khác nhau
    thread::spawn(move || {
        data.push(4); // data moved vào thread này
    });
    
    // data.push(5); // Compile error! data đã moved
}
```

### Hiệu suất:
- **Zero-cost**: Ownership và borrowing checking chỉ diễn ra tại compile time
- **Predictable performance**: Không có pause do garbage collection
- **Fine-grained control**: Kiểm soát chính xác việc cấp phát và giải phóng bộ nhớ

## Tóm tắt

Ownership và Borrowing trong Rust cung cấp:
- **Memory safety** mà không cần garbage collector
- **Thread safety** thông qua compile-time checks
- **Zero runtime cost** cho memory management
- **Ngăn chặn** use-after-free, double-free, data races
- **Kiểm soát chính xác** lifecycle của dữ liệu

Đây là nền tảng giúp Rust trở thành ngôn ngữ "fast, safe, concurrent" - nhanh, an toàn và hỗ trợ đồng thời hiệu quả.

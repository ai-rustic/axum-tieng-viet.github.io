# Traits và Generics trong Rust cho Axum

Khi học Axum, hai khái niệm quan trọng nhất trong Rust mà bạn cần nắm vững là **Traits** và **Generics**. Chúng là nền tảng để hiểu cách Axum hoạt động và viết code hiệu quả.

## Traits - Đặc tính (Interface)

### Khái niệm
Traits trong Rust tương tự như interfaces trong các ngôn ngữ khác. Chúng định nghĩa một tập hợp các phương thức mà một kiểu dữ liệu có thể triển khai.

### Tại sao Traits và Generics quan trọng trong Axum?

1. **Type Safety**: Rust's type system đảm bảo code an toàn tại compile time
2. **Code Reusability**: Generics giúp viết code tái sử dụng cho nhiều kiểu dữ liệu
3. **Abstraction**: Traits cho phép abstract hóa behavior mà không cần biết concrete type
4. **Performance**: Zero-cost abstractions - không có overhead runtime
5. **Axum's Design**: Toàn bộ Axum được xây dựng trên traits và generics

### Cú pháp cơ bản
```rust
trait TenTrait {
    fn phuong_thuc(&self);
    fn phuong_thuc_co_gia_tri_mac_dinh(&self) {
        println!("Triển khai mặc định");
    }
}
```

### Ví dụ thực tế với Axum - Handler Trait

Trong Axum, mọi handler function đều phải implement trait `Handler`. Đây là cách Axum biết một function có thể xử lý HTTP request:

```rust
use axum::{
    extract::{Query, Path},
    response::Json,
    http::StatusCode,
};
use serde::{Deserialize, Serialize};
use std::collections::HashMap;

// Trait tùy chỉnh để xử lý business logic
trait UserService {
    fn get_user(&self, id: u32) -> Option<User>;
    fn create_user(&self, user: CreateUserRequest) -> Result<User, String>;
}

#[derive(Serialize, Deserialize, Clone)]
struct User {
    id: u32,
    name: String,
    email: String,
}

#[derive(Deserialize)]
struct CreateUserRequest {
    name: String,
    email: String,
}

// Triển khai trait cho struct cụ thể
struct DatabaseUserService;

impl UserService for DatabaseUserService {
    fn get_user(&self, id: u32) -> Option<User> {
        // Giả lập truy vấn database
        Some(User {
            id,
            name: "John Doe".to_string(),
            email: "john@example.com".to_string(),
        })
    }
    
    fn create_user(&self, user: CreateUserRequest) -> Result<User, String> {
        // Giả lập tạo user mới
        Ok(User {
            id: 1,
            name: user.name,
            email: user.email,
        })
    }
}

// Handler functions - Axum tự động implement Handler trait cho chúng
async fn get_user_handler(
    Path(user_id): Path<u32>,
) -> Result<Json<User>, StatusCode> {
    let service = DatabaseUserService;
    match service.get_user(user_id) {
        Some(user) => Ok(Json(user)),
        None => Err(StatusCode::NOT_FOUND),
    }
}

async fn create_user_handler(
    Json(payload): Json<CreateUserRequest>,
) -> Result<Json<User>, StatusCode> {
    let service = DatabaseUserService;
    match service.create_user(payload) {
        Ok(user) => Ok(Json(user)),
        Err(_) => Err(StatusCode::BAD_REQUEST),
    }
}
```

### Trait Bounds - Ràng buộc Trait

Trong Axum, bạn thường thấy trait bounds để đảm bảo kiểu dữ liệu có những đặc tính cần thiết:

```rust
use axum::extract::FromRequest;
use serde::de::DeserializeOwned;

// Function generic với trait bounds
fn process_json_data<T>() -> impl Handler<(), ()>
where
    T: DeserializeOwned + Send + 'static,
{
    |Json(payload): Json<T>| async move {
        // Xử lý dữ liệu JSON
        "Processed successfully"
    }
}
```

## Generics - Kiểu dữ liệu tổng quát

### Khái niệm
Generics cho phép bạn viết code hoạt động với nhiều kiểu dữ liệu khác nhau mà không cần lặp lại code.

### Cú pháp cơ bản
```rust
// Function generic
fn function_name<T>(param: T) -> T {
    param
}

// Struct generic
struct StructName<T> {
    field: T,
}

// Enum generic
enum EnumName<T> {
    Variant(T),
}
```

### Ví dụ thực tế với Axum - Generic Response Handler

```rust
use axum::{
    extract::{Path, Query, State},
    response::Json,
    http::StatusCode,
};
use serde::{Deserialize, Serialize};
use std::sync::Arc;

// Generic Repository pattern - hoạt động với nhiều kiểu entity
trait Repository<T> {
    async fn find_by_id(&self, id: u32) -> Option<T>;
    async fn find_all(&self) -> Vec<T>;
    async fn create(&self, entity: T) -> Result<T, String>;
    async fn update(&self, id: u32, entity: T) -> Result<T, String>;
    async fn delete(&self, id: u32) -> Result<(), String>;
}

// Generic struct cho pagination
#[derive(Serialize, Deserialize)]
struct PaginatedResponse<T> {
    data: Vec<T>,
    total: usize,
    page: usize,
    per_page: usize,
}

#[derive(Deserialize)]
struct PaginationParams {
    page: Option<usize>,
    per_page: Option<usize>,
}

// Generic handler cho việc lấy danh sách có phân trang
async fn get_paginated_list<T, R>(
    Query(params): Query<PaginationParams>,
    State(repository): State<Arc<R>>,
) -> Result<Json<PaginatedResponse<T>>, StatusCode>
where
    T: Serialize + Send,
    R: Repository<T> + Send + Sync,
{
    let page = params.page.unwrap_or(1);
    let per_page = params.per_page.unwrap_or(10);
    
    let all_items = repository.find_all().await;
    let total = all_items.len();
    
    // Tính toán pagination
    let start = (page - 1) * per_page;
    let end = std::cmp::min(start + per_page, total);
    let data = all_items.into_iter().skip(start).take(per_page).collect();
    
    Ok(Json(PaginatedResponse {
        data,
        total,
        page,
        per_page,
    }))
}

// Generic error handler
#[derive(Serialize)]
struct ApiError<T> {
    message: String,
    details: Option<T>,
    code: u16,
}

impl<T> ApiError<T> {
    fn new(message: &str, code: u16, details: Option<T>) -> Self {
        Self {
            message: message.to_string(),
            details,
            code,
        }
    }
}

// Generic result type cho API
type ApiResult<T, E = String> = Result<Json<T>, (StatusCode, Json<ApiError<E>>)>;

// Generic handler với custom error handling
async fn get_item_by_id<T, R, E>(
    Path(id): Path<u32>,
    State(repository): State<Arc<R>>,
) -> ApiResult<T, E>
where
    T: Serialize + Send,
    R: Repository<T> + Send + Sync,
    E: Serialize + Send,
{
    match repository.find_by_id(id).await {
        Some(item) => Ok(Json(item)),
        None => Err((
            StatusCode::NOT_FOUND,
            Json(ApiError::new("Item not found", 404, None)),
        )),
    }
}
```

### Generics với Extractors trong Axum

Axum sử dụng generics rất nhiều trong các extractors:

```rust
use axum::extract::{Json, Query, Path};
use serde::{Deserialize, Serialize};

// Generic extractor cho query parameters
#[derive(Deserialize)]
struct SearchParams<T> {
    query: String,
    filters: Option<T>,
    sort_by: Option<String>,
}

#[derive(Deserialize)]
struct ProductFilters {
    category: Option<String>,
    min_price: Option<f64>,
    max_price: Option<f64>,
}

#[derive(Serialize)]
struct Product {
    id: u32,
    name: String,
    price: f64,
    category: String,
}

// Handler sử dụng generic extractor
async fn search_products(
    Query(params): Query<SearchParams<ProductFilters>>,
) -> Json<Vec<Product>> {
    // Logic tìm kiếm sản phẩm
    let products = vec![
        Product {
            id: 1,
            name: "Laptop".to_string(),
            price: 999.99,
            category: "Electronics".to_string(),
        },
    ];
    
    Json(products)
}

// Generic validation function
use validator::Validate;

fn validate_and_extract<T>(json: Json<T>) -> Result<T, ValidationError>
where
    T: Validate,
{
    json.validate()?;
    Ok(json.0)
}
```

## Kết hợp Traits và Generics trong Axum

### Service Layer Pattern với Traits và Generics

```rust
use async_trait::async_trait;
use axum::{
    extract::State,
    response::Json,
    http::StatusCode,
};
use std::sync::Arc;
use serde::{Serialize, Deserialize};

// Generic trait cho service layer
#[async_trait]
trait Service<T, CreateDto, UpdateDto> {
    type Error;
    
    async fn get_all(&self) -> Result<Vec<T>, Self::Error>;
    async fn get_by_id(&self, id: u32) -> Result<Option<T>, Self::Error>;
    async fn create(&self, dto: CreateDto) -> Result<T, Self::Error>;
    async fn update(&self, id: u32, dto: UpdateDto) -> Result<T, Self::Error>;
    async fn delete(&self, id: u32) -> Result<(), Self::Error>;
}

// Generic handler factory
fn create_crud_handlers<T, CreateDto, UpdateDto, S>()
where
    T: Serialize + Send + 'static,
    CreateDto: for<'de> Deserialize<'de> + Send + 'static,
    UpdateDto: for<'de> Deserialize<'de> + Send + 'static,
    S: Service<T, CreateDto, UpdateDto> + Send + Sync + 'static,
    S::Error: std::fmt::Display,
{
    // Tạo các handler cho CRUD operations
}

// Middleware generic cho logging
use tower::{Service as TowerService, ServiceExt};
use axum::middleware::Next;
use axum::extract::Request;

async fn logging_middleware<B>(
    request: Request<B>,
    next: Next<B>,
) -> axum::response::Response {
    let method = request.method().clone();
    let uri = request.uri().clone();
    
    println!("Request: {} {}", method, uri);
    
    let response = next.run(request).await;
    
    println!("Response status: {}", response.status());
    
    response
}
```
---

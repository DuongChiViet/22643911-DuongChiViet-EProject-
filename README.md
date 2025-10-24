# 🧩 Microservices E-Commerce Platform

### 🐳 Node.js | 🐇 RabbitMQ | 🔐 JWT | 🚪 API Gateway | 🧱 MongoDB

---

## 🚀 Giới thiệu

Dự án minh họa cách xây dựng **hệ thống thương mại điện tử (E-commerce)** theo **kiến trúc Microservices**, trong đó các chức năng chính được tách thành các service độc lập:

* 👤 **Auth Service:** Quản lý người dùng, đăng ký/đăng nhập & JWT
* 🛍️ **Product Service:** Quản lý sản phẩm & tồn kho
* 🧾 **Order Service:** Quản lý đơn hàng & cập nhật tồn kho qua RabbitMQ
* 🚪 **API Gateway:** Cổng duy nhất nhận và định tuyến request

Hệ thống vận hành trên Docker, sử dụng RabbitMQ để giao tiếp bất đồng bộ giữa các service.

---

## ⚙️ 1. Cài đặt RabbitMQ trên Docker

Chạy lệnh sau để khởi tạo RabbitMQ:

```shell
docker-compose up
```

🔗 Truy cập: [http://localhost:15672](http://localhost:15672/)  
👤 Tài khoản: `guest` / `guest`

📸 **Giao diện quản lý RabbitMQ**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/rabitmq.jpg" alt="RabbitMQ Setup" width="800"/>

---

## 🧱 2. Khởi tạo các Container

📸 **Tất cả các Container đang chạy**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/allcontainer.jpg" alt="All Containers" width="800"/>

---

## 🌐 3. Cấu hình API Gateway

Cập nhật file cấu hình để định tuyến đến đúng các service (Auth, Product, Order).

📸 **Cấu hình API Gateway**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/cauhinhapi-gateway.jpg" alt="Config API Gateway" width="800"/>

---

## 🔑 4. Tạo JWT khi đăng nhập

Thêm logic ký **JWT Token** trong Auth Service để xác thực người dùng.

📸 **Logic tạo JWT**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/taojwt.jpg" alt="JWT Logic" width="800"/>

---

## 🧪 5. Kiểm thử API với Postman

### 🧍‍♂️ Đăng ký tài khoản

`POST /auth/api/v1/register`

📸 **Kiểm thử đăng ký**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/kiem-thu-dang-ky.jpg" alt="Register Test" width="800"/>

📦 **Kết quả trong MongoDB sau khi đăng ký:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/kiem-tra-mongo-sau-khi-dang-ky.jpg" alt="MongoDB Register Result" width="800"/>

📸 **Minh chứng test đăng ký trên Docker:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/minh-chung-test-dang-ky-tren-docker.jpg" alt="Docker Register Test" width="800"/>

---

### 🔐 Đăng nhập tài khoản

`POST /auth/api/v1/login`

📸 **Kiểm tra đăng nhập và lấy token**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/kiem-tra-dang-nhap-lay-token.jpg" alt="Login Test" width="800"/>

✅ Nhận **JWT Token**

---

### 🛒 Thêm sản phẩm

`POST /products/api/v1/products/add`

Truyền token vào header:
```
Authorization: Bearer <JWT_TOKEN>
```

📸 **Kiểm thử thêm sản phẩm:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/kiem-thu-them-san-pham.jpg" alt="Add Product Test" width="800"/>

� **Truyền token và thêm thành công sản phẩm:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/truyen-token-va-them-thanh-cong-san-pham.jpg" alt="Add Product Success" width="800"/>

📦 **Kết quả trong MongoDB sau khi thêm sản phẩm:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/ket-qua-mongo-sau-khi-them-san-pham.jpg" alt="MongoDB Product Result" width="800"/>

---

### 🧾 Mua sản phẩm (Tạo đơn hàng)

`POST /products/api/v1/buy`

Truyền `ids` và `quantity` trong body.

📸 **Kiểm thử mua sản phẩm:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/kiem-thu-mua-san-pham.jpg" alt="Buy Product Test" width="800"/>

✅ **Kết quả sau khi mua sản phẩm thành công:**  
<img src="https://raw.githubusercontent.com/DuongChiViet/22643911-DuongChiViet-EProject-/main/public/img/ket-qua-sau-khi-mua-san-pham.jpg" alt="Buy Product Result" width="800"/>

---

## 🧠 Tổng kết hệ thống

### 💡 1. Hệ thống giải quyết vấn đề gì?

Giải quyết bài toán **E-commerce**, với 3 module chính: **Auth**, **Product**, **Order**.

---

### 🧩 2. Gồm bao nhiêu dịch vụ?

Tổng cộng **6 dịch vụ**:

* **Ứng dụng:** `viet_api_gateway`, `viet_auth_service`, `viet_product_service`, `viet_order_service`
* **Hạ tầng:** `viet_mongodb`, `viet_rabbitmq`

---

### 🧰 3. Ý nghĩa từng dịch vụ

| Dịch vụ | Vai trò |
|---------|---------|
| 🗄️ `viet_mongodb` | Lưu dữ liệu (User, Product, Order) |
| 🐇 `viet_rabbitmq` | Hàng đợi tin nhắn bất đồng bộ |
| 🚪 `viet_api_gateway` | Cổng định tuyến request |
| 👤 `viet_auth_service` | Xử lý đăng ký, đăng nhập, JWT |
| 🛍️ `viet_product_service` | Quản lý sản phẩm & tồn kho |
| 🧾 `viet_order_service` | Xử lý đơn hàng & sự kiện qua RabbitMQ |

---

### 🧠 4. Mẫu thiết kế sử dụng

* 🧩 **Microservices Architecture**
* 🚪 **API Gateway Pattern**
* 🗃️ **Database per Service**
* 📬 **Event-Driven / Pub-Sub (RabbitMQ)**

---

### 🔄 5. Giao tiếp giữa các service

* **Đồng bộ (HTTP):** `Client → API Gateway → Service`
* **Bất đồng bộ (RabbitMQ):** `Order Service → RabbitMQ → Product Service`

---

## 🌟 Kết luận

✅ Hệ thống microservices hoạt động ổn định với giao tiếp đồng bộ & bất đồng bộ.  
✅ RabbitMQ giúp tách biệt service, tăng khả năng mở rộng và chịu lỗi.  
✅ API Gateway & JWT bảo mật luồng giao tiếp giữa client và backend.

---

## � Hướng dẫn chạy dự án

### Yêu cầu hệ thống
- Docker & Docker Compose
- Node.js (v14+)
- MongoDB
- RabbitMQ

### Các bước thực hiện

1. **Clone repository**
```bash
git clone https://github.com/DuongChiViet/22643911-DuongChiViet-EProject-.git
cd 22643911-DuongChiViet-EProject-
```

2. **Tạo file .env** (nếu chưa có)
```env
MONGODB_AUTH_URI=mongodb://duongchiviet:123456@viet_mongodb:27017/AuthService?authSource=admin
JWT_SECRET=yourSecretKey
MONGODB_PRODUCT_URI=mongodb://duongchiviet:123456@viet_mongodb:27017/ProductService?authSource=admin
MONGODB_ORDER_URI=mongodb://duongchiviet:123456@viet_mongodb:27017/OrderService?authSource=admin
```

3. **Khởi động tất cả services**
```bash
docker-compose up --build
```

4. **Truy cập các service**
- API Gateway: http://localhost:3003
- Auth Service: http://localhost:3000
- Product Service: http://localhost:3001
- Order Service: http://localhost:3002
- RabbitMQ Management: http://localhost:15672 (guest/guest)

---

> 💻 **Tác giả:** DƯƠNG CHÍ VIỆT  
> 📅 **Cập nhật lần cuối:** 2025-10-24  
> 🎓 **MSSV:** 22643911  
> 📦 **GitHub:** [https://github.com/DuongChiViet/22643911-DuongChiViet-EProject-](https://github.com/DuongChiViet/22643911-DuongChiViet-EProject-)

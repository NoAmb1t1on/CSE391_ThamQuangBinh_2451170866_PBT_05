# PBT_05:
---
## Phần A:
### Câu A1(13_creating_responsive_layouts.md - 3. ⚙️ Core Technical Truth - 1. Viewport Meta Tag & 2. Mobile-First vs Desktop-First):
1. Thẻ html:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- `width=device-width`: Chiều rộng trang bằng chiều rộng thiết bị.
- `initial-scale=1.0`: Tỷ lệ thu phóng ban đầu là 100%.
2. Thiếu thẻ này: iPhone tự hiểu là màn hình desktop (980px) và tự động thu nhỏ (zoom out) toàn bộ trang web lại khiến chữ và hình ảnh rất nhỏ.
3. Sự khác nhau giữa Mobile-First và Desktop-First:
  - Mobile-First: Code màn hình nhỏ trước, dùng min-width tăng dần cho màn hình lớn.
  - Desktop-First: Code màn hình lớn trước, dùng max-width giảm dần cho màn hình nhỏ.
- Mobile-First:
```css
.sidebar {
  display: none;
}
@media (min-width: 768px) {
  .sidebar {
    display: block;
  }
}
```
- Desktop-First:
```css
.sidebar {
  display: none;
}
@media (min-width: 768px) {
  .sidebar {
    display: block;
  }
}
```
- Mobile-First được khuyên dùng vì: Tối ưu hiệu năng cho máy cấu hình yếu/mạng chậm, tập trung nội dung cốt lõi và tránh ghi đè CSS chồng chéo.

### Câu A2(13_creating_responsive_layouts.md - 3. ⚙️ Core Technical Truth - 3. Breakpoints tiêu chuẩn):

| Kích thước | Thiết bị | Số cột lưới sản phẩm |
|------------|----------|----------------------|
| 576px | Điện thoại | 1 cột |
| 576px | Điện thoại ngang | 2 cột |
| 768px | Máy tính bảng | 3 cột |
| 992px | Laptop nhỏ | 4 cột |
|1200px | Desktop lớn | 4 hoặc 6 cột |

### Câu A3(13_creating_responsive_layouts.md - 3. ⚙️ Core Technical Truth - 4. Áp dụng Media Queries thực tế): 

| Chiều rộng màn hình |	.container width |
|---------------------|------------------|
| 375px |	100% |
| 600px | 540px |
| 800px |	720px |
| 1000px | 960px |
| 1400px | 1140px |

### Câu A4(16_sass_scss.md - 3. ⚙️ Core Technical Truth):
1. Variables: Lưu giá trị vào biến để tái sử dụng.
```scss
$primary-color: #3498db;
button { background-color: $primary-color; }
```
2. Nesting: Viết CSS lồng nhau theo cấu trúc HTML.
```scss
nav {
  ul {
    li { display: inline-block; }
  }
}
```
3. Mixins: Định nghĩa khối CSS dùng nhiều lần, có tham số.
```scss
@mixin flex-center($dir) {
  display: flex; justify-content: center; align-items: center; flex-direction: $dir;
}
.box { @include flex-center(row); }
```
4. @extend: Kế thừa lại toàn bộ thuộc tính của một bộ chọn khác.
```scss
.msg { border: 1px solid; padding: 10px; }
.err { @extend .msg; color: red; }
```
- Trình duyệt không đọc được file `.scss` là vì: Trình duyệt chỉ hiểu cú pháp CSS chuẩn, không có bộ dịch cú pháp nâng cao của SCSS. Cần dùng công cụ biên dịch (Sass Compiler, Live Sass) để chuyển .scss thành .css.
---
## Phần C:
### Câu C1:
1. ScreenShots:
- Mobile(375px):

<img width="795" height="909" alt="image" src="https://github.com/user-attachments/assets/30eb022a-e573-487b-b447-9a850fe1bb5c" />

- Tablet(768px):

<img width="1165" height="915" alt="image" src="https://github.com/user-attachments/assets/fd41f36e-11bc-4bc4-ba1c-71c4b8f815b8" />

- Desktop(1440px):

<img width="1338" height="915" alt="image" src="https://github.com/user-attachments/assets/50a22f3c-4e85-4530-91fc-adbc351d1985" />

2. Phân tích:
- **Navigation (Thanh điều hướng):**
    * **Mobile (375px) & Tablet (768px):** Thanh tìm kiếm (Search bar), logo Shopee, giỏ hàng và thanh menu phụ phía trên giữ nguyên bố cục dàn ngang cố định. Shopee chọn cách thu nhỏ tỷ lệ hiển thị toàn trang (zoom out nhẹ) thay vì chuyển đổi sang menu dạng Hamburger để giữ nguyên trải nghiệm tìm kiếm cốt lõi.
    * **Desktop (1440px):** Khoảng trống hai bên được nới rộng ra (nằm trong container cố định), thanh tìm kiếm dài hơn, giúp giao diện thoáng và dễ thao tác hơn bằng chuột.

* **Lưới content (Content Grid):**
    * **Mobile (375px):** Dàn lưới danh mục sản phẩm hiển thị **10 cột** (chia làm 2 hàng, mỗi hàng 10 ô nhỏ, người dùng vuốt ngang để xem tiếp). Lưới sản phẩm Flash Sale hiển thị **6 cột** sản phẩm trọn vẹn trong khung nhìn.
    * **Tablet (768px):** Do không đổi breakpoint linh hoạt mà chỉ tăng chiều rộng hiển thị, lưới danh mục sản phẩm giãn rộng ra nhưng vẫn giữ nguyên cấu trúc **10 cột**, lưới Flash Sale hiển thị rõ các sản phẩm lớn hơn.
    * **Desktop (1440px):** Các ô danh mục và sản phẩm đạt kích thước chuẩn, hiển thị **10 cột** danh mục và tối ưu không gian hiển thị rộng theo chiều ngang.

* **Elements bị ẩn trên mobile:**
    * Giao diện máy tính của Shopee bản web không ẩn đi phần tử nào đáng kể khi xuống Mobile/Tablet mà giữ nguyên cấu trúc (chỉ thu nhỏ tỷ lệ các banner quảng cáo chạy slide phía trên). Nút chat tích hợp góc dưới bên phải được giữ lại trên tất cả các màn hình.

* **Font size (Kích thước chữ):**
    * Font size hệ thống không tự động thay đổi (re-scale) độc lập thông qua media queries, mà toàn bộ chữ, icon, và hình ảnh tự động thu nhỏ lại theo tỷ lệ chiều rộng màn hình thiết bị do cơ chế layout đặc thù của Shopee bản PC khi xem trên trình duyệt di động.

3. Các media:

<img width="1912" height="171" alt="image" src="https://github.com/user-attachments/assets/a33d0034-5b95-4b6b-850b-8b8dc7a7116e" />

<img width="1917" height="721" alt="image" src="https://github.com/user-attachments/assets/b107842e-4f96-459e-ad5f-2f94d6e02078" />

### Câu C2:
1. Thiết kế Wireframe cấu trúc layout:
- Mobile (375px):
  - Bố cục: Xếp dọc 1 cột từ trên xuống dưới.
  - Vị trí: Header (Logo + Icon gọi điện) -> Hero Image (Chiều cao thu nhỏ) -> Grid ảnh món ăn (1 cột dọc) -> Form đặt bàn -> Google Maps -> Footer.
    - Phần tử ẩn: Ẩn bớt các đoạn văn mô tả dài của Hero, số điện thoại dạng chữ chuyển thành nút bấm gọi nhanh.
- Tablet (768px): Bố cục: Chuyển đổi lưới.
  - Vị trí: Grid ảnh món ăn chuyển thành 2 cột x 3 hàng. Khối Form đặt bàn và Bản đồ Google Maps chia đôi nằm song song nhau (mỗi bên chiếm 50% chiều rộng).
- Desktop (1440px):
  - Bố cục: Cấu trúc đa cột có container giới hạn độ rộng (`max-width: 1200px`).
  - Vị trí: Grid ảnh món ăn hiển thị 3 cột x 2 hàng. Phần thân dưới chia làm 2 cột lớn: Bên trái (70%) là Form đặt bàn + Bản đồ xếp dọc; Bên phải (30 làm Sidebar) hiển thị thông tin ưu đãi hoặc giờ mở cửa.
 
2. CSS Skeleton (Mobile-First Layout)
```css
.wrapper {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

.header { display: flex; justify-content: space-between; }
.hero { height: 300px; }
.dish-grid { display: grid; grid-template-columns: 1fr; gap: 10px; }
.booking-form { width: 100%; }
.map { width: 100%; height: 250px; }
.sidebar { display: none; }
.footer { text-align: center; }

@media (min-width: 768px) {
  .dish-grid { grid-template-columns: repeat(2, 1fr); }
  .bottom-section { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
}

@media (min-width: 1200px) {
  .wrapper { max-width: 1200px; margin: 0 auto; }
  .dish-grid { grid-template-columns: repeat(3, 1fr); }
  .main-content { display: grid; grid-template-columns: 7fr 3fr; gap: 30px; }
  .sidebar { display: block; }
}
```
--- 
## Phần B
### Câu B3:
- Lệnh compile:
Bash
sass scss/style.scss css/style.css

# 📝 PROMPT LOG — Bài kiểm tra Giữa kỳ Thiết kế Web (Pure HTML & CSS)

---

## 1. Thông tin chung

| Mục | Chi tiết |
|---|---|
| **Họ và tên** | Nguyễn Tấn Điền |
| **MSSV** | 125000260 |
| **Trường / Khoa** | Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU) |
| **Đề tài** | **AutoPrestige Vietnam** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (Hạng Vừa, Hạng Sang, Siêu Xe Cao Cấp) |
| **Công cụ AI sử dụng** | Google Antigravity & Gemini |
| **Công nghệ xây dựng** | **100% Pure HTML5 & CSS3** (Tuyệt đối không dùng JavaScript hay thư viện script ngoài) |
| **GitHub Repository** | [https://github.com/NTanDien/Dien_NguyenTan_125000260.git](https://github.com/NTanDien/Dien_NguyenTan_125000260.git) |
| **Live Preview (GitHub Pages)** | [https://ntandien.github.io/Dien_NguyenTan_125000260/](https://ntandien.github.io/Dien_NguyenTan_125000260/) |

---

## 2. Yêu cầu ban đầu (System / Initial Prompt)

> **Prompt gửi cho AI:**
>
> Xây dựng một website hoàn chỉnh cho đề tài **"AutoPrestige Vietnam"** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc chuẩn HTML5 & CSS3 thuần:
>
> - **Semantic HTML5 nghiêm ngặt**: sử dụng đầy đủ các thẻ ngữ nghĩa `header`, `nav`, `main`, `section`, `article`, `figure`, `figcaption`, `aside`, `footer` (tuyệt đối không lạm dụng thẻ generic `div`).
> - **Công nghệ thuần HTML & CSS (No JavaScript)**:
>   + Toàn bộ tính năng tương tác (Menu di động, Bộ lọc phân khúc xe, Cửa sổ popup xem chi tiết từng mẫu xe) đều phải sử dụng các kỹ thuật CSS hiện đại (`:target`, `CSS Checkbox Hack`, `:checked ~ label`, `:has()`).
>   + Không sử dụng bất kỳ thẻ `<script>` hay file script JS nào.
> - **Hero Section nổi bật**: Tích hợp video chạy nền xe hơi thể thao đang lướt trên đường cao tốc (file MP4 lưu trực tiếp trong thư mục `assets/` của dự án), lớp phủ overlay gradient sang trọng cùng tiêu đề thu hút khách hàng.
> - **Showroom 12 mẫu xe phong phú**: Trải đều 3 phân khúc (Hạng Vừa & Gia Đình, Sedan & SUV Hạng Sang, Siêu Xe Cao Cấp). Mỗi xe có ảnh đại diện, giá bán niêm yết, thông số cốt lõi và nút bấm "Chi tiết" & "Lái thử".
> - **Cửa sổ xem chi tiết xe Pure CSS (`:target`)**: Bấm "Chi tiết" sẽ mở popup hiển thị bảng thông số kỹ thuật chuyên sâu (động cơ, mã lực, hộp số, gia tốc, vận tốc tối đa, mức tiêu hao, công nghệ an toàn...), có nút đóng bằng CSS.
> - **Bảng so sánh & Form đăng ký**: So sánh trực quan 3 phân khúc xe, form đặt lịch lái thử có hiệu ứng `:focus` nổi bật.
> - **Footer**: Ghi rõ thông tin sinh viên: Nguyễn Tấn Điền — MSSV: 125000260 — Khoa CNTT, Trường Đại học Lạc Hồng.

---

## 3. Quá trình tinh chỉnh & Giải quyết sự cố

### 🔧 Lần 1: Dựng khung Semantic HTML5 & Quản lý giao diện bằng CSS Variables `:root`

**Vấn đề nhận diện:**
Bản phác thảo ban đầu thường dùng quá nhiều thẻ `div` lồng nhau và mã màu CSS rời rạc, khó duy trì tính nhất quán cho một showroom xe sang.

**Prompt tinh chỉnh gửi AI:**
> Refactor toàn bộ HTML sang chuẩn Semantic:
> - Từng chiếc xe phải là thẻ `<article class="car-card">`.
> - Ảnh xe nằm trong `<figure>`, giá xe dùng `<figcaption>`.
> - Khu vực phân loại dùng `<nav>` và mẹo tư vấn chuyên gia dùng thẻ `<aside>`.
> - Quản lý toàn bộ màu sắc, typography, bo góc và bóng đổ tại `:root` trong `style.css` để đồng bộ phong cách dark luxury.

**Kết quả:**
- Cấu trúc trang web trong sáng, chuẩn SEO và ngữ nghĩa cao.
- Hệ thống biến `:root` giúp thay đổi màu chủ đạo, gradient và hiệu ứng hover đồng loạt một cách nhanh chóng.

---

### 🔧 Lần 2: Chuyển đổi 100% tính năng sang Pure CSS (Loại bỏ hoàn toàn JavaScript)

**Vấn đề nhận diện:**
Yêu cầu môn học chỉ cho phép sử dụng thuần HTML & CSS, không được dùng JavaScript. Các tính năng như: Hamburger Menu trên mobile, Bộ lọc phân khúc xe, và Popup xem chi tiết xe vốn dựa vào JS event listener cần được viết lại hoàn toàn bằng cơ chế CSS hiện đại.

**Prompt tinh chỉnh gửi AI:**
> Hãy xóa bỏ toàn bộ thẻ `<script>` và thư viện JS bên ngoài. Thay thế toàn bộ logic tương tác bằng Pure CSS:
> 1. **Menu di động (Hamburger Nav):** Sử dụng kỹ thuật *Checkbox Hack* (`input[type="checkbox"]` ẩn + `label` + `:checked ~ .nav-links`).
> 2. **Bộ lọc phân khúc xe (Showroom Filter):** Sử dụng các `input[type="radio"]` cho từng phân khúc kết hợp CSS `:has()` selector hiện đại (`.showroom:has(#filter-family:checked) .car-card:not([data-segment="family"]) { display: none; }`).
> 3. **Modal xem chi tiết 12 xe:** Sử dụng CSS pseudo-class `:target` (`.modal-target:target { opacity: 1; pointer-events: auto; }`) kết hợp liên kết thẻ `<a href="#id-xe">` và nút đóng `<a href="#showroom">`.

**Kết quả:**
- Trang web chạy **mượt mà 100% bằng HTML và CSS thuần**, tốc độ tải trang cực nhanh vì không phụ thuộc vào JS engine.
- Menu mobile bật tắt trơn tru, bộ lọc xe ẩn hiện tức thời, 12 modal xem chi tiết xe hoạt động hoàn hảo và đóng mở tự nhiên mà không cần một dòng code JavaScript nào.

---

## 4. Đánh giá cá nhân

### ✅ AI giúp tiết kiệm thời gian ở phần nào?

| Phần việc | Mức tiết kiệm | Ghi chú |
|---|---|---|
| Dựng khung HTML5 Semantic & Bảng thông số 12 xe | ⭐⭐⭐⭐⭐ | Tiết kiệm hàng giờ nhập liệu thủ công thông số kỹ thuật (động cơ, mã lực, hộp số, an toàn...) của 12 dòng xe. |
| Xây dựng cơ chế tương tác Pure CSS (`:target`, `:has()`, Checkbox Hack) | ⭐⭐⭐⭐⭐ | AI đề xuất ngay các cú pháp CSS hiện đại thay thế hoàn hảo cho JavaScript mà vẫn giữ trọn vẹn trải nghiệm người dùng. |
| Thiết kế bảng màu Dark Luxury & CSS Variables | ⭐⭐⭐⭐ | Phối màu neon accent (`#e94560`) trên nền tối (`#0f0f1a`) tạo cảm giác sang trọng đậm chất showroom xe hơi. |
| Responsive Layout không cần thư viện | ⭐⭐⭐⭐ | Tự động thích ứng trên mọi kích thước màn hình từ Desktop đến điện thoại chỉ với CSS Grid và Flexbox thuần. |

### 📖 Bài học rút ra khi prompt cho AI

1. **Hiểu rõ giới hạn công nghệ đề bài yêu cầu:** Nếu đề bài quy định "chỉ dùng HTML & CSS", cần nêu rõ ràng ngay từ đầu để AI định hướng giải pháp bằng CSS thuần (như `:target`, `:has()`, `:checked`), tránh việc tích hợp sẵn thư viện script bên ngoài.
2. **Khai thác tối đa sức mạnh của CSS3 hiện đại:** Rất nhiều tính năng tương tác người dùng hiện nay (Tabs, Modal, Dropdown, Menu) hoàn toàn có thể hiện thực hóa đẹp mắt bằng CSS mà không cần JavaScript.
3. **Prompt theo luồng kiến trúc (Structure -> Style -> Interaction):** Hướng dẫn AI từng bước sẽ cho ra mã nguồn sạch, dễ đọc và chuẩn chỉnh cho bài thi giữa kỳ.

---

> **Nguyễn Tấn Điền — MSSV: 125000260**
> Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU)
> Ngày thực hiện: 20/10/2026

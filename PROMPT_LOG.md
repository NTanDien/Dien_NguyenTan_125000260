# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)
- **Họ và tên:** Nguyễn Tấn Điền
- **MSSV:** 125000260
- **Tên đề tài Website:** AutoPrestige Vietnam — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (Từ Hạng Vừa, Hạng Sang đến Siêu Xe Cao Cấp)
- **Công cụ AI đã sử dụng:** Google Antigravity, Gemini, Claude

## 1. Yêu cầu ban đầu (System/Initial Prompt)
> "Hãy đóng vai trò là một Senior Front-end Developer và UI/UX Designer hàng đầu. Xây dựng một website hoàn chỉnh cho đề tài **AutoPrestige Vietnam** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (Hạng Vừa & Gia Đình, Sedan & SUV Hạng Sang, Siêu Xe Cao Cấp).
> 
> Yêu cầu kỹ thuật bắt buộc:
> 1. Chuẩn Semantic HTML5: Sử dụng đúng tối thiểu 5 thành phần `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>`, `<aside>`, `<footer>`. Không lạm dụng thẻ `<div>`.
> 2. CSS Variables (:root): Quản lý tập trung toàn bộ màu sắc, typography, spacing, radius và shadow. Sử dụng Flexbox & CSS Grid cho bố cục, có responsive cơ bản dưới 920px và mobile.
> 3. Tương tác & Hiệu ứng thư viện:
>    - Tích hợp CDN Animate.css (v4.1.1) cho các phần tử chính như tiêu đề, Hero Section, CTA buttons.
>    - Tích hợp CDN AOS (Animate On Scroll v2.3.1) cho hiệu ứng xuất hiện khi cuộn trang sinh động.
>    - Tự viết hiệu ứng `:hover`, `:focus` bằng CSS cho nút bấm, card xe (`.car-card`), card dịch vụ và ô input.
> 4. Tính năng Showroom: Hero Section có video xe chạy trên cao tốc, bộ lọc phân khúc xe, lưới 12 mẫu xe kèm bảng thông số kỹ thuật chi tiết khi xem từng xe, bảng so sánh phân khúc, form đặt lịch lái thử có kiểm tra `:focus`, và footer có thông tin sinh viên thực hiện: Nguyễn Tấn Điền - MSSV: 125000260."

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)
### Lần 1: Dựng khung Semantic HTML & CSS Variable
- **Prompt đã dùng:**
  > "Hãy kiểm tra và refactor lại toàn bộ mã nguồn HTML và CSS vừa tạo:
  > - Thay toàn bộ các thẻ generic `div` ở các phần tử mang ý nghĩa nội dung: mỗi dòng xe trong showroom chuyển thành thẻ `<article class="car-card" tabindex="0">`, ảnh xe phải bọc trong `<figure>`, giá bán hiển thị trong `<figcaption>`, thanh điều hướng và bộ lọc dùng `<nav>`, mẹo tư vấn dùng `<aside>`.
  > - Trong CSS, thiết lập toàn bộ biến tại `:root` bao gồm: `--primary-color`, `--accent-color`, `--dark-surface`, `--card-bg`, font chữ `Plus Jakarta Sans` & `Inter`, các nấc spacing (`--space-xs` đến `--space-3xl`), border-radius và box-shadow. Chuyển sang phong cách giao diện sáng (Modern Luxury Light Theme) sang trọng, lịch lãm."

- **Kết quả AI tạo ra:**
  - AI đã thay thế toàn bộ các khối `div` chính thành các thẻ ngữ nghĩa Semantic HTML5 chuẩn mực (`header`, `nav`, `main`, `section`, `article`, `figure`, `figcaption`, `aside`, `footer`).
  - Toàn bộ màu sắc và khoảng cách được khai báo đồng bộ vào `:root`, chuyển giao diện sang nền sáng ngọc trai thanh lịch `#f8fafc`, tôn vinh hình ảnh các dòng xe.

- **Nhận xét & Tinh chỉnh của SV:**
  - AI xài thẻ `<div>` nhiều quá ở bản nháp ban đầu, đã nhắc AI sửa lại thành `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>`.
  - Một số link ảnh xe trên Unsplash bị mã lỗi 404 dẫn đến mất hình ảnh sản phẩm, SV đã phát hiện và yêu cầu AI rà soát toàn bộ HTTP status của ảnh để thay thế bằng các link ảnh sắc nét $100\%$ không bị lỗi.
  - Thêm thuộc tính `tabindex="0"` vào thẻ `<article>` và viết hiệu ứng `:focus-visible` giúp người dùng điều hướng bằng phím Tab thuận tiện (chuẩn Accessibility).

### Lần 2: Tích hợp thư viện Animate.css & AOS
- **Prompt đã dùng:**
  > "Hãy tích hợp hai thư viện Animate.css và AOS (Animate On Scroll) qua CDN:
  > - Thêm link stylesheet Animate.css v4.1.1 và AOS v2.3.1 vào `<head>`.
  > - Gắn class `animate__animated animate__fadeInUp` và `animate__bounceIn` vào tiêu đề và nút bấm Hero Section.
  > - Gắn thuộc tính `data-aos="fade-up"` vào các tiêu đề section, lưới thẻ xe, thẻ dịch vụ, bảng so sánh và form liên hệ.
  > - Nhúng script khởi tạo `AOS.init()` trước thẻ đóng `</body>`."

- **Thách thức gặp phải:**
  - Khi hover chuột vào thẻ xe `.car-card`, hiệu ứng nâng thẻ `transform: translateY(-8px)` bị mất hoặc giật cục, không hoạt động trơn tru. Nguyên nhân do thư viện AOS tự động gán inline styles `transform: translate3d(0, 0, 0)` khi cuộn trang, dẫn đến xung đột với thuộc tính `transform` của CSS hover.
  - Trang web xuất hiện thanh cuộn ngang (horizontal scrollbar) không mong muốn khi AOS animate các phần tử từ ngoài màn hình vào.

- **Cách sửa prompt (Debug prompt):**
  > "Khắc phục 2 lỗi xung đột thư viện:
  > 1. Trong `style.css`, tách riêng thuộc tính transition thành `transition: transform var(--transition-base), box-shadow var(--transition-base), border-color var(--transition-base);` (tuyệt đối không dùng `transition: all`). Trong script khởi tạo, thêm cấu hình `{ once: true, duration: 800, offset: 60 }` để AOS chỉ kích hoạt 1 lần duy nhất rồi nhường quyền điều khiển `transform` cho CSS `:hover`.
  > 2. Thêm thuộc tính `overflow-x: hidden` trên cả thẻ `html` và `body` để triệt tiêu hoàn toàn hiện tượng thanh cuộn ngang do AOS tạo ra."

## 3. Đánh giá cá nhân về quá trình Vibe Coding
- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**
  - AI giúp tiết kiệm nhiều thời gian nhất ở khâu **dựng khung Semantic HTML5 và nhập liệu thông số kỹ thuật chi tiết của 12 dòng xe** (động cơ, mã lực, hộp số, mô-men xoắn, an toàn). Nếu làm thủ công sẽ mất nhiều giờ để tìm kiếm và định dạng dữ liệu.
  - Tiết kiệm thời gian thiết lập hệ thống CSS Variables (`:root`) đồng bộ và viết các media queries responsive đa thiết bị.

- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**
  - **Prompt phải cụ thể và có ràng buộc kỹ thuật rõ ràng:** Cần chỉ định chính xác tên thẻ HTML (`article`, `figure` thay vì `div`), tên thư viện (`Animate.css`, `AOS`) và quy chuẩn cấu trúc để AI không sinh code tự do hoặc dùng các phương án generic.
  - **Chia nhỏ quá trình thành các lần lặp (Iterations):** Không nên yêu cầu tất cả trong một lần prompt duy nhất. Hãy chia thành Lần 1 (khung cấu trúc & CSS variables) và Lần 2 (tích hợp thư viện hiệu ứng & debug).
  - **Luôn kiểm tra và nghiệm thu thực tế:** AI có thể sử dụng link tài nguyên lỗi (như link ảnh 404) hoặc tạo xung đột CSS (`transform` giữa AOS và `:hover`). Sinh viên cần hiểu rõ bản chất kỹ thuật để debug prompt và dẫn dắt AI tạo ra sản phẩm hoàn chỉnh nhất.

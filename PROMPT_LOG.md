# 📝 PROMPT LOG — Bài kiểm tra Giữa kỳ môn Thiết kế Web

---

## 1. Thông tin chung

| Mục | Chi tiết |
|---|---|
| **Họ và tên** | Nguyễn Tấn Điền |
| **MSSV** | 125000260 |
| **Trường / Khoa** | Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU) |
| **Đề tài** | **AutoPrestige Vietnam** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (Từ Hạng Vừa, Hạng Sang đến Siêu Xe Cao Cấp) |
| **Công cụ AI sử dụng** | Google Antigravity & Gemini |
| **GitHub Repository** | [https://github.com/NTanDien/Dien_NguyenTan_125000260.git](https://github.com/NTanDien/Dien_NguyenTan_125000260.git) |
| **Link Live Preview (GitHub Pages)** | [https://ntandien.github.io/Dien_NguyenTan_125000260/](https://ntandien.github.io/Dien_NguyenTan_125000260/) |

---

## 2. Yêu cầu ban đầu (System / Initial Prompt)

> **Prompt tổng quan khởi tạo khung website:**
>
> Hãy tạo một trang web hoàn chỉnh cho đề tài **"AutoPrestige Vietnam"** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (từ Hạng Vừa & Gia Đình, Sedan & SUV Hạng Sang đến Siêu Xe Cao Cấp) đáp ứng đầy đủ yêu cầu kiểm tra giữa kỳ:
>
> - **Chuẩn Semantic HTML5 nghiêm ngặt:** Sử dụng đúng và đầy đủ các thẻ ngữ nghĩa: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<figcaption>`, `<aside>`, `<footer>` (tuyệt đối không lạm dụng thẻ generic `<div>`).
> - **CSS & CSS Variables:** Sử dụng `:root` quản lý toàn bộ hệ thống màu sắc (`--primary-color`, `--accent-color`, `--dark-surface`...), font chữ (`Plus Jakarta Sans` & `Inter`), spacing, bo góc và đổ bóng. Bố cục hiện đại kết hợp CSS Grid và Flexbox, responsive mượt mà dưới 920px.
> - **Tương tác & Thư viện hiệu ứng:**
>   + Tích hợp thư viện **Animate.css (v4.1.1)** cho tiêu đề, huy hiệu và nút CTA trong Hero Section.
>   + Tích hợp thư viện **AOS (Animate On Scroll v2.3.1)** cho các section và card khi cuộn trang.
>   + Tự viết hiệu ứng `:hover`, `:focus` mượt mà cho nút bấm, card xe (`.car-card`), card dịch vụ và form input.
> - **Các tính năng showroom xe hơi:**
>   + Hero Showroom ấn tượng với video nền xe chạy trên cao tốc (`assets/hero-car-loop.mp4`).
>   + Bộ lọc phân khúc xe và lưới 12 mẫu xe đa dạng kèm popup xem chi tiết thông số kỹ thuật từng xe.
>   + Bảng so sánh 3 phân khúc xe kèm mẹo từ chuyên gia (`<aside>`).
>   + Form Đặt lịch lái thử & Nhận báo giá lăn bánh có kiểm tra `:focus`.
>   + Footer đầy đủ thông tin sinh viên thực hiện: **Nguyễn Tấn Điền - MSSV: 125000260 - Khoa CNTT, Trường Đại học Lạc Hồng**.

---

## 3. Quá trình tinh chỉnh & Giải quyết sự cố (Iterations)

### 🔧 Lần 1: Dựng khung Semantic HTML & Thiết lập CSS Variables `:root`

* **Prompt đã dùng:**
  > "Hãy tái cấu trúc toàn bộ HTML theo chuẩn Semantic nghiêm ngặt:
  > - Thay thế các thẻ generic `div` thành thẻ ngữ nghĩa: mỗi mẫu xe là một `<article class="car-card">` có `tabindex="0"`, ảnh xe bọc trong `<figure>`, giá tiền đặt trong `<figcaption>`, thanh lọc xe đặt trong `<nav aria-label="...">`, mẹo tư vấn bọc bằng `<aside>`.
  > - Thiết lập toàn bộ bảng màu và quy chuẩn thiết kế tại `:root` trong `style.css` bao gồm: màu nền sáng sang trọng (`--primary-color: #f8fafc; --card-bg: #ffffff;`), màu nhấn đỏ ruby (`--accent-color: #e11d48;`), màu chữ tương phản cao, typography cùng hệ thống spacing, border-radius và box-shadow."

* **Kết quả AI:**
  - AI đã refactor toàn bộ mã nguồn sang chuẩn HTML5 Semantic với hơn 8 loại thẻ ngữ nghĩa khác nhau.
  - Xây dựng thành công hệ thống hơn 25 biến CSS trong `:root`, giúp giao diện sáng sủa, thanh lịch và đồng bộ phong cách showroom hiện đại.

* **Nhận xét & Tinh chỉnh:**
  - Cấu trúc layout rất chuẩn chỉnh, tuy nhiên các thẻ xe và nút bấm cần được bổ sung thêm hiệu ứng `:focus-visible` để đạt chuẩn trợ năng (Accessibility) và tăng trải nghiệm thị giác khi rê chuột.

---

### 🔧 Lần 2: Tích hợp Animate.css, AOS & Debug xử lý xung đột Animation khi cuộn / hover

* **Prompt đã dùng:**
  > "Hãy tích hợp CDN của thư viện **Animate.css (v4.1.1)** và **AOS (v2.3.1)** vào website:
  > - Sử dụng Animate.css (`animate__fadeInUp`, `animate__bounceIn`, `animate__delay-1s`) cho tiêu đề, badge và nút CTA trong Hero Section.
  > - Gắn `data-aos="fade-up"` vào các tiêu đề section, lưới 12 thẻ xe, thẻ dịch vụ, bảng so sánh và form đăng ký.
  > - **Thách thức:** Xử lý triệt để xung đột `transform` giữa hiệu ứng `:hover` của CSS (`transform: translateY(-8px)`) và thuộc tính `transform` do AOS điều khiển khi cuộn trang, tránh hiện tượng card bị giật hoặc mất hiệu ứng hover."

* **Thách thức gặp phải & Cách debug prompt:**
  - Khi AOS kích hoạt hiệu ứng cuộn, thư viện này tự động gán inline styles `transform: translate3d(...)` vào phần tử. Nếu trong CSS dùng `transition: all`, thuộc tính này sẽ ghi đè và làm mất hiệu ứng hover nâng card của người dùng.
  - **Cách debug & xử lý:** 
    1. Trong CSS, tách bạch rõ ràng các thuộc tính transition: `transition: transform var(--transition-base), box-shadow var(--transition-base), border-color var(--transition-base);` (tuyệt đối không dùng `transition: all`).
    2. Khởi tạo AOS với tùy chọn `{ once: true, duration: 800, offset: 60 }` để sau khi phần tử xuất hiện trong khung nhìn, AOS hoàn tất animation và trả lại toàn quyền điều khiển `transform: translateY(-8px)` cho trạng thái `:hover`.
    3. Thêm `overflow-x: hidden` trên cả `html` và `body` để loại bỏ thanh cuộn ngang ngoài ý muốn khi AOS dịch chuyển phần tử từ ngoài màn hình vào.

---

## 4. Đánh giá cá nhân

### ✅ AI giúp tiết kiệm thời gian ở phần nào?

1. **Khởi tạo bộ khung Semantic HTML5 và CSS Variables (Tiết kiệm ~80% thời gian):** AI tạo ra cấu trúc chuẩn chỉ trong vài giây, bao gồm đầy đủ dữ liệu thông số kỹ thuật chi tiết của 12 dòng xe hơi từ phổ thông đến siêu xe.
2. **Gợi ý giải pháp kiến trúc và tích hợp thư viện (Tiết kiệm ~70% thời gian):** AI cung cấp chính xác các đường dẫn CDN, cấu hình thuộc tính data của AOS và các class của Animate.css mà không cần phải tra cứu thủ công tài liệu.
3. **Phát hiện và xử lý lỗi xung đột CSS/JS:** AI phân tích chính xác nguyên nhân gây giật layout giữa thuộc tính `transform` của AOS và CSS hover, từ đó đưa ra hướng khắc phục chuẩn mực.

### 📖 Bài học rút ra khi prompt cho AI

1. **Bám sát đề bài và tiêu chí chấm điểm:** Cần đưa các yêu cầu kỹ thuật cốt lõi (như Semantic HTML5, CSS Variables, thư viện Animate.css, AOS, cấu trúc nộp bài) trực tiếp vào prompt để AI không bỏ sót bất kỳ hạng mục nào trong barem điểm.
2. **Chia nhỏ bài toán theo từng bước lặp (Iteration):** Thay vì yêu cầu tất cả trong một lần duy nhất, việc phân chia thành Lần 1 (dựng khung cấu trúc & style) và Lần 2 (tích hợp thư viện & debug chuyển động) giúp kiểm soát chất lượng code chặt chẽ và không phát sinh lỗi chồng chéo.
3. **Đóng vai trò là người định hướng:** AI là công cụ tăng năng suất đắc lực, nhưng lập trình viên phải là người thấu hiểu bản chất kỹ thuật (tại sao xảy ra xung đột `transform`, cơ chế hoạt động của `overflow-x`) để ra lệnh điều chỉnh đúng trọng tâm.

---

> **Nguyễn Tấn Điền — MSSV: 125000260**  
> Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU)  
> Ngày hoàn thành: 20/10/2026

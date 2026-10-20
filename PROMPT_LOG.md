# 📝 PROMPT LOG — Bài kiểm tra Giữa kỳ Thiết kế Web

---

## 1. Thông tin chung

| Mục | Chi tiết |
|---|---|
| **Họ và tên** | Nguyễn Tấn Điền |
| **MSSV** | 125000260 |
| **Trường / Khoa** | Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU) |
| **Đề tài** | **AutoPrestige Vietnam** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (Hạng Vừa, Hạng Sang, Siêu Xe Cao Cấp) |
| **Công cụ AI sử dụng** | Google Antigravity & Gemini |
| **GitHub Repository** | [https://github.com/NTanDien/Dien_NguyenTan_125000260.git](https://github.com/NTanDien/Dien_NguyenTan_125000260.git) |
| **Live Preview (GitHub Pages)** | [https://ntandien.github.io/Dien_NguyenTan_125000260/](https://ntandien.github.io/Dien_NguyenTan_125000260/) |

---

## 2. Yêu cầu ban đầu (System / Initial Prompt)

> **Prompt gửi cho AI:**
>
> Tạo một trang web hoàn chỉnh cho đề tài **"AutoPrestige Vietnam"** — Nền tảng Quảng bá & Trải nghiệm Xe Hơi Đa Phân Khúc (từ Hạng Vừa, Hạng Sang đến Siêu Xe Cao Cấp). Yêu cầu cụ thể:
>
> - **Semantic HTML5 nghiêm ngặt**: sử dụng `header`, `nav`, `main`, `section`, `article`, `figure`, `figcaption`, `aside`, `footer`. Tuyệt đối không lạm dụng thẻ `div`.
> - **Tích hợp CDN**: Google Fonts (`Plus Jakarta Sans` & `Inter`), FontAwesome 6, Animate.css (v4.1.1) cho Hero Section, AOS (v2.3.1) cho hiệu ứng khi cuộn trang.
> - **Các thành phần chính**:
>   1. Thanh điều hướng (`header` + `nav`) có responsive hamburger menu.
>   2. Hero Showroom với hiệu ứng Animate.css và ảnh xe sang từ Unsplash.
>   3. Bộ lọc phân khúc xe bằng JavaScript (Tất cả / Hạng Vừa & Gia Đình / Sedan & SUV Hạng Sang / Siêu Xe Cao Cấp) cùng lưới 6 mẫu xe dùng `article.car-card[tabindex="0"]`, mỗi xe có `figure`, `figcaption` giá, 3 thông số kỹ thuật, nút "Đặt lịch lái thử" tự động điền tên xe xuống form.
>   4. Dịch vụ & Quyền lợi (Trả góp 5.9%, Thu cũ đổi mới, Bảo hành 5 năm, Cứu hộ 24/7).
>   5. Bảng so sánh tư vấn 3 phân khúc xe.
>   6. Form Đặt lịch lái thử & Nhận báo giá lăn bánh (có hiệu ứng `:focus`).
>   7. Footer với thông tin sinh viên: Nguyễn Tấn Điền — MSSV: 125000260 — Khoa CNTT, Trường Đại học Lạc Hồng.
> - **CSS**: dùng `:root` (CSS Variables), Flexbox + Grid, Responsive < 920px, hiệu ứng `:hover` và `:focus` mượt mà.

---

## 3. Quá trình tinh chỉnh & Giải quyết sự cố

### 🔧 Lần 1: Dựng khung Semantic HTML5 & Thiết lập CSS Variables `:root`

**Vấn đề nhận diện:**
Bản dựng đầu tiên AI tạo ra sử dụng quá nhiều thẻ `<div>` generic — không đạt chuẩn Semantic HTML5 theo yêu cầu đề thi. Cần thay thế toàn bộ bằng các thẻ ngữ nghĩa phù hợp.

**Prompt tinh chỉnh gửi AI:**

> Hãy refactor toàn bộ cấu trúc HTML:
> - Thay tất cả `div.car-card` thành `article.car-card` với `tabindex="0"`.
> - Bọc ảnh xe bằng `figure` thay vì `div`, giá xe dùng `figcaption`.
> - Khu vực lọc phân khúc dùng `nav[aria-label]` thay vì `div`.
> - Mẹo so sánh cuối section dùng `aside` thay vì `div`.
> - Đảm bảo mỗi `section` đều có `header.section-header` chứa tiêu đề.
>
> Với CSS, hãy khai báo toàn bộ biến vào `:root` gồm: `--primary-color`, `--accent-color`, `--dark-surface`, `--card-bg`, `--text-primary`, `--text-secondary`, `--border-color`, `--font-heading`, `--font-body`, các biến spacing (`--space-xs` đến `--space-3xl`), bo góc (`--radius-sm/md/lg/full`) và đổ bóng (`--shadow-sm/md/lg/glow`).

**Kết quả:**
- HTML đạt chuẩn Semantic: mỗi mẫu xe là `<article>`, ảnh trong `<figure>`, giá trong `<figcaption>`, bộ lọc dùng `<nav>`, mẹo cuối bảng so sánh dùng `<aside>`.
- CSS Variables được quản lý tập trung tại `:root`, dễ bảo trì và thay đổi theme sau này.
- Toàn bộ layout chuyển sang CSS Grid (lưới xe 3 cột, dịch vụ 4 cột, footer 3 cột) kết hợp Flexbox cho nav, filter bar và CTA buttons.

---

### 🔧 Lần 2: Tích hợp Animate.css, AOS & Debug xung đột `transform` khi `:hover`

**Vấn đề nhận diện:**
Sau khi tích hợp thư viện Animate.css cho Hero và AOS cho hiệu ứng cuộn, phát hiện **hai sự cố**:

1. **Xung đột `transform`**: Khi hover vào `.car-card`, hiệu ứng `transform: translateY(-8px)` bị ghi đè bởi thuộc tính `transform` nội bộ mà AOS thêm vào (AOS dùng `transform: translate3d(0, Xpx, 0)` rồi reset về `none`). Kết quả là hover animation bị mất hoặc giật.
2. **Lỗi filter + AOS**: Khi nhấn nút lọc phân khúc xe, các card bị ẩn/hiện bằng `display: none` nhưng AOS không tự cập nhật lại vị trí, dẫn đến một số card không xuất hiện animation khi được hiển thị trở lại.

**Prompt tinh chỉnh gửi AI:**

> Có 2 bug cần fix:
>
> **Bug 1 — Xung đột transform AOS vs hover:**
> Hiệu ứng hover `translateY(-8px)` trên `.car-card` bị AOS ghi đè. Hãy tách riêng `transition` property trong CSS: chỉ khai báo `transition: transform, box-shadow, border-color` cho card, KHÔNG dùng `transition: all` (sẽ xung đột với AOS transition). Đồng thời đặt `[data-aos]` init với `once: true` để AOS chỉ chạy 1 lần rồi gỡ style, trả lại quyền transform cho CSS hover.
>
> **Bug 2 — Filter không refresh AOS:**
> Sau khi lọc xe (ẩn/hiện card), gọi `setTimeout(() => AOS.refresh(), 100)` để AOS tính toán lại vị trí các phần tử visible.

**Kết quả:**
- **Bug 1 đã fix**: Khai báo `transition` tường minh từng property (không dùng `all`), kết hợp `AOS.init({ once: true })` → AOS animate 1 lần rồi remove attribute, hover effect hoạt động mượt mà.
- **Bug 2 đã fix**: Thêm `AOS.refresh()` trong callback của filter → card mới hiển thị vẫn có animation đúng.
- Bổ sung `overflow-x: hidden` trên `html` và `body` để tránh thanh cuộn ngang do AOS animate từ ngoài viewport.

---

## 4. Đánh giá cá nhân

### ✅ AI giúp tiết kiệm thời gian ở phần nào?

| Phần việc | Mức tiết kiệm | Ghi chú |
|---|---|---|
| Dựng cấu trúc HTML5 Semantic | ⭐⭐⭐⭐⭐ | AI tạo bộ khung `header/nav/main/section/article/figure/aside/footer` rất nhanh, chỉ cần review và chỉnh sửa nhỏ. |
| Thiết lập CSS Variables `:root` | ⭐⭐⭐⭐⭐ | Hệ thống 30+ biến CSS được AI sinh ra đồng bộ, tiết kiệm rất nhiều thời gian so với tự đặt tên và quản lý. |
| Tích hợp CDN & thư viện bên ngoài | ⭐⭐⭐⭐ | AI nhớ chính xác URL CDN, version, và cách khởi tạo (AOS.init, class Animate.css). |
| Responsive layout | ⭐⭐⭐⭐ | Media queries cho Grid/Flexbox fallback được AI viết nhanh và chính xác. |
| Debug xung đột CSS/JS | ⭐⭐⭐ | AI gợi ý hướng fix (tách transition, AOS once), nhưng cần dev hiểu gốc vấn đề để prompt đúng. |

### 📖 Bài học rút ra khi prompt cho AI

1. **Prompt càng chi tiết, kết quả càng chính xác**: Thay vì nói "tạo trang web bán xe", cần liệt kê rõ từng section, thẻ HTML muốn dùng, thư viện cần tích hợp, và tính năng cụ thể (bộ lọc, auto-fill form...). Prompt mơ hồ sẽ cho ra code generic, không đạt yêu cầu.

2. **Chia nhỏ vấn đề thành từng lần prompt**: Không nên nhồi tất cả yêu cầu vào 1 prompt duy nhất. Lần 1 tập trung cấu trúc HTML + CSS, lần 2 mới xử lý animation/interaction. Điều này giúp AI tập trung và giảm lỗi.

3. **Phải hiểu code để review và debug**: AI không phải lúc nào cũng đúng. Ví dụ bug xung đột `transform` giữa AOS và CSS hover — nếu không hiểu cơ chế hoạt động của AOS (inject inline style) và CSS specificity, sẽ không biết cách mô tả bug cho AI fix.

4. **Dùng AI như "pair programmer", không phải "auto-pilot"**: AI mạnh ở tốc độ sinh code boilerplate và gợi ý giải pháp, nhưng developer vẫn phải là người quyết định kiến trúc, kiểm tra chất lượng và đảm bảo tính nhất quán.

---

> **Nguyễn Tấn Điền — MSSV: 125000260**
> Khoa Công nghệ Thông tin — Trường Đại học Lạc Hồng (LHU)
> Ngày thực hiện: 20/10/2026

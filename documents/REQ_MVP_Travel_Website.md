# 📘 YÊU CẦU MVP WEBSITE DU LỊCH ĐA NĂNG

## 1. 🎯 Mục tiêu tổng thể
Phát triển một **MVP (Minimum Viable Product)** cho website du lịch đa năng, phù hợp với dự án cá nhân, sử dụng công cụ miễn phí, và không cần triển khai thực tế ngay. MVP tập trung vào 3 chức năng cốt lõi:
- **Lập kế hoạch hành trình**: Tạo và quản lý lịch trình du lịch.
- **Khám phá & đánh giá địa điểm**: Tìm kiếm và đánh giá địa điểm du lịch.
- **Đặt chỗ**: Giả lập đặt chỗ dịch vụ (khách sạn, vé, nhà hàng).
MVP là bước đầu để học hỏi, thử nghiệm, và đặt nền tảng mở rộng dần đến các chức năng đầy đủ trong **REQ_FULL_Travel_Website_Updated.md** (7 chức năng).

## 2. 👥 Đối tượng sử dụng
- **Người dùng cuối**: Du khách tự túc, lập kế hoạch, khám phá địa điểm, đặt chỗ giả lập.
- **Quản trị viên (bạn)**: Nhập dữ liệu địa điểm, quản lý hệ thống.

## 3. 🧱 Chức năng chính

### A. Lập kế hoạch hành trình (Itinerary Planner)
- **Tạo kế hoạch**:
  - Đặt tên, chọn ngày đi/về, điểm đến (từ danh sách địa điểm tĩnh).
  - Giao diện kéo-thả để thêm địa điểm, hoạt động, thời gian.
- **Bản đồ tương tác**:
  - Hiển thị lộ trình di chuyển bằng **OpenStreetMap** + **Leaflet**.
  - Hỗ trợ zoom, kéo-thả để xem địa điểm.
- **Xuất PDF**:
  - Xuất kế hoạch (địa điểm, thời gian, mô tả) thành file PDF bằng **jsPDF**.
- **Xem ngoại tuyến**:
  - Lưu kế hoạch vào **localStorage** để xem khi không có internet.
- **Quản lý chi phí**:
  - Nhập chi phí thủ công cho mỗi địa điểm/hoạt động.
  - Tính tổng chi phí cơ bản.

### B. Khám phá & đánh giá địa điểm (Explore & Review Places)
- **Tìm kiếm địa điểm**:
  - Bộ lọc cơ bản: Tên, danh mục (bãi biển, nhà hàng, bảo tàng).
  - Dữ liệu từ file JSON tĩnh hoặc **OpenStreetMap Nominatim** (cache vào Supabase).
- **Hiển thị thông tin**:
  - Ảnh, mô tả, giờ mở cửa, vị trí (tọa độ từ OpenStreetMap).
  - Bản đồ tương tác tích hợp Leaflet.
- **Đánh giá**:
  - Hệ thống 5 sao + bình luận.
  - Lưu đánh giá vào **Supabase**.
  - Hiển thị danh sách đánh giá theo thời gian.

### C. Đặt chỗ (Booking: Khách sạn, Vé, Nhà hàng)
- **Hiển thị dịch vụ**:
  - Danh sách dịch vụ (khách sạn, vé, nhà hàng) từ file JSON hoặc Supabase.
  - Thông tin: Ảnh, giá, mô tả, chính sách hủy (tĩnh).
- **Form đặt chỗ giả lập**:
  - Nhập thông tin: Tên, ngày, số người.
  - Lưu vào Supabase, hiển thị xác nhận giả lập (không tích hợp thanh toán).
- **Đánh giá dịch vụ**:
  - Sau khi “đặt chỗ”, người dùng có thể đánh giá 5 sao + bình luận.

## 4. ⚙️ Yêu cầu hệ thống

### Giao diện người dùng
- **Responsive**: Hỗ trợ desktop, mobile (React + Tailwind CSS).
- **Dark/light mode**: Tùy chọn giao diện sáng/tối.
- **UX tối ưu**: Giao diện đơn giản, dễ thao tác (kéo-thả, form nhập liệu).
- **Ngôn ngữ**: Tiếng Việt, tiếng Anh (dùng i18n).
- **Accessibility**: Tuân thủ WCAG cơ bản (aria-label, tab navigation).

### Backend & API
- **RESTful API**: Xây bằng Node.js + Express.
  - Endpoint: Lấy danh sách địa điểm, lưu kế hoạch, lưu đánh giá, lưu đặt chỗ.
- **API bên thứ ba**:
  - **OpenStreetMap + Leaflet**: Hiển thị bản đồ, lộ trình.
  - **Nominatim**: Tìm kiếm địa điểm (cache vào Supabase để tránh vượt hạn mức).
- **API nội bộ**:
  - Quản lý kế hoạch, địa điểm, đánh giá, đặt chỗ (Supabase).

### Dữ liệu & bảo mật
- **Cơ sở dữ liệu**: **PostgreSQL** (Supabase miễn phí, 500MB).
  - Bảng: Địa điểm (tên, mô tả, ảnh, tọa độ), kế hoạch (ngày, địa điểm, chi phí), đánh giá (sao, bình luận), đặt chỗ (người dùng, dịch vụ, ngày).
- **Bảo mật**:
  - HTTPS (miễn phí qua Vercel).
  - JWT cho xác thực cơ bản (Supabase Auth).
  - Lưu ảnh trong Supabase Storage (miễn phí, 1GB).
- **Dữ liệu tĩnh**:
  - File JSON chứa 50-100 địa điểm (khách sạn, nhà hàng, điểm tham quan).
  - Nhập thủ công hoặc crawl từ nguồn công khai (Wikipedia, OpenStreetMap).

### Hiệu năng & khả năng mở rộng
- **Hiệu năng**: Tải trang < 3s, hỗ trợ 50-100 user đồng thời (chạy local hoặc Vercel).
- **Triển khai**: Vercel (miễn phí, 100GB băng thông/tháng).
- **Kiến trúc**: Monolith (React + Node.js), không dùng microservice.
- **Cache**: Lưu dữ liệu OpenStreetMap vào Supabase để giảm truy vấn API.

## 5. 🧪 Lộ trình mở rộng tương lai
MVP là nền tảng để phát triển dần các chức năng đầy đủ trong **REQ_FULL_Travel_Website_Updated.md** qua 3 giai đoạn tiếp theo:
- **Giai đoạn 2 (6-9 tháng)**:
  - Thêm **Community Sharing**: Blog, tương tác, gamification cơ bản (điểm thưởng).
  - Thêm **Accounts & Permissions**: Đăng ký/đăng nhập, phân quyền cơ bản.
- **Giai đoạn 3 (9-12 tháng)**:
  - Thêm **Business Management**: Đăng ký business, dashboard, tranh chấp cơ bản.
  - Cập nhật Booking: Tích hợp dịch vụ business nội bộ.
- **Giai đoạn 4 (9-12 tháng)**:
  - Thêm **AI Personalization**: Gợi ý địa điểm (TensorFlow.js), chatbot (Dialogflow).
  - Cập nhật Explore: Sự kiện địa phương (OpenDataSoft), nhãn bền vững.
  - Gamification nâng cao: Bảng xếp hạng, thử thách du lịch.

## 6. 📚 Công cụ miễn phí
- **Frontend**: React, Tailwind CSS, React Router.
- **Backend**: Node.js, Express, Supabase (PostgreSQL, Auth, Storage).
- **Bản đồ**: OpenStreetMap, Leaflet, Nominatim.
- **PDF**: jsPDF.
- **Triển khai**: Vercel.
- **Phát triển**: VS Code, Git/GitHub, Figma (free), Postman.

## 7. 🧑‍🤝‍🧑 Các bên liên quan
- **Người dùng cuối**: Sử dụng MVP để lập kế hoạch, khám phá, đặt chỗ giả lập.
- **Quản trị viên (bạn)**: Nhập dữ liệu, quản lý hệ thống, kiểm thử.

## 8. ⏳ Thời gian phát triển
- **Tổng thời gian**: 6-9 tháng (10-20 giờ/tuần).
  - Tháng 1: Học React, Supabase, thiết kế UI (Figma).
  - Tháng 2-4: Xây Itinerary Planner (kéo-thả, OpenStreetMap, jsPDF).
  - Tháng 5-6: Xây Explore & Review Places (tìm kiếm, đánh giá).
  - Tháng 7-8: Xây Booking (form giả lập, Supabase).
  - Tháng 9 (tùy chọn): Test, tối ưu, triển khai trên Vercel.

## 9. 💰 Chi phí
- **Tổng chi phí**: $0 (tất cả công cụ miễn phí).
- **Hạn mức**:
  - Supabase: 500MB (đủ cho 100-200 địa điểm).
  - Vercel: 100GB băng thông/tháng (đủ cho MVP).
  - OpenStreetMap: Cache dữ liệu để tránh vượt hạn mức (~1 truy vấn/giây).

## 10. 📈 Kết quả mong đợi
- Website chạy local hoặc trên Vercel, hỗ trợ:
  - Lập kế hoạch hành trình với bản đồ và PDF.
  - Tìm kiếm, đánh giá địa điểm.
  - Giả lập đặt chỗ dịch vụ.
- Nền tảng học hỏi React, Node.js, PostgreSQL, và API bản đồ.
- Sẵn sàng mở rộng sang các chức năng đầy đủ (Community, AI, Business) trong 2-3 năm.
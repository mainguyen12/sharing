# Experience Sharing

### 1. Vấn đề người dùng gặp phải

Khi triển khai hệ thống check-in bằng vị trí và khuôn mặt tại công ty
Liberty: - Với văn phòng nhỏ (100 user), hệ thống hoạt động ổn định do
chỉ cần 1 tọa độ trung tâm và bán kính 50m.\

- Nhưng khi mở rộng quy mô (1000 user, khuôn viên rộng), nhiều nhân viên
  báo **không thể check-in dù vẫn ở trong công ty**. Điều này gây gián
  đoạn trải nghiệm và ảnh hưởng trực tiếp đến công tác chấm công.

### 2. Giá trị tôi mong muốn mang lại

Đảm bảo **mọi nhân viên đều có thể check-in thuận tiện và chính xác**,
bất kể vị trí trong khuôn viên rộng, đồng thời giảm thiểu lỗi sai, giúp
HR và quản lý tiết kiệm thời gian xử lý thủ công.

### 3. Cách tiếp cận vấn đề

Tôi đặt ra nhiều giả thiết để xác định nguyên nhân:\

1. Mạng yếu hoặc mất kết nối.\
2. Thiết bị chưa bật định vị.\
3. Admin chưa cấu hình vị trí công ty cho user.\
4. Bán kính check-in cố định không phù hợp với diện tích lớn.

### 4. Giải pháp tôi triển khai

- **Xử lý giả thiết 1:** Bổ sung UI thông báo rõ ràng khi user mất kết
  nối/tín hiệu kém → giúp họ hiểu thay vì nhầm lẫn.\
- **Xử lý giả thiết 2:** Đảm bảo app luôn yêu cầu quyền định vị trước
  khi vào check-in.\
- **Xử lý giả thiết 3:** Do công ty không có hệ thống log, tôi tạm
  dùng **Google Sheets + App Script để ghi log**. Từ đó phát hiện
  nhiều user chưa được set vị trí công ty → tôi chủ động làm việc với
  PM và HR đối tác để khắc phục.\
- **Xử lý giả thiết 4:**
  - Bổ sung UI hiển thị khoảng cách của user đến điểm check-in gần
    nhất để minh bạch hơn.\
  - Phân tích log trên bản đồ, nhận thấy nhiều user vẫn trong khuôn
    viên nhưng nằm ngoài bán kính 50m. Từ đó tôi đề xuất **thay đổi
    cơ chế check-in từ 1 tọa độ + bán kính → xác định theo polygon
    (đa giác)**, phản ánh chính xác ranh giới công ty.

### 5. Kết quả đạt được

- Tỷ lệ phản ánh lỗi check-in giảm đáng kể (giảm hơn 70% sau khi mở
  rộng test).\
- Người dùng yên tâm hơn nhờ UI minh bạch (hiển thị nguyên nhân lỗi và
  khoảng cách).\
- Bộ phận HR giảm khối lượng xử lý thủ công, tiết kiệm thời gian đối
  soát.\
- Giải pháp polygon tạo nền tảng mở rộng cho nhiều văn phòng/khuôn
  viên khác trong tương lai.

### 6. Cách tôi đo lường và xác định vấn đề

- **Ghi log:** dùng Google Sheets + App Script để thu thập vị trí user
  khi lỗi xảy ra.\
- **Phân tích dữ liệu:** so sánh vị trí thực tế user với khu vực
  check-in để xác định nguyên nhân.
- **Đo lường kết quả:** theo dõi số lượng log và lỗi phản ánh từ user
  trước và sau khi cải tiến → số liệu giảm mạnh, xác nhận giải pháp
  hiệu quả.

# Tài liệu Yêu cầu Sản phẩm (PRD)
# Ứng dụng PickleBall Dating

---

## Mục lục

1. [Tóm tắt Tổng quan](#tóm-tắt-tổng-quan)
2. [Bảng Tính năng](#bảng-tính-năng)
3. [Chi tiết Tính năng](#chi-tiết-tính-năng)
4. [Vai trò và Quyền hạn Người dùng](#vai-trò-và-quyền-hạn-người-dùng)
5. [Yêu cầu Phi chức năng](#yêu-cầu-phi-chức-năng)
6. [Giả định và Ràng buộc](#giả-định-và-ràng-buộc)
7. [Ngoài Phạm vi (v1.0)](#ngoài-phạm-vi-v10)

---

## Tóm tắt Tổng quan

### Tầm nhìn

PickleBall Dating App là ứng dụng di động kết nối cộng đồng người chơi pickleball, giúp họ tìm sân tập luyện, tìm bạn chơi phù hợp và kết nối với huấn luyện viên. Ứng dụng sử dụng cơ chế ghép đôi kiểu Tinder để tạo trải nghiệm tìm kiếm thú vị và hiệu quả.

### Đối tượng Người dùng

1. **Chủ sân:** Người sở hữu/quản lý sân pickleball muốn cho thuê sân và tiếp cận khách hàng
2. **Người chơi:** Người chơi pickleball muốn tìm sân, tìm bạn chơi, tìm đối thủ
3. **Huấn luyện viên (HLV):** Người dạy pickleball muốn kết nối với học viên

### Giá trị Cốt lõi

- **Cho chủ sân:** Kênh tiếp thị hiệu quả, quản lý đặt sân dễ dàng trên điện thoại
- **Cho người chơi:** Tìm bạn chơi phù hợp theo trình độ, vị trí, lịch trình; Đặt sân nhanh chóng
- **Cho HLV:** Tiếp cận học viên tiềm năng, xây dựng thương hiệu cá nhân

---

## Bảng Tính năng

| Mã | Tên Tính năng | Mô tả | Độ ưu tiên | Phụ thuộc |
|----|---------------|-------|------------|-----------|
| F01 | Đăng ký và Xác thực Người dùng | Đăng ký và đăng nhập bằng email/password hoặc OTP | Must | - |
| F02 | Quản lý Hồ sơ Người dùng | Quản lý thông tin cá nhân, trình độ, lịch trình | Must | F01 |
| F03 | Quản lý Sân | Chủ sân tạo và quản lý thông tin sân | Must | F01 |
| F04 | Quản lý Sân con | Quản lý các sân con trong sân lớn | Must | F03 |
| F05 | Quản lý Khung giờ | Tạo và quản lý khung giờ cho thuê | Must | F04 |
| F06 | Tìm kiếm và Khám phá Sân | Người chơi tìm kiếm và xem thông tin sân | Must | F03 |
| F07 | Đặt Sân | Đặt sân và chờ chủ sân xác nhận | Must | F05, F06 |
| F08 | Quản lý Đặt sân | Chủ sân quản lý các yêu cầu đặt sân | Must | F07 |
| F09 | Ghép đôi Người chơi - Tìm Đối thủ | Tìm đối thủ đánh đơn với cơ chế swipe | Must | F02, F07 |
| F10 | Ghép đôi Người chơi - Tìm Bạn chơi | Tìm bạn chơi để tạo đội | Should | F02 |
| F11 | Ghép đôi Người chơi - Tìm Đội Thi đấu | Tìm đội thi đấu với cơ chế swipe | Should | F02, F10, F07 |
| F12 | Hồ sơ HLV và Tìm kiếm | HLV tạo hồ sơ, người chơi tìm HLV | Should | F01, F02 |
| F13 | Ghép đôi với HLV | Tìm HLV với cơ chế swipe | Should | F12 |
| F14 | Chat trong Ứng dụng | Nhắn tin giữa các người dùng đã ghép đôi | Must | F01 |
| F15 | Thông báo Đẩy | Thông báo về ghép đôi, đặt sân, tin nhắn | Must | F01 |
| F16 | Bảng Thống kê | Thống kê cho chủ sân | Could | F07, F08 |

---

## Chi tiết Tính năng

### F01: Đăng ký và Xác thực Người dùng

**Câu chuyện Người dùng:**
Là một người dùng mới, tôi muốn đăng ký và đăng nhập vào ứng dụng để có thể truy cập các tính năng dựa trên vai trò của tôi.

**Mô tả:**
Hệ thống xác thực cho phép người dùng đăng ký tài khoản mới và đăng nhập. Hỗ trợ 2 phương thức: email/password và OTP qua số điện thoại. Người dùng phải chọn vai trò khi đăng ký (Chủ sân, Người chơi, hoặc HLV). Một người chỉ có thể có 1 vai trò duy nhất.

**Tiêu chí Chấp nhận:**
- [ ] Người dùng có thể đăng ký bằng email và password
- [ ] Người dùng có thể đăng ký/đăng nhập bằng số điện thoại và OTP
- [ ] Password phải có ít nhất 8 ký tự, bao gồm chữ và số
- [ ] OTP có hiệu lực trong 5 phút
- [ ] Người dùng phải chọn 1 trong 3 vai trò: Chủ sân, Người chơi, HLV
- [ ] Không thể thay đổi vai trò sau khi đăng ký
- [ ] Hệ thống gửi email xác nhận khi đăng ký bằng email
- [ ] Người dùng có thể đặt lại password qua email hoặc OTP

**Trường hợp Đặc biệt:**
- Email đã tồn tại trong hệ thống
- Số điện thoại đã được sử dụng
- OTP nhập sai quá 5 lần -> khóa tạm thời 15 phút
- Mất kết nối khi đang xác thực OTP

---

### F02: Quản lý Hồ sơ Người dùng

**Câu chuyện Người dùng:**
Là một người dùng, tôi muốn quản lý thông tin hồ sơ của mình để người khác có thể biết về tôi và hệ thống có thể ghép đôi tôi một cách phù hợp.

**Mô tả:**
Người dùng có thể cập nhật thông tin cá nhân. Đối với người chơi, họ có thể khai báo trình độ và lịch trình rảnh để hệ thống ghép đôi chính xác hơn.

**Tiêu chí Chấp nhận:**
- [ ] Người dùng có thể cập nhật: Họ tên, Ảnh đại diện, Ngày sinh, Giới tính, Số điện thoại
- [ ] Người chơi có thể khai báo trình độ từ 1-5 (1: Mới bắt đầu, 5: Chuyên nghiệp)
- [ ] Người chơi có thể thiết lập lịch trình rảnh (ngày trong tuần + khung giờ)
- [ ] Người chơi có thể cập nhật vị trí hiện tại hoặc vị trí ưu tiên
- [ ] Ảnh đại diện được cắt thành hình tròn, kích thước tối đa 5MB
- [ ] Thông tin bắt buộc: Họ tên, Giới tính, Ngày sinh

**Trường hợp Đặc biệt:**
- Tải lên ảnh quá lớn (> 5MB)
- Định dạng ảnh không hỗ trợ
- Thay đổi số điện thoại cần xác thực lại OTP

**Trường Dữ liệu - Người chơi:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| full_name | String | Có | Họ và tên |
| avatar | Image | Không | Ảnh đại diện |
| date_of_birth | Date | Có | Ngày sinh |
| gender | Enum | Có | Nam/Nữ/Khác |
| phone | String | Có | Số điện thoại |
| skill_level | Integer | Không | Trình độ 1-5 |
| location | GeoPoint | Không | Vị trí ưu tiên |
| availability | JSON | Không | Lịch trình rảnh |

---

### F03: Quản lý Sân

**Câu chuyện Người dùng:**
Là một chủ sân, tôi muốn tạo và quản lý thông tin sân của mình để người chơi có thể tìm thấy và đặt sân.

**Mô tả:**
Chủ sân có thể tạo sân pickleball với đầy đủ thông tin: tên sân, địa chỉ, người liên hệ, số điện thoại, mô tả, hình ảnh. Đây là sân "cha" chứa các sân con bên trong.

**Tiêu chí Chấp nhận:**
- [ ] Chủ sân có thể tạo sân mới với thông tin cơ bản
- [ ] Chủ sân có thể tải lên tối đa 10 hình ảnh cho sân
- [ ] Địa chỉ sân được chuyển đổi thành tọa độ để hiển thị trên bản đồ
- [ ] Chủ sân có thể cập nhật thông tin sân bất kỳ lúc nào
- [ ] Chủ sân có thể tạm đóng/mở lại sân
- [ ] Chủ sân có thể xóa sân (chỉ khi không có đặt sân đang chờ)

**Trường hợp Đặc biệt:**
- Địa chỉ không hợp lệ, không thể chuyển đổi thành tọa độ
- Xóa sân khi còn đặt sân chưa hoàn thành
- Tải lên hình ảnh quá lớn hoặc sai định dạng

**Trường Dữ liệu - Sân:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| name | String | Có | Tên sân |
| address | String | Có | Địa chỉ đầy đủ |
| location | GeoPoint | Có | Tọa độ GPS |
| contact_name | String | Có | Người liên hệ |
| contact_phone | String | Có | SĐT liên hệ |
| description | Text | Không | Mô tả sân |
| images | Array[Image] | Không | Tối đa 10 ảnh |
| status | Enum | Có | Hoạt động/Tạm đóng |
| amenities | Array[String] | Không | Tiện ích (đỗ xe, WC, nước...) |

---

### F04: Quản lý Sân con

**Câu chuyện Người dùng:**
Là một chủ sân, tôi muốn quản lý từng sân con trong cơ sở của mình để người chơi có thể đặt sân cụ thể.

**Mô tả:**
Một sân lớn có thể có nhiều sân con (ví dụ: Sân A, Sân B, Sân C). Chủ sân quản lý từng sân con riêng biệt để người chơi có thể đặt cụ thể.

**Tiêu chí Chấp nhận:**
- [ ] Chủ sân có thể tạo nhiều sân con trong 1 sân lớn
- [ ] Mỗi sân con có tên riêng (VD: Sân A, Sân 1)
- [ ] Chủ sân có thể đặt trạng thái cho từng sân con (Hoạt động/Bảo trì)
- [ ] Chủ sân có thể xóa sân con (chỉ khi không có đặt sân đang chờ)
- [ ] Hiển thị số lượng sân con trên trang thông tin sân

**Trường hợp Đặc biệt:**
- Xóa sân con khi còn đặt sân
- Đặt trạng thái "Bảo trì" khi có đặt sân sắp tới

**Trường Dữ liệu - Sân con:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| court_id | Reference | Có | Sân cha |
| name | String | Có | Tên sân con |
| status | Enum | Có | Hoạt động/Bảo trì |

---

### F05: Quản lý Khung giờ

**Câu chuyện Người dùng:**
Là một chủ sân, tôi muốn tạo các khung giờ cho sân của mình để người chơi có thể xem lịch trống và đặt sân.

**Mô tả:**
Chủ sân tạo các khung giờ cho thuê cho từng sân con. Mỗi khung giờ có thời gian bắt đầu, kết thúc và giá thuê.

**Tiêu chí Chấp nhận:**
- [ ] Chủ sân có thể tạo khung giờ cho từng sân con
- [ ] Khung giờ có: Giờ bắt đầu, Giờ kết thúc, Giá thuê
- [ ] Chủ sân có thể tạo khung giờ lặp lại theo ngày trong tuần
- [ ] Chủ sân có thể tạo khung giờ cho ngày cụ thể
- [ ] Khung giờ tối thiểu là 30 phút
- [ ] Không cho phép khung giờ chồng chéo trên cùng 1 sân con
- [ ] Chủ sân có thể xóa/sửa khung giờ (chỉ khi chưa có đặt sân)

**Trường hợp Đặc biệt:**
- Tạo khung giờ chồng chéo
- Sửa khung giờ đã có người đặt
- Xóa khung giờ đã có đặt sân

**Trường Dữ liệu - Khung giờ:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| sub_court_id | Reference | Có | Sân con |
| start_time | Time | Có | Giờ bắt đầu |
| end_time | Time | Có | Giờ kết thúc |
| price | Decimal | Có | Giá thuê (VND) |
| day_of_week | Integer | Không | 0-6 (CN-T7), null = ngày cụ thể |
| specific_date | Date | Không | Ngày cụ thể nếu không lặp lại |
| is_available | Boolean | Có | Còn trống hay không |

---

### F06: Tìm kiếm và Khám phá Sân

**Câu chuyện Người dùng:**
Là một người chơi, tôi muốn tìm kiếm và duyệt các sân có sẵn để có thể tìm nơi chơi phù hợp.

**Mô tả:**
Người chơi có thể tìm kiếm sân theo vị trí, xem thông tin chi tiết, hình ảnh và các khung giờ còn trống.

**Tiêu chí Chấp nhận:**
- [ ] Hiển thị danh sách sân gần vị trí hiện tại của người chơi
- [ ] Có thể lọc theo khoảng cách (1km, 3km, 5km, 10km)
- [ ] Có thể tìm kiếm theo tên sân
- [ ] Hiển thị thông tin sân: Tên, Địa chỉ, Khoảng cách, Số sân con, Hình ảnh
- [ ] Xem chi tiết sân: Mô tả, Tiện ích, Tất cả hình ảnh
- [ ] Xem danh sách sân con và trạng thái
- [ ] Xem các khung giờ còn trống theo ngày

**Trường hợp Đặc biệt:**
- Không có sân nào trong bán kính tìm kiếm
- Vị trí GPS không bật
- Sân không có hình ảnh

---

### F07: Đặt Sân

**Câu chuyện Người dùng:**
Là một người chơi, tôi muốn đặt một khung giờ sân để có thể đảm bảo chỗ chơi.

**Mô tả:**
Người chơi chọn khung giờ và gửi yêu cầu đặt sân. Yêu cầu sẽ ở trạng thái "Chờ xác nhận" cho đến khi chủ sân chấp nhận hoặc từ chối. Thanh toán thực hiện tại sân.

**Tiêu chí Chấp nhận:**
- [ ] Người chơi có thể chọn khung giờ và gửi yêu cầu đặt sân
- [ ] Yêu cầu đặt sân bao gồm: Sân con, Khung giờ, Ngày, Ghi chú
- [ ] Trạng thái đặt sân: Chờ xác nhận -> Đã xác nhận/Bị từ chối
- [ ] Người chơi nhận thông báo khi đặt sân được xác nhận hoặc từ chối
- [ ] Người chơi có thể hủy đặt sân khi còn ở trạng thái Chờ xác nhận
- [ ] Người chơi có thể xem lịch sử đặt sân của mình
- [ ] Không cho đặt khung giờ đã có người đặt (đã xác nhận)

**Trường hợp Đặc biệt:**
- 2 người đặt cùng khung giờ cùng lúc (xung đột đồng thời)
- Chủ sân không phản hồi trong thời gian dài
- Người chơi hủy sau khi đã được xác nhận

**Trường Dữ liệu - Đặt sân:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| player_id | Reference | Có | Người đặt |
| sub_court_id | Reference | Có | Sân con |
| time_slot_id | Reference | Có | Khung giờ |
| booking_date | Date | Có | Ngày đặt sân |
| status | Enum | Có | Chờ xác nhận/Đã xác nhận/Bị từ chối/Đã hủy |
| note | Text | Không | Ghi chú của người đặt |
| reject_reason | Text | Không | Lý do từ chối (nếu có) |
| created_at | DateTime | Có | Thời gian tạo |

---

### F08: Quản lý Đặt sân

**Câu chuyện Người dùng:**
Là một chủ sân, tôi muốn quản lý các yêu cầu đặt sân để có thể xác nhận hoặc từ chối đặt chỗ.

**Mô tả:**
Chủ sân xem danh sách yêu cầu đặt sân và quyết định chấp nhận hoặc từ chối. Có thể xem lịch đặt sân theo ngày.

**Tiêu chí Chấp nhận:**
- [ ] Chủ sân nhận thông báo khi có yêu cầu đặt sân mới
- [ ] Hiển thị danh sách đặt sân theo trạng thái (Chờ xác nhận/Đã xác nhận/Tất cả)
- [ ] Chủ sân có thể xem chi tiết đặt sân: Thông tin người đặt, Sân, Khung giờ, Ghi chú
- [ ] Chủ sân có thể Chấp nhận hoặc Từ chối đặt sân
- [ ] Khi từ chối, chủ sân có thể nhập lý do
- [ ] Xem lịch đặt sân dạng Lịch theo ngày/tuần
- [ ] Lọc đặt sân theo sân con

**Trường hợp Đặc biệt:**
- Nhiều đặt sân đang chờ cho cùng khung giờ
- Chủ sân không trực tuyến để xử lý đặt sân
- Đặt sân tự động hủy nếu không xử lý sau X giờ (tùy chọn - Could have)

---

### F09: Ghép đôi Người chơi - Tìm Đối thủ (Đánh đơn)

**Câu chuyện Người dùng:**
Là một người chơi, tôi muốn tìm đối thủ để đánh đơn bằng cơ chế swipe để có thể dễ dàng tìm người chơi cùng.

**Mô tả:**
Người chơi tìm đối thủ đánh đơn bằng cách swipe. Hệ thống gợi ý dựa trên vị trí, trình độ và lịch trình. Khi cả 2 người cùng swipe phải (Thích), tạo ghép đôi và có thể đặt sân.

**Tiêu chí Chấp nhận:**
- [ ] Hiển thị thẻ hồ sơ người chơi với: Ảnh đại diện, Tên, Tuổi, Trình độ, Khoảng cách
- [ ] Swipe phải = Thích, Swipe trái = Bỏ qua
- [ ] Ghép đôi xảy ra khi cả 2 người cùng Thích nhau
- [ ] Gợi ý dựa trên: Vị trí (gần nhất), Trình độ (tương đương), Lịch trình (trùng khung giờ)
- [ ] Khi ghép đôi thành công:
  - Nếu trùng đúng 1 khung giờ rảnh -> Chuyển đến màn hình đặt sân
  - Nếu trùng nhiều khung giờ -> Hiển thị danh sách khung giờ để chọn, sau đó đặt sân
- [ ] Người dùng nhận thông báo khi có ghép đôi mới
- [ ] Xem danh sách các ghép đôi của mình

**Thuật toán Ghép đôi (Thứ tự Ưu tiên):**
1. Lịch trình trùng nhau (có ít nhất 1 khung giờ chung)
2. Khoảng cách gần (trong bán kính 10km)
3. Trình độ chênh lệch không quá 1 bậc

**Trường hợp Đặc biệt:**
- Không có người chơi nào phù hợp trong khu vực
- Người chơi chưa thiết lập lịch trình
- Người chơi đã swipe hết tất cả gợi ý
- Ghép đôi nhưng không ai đặt sân

**Trường Dữ liệu - Ghép đôi:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| player1_id | Reference | Có | Người chơi 1 |
| player2_id | Reference | Có | Người chơi 2 |
| match_type | Enum | Có | Đơn/Đôi/Bạn chơi/HLV |
| status | Enum | Có | Chờ/Đã ghép/Hết hạn |
| matched_at | DateTime | Không | Thời gian ghép đôi |
| common_slots | JSON | Không | Các khung giờ trùng nhau |

---

### F10: Ghép đôi Người chơi - Tìm Bạn chơi

**Câu chuyện Người dùng:**
Là một người chơi, tôi muốn tìm bạn chơi đôi để có thể tạo đội cho các trận đánh đôi.

**Mô tả:**
Người chơi tìm bạn chơi để tạo thành 1 đội (team). Sau khi ghép đôi, 2 người trở thành đồng đội và có thể cùng tìm đối thủ (F11).

**Tiêu chí Chấp nhận:**
- [ ] Giao diện swipe tương tự F09
- [ ] Gợi ý dựa trên: Vị trí, Trình độ tương đương, Lịch trình trùng
- [ ] Khi ghép đôi, 2 người trở thành "Đồng đội" (đội)
- [ ] Mỗi người chỉ có thể có 1 đồng đội tại 1 thời điểm
- [ ] Có thể hủy liên kết đồng đội bất kỳ lúc nào
- [ ] Sau khi có đồng đội, có thể sử dụng F11 để tìm đội thi đấu

**Trường hợp Đặc biệt:**
- Đã có đồng đội, muốn đổi đồng đội mới
- Đồng đội hủy liên kết
- Tìm đồng đội nhưng chưa thiết lập lịch trình

---

### F11: Ghép đôi Người chơi - Tìm Đội Thi đấu (Đội vs Đội)

**Câu chuyện Người dùng:**
Là một đội đánh đôi, tôi muốn tìm đội khác để thi đấu để có thể chơi trận đánh đôi.

**Mô tả:**
Sau khi có đồng đội (F10), đội có thể tìm đối thủ khác để đánh đôi. Tương tự F09 nhưng ghép đôi giữa 2 đội.

**Tiêu chí Chấp nhận:**
- [ ] Chỉ khả dụng khi người chơi đã có đồng đội
- [ ] Hiển thị thẻ hồ sơ của đội: Ảnh đại diện 2 người, Tên đội/Tên 2 người, Trình độ trung bình
- [ ] Swipe để tìm đối thủ
- [ ] Khi ghép đôi:
  - Nếu trùng 1 khung giờ -> Đặt sân
  - Nếu trùng nhiều khung giờ -> Chọn khung giờ rồi đặt sân
- [ ] Cả 4 người đều nhận thông báo khi ghép đôi

**Trường hợp Đặc biệt:**
- 1 trong 2 người của đội không rảnh khung giờ đã chọn
- Đồng đội hủy liên kết giữa chừng

---

### F12: Hồ sơ HLV và Tìm kiếm

**Câu chuyện Người dùng:**
Là một huấn luyện viên, tôi muốn tạo hồ sơ của mình để người chơi có thể tìm thấy và học từ tôi.
Là một người chơi, tôi muốn tìm huấn luyện viên để có thể nâng cao kỹ năng.

**Mô tả:**
Huấn luyện viên tạo hồ sơ với thông tin chuyên môn. Người chơi có thể tìm kiếm và xem hồ sơ HLV.

**Tiêu chí Chấp nhận:**
- [ ] HLV có thể tạo hồ sơ với: Giới thiệu, Kinh nghiệm, Chuyên môn, Giá/giờ, Địa điểm dạy
- [ ] HLV có thể tải lên video/hình ảnh minh họa
- [ ] Người chơi có thể tìm HLV theo vị trí
- [ ] Người chơi có thể xem chi tiết hồ sơ HLV
- [ ] HLV có thể thiết lập lịch trình dạy

**Trường Dữ liệu - Hồ sơ HLV:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| user_id | Reference | Có | Liên kết Người dùng |
| bio | Text | Không | Giới thiệu bản thân |
| experience_years | Integer | Không | Số năm kinh nghiệm |
| specialties | Array[String] | Không | Chuyên môn |
| hourly_rate | Decimal | Không | Giá/giờ (VND) |
| teaching_locations | Array[GeoPoint] | Không | Địa điểm dạy |
| availability | JSON | Không | Lịch trình dạy |
| media | Array[URL] | Không | Video/Hình ảnh |

---

### F13: Ghép đôi với HLV

**Câu chuyện Người dùng:**
Là một người chơi, tôi muốn tìm huấn luyện viên bằng cơ chế swipe để có thể dễ dàng kết nối với HLV phù hợp.

**Mô tả:**
Người chơi tìm HLV bằng cách swipe. Khi ghép đôi, cả 2 có thể chat để sắp xếp lịch học.

**Tiêu chí Chấp nhận:**
- [ ] Hiển thị thẻ HLV với: Ảnh đại diện, Tên, Kinh nghiệm, Giá/giờ, Khoảng cách
- [ ] Swipe phải = Quan tâm, Swipe trái = Bỏ qua
- [ ] Ghép đôi khi cả Người chơi và HLV cùng Thích nhau
- [ ] Sau khi ghép đôi, mở khóa chat để trao đổi chi tiết
- [ ] Không tự động đặt sân (tự thỏa thuận)

**Trường hợp Đặc biệt:**
- HLV không phản hồi sau khi ghép đôi
- Người chơi muốn học nhóm (nhiều người chơi 1 HLV) - Ngoài phạm vi v1

---

### F14: Chat trong Ứng dụng

**Câu chuyện Người dùng:**
Là một người dùng, tôi muốn chat với những người đã ghép đôi với mình để có thể phối hợp và liên lạc.

**Mô tả:**
Hệ thống chat cho phép người dùng đã ghép đôi nhắn tin với nhau. Hỗ trợ tin nhắn văn bản và hình ảnh.

**Tiêu chí Chấp nhận:**
- [ ] Chỉ mở chat giữa những người đã ghép đôi
- [ ] Gửi và nhận tin nhắn văn bản
- [ ] Gửi hình ảnh (tối đa 5 ảnh/lần, mỗi ảnh tối đa 5MB)
- [ ] Hiển thị trạng thái tin nhắn: Đã gửi, Đã nhận, Đã đọc
- [ ] Hiển thị thời gian gửi tin nhắn
- [ ] Thông báo đẩy khi có tin nhắn mới (khi ứng dụng ở nền)
- [ ] Hiển thị số tin nhắn chưa đọc trên biểu tượng chat

**Trường hợp Đặc biệt:**
- Gửi tin nhắn khi mất mạng
- Người nhận chặn hoặc báo cáo
- Tin nhắn chưa tải lên hình ảnh thành công

**Trường Dữ liệu - Tin nhắn:**
| Trường | Kiểu | Bắt buộc | Mô tả |
|--------|------|----------|-------|
| conversation_id | Reference | Có | Cuộc hội thoại |
| sender_id | Reference | Có | Người gửi |
| content | Text | Không | Nội dung văn bản |
| images | Array[URL] | Không | Hình ảnh đính kèm |
| status | Enum | Có | Đã gửi/Đã nhận/Đã đọc |
| created_at | DateTime | Có | Thời gian gửi |

---

### F15: Thông báo Đẩy

**Câu chuyện Người dùng:**
Là một người dùng, tôi muốn nhận thông báo đẩy để không bỏ lỡ các cập nhật quan trọng.

**Mô tả:**
Hệ thống gửi thông báo đẩy cho các sự kiện quan trọng.

**Tiêu chí Chấp nhận:**
- [ ] Thông báo khi có ghép đôi mới
- [ ] Thông báo khi có tin nhắn mới
- [ ] Thông báo khi có yêu cầu đặt sân mới (cho chủ sân)
- [ ] Thông báo khi đặt sân được xác nhận/từ chối (cho người chơi)
- [ ] Thông báo nhắc lịch đánh trước 1 giờ
- [ ] Người dùng có thể bật/tắt từng loại thông báo trong Cài đặt

**Các Loại Thông báo:**
| Loại | Người nhận | Kích hoạt |
|------|------------|-----------|
| GHEP_DOI_MOI | Người chơi/HLV | Khi 2 người ghép đôi thành công |
| TIN_NHAN_MOI | Tất cả | Khi nhận tin nhắn mới |
| DAT_SAN_MOI | Chủ sân | Khi có yêu cầu đặt sân |
| DAT_SAN_XAC_NHAN | Người chơi | Khi đặt sân được xác nhận |
| DAT_SAN_TU_CHOI | Người chơi | Khi đặt sân bị từ chối |
| NHAC_LICH_DANH | Người chơi | 1 giờ trước giờ đánh |

---

### F16: Bảng Thống kê

**Câu chuyện Người dùng:**
Là một chủ sân, tôi muốn xem thống kê về sân của mình để có thể hiểu hiệu quả kinh doanh.

**Mô tả:**
Bảng điều khiển hiển thị các số liệu thống kê cho chủ sân.

**Tiêu chí Chấp nhận:**
- [ ] Tổng số lượt đặt sân (theo tháng/tuần)
- [ ] Tỷ lệ sân được đặt (tỷ lệ lấp đầy)
- [ ] Doanh thu ước tính (dựa trên giá khung giờ)
- [ ] Sân con được đặt nhiều nhất
- [ ] Khung giờ được đặt nhiều nhất
- [ ] Biểu đồ xu hướng theo thời gian

**Trường hợp Đặc biệt:**
- Chưa có dữ liệu (sân mới tạo)
- Dữ liệu quá nhiều (phân trang/tải chậm)

---

## Vai trò và Quyền hạn Người dùng

### Vai trò: Chủ sân

| Quyền hạn | Mô tả |
|-----------|-------|
| TẠO_SÂN | Tạo sân mới |
| QUẢN_LÝ_SÂN | Sửa/Xóa sân của mình |
| QUẢN_LÝ_SÂN_CON | Thêm/Sửa/Xóa sân con |
| QUẢN_LÝ_KHUNG_GIỜ | Thêm/Sửa/Xóa khung giờ |
| XEM_ĐẶT_SÂN | Xem danh sách đặt sân |
| QUẢN_LÝ_ĐẶT_SÂN | Xác nhận/Từ chối đặt sân |
| XEM_THỐNG_KÊ | Xem thống kê |
| CHAT | Chat với người đặt sân |

### Vai trò: Người chơi

| Quyền hạn | Mô tả |
|-----------|-------|
| TÌM_SÂN | Tìm kiếm sân |
| ĐẶT_SÂN | Đặt sân |
| XEM_ĐẶT_SÂN_CỦA_MÌNH | Xem đặt sân của mình |
| HỦY_ĐẶT_SÂN | Hủy đặt sân (khi còn chờ xác nhận) |
| SWIPE_NGƯỜI_CHƠI | Tìm đối thủ/bạn chơi |
| SWIPE_HLV | Tìm HLV |
| QUẢN_LÝ_ĐỒNG_ĐỘI | Quản lý đồng đội |
| CHAT | Chat với các ghép đôi |

### Vai trò: Huấn luyện viên

| Quyền hạn | Mô tả |
|-----------|-------|
| QUẢN_LÝ_HỒ_SƠ_HLV | Quản lý hồ sơ HLV |
| XEM_NGƯỜI_QUAN_TÂM | Xem người quan tâm |
| SWIPE_NGƯỜI_CHƠI | Chọn học viên |
| CHAT | Chat với các ghép đôi |

---

## Yêu cầu Phi chức năng

### Hiệu suất

- Thời gian tải ứng dụng: < 3 giây trên 4G
- Thời gian phản hồi API: < 500ms cho các API thông thường
- Tải hình ảnh: Sử dụng lazy loading và cache
- Hoạt ảnh swipe: 60fps, không giật lag
- Hỗ trợ 10.000 người dùng đồng thời trong giai đoạn 1

### Bảo mật

- HTTPS cho tất cả API calls
- JWT token cho xác thực, hết hạn sau 7 ngày
- Refresh token hết hạn sau 30 ngày
- Mã hóa password bằng bcrypt
- Giới hạn tốc độ: 100 yêu cầu/phút/người dùng
- Xác thực đầu vào cho tất cả biểu mẫu
- Ngăn chặn SQL injection
- Bảo vệ XSS

### Khả năng Mở rộng

- Mở rộng ngang cho backend
- CDN cho tài nguyên tĩnh (hình ảnh)
- Đánh chỉ mục cơ sở dữ liệu cho các truy vấn thường xuyên
- Lớp cache (Redis) cho phiên và dữ liệu truy cập thường xuyên

### Khả năng Sử dụng

- Hỗ trợ tiếng Việt
- Thiết kế đáp ứng cho nhiều kích thước màn hình
- Chế độ ngoại tuyến: Xem dữ liệu đã cache khi mất mạng
- Thông báo lỗi rõ ràng, hướng dẫn người dùng

### Tương thích

- iOS 13.0+
- Android 8.0+ (API level 26)
- Ứng dụng lai (React Native hoặc Flutter)

### Độ tin cậy

- Mục tiêu thời gian hoạt động: 99.5%
- Tự động thử lại cho các yêu cầu thất bại
- Suy giảm ưu nhã khi 1 dịch vụ ngừng hoạt động

---

## Giả định và Ràng buộc

### Giả định

1. Người dùng có điện thoại thông minh với kết nối internet
2. Người dùng cho phép truy cập vị trí (GPS)
3. Chủ sân có khả năng sử dụng điện thoại thông minh cơ bản
4. Thanh toán thực hiện trực tiếp tại sân (không qua ứng dụng)
5. Mỗi người chỉ dùng 1 tài khoản với 1 vai trò
6. Sân pickleball đã tồn tại và hoạt động (không phải sân ảo)

### Ràng buộc

1. **Ngân sách:** Không tích hợp cổng thanh toán trong v1.0
2. **Thời gian:** MVP trong 3 tháng
3. **Công nghệ:** Ứng dụng lai để tiết kiệm thời gian và chi phí
4. **Khu vực:** Tập trung thị trường Việt Nam trước
5. **Ngôn ngữ:** Chỉ hỗ trợ tiếng Việt trong v1.0

---

## Ngoài Phạm vi (v1.0)

Các tính năng sau sẽ KHÔNG có trong phiên bản 1.0:

1. **Giải đấu** - Tạo và quản lý giải đấu
2. **Cổng Thanh toán** - Thanh toán trực tuyến qua ứng dụng
3. **Đánh giá và Nhận xét** - Đánh giá sân và người chơi
4. **Đặt cọc** - Hệ thống đặt cọc khi đặt sân
5. **Chính sách Hủy** - Chính sách hủy và hoàn tiền tự động
6. **Trang Quản trị Web** - Giao diện web cho chủ sân
7. **Đa ngôn ngữ** - Hỗ trợ nhiều ngôn ngữ
8. **Dạy Nhóm** - Lớp học nhóm với 1 HLV
9. **Tính năng Xã hội** - Chia sẻ, theo dõi, bảng xếp hạng
10. **Phân tích Nâng cao** - Phân tích nâng cao cho người chơi
11. **Gọi Video** - Gọi video trong ứng dụng
12. **Chương trình Khách hàng Thân thiết** - Chương trình tích điểm

---

## Phụ lục

### Bảng Thuật ngữ

| Thuật ngữ | Định nghĩa |
|-----------|------------|
| Sân | Sân pickleball lớn (cơ sở) |
| Sân con | Sân nhỏ bên trong sân lớn |
| Khung giờ | Khoảng thời gian cho thuê |
| Đặt sân | Yêu cầu thuê sân |
| Ghép đôi | Kết nối thành công giữa 2 người/đội |
| Đồng đội | Bạn chơi trong đội đánh đôi |
| Swipe | Thao tác vuốt để Thích/Bỏ qua |

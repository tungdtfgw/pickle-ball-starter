# User Profile - Player Screen

## Screen Overview

Màn hình Hồ sơ cho phép người chơi quản lý toàn bộ thông tin cá nhân, bao gồm thông tin cơ bản (tên, ảnh đại diện, ngày sinh, giới tính), thông tin chơi bóng (trình độ), lịch trình rảnh và vị trí ưu tiên. Screen có 2 trạng thái chính: **View Mode** (xem thông tin) và **Edit Mode** (chỉnh sửa thông tin).

---

## Mục đích

Người chơi sử dụng screen này để:
- Xem và cập nhật thông tin cá nhân
- Khai báo trình độ chơi để hệ thống ghép đôi chính xác
- Thiết lập lịch trình rảnh để tìm đối thủ/bạn chơi có lịch trùng
- Cập nhật vị trí ưu tiên để tìm sân và người chơi gần nhất

---

## Các Section Chính

### 1. Header Section

**View Mode:**
- Back button (icon mũi tên trái) ở góc trái
- Title: "Hồ sơ của tôi" (center)
- Edit button (icon bút chì) ở góc phải

**Edit Mode:**
- Cancel button (text "Hủy") ở góc trái
- Title: "Chỉnh sửa hồ sơ" (center)
- Save button (text "Lưu") ở góc phải

**Tương tác:**
- Tap Back button → Quay về màn hình trước
- Tap Edit button → Chuyển sang Edit Mode, các field trở thành editable
- Tap Cancel → Hiện confirm dialog nếu có thay đổi
- Tap Save → Validate và lưu thông tin

**Hiệu ứng:**
- Fade transition giữa View và Edit mode
- Save button disable khi form invalid (màu xám)

---

### 2. Avatar & Basic Info Section

**Components:**

#### 2.1. Avatar (Large, 120x120px)
- **View Mode:**
  - Hiển thị ảnh đại diện hình tròn
  - Border 2px màu primary khi có ảnh
  - Icon placeholder (user icon) nếu chưa có ảnh

- **Edit Mode:**
  - Overlay với icon camera ở giữa
  - Text "Đổi ảnh" bên dưới icon

**Tương tác:**
- Tap avatar trong Edit Mode → Hiện Bottom Sheet với 2 options:
  - "Chụp ảnh mới" (icon camera)
  - "Chọn từ thư viện" (icon gallery)
- Chọn "Chụp ảnh mới" → Mở camera (selfie mode)
- Chọn "Chọn từ thư viện" → Mở gallery
- Sau khi chọn ảnh → Màn hình crop ảnh hình tròn (zoom/pan)
- Tap "Xác nhận" → Upload ảnh và hiển thị loading spinner trên avatar

**Hiệu ứng:**
- Bottom Sheet slide up from bottom
- Loading spinner khi upload
- Fade in khi ảnh mới hiển thị

#### 2.2. Full Name
- **View Mode:** Text hiển thị tên (font size 20, bold)
- **Edit Mode:** Text input với placeholder "Nhập họ và tên"

**Validation:**
- Bắt buộc
- 2-50 ký tự
- Chỉ chữ cái, dấu cách, dấu ngoặc
- Show error text bên dưới nếu invalid

#### 2.3. Age, Gender, Badge
- **Age:** Calculated từ date of birth, hiển thị "X tuổi" (không editable)
- **Gender:** Icon + text (Nam/Nữ/Khác)
- **Badge:** Chip hiển thị "Level X" dựa vào skill level (1-5)

---

### 3. Personal Information Section

**Title:** "Thông tin cá nhân" (section header)

#### 3.1. Date of Birth
- **View Mode:** "Ngày sinh: DD/MM/YYYY"
- **Edit Mode:** Date picker field

**Tương tác:**
- Tap field → Hiện date picker modal
- Chọn ngày → Auto-calculate age và hiển thị

**Validation:**
- Tuổi >= 13
- Không phải ngày tương lai

#### 3.2. Gender
- **View Mode:** "Giới tính: Nam/Nữ/Khác"
- **Edit Mode:** Segmented control với 3 options (Nam | Nữ | Khác)

**Tương tác:**
- Tap để chọn
- Highlight option được chọn (primary color)

#### 3.3. Phone Number
- **View Mode:** "SĐT: 0xxxxxxxxx"
- **Edit Mode:** Input với note "Thay đổi SĐT cần xác thực OTP"

**Tương tác:**
- Tap để edit → Hiện modal nhập SĐT mới
- Nhập SĐT mới → Tap "Gửi OTP"
- Kiểm tra SĐT chưa tồn tại → Gửi OTP
- Nhập OTP → Validate → Cập nhật SĐT

**Validation:**
- 10 chữ số
- Bắt đầu bằng 0
- Chưa được sử dụng bởi user khác

---

### 4. Skill & Stats Section (Người chơi)

**Title:** "Thông tin chơi bóng" (section header)

#### 4.1. Skill Level Selector
- **View Mode:**
  - Display: "Trình độ: ★★★☆☆ (3 - Trung bình)"
  - 5 sao, fill theo level
  - Text mô tả trình độ

- **Edit Mode:**
  - Slider (1-5) hoặc 5 star buttons để chọn
  - Text mô tả hiển thị dynamic khi chọn:
    - 1: "Mới bắt đầu - Chưa biết luật, cần học cơ bản"
    - 2: "Cơ bản - Biết luật, đánh được nhưng chưa ổn định"
    - 3: "Trung bình - Đánh ổn định, biết chiến thuật cơ bản"
    - 4: "Khá - Đánh tốt, có kỹ thuật và chiến thuật"
    - 5: "Chuyên nghiệp - Trình độ thi đấu, rất giỏi"

**Tương tác:**
- Kéo slider hoặc tap vào sao
- Mô tả cập nhật real-time
- Auto-save khi thay đổi (không cần tap Save button)

**Hiệu ứng:**
- Smooth slider animation
- Star fill animation (scale + color transition)

#### 4.2. Stats Display (Read-only, future feature)
- Matches played: 0 (placeholder)
- Win rate: 0% (placeholder)
- Note text: "Thống kê sẽ được cập nhật sau các trận đấu"

---

### 5. Availability Section (Lịch trình rảnh)

**Title:** "Lịch trình rảnh" (section header)

**View Mode:**
- Danh sách ngày trong tuần + khung giờ đã chọn
- Format: "Thứ 2: Sáng, Tối"
- Nếu chưa thiết lập: Text "Chưa thiết lập lịch trình" (màu xám)

**Edit Mode:**
- Button: "Chỉnh sửa lịch trình" → Navigate đến Availability Editor Screen

**Availability Editor Screen (Modal/Separate Screen):**

#### Layout:
- Header: "Thiết lập lịch trình rảnh"
- Danh sách 7 ngày: T2, T3, T4, T5, T6, T7, CN
- Mỗi ngày có 4 checkbox cho khung giờ:
  - ☐ Sáng (6:00 - 11:00)
  - ☐ Trua (11:00 - 14:00)
  - ☐ Chiều (14:00 - 18:00)
  - ☐ Tối (18:00 - 22:00)

#### Tương tác:
- Tap checkbox để toggle on/off
- Button "Sao chép" (mỗi ngày) → Chọn ngày khác để áp dụng lịch giống nhau
- Button "Xóa tất cả" → Confirm dialog → Bỏ chọn tất cả
- Button "Lưu" → Lưu lịch trình và quay lại Profile screen

**Hiệu ứng:**
- Checkbox animation (checkmark slide in)
- Modal slide up from bottom

---

### 6. Location Section (Vị trí ưu tiên)

**Title:** "Vị trí ưu tiên" (section header)

**View Mode:**
- Icon bản đồ + Text địa chỉ (nếu đã thiết lập)
- Nếu chưa: Text "Chưa thiết lập vị trí" (màu xám)

**Edit Mode:**
- Button: "Chỉnh sửa vị trí" → Navigate đến Location Picker Screen

**Location Picker Screen (Modal/Separate Screen):**

#### Layout:
- Header: "Chọn vị trí ưu tiên"
- Map view full screen
- Marker ở vị trí đang chọn
- Search bar ở trên map
- Bottom panel với:
  - Button "Sử dụng vị trí hiện tại" (GPS icon)
  - Address text (hiển thị địa chỉ của marker)
  - Button "Xác nhận"

#### Tương tác:
- **Option A:** Tap "Sử dụng vị trí hiện tại"
  - Check GPS permission → Yêu cầu nếu chưa cấp
  - Lấy GPS → Di chuyển map đến vị trí hiện tại
  - Đặt marker

- **Option B:** Kéo map
  - Marker cố định ở center
  - Kéo map để chọn vị trí
  - Address text cập nhật real-time

- **Option C:** Nhập địa chỉ vào search bar
  - Autocomplete suggestions
  - Chọn địa chỉ → Map jump đến vị trí đó

- Tap "Xác nhận" → Lưu tọa độ + địa chỉ và quay lại Profile

**Hiệu ứng:**
- Map zoom animation
- Marker drop animation

**Error Handling:**
- GPS tắt → Show dialog "Không thể lấy vị trí. Vui lòng nhập địa chỉ thủ công"
- Permission denied → Show error với hướng dẫn bật GPS
- Địa chỉ không tìm thấy → Show toast "Không tìm thấy địa chỉ"

---

### 7. Additional Info Section

**Title:** "Thông tin thêm" (section header)

#### 7.1. Bio/Description
- **View Mode:** Text paragraph (max 200 ký tự)
- **Edit Mode:** TextArea với character counter "X/200"

**Placeholder:** "Viết vài dòng về bản thân, sở thích chơi pickleball..."

#### 7.2. Sports Clubs (Optional, future)
- Placeholder: "Chức năng sẽ được bổ sung"

---

### 8. Action Buttons Section

**Buttons:**
- **Settings Button:** "Cài đặt" → Navigate to Settings Screen
- **Logout Button:** "Đăng xuất" (màu đỏ) → Confirm dialog → Logout

**Hiệu ứng:**
- Button press scale animation
- Logout confirmation dialog slide in

---

## Navigation

### Đến screen này từ:
- Tab bar (Profile tab)
- Side menu (nếu có)
- Onboarding flow (sau khi đăng ký)

### Từ screen này đến:
- Availability Editor Screen (Chỉnh sửa lịch trình)
- Location Picker Screen (Chọn vị trí)
- Settings Screen (Cài đặt)
- Login Screen (sau khi Logout)

---

## States

### 1. View Mode (Default)
- Tất cả fields read-only
- Edit button visible
- Scroll to view toàn bộ thông tin

### 2. Edit Mode
- Basic info fields editable
- Save/Cancel buttons visible
- Validation real-time

### 3. Loading State
- Khi đang lưu thông tin
- Disable tất cả interactions
- Show loading spinner (full screen overlay)

### 4. Error State
- Khi lưu thất bại
- Show error toast/alert: "Không thể lưu thông tin. Vui lòng thử lại"
- Giữ nguyên Edit Mode để user retry

### 5. Offline State
- Khi mất mạng
- Show banner: "Mất kết nối. Thay đổi sẽ được lưu khi có mạng"
- Cache thay đổi vào local storage
- Auto-sync khi online lại

---

## Ghi chú

### UX Considerations:
1. **Profile Completion Indicator:**
   - Hiển thị % hoàn thiện profile ở đầu screen
   - Ví dụ: "Hồ sơ hoàn thiện 60%" với progress bar
   - Khuyến khích user điền đủ thông tin

2. **Onboarding:**
   - Với user mới, highlight các trường chưa điền
   - Tooltip gợi ý "Thiết lập trình độ để tìm đối thủ phù hợp"

3. **Privacy:**
   - Thông tin này chỉ hiển thị cho người đã ghép đôi
   - SĐT không hiển thị công khai
   - Vị trí chỉ hiển thị khoảng cách, không hiển thị tọa độ cụ thể

4. **Validation:**
   - Real-time validation khi nhập
   - Inline error messages (màu đỏ, dưới field)
   - Disable Save button khi có lỗi

5. **Auto-save vs Manual save:**
   - Skill level: Auto-save (không cần tap Save)
   - Basic info: Manual save (tap Save button)
   - Availability, Location: Save trong sub-screen riêng

6. **Image Upload:**
   - Max size: 5MB
   - Formats: JPG, PNG, HEIC
   - Auto-compress đến 400x400px
   - Crop thành hình tròn
   - Show upload progress bar

### Edge Cases:
1. **Date of Birth < 13 tuổi:**
   - Show error: "Bạn phải từ 13 tuổi trở lên để sử dụng ứng dụng"

2. **Phone số đã tồn tại:**
   - Show error: "Số điện thoại này đã được đăng ký bởi người dùng khác"

3. **Upload ảnh quá lớn:**
   - Show error: "Ảnh quá lớn. Vui lòng chọn ảnh nhỏ hơn 5MB"

4. **Unsaved changes:**
   - Khi tap Back/Cancel trong Edit Mode
   - Dialog: "Bạn có thay đổi chưa lưu. Bạn có muốn hủy bỏ?"
   - Buttons: "Hủy bỏ" (destructive) | "Tiếp tục chỉnh sửa"

5. **OTP timeout:**
   - OTP hết hạn sau 5 phút
   - Show countdown timer "X:XX còn lại"
   - Button "Gửi lại OTP" khi hết hạn

6. **GPS không khả dụng:**
   - Fallback: Cho phép nhập địa chỉ thủ công
   - Không block user nếu không bật GPS

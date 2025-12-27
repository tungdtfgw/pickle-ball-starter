# Create First Court Screen

## Screen Overview

Màn hình "Tạo Sân Đầu Tiên" xuất hiện sau khi Chủ sân hoàn thành đăng ký tài khoản (F01). Đây là bước onboarding quan trọng để Chủ sân tạo sân pickleball đầu tiên của mình trên ứng dụng. Screen này tập trung vào thu thập thông tin cơ bản về sân, địa chỉ, hình ảnh và tiện ích, giúp người chơi có thể tìm thấy và đặt sân.

---

## Mục đích

Màn hình này giúp Chủ sân:
- Tạo sân pickleball đầu tiên một cách dễ dàng
- Cung cấp đầy đủ thông tin cần thiết để người chơi tìm thấy sân
- Hiểu rõ quy trình tạo sân → tạo sân con → tạo khung giờ
- Chuẩn bị sân để bắt đầu nhận đặt sân từ người chơi

---

## Onboarding Context

**Khi nào screen này xuất hiện:**
- Sau khi Chủ sân đăng ký tài khoản thành công (F01)
- Chưa có sân nào trong hệ thống
- Bắt buộc hoàn thành để có thể sử dụng các tính năng quản lý

**Onboarding Flow:**
```
Đăng ký (F01) → Chọn vai trò "Chủ sân"
→ Create First Court (Screen này)
→ Add Subcourts (F04)
→ Setup Time Slots (F05)
→ Dashboard
```

---

## Các thành phần chính

### 1. Header Section

**Components:**

#### 1.1. Progress Indicator (Top)
- **Mô tả:** Thanh tiến trình hiển thị bước hiện tại trong quy trình tạo sân
- **Layout:**
  - Horizontal stepper với 3 bước
  - Step 1: "Thông tin sân" (Active - màu primary)
  - Step 2: "Sân con" (Inactive - màu xám)
  - Step 3: "Khung giờ" (Inactive - màu xám)
  - Line nối giữa các bước

**Tương tác:**
- Read-only, không thể tap để chuyển bước
- Hiển thị user đang ở bước nào

**Hiệu ứng:**
- Step active có animation pulse nhẹ
- Line nối có gradient từ xanh (completed) sang xám (pending)

#### 1.2. Title & Navigation
- **Title:** "Tạo sân đầu tiên" (center, font size 18, bold)
- **Skip button:** "Bỏ qua" (top right, text button)
  - Tap → Hiện confirm dialog

**Skip Confirmation Dialog:**
- Title: "Bỏ qua tạo sân?"
- Message: "Bạn có thể tạo sân sau trong phần Quản lý sân. Bạn sẽ không thể nhận đặt sân nếu chưa tạo sân."
- Buttons:
  - "Tiếp tục tạo" (Primary)
  - "Bỏ qua" (Destructive)

**Hiệu ứng:**
- Dialog slide in from center với backdrop overlay

---

### 2. Welcome Message Section

**Mô tả:** Thông điệp chào mừng và hướng dẫn ngắn gọn

**Components:**
- Icon sân pickleball (hoặc illustration)
- Heading: "Chào mừng đến PickleBall Dating!"
- Subheading: "Hãy tạo sân đầu tiên để bắt đầu nhận đặt sân từ người chơi"
- Small text: "Bạn có thể chỉnh sửa thông tin sân bất kỳ lúc nào"

**Hiệu ứng:**
- Fade in animation khi screen load
- Icon có slight bounce animation

---

### 3. Court Basic Information Section

**Title:** "Thông tin cơ bản" (section header)

#### 3.1. Court Name Input
- **Label:** "Tên sân" (required indicator *)
- **Input field:**
  - Placeholder: "VD: Sân Pickleball Thảo Điền"
  - Max length: 100 ký tự
  - Character counter: "X/100"

**Tương tác:**
- Focus → Border màu primary
- Real-time validation on blur

**Validation:**
- Bắt buộc
- Minimum 2 ký tự
- Maximum 100 ký tự
- Không chứa ký tự đặc biệt ngoại trừ: dấu cách, dấu gạch ngang, dấu ngoặc
- Error: "Tên sân phải từ 2-100 ký tự"

**Hiệu ứng:**
- Error text fade in màu đỏ bên dưới input
- Border input chuyển sang đỏ khi error

#### 3.2. Contact Person Input
- **Label:** "Người liên hệ" (required *)
- **Placeholder:** "Tên người quản lý sân"

**Validation:**
- Bắt buộc
- 2-50 ký tự
- Error: "Vui lòng nhập tên người liên hệ"

#### 3.3. Contact Phone Input
- **Label:** "Số điện thoại liên hệ" (required *)
- **Placeholder:** "0xxxxxxxxx"
- **Keyboard type:** Number pad
- **Format:** Auto-format với dấu cách (0901 234 567)

**Validation:**
- Bắt buộc
- 10-11 chữ số
- Bắt đầu bằng 0
- Error: "Số điện thoại không hợp lệ"

**Hiệu ứng:**
- Auto-format khi nhập (thêm dấu cách)

---

### 4. Court Address Section

**Title:** "Địa chỉ sân" (section header)

#### 4.1. Address Input
- **Label:** "Địa chỉ" (required *)
- **Input field:**
  - Placeholder: "Nhập địa chỉ chi tiết (số nhà, đường, phường, quận/huyện, TP)"
  - Multiline: 2-3 lines
  - Autocomplete suggestions (Google Places API)

**Tương tác:**
- Nhập địa chỉ → Hiện dropdown suggestions
- Chọn suggestion → Auto-fill địa chỉ + trigger geocoding

**Validation:**
- Bắt buộc
- 10-200 ký tự
- Error: "Vui lòng nhập địa chỉ chi tiết"

#### 4.2. Map Preview Section
- **Mô tả:** Mini map hiển thị vị trí sân sau khi nhập địa chỉ
- **Layout:**
  - Map view (height 200dp)
  - Marker ở vị trí đã geocode
  - Button "Chỉnh sửa trên bản đồ" ở góc bottom-right của map

**Geocoding Flow:**
1. User nhập địa chỉ hoặc chọn suggestion
2. System call Geocoding API
3. **Nếu thành công:**
   - Hiện mini map với marker
   - Address text hiển thị địa chỉ đã format
4. **Nếu thất bại:**
   - Hiện error: "Không tìm thấy địa chỉ. Vui lòng chọn vị trí trên bản đồ"
   - Auto-open Map Editor Modal

**Tương tác:**
- Tap "Chỉnh sửa trên bản đồ" → Open Map Editor Modal
- Tap vào map preview → Open Map Editor Modal

**Hiệu ứng:**
- Map fade in khi geocoding thành công
- Marker drop animation

#### 4.3. Map Editor Modal (Full Screen)

**Header:**
- Title: "Chỉnh sửa vị trí sân"
- Close button (X) top-left
- Confirm button "Xác nhận" top-right (enabled khi có marker)

**Components:**
- **Search Bar** (top, trên map)
  - Placeholder: "Tìm kiếm địa điểm"
  - Autocomplete suggestions
  - Clear button (X)

- **Full Screen Map**
  - Marker cố định ở center
  - Current location button (bottom-right)
  - Zoom in/out buttons (right side)

- **Bottom Panel** (slide up, height ~30% screen)
  - Icon pin + Text: "Vị trí đã chọn"
  - Address text (dynamic update khi kéo map)
  - Button "Sử dụng vị trí hiện tại" (GPS icon)
  - Button "Xác nhận" (Primary, full width)

**Tương tác:**

**Option A: Kéo map để chọn vị trí**
1. Marker cố định ở center
2. User kéo map
3. Address text update real-time (reverse geocoding)
4. Tap "Xác nhận" → Lưu tọa độ + địa chỉ, đóng modal

**Option B: Tìm kiếm địa chỉ**
1. Tap search bar → Keyboard slide up
2. Nhập địa chỉ → Autocomplete suggestions
3. Chọn suggestion → Map jump đến vị trí
4. Tap "Xác nhận" → Lưu

**Option C: Sử dụng GPS hiện tại**
1. Tap "Sử dụng vị trí hiện tại"
2. Check GPS permission
   - Nếu chưa cấp → Request permission
   - Nếu từ chối → Error "Vui lòng cấp quyền truy cập vị trí"
3. Lấy GPS → Map jump đến vị trí hiện tại
4. Tap "Xác nhận" → Lưu

**Hiệu ứng:**
- Map zoom/pan smooth animation
- Address text fade update
- Bottom panel slide up from bottom

**Error Handling:**
- GPS tắt → Toast "Vui lòng bật GPS để sử dụng vị trí hiện tại"
- Permission denied → Dialog hướng dẫn bật GPS trong Settings
- Reverse geocoding failed → Hiện tọa độ thay vì địa chỉ

---

### 5. Court Photos Section

**Title:** "Hình ảnh sân" (section header)
**Helper text:** "Tối đa 10 ảnh, mỗi ảnh tối đa 5MB"

#### 5.1. Photo Grid
- **Layout:** Grid 3 columns
- **Photo Item:**
  - Thumbnail 100x100dp, border radius 8dp
  - Remove button (X) ở góc top-right
  - Loading spinner khi đang upload

- **Add Photo Button:**
  - Card với icon camera + text "Thêm ảnh"
  - Dashed border
  - Tap → Open Photo Picker Bottom Sheet

**Photo Picker Bottom Sheet:**
- **Options:**
  - "Chụp ảnh mới" (icon camera)
  - "Chọn từ thư viện" (icon gallery)
  - "Hủy"

**Tương tác:**

**Option A: Chụp ảnh**
1. Tap "Chụp ảnh mới"
2. Check camera permission → Request nếu chưa cấp
3. Mở camera (back camera)
4. Chụp ảnh
5. Preview screen với "Chụp lại" | "Sử dụng"
6. Tap "Sử dụng" → Upload ảnh

**Option B: Chọn từ thư viện**
1. Tap "Chọn từ thư viện"
2. Check photo library permission → Request nếu chưa cấp
3. Mở gallery (multi-select enabled)
4. Chọn ảnh (max = 10 - số ảnh hiện tại)
5. Tap "Xong" → Upload từng ảnh

**Upload Flow:**
1. Show loading spinner trên thumbnail
2. Auto-compress ảnh về max 1200x800px
3. Upload lên server
4. **Success:** Hiện thumbnail, remove loading
5. **Failed:** Hiện icon error, retry button

**Validation:**
- Tối đa 10 ảnh
- Mỗi ảnh tối đa 5MB
- Format: JPG, PNG, HEIC
- Error khi vượt quá:
  - "Bạn chỉ có thể tải lên tối đa 10 ảnh"
  - "Ảnh quá lớn. Vui lòng chọn ảnh nhỏ hơn 5MB"

**Hiệu ứng:**
- Grid item slide in khi thêm ảnh
- Remove button fade in on press (long press)
- Upload progress bar bên dưới thumbnail

---

### 6. Court Type Selection Section

**Title:** "Loại sân" (section header)

#### 6.1. Court Type Chips
- **Layout:** Horizontal scrollable chips (nếu nhiều options)
- **Options:**
  - "Sân trong nhà" (Indoor)
  - "Sân ngoài trời" (Outdoor)
  - "Cả hai" (Both)

**Tương tác:**
- Tap chip → Toggle select/deselect
- Ít nhất 1 chip phải được chọn

**States:**
- **Default:** Border gray, background white
- **Selected:** Border primary, background light primary (10% opacity)
- **Error:** Border red (khi chưa chọn gì và submit)

**Validation:**
- Bắt buộc chọn ít nhất 1 option
- Error: "Vui lòng chọn loại sân"

**Hiệu ứng:**
- Chip scale animation khi tap
- Background color transition smooth

---

### 7. Number of Subcourts Input

**Title:** "Số lượng sân con" (section header)
**Helper text:** "Số sân nhỏ bên trong sân lớn (VD: Sân A, Sân B, Sân C)"

#### 7.1. Number Input
- **Layout:** Stepper (- button | Number display | + button)
- **Min:** 1
- **Max:** 20
- **Default:** 1

**Tương tác:**
- Tap "-" → Giảm số, disable khi = 1
- Tap "+" → Tăng số, disable khi = 20
- Có thể nhập trực tiếp (tap vào number → keyboard numeric)

**Validation:**
- Bắt buộc
- Range: 1-20
- Error: "Số sân con phải từ 1 đến 20"

**Hiệu ứng:**
- Number pulse animation khi thay đổi
- Button disable có opacity 0.5

---

### 8. Court Amenities Section

**Title:** "Tiện ích" (section header, optional)
**Helper text:** "Chọn các tiện ích có sẵn tại sân"

#### 8.1. Amenities Checkbox List
- **Layout:** Grid 2 columns, checkboxes
- **Options:**
  - ☐ Bãi đỗ xe
  - ☐ WC/Vệ sinh
  - ☐ Nước uống
  - ☐ Quán cafe/Căng tin
  - ☐ WiFi miễn phí
  - ☐ Đèn chiếu sáng
  - ☐ Phòng thay đồ
  - ☐ Cho thuê vợt
  - ☐ Khác

**Tương tác:**
- Tap checkbox → Toggle on/off
- Nếu chọn "Khác" → Hiện text input để nhập tiện ích khác

**Validation:**
- Không bắt buộc (optional)
- Nếu chọn "Khác" phải nhập text

**Hiệu ứng:**
- Checkbox checkmark slide in
- Text input slide down khi chọn "Khác"

---

### 9. Operating Hours Section

**Title:** "Giờ mở cửa" (section header)

#### 9.1. Opening Time
- **Label:** "Giờ mở cửa"
- **Input:** Time picker
- **Placeholder:** "06:00"

**Tương tác:**
- Tap → Hiện time picker modal (wheel style hoặc clock style)
- Chọn giờ → Auto-format "HH:MM"

#### 9.2. Closing Time
- **Label:** "Giờ đóng cửa"
- **Input:** Time picker
- **Placeholder:** "22:00"

**Validation:**
- Closing time phải > Opening time
- Error: "Giờ đóng cửa phải sau giờ mở cửa"

**Hiệu ứng:**
- Time picker modal slide up from bottom
- Selected time highlight

---

### 10. Description Section (Optional)

**Title:** "Mô tả sân" (section header, optional)
**Helper text:** "Viết vài dòng giới thiệu về sân của bạn"

#### 10.1. Description TextArea
- **Placeholder:** "VD: Sân pickleball tiêu chuẩn quốc tế, mặt sân acrylic chuyên nghiệp..."
- **Max length:** 1000 ký tự
- **Character counter:** "X/1000"
- **Lines:** 4-6 lines, expandable

**Tương tác:**
- Focus → Expand textarea
- Real-time character count

**Validation:**
- Không bắt buộc
- Max 1000 ký tự
- Error: "Mô tả không được vượt quá 1000 ký tự"

---

### 11. Action Buttons Section

**Layout:** Fixed bottom, 2 buttons side-by-side

#### 11.1. Save as Draft Button (Secondary)
- **Text:** "Lưu nháp"
- **Style:** Outline, border gray
- **Width:** 40%

**Tương tác:**
- Tap → Lưu thông tin vào local storage
- Toast: "Đã lưu nháp. Bạn có thể tiếp tục sau"
- Navigate to Dashboard

**Hiệu ứng:**
- Button scale on press
- Toast slide down from top

#### 11.2. Continue Button (Primary)
- **Text:** "Tiếp tục"
- **Style:** Solid primary color
- **Width:** 60%

**States:**
- **Enabled:** Khi form valid (tất cả required fields đã điền đúng)
- **Disabled:** Khi form invalid (màu xám, opacity 0.5)
- **Loading:** Spinner + "Đang xử lý..."

**Tương tác:**
- Tap → Validate toàn bộ form
- **Nếu valid:**
  1. Upload ảnh (nếu chưa upload)
  2. Tạo sân mới trong database
  3. Success → Navigate to Add Subcourts Screen (F04)
- **Nếu invalid:**
  - Scroll to field đầu tiên có lỗi
  - Highlight field error

**Hiệu ứng:**
- Loading overlay full screen khi submit
- Success checkmark animation trước khi navigate

---

## Navigation

### Đến screen này từ:
- **Post-Registration Flow:** Sau khi Chủ sân hoàn thành đăng ký (F01)
- **Dashboard:** Nếu Chủ sân skip lúc đầu, có button "Tạo sân" trên Dashboard

### Từ screen này đến:
- **Skip flow:** Dashboard (Chủ sân chưa có sân)
- **Save Draft:** Dashboard (Draft được lưu)
- **Success flow:** Add Subcourts Screen (F04) - Tiếp theo trong onboarding

**Onboarding Sequence:**
```
Create First Court (Screen này)
→ Add Subcourts (F04)
→ Setup Time Slots (F05)
→ Dashboard
```

---

## Component States

### Input Fields
- **Default:** Border gray, placeholder visible
- **Focus:** Border primary, placeholder float to top
- **Valid:** Border green (subtle), no error text
- **Error:** Border red, error text below field
- **Disabled:** Background light gray, no interaction

### Buttons
- **Default:** Primary color, white text
- **Pressed:** Scale 0.98, darker shade
- **Loading:** Spinner center, text "Đang xử lý..."
- **Disabled:** Gray background, opacity 0.5

### Photo Items
- **Default:** Thumbnail display
- **Loading:** Spinner overlay, blur thumbnail
- **Error:** Red border, retry icon
- **Hover:** Remove (X) button visible

### Map Preview
- **Loading:** Skeleton loader
- **Success:** Map with marker
- **Error:** Placeholder với text "Không tìm thấy vị trí"

---

## Validation Rules Summary

### Required Fields (*)
1. **Tên sân:**
   - 2-100 ký tự
   - Không ký tự đặc biệt (trừ dấu cách, gạch ngang, ngoặc)

2. **Người liên hệ:**
   - 2-50 ký tự

3. **Số điện thoại:**
   - 10-11 chữ số
   - Bắt đầu bằng 0

4. **Địa chỉ:**
   - 10-200 ký tự
   - Phải geocode thành công (có tọa độ GPS)

5. **Loại sân:**
   - Ít nhất 1 option được chọn

6. **Số sân con:**
   - 1-20 sân

### Optional Fields
- **Hình ảnh:** 0-10 ảnh, mỗi ảnh ≤ 5MB
- **Tiện ích:** Không bắt buộc
- **Giờ mở/đóng cửa:** Có default values
- **Mô tả:** 0-1000 ký tự

---

## Error Handling

### Error Scenarios

#### 1. Geocoding Failed
- **Trigger:** Không thể chuyển địa chỉ thành tọa độ
- **Response:**
  - Hiện error text: "Không tìm thấy địa chỉ. Vui lòng nhập chi tiết hơn hoặc chọn trên bản đồ"
  - Auto-open Map Editor Modal
  - User phải chọn vị trí trên map thủ công

#### 2. Photo Upload Failed
- **Trigger:** Network error hoặc file quá lớn
- **Response:**
  - Hiện icon error trên thumbnail
  - Retry button
  - Toast: "Upload ảnh thất bại. Vui lòng thử lại"
  - Cho phép remove ảnh lỗi và upload ảnh mới

#### 3. GPS Permission Denied
- **Trigger:** User từ chối cấp quyền GPS
- **Response:**
  - Dialog: "Ứng dụng cần quyền truy cập vị trí để chọn sân trên bản đồ. Vui lòng cấp quyền trong Cài đặt"
  - Button "Mở Cài đặt" → Deep link to app settings
  - Button "Nhập thủ công" → Close dialog, user nhập địa chỉ

#### 4. Form Validation Failed
- **Trigger:** User tap "Tiếp tục" khi form invalid
- **Response:**
  - Scroll to field đầu tiên có lỗi
  - Highlight tất cả fields có lỗi (border đỏ)
  - Show error text bên dưới mỗi field
  - Shake animation cho button "Tiếp tục"
  - Toast: "Vui lòng kiểm tra lại thông tin"

#### 5. Network Error During Submit
- **Trigger:** Mất mạng khi tạo sân
- **Response:**
  - Dialog: "Không có kết nối mạng. Thông tin đã được lưu tạm. Vui lòng thử lại khi có mạng"
  - Button "Thử lại"
  - Button "Lưu nháp"
  - Auto-retry khi online lại

#### 6. Server Error (500)
- **Trigger:** Server lỗi
- **Response:**
  - Dialog: "Đã xảy ra lỗi. Vui lòng thử lại sau"
  - Button "Thử lại"
  - Button "Lưu nháp"

#### 7. Camera/Gallery Permission Denied
- **Trigger:** User từ chối quyền camera/gallery
- **Response:**
  - Dialog hướng dẫn bật quyền trong Settings
  - Button "Mở Cài đặt"
  - Button "Hủy" → User có thể skip thêm ảnh

---

## Loading States

### 1. Geocoding Loading
- **When:** Sau khi nhập/chọn địa chỉ
- **Display:** Skeleton loader thay map preview
- **Duration:** 1-3 giây

### 2. Photo Upload Loading
- **When:** Sau khi chọn ảnh
- **Display:**
  - Spinner overlay trên thumbnail
  - Progress bar bên dưới (0-100%)
- **Duration:** Tùy kích thước ảnh và mạng

### 3. Form Submit Loading
- **When:** Tap "Tiếp tục" và đang xử lý
- **Display:**
  - Full screen overlay với spinner
  - Text: "Đang tạo sân..."
  - Disable tất cả interactions
- **Duration:** 2-5 giây

### 4. Map Loading
- **When:** Mở Map Editor Modal
- **Display:**
  - Map tiles loading
  - Skeleton loader cho address text
- **Duration:** 1-2 giây

---

## Success States

### 1. Court Created Successfully
- **Flow:**
  1. Show success checkmark animation (Lottie)
  2. Toast: "Tạo sân thành công! Tiếp theo, hãy thêm sân con"
  3. Navigate to Add Subcourts Screen (F04)

### 2. Draft Saved
- **Flow:**
  1. Toast: "Đã lưu nháp. Bạn có thể tiếp tục sau"
  2. Navigate to Dashboard
  3. Dashboard hiển thị banner: "Bạn có bản nháp chưa hoàn thành. Tiếp tục tạo sân?"

### 3. Photo Uploaded
- **Flow:**
  1. Upload progress 100%
  2. Checkmark animation trên thumbnail
  3. Remove loading spinner

---

## Platform-Specific Considerations

### iOS
- **Auto-fill OTP:** Không áp dụng (screen này không có OTP)
- **Photo Picker:** Sử dụng PHPickerViewController (iOS 14+)
- **Camera:** Sử dụng UIImagePickerController
- **Map:** Apple MapKit hoặc Google Maps SDK
- **Haptic Feedback:** Light impact khi tap buttons
- **Keyboard:** Auto-dismiss khi tap outside input

### Android
- **Photo Picker:** Sử dụng Photo Picker API (Android 13+) hoặc Intent.ACTION_PICK
- **Camera:** Sử dụng Intent.ACTION_IMAGE_CAPTURE
- **Map:** Google Maps SDK
- **Keyboard:** IME action "Next" cho inputs, "Done" cho last input
- **Back Button:** Confirm dialog nếu có unsaved changes

### Both Platforms
- **GPS Permission:** Request khi user tap "Sử dụng vị trí hiện tại"
- **Camera Permission:** Request khi user tap "Chụp ảnh mới"
- **Gallery Permission:** Request khi user tap "Chọn từ thư viện"
- **Offline Mode:** Lưu nháp vào local storage, sync khi online

---

## Ghi chú

### UX Considerations

#### 1. Progressive Disclosure
- Không hiển thị tất cả fields cùng lúc
- Scroll flow: Basic info → Address → Photos → Details
- Section headers rõ ràng
- Helper text gợi ý cho từng section

#### 2. Smart Defaults
- **Số sân con:** Default = 1 (phổ biến nhất)
- **Giờ mở cửa:** Default = 06:00
- **Giờ đóng cửa:** Default = 22:00
- **Loại sân:** Không default (bắt user chọn)

#### 3. Error Prevention
- Real-time validation khi blur
- Disable submit button khi form invalid
- Helper text rõ ràng cho mỗi field
- Example placeholder (VD: Sân Pickleball...)

#### 4. Save Draft Strategy
- Auto-save draft mỗi 30 giây
- Lưu vào local storage
- Restore draft khi user quay lại
- Clear draft sau khi submit thành công

#### 5. Photo Management
- Ảnh đầu tiên = ảnh đại diện sân
- Cho phép kéo thả để sắp xếp thứ tự (optional, v2)
- Auto-compress ảnh trước khi upload
- Upload song song (max 3 ảnh cùng lúc)

#### 6. Onboarding Guidance
- Tooltip hint cho các field quan trọng (first-time only)
- Progress indicator rõ ràng
- "Bỏ qua" option cho user muốn làm sau
- Reminder notification nếu skip

### Edge Cases

#### 1. User với nhiều sân
- Screen này chỉ cho sân đầu tiên
- Sân thứ 2+ dùng screen "Add Court" khác (giống nhau nhưng không có onboarding context)

#### 2. GPS không khả dụng
- Fallback: Nhập địa chỉ thủ công
- Geocode từ địa chỉ text
- Nếu geocode fail → Bắt buộc chọn trên map

#### 3. Slow network
- Show upload progress bar
- Retry button cho failed uploads
- Allow user to continue nhập thông tin khác trong khi upload ảnh

#### 4. Unsaved changes
- Warn user khi tap Back/Skip nếu có thay đổi
- Dialog: "Bạn có thay đổi chưa lưu. Lưu nháp trước khi thoát?"

#### 5. Duplicate court name
- Không validate (cho phép trùng tên)
- Chủ sân có thể có nhiều sân cùng tên ở địa chỉ khác

#### 6. Very long court name
- Truncate trong list view
- Show full name trong detail view
- Character counter warning khi gần max

### Post-Creation Flow

**Sau khi tạo sân thành công:**

1. **Navigate to Add Subcourts (F04):**
   - Pre-fill số sân con từ input
   - Gợi ý tên: "Sân 1", "Sân 2", ...
   - Cho phép edit tên sân con

2. **After Subcourts → Setup Time Slots (F05):**
   - Chọn sân con để tạo khung giờ
   - Template giờ phổ biến (6h-7h, 7h-8h, ...)
   - Bulk create khung giờ

3. **After Time Slots → Dashboard:**
   - Celebration animation
   - Message: "Chúc mừng! Sân của bạn đã sẵn sàng nhận đặt sân"
   - CTA: "Xem sân của tôi"

---

## Design Specifications

### Color Palette
- **Primary:** #00C853 (Green - pickleball theme)
- **Secondary:** #FF6F00 (Orange)
- **Success:** #388E3C (Dark green)
- **Error:** #D32F2F (Red)
- **Background:** #FFFFFF
- **Surface:** #F5F5F5 (section backgrounds)
- **Border:** #E0E0E0 (default), #00C853 (focus), #D32F2F (error)
- **Text Primary:** #212121
- **Text Secondary:** #757575
- **Text Hint:** #9E9E9E

### Typography
- **Screen Title:** Bold, 18sp, #212121
- **Section Headers:** SemiBold, 16sp, #212121
- **Input Labels:** Medium, 14sp, #757575
- **Input Text:** Regular, 16sp, #212121
- **Placeholder:** Regular, 16sp, #9E9E9E
- **Helper Text:** Regular, 12sp, #757575
- **Error Text:** Regular, 12sp, #D32F2F
- **Button Text:** Medium, 16sp, #FFFFFF (primary), #00C853 (secondary)

### Spacing (8pt Grid)
- **Screen padding:** 16dp
- **Section spacing:** 24dp
- **Input spacing:** 16dp
- **Label to input:** 8dp
- **Helper/Error text:** 4dp below input
- **Button height:** 48dp
- **Button spacing:** 12dp between buttons

### Border Radius
- **Inputs:** 8dp
- **Buttons:** 8dp
- **Cards:** 12dp
- **Photo thumbnails:** 8dp
- **Chips:** 16dp (pill shape)

### Elevation/Shadow
- **Map preview:** elevation 2dp
- **Bottom Sheet:** elevation 8dp
- **Modal:** elevation 16dp
- **Buttons (pressed):** elevation 4dp

### Animations
- **Transition duration:** 300ms
- **Easing:** Ease-in-out
- **Error shake:** 3 shakes, 100ms each
- **Success checkmark:** Lottie animation, 1.5s
- **Photo upload:** Progress bar, smooth transition
- **Map marker drop:** 500ms, bounce easing

### Accessibility
- **Touch targets:** Minimum 44x44dp
- **Color contrast:** 4.5:1 (text), 3:1 (UI)
- **Screen reader:** All inputs labeled
- **Focus indicators:** Visible borders
- **Error announcements:** Read by screen reader

---

## Data Structure (Input → Output)

### Input Data (From User)
```json
{
  "name": "Sân Pickleball Thảo Điền",
  "address": "123 Đường Nguyễn Văn Hưởng, P.Thảo Điền, Q.2, TP.HCM",
  "location": {
    "latitude": 10.8006,
    "longitude": 106.7302
  },
  "contact_name": "Nguyễn Văn A",
  "contact_phone": "0901234567",
  "images": [
    "https://cdn.example.com/image1.jpg",
    "https://cdn.example.com/image2.jpg"
  ],
  "court_type": ["indoor", "outdoor"],
  "number_of_subcourts": 3,
  "amenities": [
    "parking",
    "restroom",
    "water",
    "lighting"
  ],
  "opening_time": "06:00",
  "closing_time": "22:00",
  "description": "Sân pickleball tiêu chuẩn quốc tế..."
}
```

### Output (Saved to Database)
```json
{
  "id": "court_123abc",
  "owner_id": "user_456def",
  "name": "Sân Pickleball Thảo Điền",
  "address": "123 Đường Nguyễn Văn Hưởng, P.Thảo Điền, Q.2, TP.HCM",
  "location": {
    "latitude": 10.8006,
    "longitude": 106.7302
  },
  "contact_name": "Nguyễn Văn A",
  "contact_phone": "0901234567",
  "images": [
    "https://cdn.example.com/image1.jpg",
    "https://cdn.example.com/image2.jpg"
  ],
  "court_type": ["indoor", "outdoor"],
  "amenities": ["parking", "restroom", "water", "lighting"],
  "opening_time": "06:00",
  "closing_time": "22:00",
  "description": "Sân pickleball tiêu chuẩn quốc tế...",
  "status": "active",
  "created_at": "2025-12-27T10:30:00Z",
  "updated_at": "2025-12-27T10:30:00Z"
}
```

### Next Step: Create Subcourts
- Number of subcourts: 3
- Auto-generate names: "Sân 1", "Sân 2", "Sân 3"
- Link to court_id: "court_123abc"

---

## File Size Estimate
**~14KB** (similar to previous screens, comprehensive documentation)

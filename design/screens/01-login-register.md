# Login/Register Screen

## Screen Overview

Màn hình đầu tiên sau Welcome screen, cho phép người dùng mới đăng ký tài khoản hoặc người dùng cũ đăng nhập bằng Email/Password hoặc Số điện thoại/OTP. Khi đăng ký, người dùng phải chọn vai trò (Chủ sân/Người chơi/HLV) và không thể thay đổi sau này.

---

## Mục đích

- Cho phép người dùng mới tạo tài khoản với 1 trong 3 vai trò
- Cho phép người dùng cũ đăng nhập vào hệ thống
- Hỗ trợ 2 phương thức xác thực: Email/Password và OTP
- Xác thực tài khoản qua email hoặc OTP

---

## Tab/Mode Chính

### 1. Welcome State (Initial)
**Mô tả:** Trạng thái ban đầu khi người dùng mở screen

**Các thành phần:**
- Logo PickleBall Dating (centered, với animation fade in)
- Slogan/Tagline ngắn
- 2 buttons chính:
  - **Button "Đăng ký"** (Primary, gradient background)
  - **Button "Đăng nhập"** (Secondary, outline style)

**Tương tác:**
- Tap "Đăng ký" → Chuyển sang Registration Method Selection
- Tap "Đăng nhập" → Chuyển sang Login Method Selection

---

### 2. Registration Method Selection
**Mô tả:** Người dùng chọn phương thức đăng ký

**Các thành phần:**
- Header: "Chọn phương thức đăng ký" + Back button
- 2 Cards lựa chọn:
  - **Card "Đăng ký bằng Email"** (Icon email + text)
  - **Card "Đăng ký bằng Số điện thoại"** (Icon phone + text)

**Tương tác:**
- Tap Email card → Chuyển sang Email Registration Form
- Tap Phone card → Chuyển sang Phone Registration Form
- Tap Back → Quay lại Welcome State

**Animation:**
- Cards slide up from bottom

---

### 3. Email Registration Form
**Mô tả:** Form đăng ký bằng Email/Password

**Các thành phần:**

1. **Header Section**
   - Title: "Đăng ký tài khoản"
   - Back button (top left)

2. **Input Fields**
   - **Email Input**
     - Placeholder: "Email"
     - Validation: Real-time kiểm tra format email
     - Error state: Border đỏ + text lỗi bên dưới
   - **Password Input**
     - Placeholder: "Mật khẩu"
     - Toggle icon "eye" để show/hide password
     - Validation: ≥8 ký tự, có chữ và số
     - Helper text: "Tối thiểu 8 ký tự, bao gồm chữ và số"
   - **Confirm Password Input**
     - Placeholder: "Xác nhận mật khẩu"
     - Validation: Khớp với password
     - Error: "Mật khẩu không khớp"

3. **Role Selection Section**
   - Label: "Chọn vai trò của bạn" (required indicator *)
   - 3 Role Cards (radio button style):
     - **Chủ sân**: Icon stadium + "Quản lý sân pickleball"
     - **Người chơi**: Icon racket + "Tìm sân và đối thủ"
     - **Huấn luyện viên**: Icon whistle + "Dạy và kết nối học viên"
   - Chỉ chọn được 1 role tại 1 thời điểm
   - Highlight card được chọn (border màu primary, background light)

4. **Terms & Conditions**
   - Checkbox: "Tôi đồng ý với Điều khoản và Điều kiện"
   - Link: Tap "Điều khoản và Điều kiện" mở modal

5. **Primary Button**
   - Text: "Đăng ký"
   - Disabled state khi chưa valid (màu xám, không tương tác được)
   - Loading state khi đang submit (spinner + "Đang xử lý...")

6. **Footer Link**
   - Text: "Đã có tài khoản? Đăng nhập"
   - Tap → Chuyển sang Login Method Selection

**Tương tác:**
- Input focus → Border thành màu primary, keyboard slide up
- Validate on blur và on submit
- Submit thành công → Show toast "Vui lòng kiểm tra email để xác nhận tài khoản"

**Validations & Errors:**
- Email đã tồn tại → "Email này đã được đăng ký. Vui lòng đăng nhập hoặc sử dụng email khác"
- Password yếu → "Mật khẩu phải có ít nhất 8 ký tự, bao gồm chữ và số"
- Confirm password không khớp → "Mật khẩu không khớp"
- Chưa chọn role → "Vui lòng chọn vai trò của bạn"
- Chưa tick Terms → "Vui lòng đồng ý với Điều khoản và Điều kiện"

**Animation:**
- Form slide in from right
- Error messages fade in/out
- Role cards có ripple effect khi tap

---

### 4. Phone Registration Form
**Mô tả:** Form đăng ký bằng Số điện thoai/OTP

**Các thành phần:**

1. **Header Section**
   - Title: "Đăng ký tài khoản"
   - Back button

2. **Phone Input Section**
   - **Phone Number Input**
     - Placeholder: "Số điện thoại (0901234567)"
     - Keyboard: Number pad
     - Validation: 10 số, bắt đầu bằng 0
     - Error: "Số điện thoại không hợp lệ"
   - **Button "Gửi mã OTP"**
     - Primary button
     - Disabled khi phone chưa valid

3. **OTP Input Section** (hiện sau khi gửi OTP)
   - Label: "Nhập mã OTP"
   - 6 input boxes (mỗi box 1 chữ số)
   - Countdown timer: "Gửi lại sau 05:00"
   - Link "Gửi lại OTP" (enabled sau khi countdown hết)
   - Auto-focus vào box tiếp theo khi nhập

4. **Role Selection Section**
   - Tương tự Email Registration Form

5. **Optional Password Section**
   - Checkbox: "Tạo mật khẩu (để đăng nhập bằng password sau này)"
   - Khi tick → Hiện 2 inputs: Password + Confirm Password
   - Validation tương tự Email form

6. **Primary Button**
   - Text: "Hoàn tất đăng ký"
   - Disabled khi OTP chưa valid hoặc role chưa chọn

7. **Footer Link**
   - Text: "Đã có tài khoản? Đăng nhập"

**Tương tác:**
- Nhập phone → Enable button "Gửi mã OTP"
- Tap "Gửi mã OTP" → Loading → OTP Input Section slide down
- Nhập OTP auto-submit khi đủ 6 số
- Countdown hết → Enable "Gửi lại OTP"

**Validations & Errors:**
- SDT không hợp lệ → "Số điện thoại không hợp lệ. Vui lòng nhập số điện thoại Việt Nam (10 số)"
- SDT đã tồn tại → "Số điện thoại này đã được đăng ký. Vui lòng đăng nhập"
- OTP sai → "Mã OTP không đúng. Vui lòng thử lại"
- OTP sai 5 lần → "Bạn đã nhập sai OTP quá nhiều lần. Vui lòng thử lại sau 15 phút"
- OTP hết hạn → "Mã OTP đã hết hạn. Vui lòng gửi lại"

**Animation:**
- OTP section slide down with fade in
- OTP boxes có scale animation khi nhập
- Countdown timer có pulse effect

---

### 5. Login Method Selection
**Mô tả:** Người dùng chọn phương thức đăng nhập

**Các thành phần:**
- Header: "Chọn phương thức đăng nhập" + Back button
- 2 Cards lựa chọn:
  - **Card "Đăng nhập bằng Email"**
  - **Card "Đăng nhập bằng Số điện thoại"**

**Tương tác:**
- Tap Email card → Chuyển sang Email Login Form
- Tap Phone card → Chuyển sang Phone Login Form
- Tap Back → Quay lại Welcome State

---

### 6. Email Login Form
**Mô tả:** Form đăng nhập bằng Email/Password

**Các thành phần:**

1. **Header Section**
   - Title: "Đăng nhập"
   - Back button

2. **Input Fields**
   - **Email Input**
     - Placeholder: "Email"
     - Validation: Format email
   - **Password Input**
     - Placeholder: "Mật khẩu"
     - Toggle show/hide password

3. **Links**
   - "Quên mật khẩu?" (aligned right, small text)
   - Tap → Chuyển sang Forgot Password Screen

4. **Primary Button**
   - Text: "Đăng nhập"
   - Loading state khi đang submit

5. **Footer Link**
   - Text: "Chưa có tài khoản? Đăng ký"
   - Tap → Chuyển sang Registration Method Selection

**Tương tác:**
- Submit thành công → Navigate to Home Screen (dựa vào role)
- Submit failed → Show error toast

**Validations & Errors:**
- Email hoặc password sai → "Email hoặc mật khẩu không đúng"
- Tài khoản chưa xác nhận → "Tài khoản chưa được xác nhận. Vui lòng kiểm tra email" + button "Gửi lại email xác nhận"
- Network error → "Không có kết nối mạng. Vui lòng kiểm tra và thử lại"

**Animation:**
- Form slide in
- Error shake animation

---

### 7. Phone Login Form
**Mô tả:** Form đăng nhập bằng OTP

**Các thành phần:**

1. **Header Section**
   - Title: "Đăng nhập"
   - Back button

2. **Phone Input Section**
   - **Phone Number Input**
   - **Button "Gửi mã OTP"**

3. **OTP Input Section** (hiện sau khi gửi OTP)
   - 6 input boxes
   - Countdown timer
   - Link "Gửi lại OTP"

4. **Primary Button**
   - Text: "Đăng nhập"

5. **Footer Link**
   - Text: "Chưa có tài khoản? Đăng ký"

**Tương tác:**
- Tương tự Phone Registration Form
- Submit thành công → Navigate to Home Screen

**Validations & Errors:**
- SDT không tồn tại → "Số điện thoại này chưa được đăng ký. Vui lòng đăng ký"
- OTP sai → "Mã OTP không đúng"

---

### 8. Forgot Password Screen
**Mô tả:** Đặt lại mật khẩu qua Email hoặc OTP

**Các thành phần:**

1. **Header Section**
   - Title: "Quên mật khẩu"
   - Back button

2. **Method Selection**
   - 2 Tabs: "Email" | "Số điện thoại"
   - Tab active có underline indicator

3. **Email Tab**
   - **Email Input**
   - **Button "Gửi link đặt lại"**
   - Success message: "Vui lòng kiểm tra email để đặt lại mật khẩu"

4. **Phone Tab**
   - **Phone Input**
   - **Button "Gửi mã OTP"**
   - **OTP Input Section**
   - **New Password Section**
     - Password Input
     - Confirm Password Input
   - **Button "Đặt lại mật khẩu"**
   - Success → Toast "Đặt lại mật khẩu thành công" → Navigate to Login

**Tương tác:**
- Tab switch với slide animation
- Email flow: Gửi email → User check email → Click link → Web view đặt lại password
- Phone flow: Gửi OTP → Nhập OTP → Nhập password mới → Submit

---

## Navigation Flow

```
Welcome State
├─→ Registration Method Selection
│   ├─→ Email Registration Form → [Success] → Email Verification Screen
│   └─→ Phone Registration Form → [Success] → Home Screen
│
└─→ Login Method Selection
    ├─→ Email Login Form
    │   ├─→ [Success] → Home Screen
    │   └─→ Forgot Password Screen → [Success] → Email Login Form
    └─→ Phone Login Form → [Success] → Home Screen
```

---

## Component States

### Input Fields
- **Default**: Border gray, placeholder visible
- **Focus**: Border primary color, placeholder move up
- **Valid**: Border green (subtle)
- **Error**: Border red, error message below
- **Disabled**: Background gray, no interaction

### Buttons
- **Default**: Primary color, white text
- **Hover/Press**: Darker shade, scale 0.98
- **Loading**: Spinner + "Đang xử lý...", disabled
- **Disabled**: Gray background, gray text, opacity 0.5

### Role Cards
- **Default**: Border gray, background white
- **Selected**: Border primary, background light primary (10% opacity)
- **Hover/Press**: Ripple effect

---

## Validations & Error Handling

### Email Validation
- Format: `xxx@xxx.xxx`
- Real-time check on blur
- Error: "Địa chỉ email không hợp lệ"

### Password Validation
- Minimum 8 ký tự
- Phải có ít nhất 1 chữ cái
- Phải có ít nhất 1 chữ số
- Maximum 50 ký tự
- Error: "Mật khẩu phải có ít nhất 8 ký tự, bao gồm chữ và số"

### Phone Validation
- Exactly 10 chữ số
- Bắt đầu bằng 0
- Chỉ chứa số (0-9)
- Error: "Số điện thoại không hợp lệ. Vui lòng nhập số điện thoại Việt Nam (10 số)"

### OTP Validation
- Exactly 6 chữ số
- Hết hạn sau 5 phút
- Maximum 5 lần nhập sai → Khóa 15 phút
- Error: "Mã OTP không đúng. Vui lòng thử lại"

### Role Selection
- Required field
- Chỉ chọn được 1 role
- Error: "Vui lòng chọn vai trò của bạn"

---

## Technical Specifications (theo UI/UX Guidelines)

### Color System
**Áp dụng từ `design/uiuxguides.md`**

| Element | Color | Hex |
|---------|-------|-----|
| Primary Button | Blue Gradient | `linear-gradient(135deg, #5B9FE3 0%, #7CB8F0 100%)` |
| Background | Sky Blue | `#B8D4F0` |
| Surface (Cards, Inputs) | White | `#FFFFFF` |
| Text Primary | Dark Gray | `#1A1A1A` |
| Text Secondary | Medium Gray | `#666666` |
| Text Tertiary (Placeholder) | Light Gray | `#999999` |
| Error | Red | `#F44336` |
| Success | Green | `#4CAF50` |
| Border Default | Light Border | `#E0E0E0` |
| Border Focus | Primary Blue | `#5B9FE3` |

### Typography (SF Pro)

| Element | Size | Weight | Line Height | Usage |
|---------|------|--------|-------------|-------|
| Screen Title | 32px | 700 Bold | 40px | "Đăng ký tài khoản", "Đăng nhập" |
| Section Label | 20px | 600 Semibold | 28px | "Chọn vai trò của bạn" |
| Body Text | 16px | 400 Regular | 24px | Input text, descriptions |
| Helper Text | 14px | 400 Regular | 20px | Validation hints, error messages |
| Button Text | 16px | 600 Semibold | 24px | All buttons |
| Caption | 12px | 400 Regular | 16px | Countdown timer, small notes |

### Spacing (Base 4px)

| Token | Value | Usage |
|-------|-------|-------|
| Screen padding | 20px | Horizontal margin |
| Section spacing | 24px | Between major sections |
| Input spacing | 16px | Between input fields |
| Component padding | 16px | Inside cards, buttons |
| Tight spacing | 8px | Icon-to-text |

### Border Radius

| Component | Radius |
|-----------|--------|
| Buttons (pill) | 24px |
| Input fields | 12px |
| Cards (Role, Method selection) | 20px |
| Modals | 20px |
| OTP input boxes | 8px |

### Shadows

```css
/* Cards & Method Selection */
box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.08);

/* Buttons (Primary) */
box-shadow: 0px 4px 12px rgba(91, 159, 227, 0.3);

/* Focused Inputs */
box-shadow: 0px 0px 0px 4px rgba(91, 159, 227, 0.1);

/* Error Inputs */
box-shadow: 0px 0px 0px 4px rgba(244, 67, 54, 0.1);
```

### Animations & Motion

**Timing Functions:**
```javascript
easeOut: cubic-bezier(0.33, 1, 0.68, 1)
easeIn: cubic-bezier(0.32, 0, 0.67, 0)
spring: cubic-bezier(0.68, -0.55, 0.265, 1.55)
```

**Durations:**
- Button press: 100ms (ease-in)
- Input focus: 200ms (ease-out)
- Screen transitions: 300ms (ease-out)
- Modal slide-up: 350ms (spring)
- Error shake: 400ms total (3 shakes)
- OTP auto-submit: 200ms delay after last digit

### Accessibility
- Minimum touch target: 44x44dp
- Color contrast ratio: 4.5:1 (text), 3:1 (UI elements)
- Screen reader support for all inputs
- Keyboard navigation support

### Edge Cases
- Mất kết nối khi submit → Retry with exponential backoff
- App killed giữa chừng đăng ký → Save draft state
- OTP SMS chậm → Show "Chưa nhận được? Gửi lại" sau 60s
- Đăng ký trên nhiều thiết bị cùng lúc → Only allow 1 active session
- Link email verification hết hạn → Show "Gửi lại email" button

### Platform-Specific
- **iOS**: Auto-fill OTP từ SMS
- **Android**: Auto-read SMS permission, auto-fill OTP
- Both: Haptic feedback on button press
- Both: Auto-dismiss keyboard khi submit

### Loading States
- Email registration: "Đang tạo tài khoản..."
- Phone registration: "Đang gửi OTP..."
- Login: "Đang đăng nhập..."
- OTP verification: "Đang xác thực..."

### Success Navigation (Post-Registration)
- **Người chơi** → Profile Completion Screen (F02)
- **Chủ sân** → Create First Court Screen (F03)
- **HLV** → Create Coach Profile Screen (F12)

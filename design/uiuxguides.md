# UI/UX Design Guidelines - PickleBallDating

> Reverse-engineered từ thiết kế tham khảo | Cập nhật: 2025-12-27

---

## 1. Ngôn ngữ thiết kế (Visual Style)

### Phong cách chủ đạo
**Modern Glassmorphism + Soft UI** với các đặc điểm:
- Gradient backgrounds (blue tones)
- Frosted glass effects trên surfaces
- Soft shadows và border-radius lớn
- Card-based layout với depth layers
- Clean, minimalist, friendly aesthetic

### Màu sắc

#### Color Palette

| Loại | Tên | Hex Code | Sử dụng |
|------|-----|----------|---------|
| **Primary** | Blue Gradient Start | `#5B9FE3` | Backgrounds, primary buttons |
| **Primary** | Blue Gradient End | `#7CB8F0` | Backgrounds, accents |
| **Secondary** | Soft Blue | `#A8C8E8` | Category pills, secondary elements |
| **Accent** | Golden Yellow | `#FFD700` | Ratings, highlights |
| **Surface** | White | `#FFFFFF` | Cards, input fields, modals |
| **Surface** | Light Glass | `#FFFFFF` (90% opacity) | Glassmorphic surfaces |
| **Background** | Sky Blue | `#B8D4F0` | Main app background |
| **Text Primary** | Dark Gray | `#1A1A1A` | Headings, body text |
| **Text Secondary** | Medium Gray | `#666666` | Subtitles, descriptions |
| **Text Tertiary** | Light Gray | `#999999` | Placeholders, disabled |
| **Success** | Green | `#4CAF50` | Success states, confirmations |
| **Error** | Red | `#F44336` | Errors, validations |
| **Warning** | Orange | `#FF9800` | Warnings, alerts |
| **Border** | Light Border | `#E0E0E0` | Dividers, card borders |

#### Gradient Definitions
```css
/* Primary Background Gradient */
background: linear-gradient(135deg, #5B9FE3 0%, #7CB8F0 100%);

/* Glassmorphic Surface */
background: rgba(255, 255, 255, 0.9);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
```

### Typography

**Font Family:** SF Pro (iOS native)

#### Type Scale

| Element | Size | Weight | Line Height | Letter Spacing |
|---------|------|--------|-------------|----------------|
| **H1** (Hero) | 48px | 700 Bold | 56px | -0.5px |
| **H2** (Page Title) | 32px | 700 Bold | 40px | -0.3px |
| **H3** (Section) | 24px | 600 Semibold | 32px | 0px |
| **H4** (Card Title) | 20px | 600 Semibold | 28px | 0px |
| **Body Large** | 18px | 400 Regular | 26px | 0px |
| **Body** | 16px | 400 Regular | 24px | 0px |
| **Body Small** | 14px | 400 Regular | 20px | 0px |
| **Caption** | 12px | 400 Regular | 16px | 0.2px |
| **Button Text** | 16px | 600 Semibold | 24px | 0.5px |

---

## 2. Mobile-First Rules

### Touch Target
- **Minimum size:** 44x44px (iOS Human Interface Guidelines)
- **Recommended size:** 48x48px for primary actions
- **Spacing between targets:** Minimum 8px

### Thumb Zone
- **Primary actions:** Bottom 1/3 của màn hình (navigation bar area)
- **Secondary actions:** Top right corner (messages, notifications)
- **Safe zones:** Tránh đặt critical buttons gần viền màn hình (16px margin)

### Layout
- **Container width:** Full width với horizontal padding 20px
- **Content max-width:** 100% (single column)
- **Safe area insets:**
  - Top: 44px (status bar) hoặc dynamic safe area
  - Bottom: 34px (home indicator on iPhone X+)
  - Horizontal: 20px

### Spacing System
**Base unit:** 4px

| Token | Value | Sử dụng |
|-------|-------|---------|
| `spacing-xs` | 4px | Icon-to-text spacing |
| `spacing-sm` | 8px | Tight element spacing |
| `spacing-md` | 16px | Default spacing, card padding |
| `spacing-lg` | 24px | Section spacing |
| `spacing-xl` | 32px | Large gaps, screen padding |
| `spacing-2xl` | 48px | Hero sections |

### Content Priority
**Hierarchy (từ cao xuống thấp):**
1. Hero/CTA chính (ví dụ: "Play. Book. Win." + Start button)
2. Search bar (luôn accessible)
3. Quick actions (Category filters, Quick Match)
4. Featured content (Cards với images)
5. Secondary navigation (Bottom tab bar)

---

## 3. Responsive Strategy

### Breakpoints

| Device | Width | Layout |
|--------|-------|--------|
| **Mobile S** | 320px - 374px | Single column, compact spacing |
| **Mobile M** | 375px - 428px | Single column, default spacing (primary target) |
| **Mobile L** | 429px - 767px | Single column, relaxed spacing |
| **Tablet** | 768px - 1023px | 2-column grid cho cards |
| **Desktop** | 1024px+ | 3-4 column grid, max-width container (1200px) |

### Layout Adaptation

#### Mobile (< 768px)
- Flexbox vertical stacking
- Full-width cards
- Horizontal scroll cho category pills
- Bottom tab navigation

#### Tablet (768px - 1023px)
- Grid 2 columns cho cards
- Side navigation (optional)
- Increased spacing (1.2x multiplier)

#### Desktop (1024px+)
- Grid 3-4 columns
- Fixed side navigation
- Hover states enabled
- Max-width container centered

### Media Scaling
```css
/* Images */
.card-image {
  width: 100%;
  aspect-ratio: 16/9;
  object-fit: cover;
  border-radius: 16px;
}

/* Avatar */
.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
}

/* Video Thumbnails */
.video-thumbnail {
  aspect-ratio: 4/3;
  position: relative;
}
```

### Typography Scaling
**Mobile-first scale với multipliers:**

| Element | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| H1 | 48px | 56px (1.17x) | 64px (1.33x) |
| H2 | 32px | 36px (1.12x) | 40px (1.25x) |
| Body | 16px | 16px | 18px (1.12x) |

---

## 4. Component Library

### Button

#### Primary Button

**Default State**
```
Background: #5B9FE3 (solid blue)
Text: #FFFFFF, 16px, Semibold
Padding: 14px 32px
Border-radius: 24px (pill-shaped)
Shadow: 0px 4px 12px rgba(91, 159, 227, 0.3)
```

**Hover State** (tablet/desktop)
```
Background: #4A8DD2 (darker 10%)
Shadow: 0px 6px 16px rgba(91, 159, 227, 0.4)
Transform: translateY(-2px)
Transition: all 200ms ease-out
```

**Pressed/Active State**
```
Background: #3976B8 (darker 20%)
Shadow: 0px 2px 8px rgba(91, 159, 227, 0.2)
Transform: translateY(0px) scale(0.98)
Transition: all 100ms ease-in
```

**Focused State** (keyboard navigation)
```
Background: #5B9FE3
Border: 2px solid #1A1A1A
Outline: 4px solid rgba(91, 159, 227, 0.2)
```

**Disabled State**
```
Background: #E0E0E0
Text: #999999
Shadow: none
Opacity: 0.6
Cursor: not-allowed
```

**Loading State**
```
Background: #5B9FE3
Text: Transparent
Spinner: White, 20px diameter
Cursor: wait
Pointer-events: none
```

#### Secondary Button (Outlined)

**Default State**
```
Background: transparent
Border: 2px solid #5B9FE3
Text: #5B9FE3, 16px, Semibold
Padding: 12px 32px (adjusted for border)
Border-radius: 24px
```

**Hover State**
```
Background: rgba(91, 159, 227, 0.1)
Border: 2px solid #4A8DD2
Text: #4A8DD2
```

**Pressed State**
```
Background: rgba(91, 159, 227, 0.2)
Transform: scale(0.98)
```

#### Tertiary Button (Text-only)

**Default State**
```
Background: transparent
Text: #5B9FE3, 16px, Semibold
Padding: 12px 16px
Border-radius: 8px
```

**Hover State**
```
Background: rgba(91, 159, 227, 0.1)
Text: #4A8DD2
```

#### Icon Button

**Default State**
```
Background: #FFFFFF
Size: 48x48px
Border-radius: 50%
Icon: #1A1A1A, 24x24px
Shadow: 0px 2px 8px rgba(0, 0, 0, 0.1)
```

**Pressed State**
```
Background: #F5F5F5
Transform: scale(0.95)
Shadow: 0px 1px 4px rgba(0, 0, 0, 0.15)
```

### Input Field

#### Text Input

**Default State**
```
Background: #FFFFFF
Border: 1px solid #E0E0E0
Border-radius: 12px
Padding: 14px 16px
Text: #1A1A1A, 16px, Regular
Placeholder: #999999
```

**Focused State**
```
Border: 2px solid #5B9FE3
Outline: 4px solid rgba(91, 159, 227, 0.1)
Placeholder: #CCCCCC
```

**Filled State**
```
Border: 1px solid #E0E0E0
Background: #FFFFFF
```

**Error State**
```
Border: 2px solid #F44336
Background: rgba(244, 67, 54, 0.05)
Text: #1A1A1A
Error message: #F44336, 12px, below input
Icon: Error icon (#F44336) on right
```

**Success State**
```
Border: 2px solid #4CAF50
Background: rgba(76, 175, 80, 0.05)
Icon: Checkmark icon (#4CAF50) on right
```

**Disabled State**
```
Background: #F5F5F5
Border: 1px solid #E0E0E0
Text: #999999
Cursor: not-allowed
```

#### Search Input

**Default State**
```
Background: #FFFFFF
Border-radius: 16px
Padding: 12px 16px 12px 48px
Icon: Search icon (#999999) positioned left
Placeholder: "Search", #999999
Shadow: 0px 2px 8px rgba(0, 0, 0, 0.08)
```

**Focused State**
```
Shadow: 0px 4px 12px rgba(91, 159, 227, 0.15)
Border: 2px solid #5B9FE3
Icon: #5B9FE3
```

**With Text State**
```
Clear button (X icon) appears on right
```

### Card

#### Standard Card

**Default State**
```
Background: #FFFFFF (hoặc rgba(255, 255, 255, 0.9) for glass)
Border-radius: 20px
Padding: 16px
Shadow: 0px 4px 16px rgba(0, 0, 0, 0.08)
Border: 1px solid rgba(255, 255, 255, 0.8)
Backdrop-filter: blur(20px) (nếu dùng glass effect)
```

**Hover State** (tablet/desktop)
```
Shadow: 0px 8px 24px rgba(0, 0, 0, 0.12)
Transform: translateY(-4px)
Transition: all 250ms ease-out
```

**Pressed State** (mobile)
```
Transform: scale(0.98)
Shadow: 0px 2px 8px rgba(0, 0, 0, 0.1)
Transition: all 150ms ease-in
```

**Loading State**
```
Background: Skeleton gradient animation
Content: Shimmer effect
```

#### Category Pill

**Default State**
```
Background: #FFFFFF
Border: 1px solid #E0E0E0
Border-radius: 20px (pill)
Padding: 10px 20px
Text: #666666, 14px, Semibold
```

**Active/Selected State**
```
Background: #5B9FE3
Border: none
Text: #FFFFFF
Shadow: 0px 2px 8px rgba(91, 159, 227, 0.3)
```

**Hover State**
```
Background: #F5F5F5
Border: 1px solid #5B9FE3
```

#### Feature Card (với image)

**Structure**
```
Card container
  ├─ Image (aspect-ratio: 16/9, border-radius: 16px 16px 0 0)
  ├─ Badge overlay (top-left): duration, rating
  ├─ Play button overlay (center): 56x56px circle
  ├─ Content area (padding: 16px)
      ├─ Title (H4, #1A1A1A)
      └─ Subtitle (#666666, 14px)
```

**Hover State** (desktop)
```
Image: Zoom 1.05x scale
Play button: Opacity 1, scale 1.1
Shadow: Enhanced
```

---

## 5. Interaction & Motion

### Micro-interactions

#### Button Press
```
Scale: 0.98
Duration: 100ms
Easing: ease-in
```

#### Toggle Switch
```
Knob transition: 250ms ease-in-out
Background color: 200ms ease
Haptic feedback: Light impact
```

#### Checkbox/Radio
```
Checkmark appearance: Scale from 0 to 1, 150ms ease-out
Background: Fade + scale, 200ms
Bounce effect on complete
```

#### Card Tap
```
Scale down: 0.98, 150ms ease-in
Scale up: 1.0, 200ms ease-out (spring)
Shadow reduce then expand
```

### Motion Design

#### Timing Functions
```css
--ease-out: cubic-bezier(0.33, 1, 0.68, 1);
--ease-in: cubic-bezier(0.32, 0, 0.67, 0);
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
--spring: cubic-bezier(0.68, -0.55, 0.265, 1.55);
```

#### Duration Scale
- **Instant:** 100ms (toggle, press)
- **Fast:** 200ms (hover, focus)
- **Standard:** 300ms (transitions, modals)
- **Slow:** 500ms (page transitions, reveals)

#### Page Transitions
```
Slide-in from right: 300ms ease-out
Fade-in: 250ms ease-in-out
Modal slide-up: 350ms spring
```

#### Scroll Animations
```
Parallax header: 0.5x scroll speed
Fade-in on scroll: Trigger at 80% viewport, 400ms ease-out
Stagger items: 50ms delay between each
```

### Special Patterns

#### Optimistic UI
- Thực hiện action ngay lập tức (không đợi server)
- Hiện loading indicator nhỏ (spinner trên button)
- Rollback + error toast nếu failed (3s duration)

#### Debounced Search
- Delay: 300ms sau keystroke cuối cùng
- Show loading indicator trong search input
- Clear previous results với fade-out 150ms

#### Skeleton Loading
```
Background: Linear gradient animation
  - Base: #E0E0E0
  - Highlight: #F5F5F5
  - Animation: Shimmer effect, 1.5s infinite
Shape: Match component structure
Duration: Until data loads (max 5s fallback)
```

#### Pull-to-Refresh
```
Pull distance: 80px trigger
Spinner: Rotate animation, #5B9FE3
Release animation: Spring ease, 400ms
Success: Checkmark + fade out
```

#### Bottom Sheet
```
Backdrop: rgba(0, 0, 0, 0.5), fade-in 200ms
Sheet slide-up: 350ms spring
Drag handle: 40px width, 4px height, centered
Dismiss: Swipe down or tap backdrop
```

#### Toast Notifications
```
Position: Top center (safe area + 16px)
Slide-in: From top, 300ms ease-out
Auto-dismiss: 3s (success), 5s (error)
Background:
  - Success: #4CAF50
  - Error: #F44336
  - Info: #5B9FE3
Text: #FFFFFF, 14px
Border-radius: 12px
Shadow: 0px 4px 12px rgba(0, 0, 0, 0.15)
```

---

## Best Practices

### Accessibility
- Contrast ratio minimum: 4.5:1 cho text, 3:1 cho large text
- Touch targets: Minimum 44x44px
- Focus indicators: Visible và high contrast
- Screen reader support: Semantic HTML, ARIA labels
- Animations: Respect `prefers-reduced-motion`

### Performance
- Image optimization: WebP format, lazy loading
- Animation: Sử dụng `transform` và `opacity` (GPU-accelerated)
- Debounce: Search inputs, scroll events
- Code splitting: Lazy load screens

### Consistency
- Sử dụng design tokens từ bảng màu và spacing system
- Component reuse: Không hardcode values
- Naming convention: BEM hoặc styled-components
- Icon set: Consistent stroke width (2px), rounded corners

---

**Lưu ý:** Guidelines này được reverse-engineer từ thiết kế tham khảo. Các trạng thái không thấy rõ trong mockup đã được bổ sung dựa trên best practices và phong cách visual hiện tại.

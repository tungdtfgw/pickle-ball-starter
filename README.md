# PickleBall Dating - Mobile App

Ứng dụng mobile kết nối cộng đồng người chơi pickleball, đặt sân, tìm đối thủ và huấn luyện viên.

## Công nghệ

- **Framework**: React Native
- **Development Tool**: Claude Code (Cursor IDE)
- **Platform**: iOS & Android

## Cấu trúc dự án

```
PickleBallDating-starter/
├── .claude/                    # Claude Code configuration
│   ├── agents/                 # Custom agents (BA, Backend, UI/UX)
│   ├── commands/               # Custom commands
│   └── settings.json           # Claude settings
├── design/                     # Tài liệu thiết kế
│   ├── flows/                  # Flow diagrams (F01-F16)
│   └── screens/                # Screen specifications
├── templates/                  # Templates cho docs
│   ├── FRONTEND_SPEC.template.md
│   └── PROJECT_STATUS.template.md
├── PRD.md                      # Product Requirements Document
├── PROJECT_STATUS.md           # Trạng thái dự án
└── CLAUDE.md                   # Hướng dẫn sử dụng Claude Code
```

## Quy trình phát triển với Claude Code

### 1. Khởi tạo môi trường

```bash
# Clone repository
git clone https://github.com/tungdtfgw/pickle-ball-starter.git
cd pickle-ball-starter

# Mở project trong Cursor
cursor .
```

### 2. Sử dụng Claude Agents

Dự án có 3 agents chuyên biệt trong `.claude/agents/`:

- **agent-ba.md**: Phân tích nghiệp vụ, viết specs, flows
- **agent-backend.md**: Thiết kế API, database, backend logic
- **agent-uiux.md**: Thiết kế UI/UX, components, styling

**Cách sử dụng:**
1. Mở Cursor IDE
2. Chọn agent phù hợp trong Claude panel
3. Chat với agent để phát triển feature

### 3. Workflow phát triển feature

#### Bước 1: Phân tích nghiệp vụ
```
@agent-ba Phân tích và viết spec cho feature [tên feature]
```
- Tạo flow diagram trong `design/flows/`
- Cập nhật `PRD.md` nếu cần

#### Bước 2: Thiết kế UI/UX
```
@agent-uiux Thiết kế màn hình cho [tên feature]
```
- Tạo screen spec trong `design/screens/`
- Định nghĩa components cần thiết

#### Bước 3: Implementation
```
@agent-backend Implement API cho [tên feature]
hoặc
Implement UI component theo spec [đường dẫn spec]
```

#### Bước 4: Review & Test
- Claude Code sẽ suggest improvements
- Run linter và fix issues
- Test trên simulator/device

### 4. Quy ước commit

```bash
# Format: <type>: <description>

feat: Thêm màn hình đăng ký
fix: Sửa lỗi validation form đăng nhập
docs: Cập nhật flow F01
style: Format code theo convention
refactor: Tái cấu trúc auth service
test: Thêm unit tests cho user profile
```

## Quy ước code

### Naming Convention

#### Python (Backend)
```python
# snake_case cho variables, functions
user_profile = get_user_profile(user_id)

# PascalCase cho Classes
class UserService:
    pass
```

#### JavaScript/React Native (Frontend)
```javascript
// camelCase cho variables, functions
const userName = getUserName();

// PascalCase cho Components
const UserProfile = () => {};

// UPPER_CASE cho constants
const API_BASE_URL = 'https://api.example.com';
```

### File Structure

```
src/
├── screens/           # Màn hình chính
├── components/        # Components tái sử dụng
├── services/          # API calls, business logic
├── utils/             # Helper functions
├── constants/         # Constants, configs
└── types/             # TypeScript types/interfaces
```

## Tài liệu quan trọng

### Product & Design
- **PRD.md**: Yêu cầu sản phẩm chi tiết
- **PROJECT_STATUS.md**: Trạng thái phát triển hiện tại
- **design/flows/**: 16 flows nghiệp vụ (F01-F16)
- **design/screens/**: Specs chi tiết từng màn hình

### Development
- **CLAUDE.md**: Hướng dẫn chi tiết sử dụng Claude Code
- **templates/**: Templates cho docs và specs

## Tips & Best Practices

### Làm việc với Claude Code

1. **Specific prompts**: Càng cụ thể càng tốt
   ```
   ❌ "Làm màn hình đăng nhập"
   ✅ "Implement màn hình đăng nhập theo spec design/screens/01-login-register.md, 
       sử dụng React Native Paper components"
   ```

2. **Reference files**: Tag files để Claude hiểu context
   ```
   Implement theo @design/flows/F01-dang-ky-xac-thuc.md
   ```

3. **Iterative development**: Làm từng bước nhỏ
   ```
   1. Tạo UI layout
   2. Thêm validation
   3. Connect API
   4. Handle errors
   ```

4. **Code review**: Yêu cầu Claude review
   ```
   Review code này và suggest improvements về performance và best practices
   ```

### Debugging

```
# Yêu cầu Claude phân tích lỗi
Lỗi này xuất hiện khi [mô tả], hãy phân tích và sửa:
[paste error log]

# Yêu cầu Claude debug
Debug function này, nó không hoạt động đúng khi [điều kiện]:
[paste code]
```

### Refactoring

```
# Yêu cầu optimize code
Refactor code này để dễ maintain và test hơn:
[paste code]

# Apply design patterns
Apply Repository pattern cho data layer này
```

## Commands hữu ích

### Git
```bash
# Check status
git status

# Commit và push
git add .
git commit -m "feat: your message"
git push

# Sync với remote
git pull
```

### Development
```bash
# Install dependencies (sau khi init React Native)
npm install
# hoặc
yarn install

# Run on iOS
npm run ios

# Run on Android
npm run android

# Start Metro bundler
npm start
```

## Troubleshooting

### Claude không hiểu context
- Tag đúng files với @ trong prompt
- Cung cấp đủ background information
- Chia nhỏ request thành các bước

### Code không chạy
- Yêu cầu Claude check linter errors
- Run `npm install` nếu thiếu dependencies
- Clear cache: `npm start -- --reset-cache`

### Git conflicts
```bash
# Yêu cầu Claude giải quyết conflict
Giúp tôi resolve git conflict này:
[paste conflict]
```

## Liên hệ & Support

- **Repository**: https://github.com/tungdtfgw/pickle-ball-starter
- **Claude Code Docs**: Xem `CLAUDE.md`

## License

[Thêm license nếu cần]

---

**Lưu ý**: Đây là dự án phát triển với AI-assisted development. Luôn review code được generate trước khi commit.

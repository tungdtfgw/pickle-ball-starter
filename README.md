# PickleBall Dating - Mobile App

Ứng dụng mẫu cho khóa học Vibe Code. 
Phát triển một mobile app kết nối cộng đồng người chơi pickleball, đặt sân, tìm đối thủ và huấn luyện viên theo mô hình phát triển Prototype

## Công nghệ

- **Framework**: React Native
- **Development Tool**: Claude Code CLI
- **Platform**: iOS & Android

## Cấu trúc dự án

```
PickleBallDating-starter/
├── .claude/                # Claude Code configuration
│   └── agents/                 # Custom agents (BA, Backend, UI/UX)
│       ├── agent-ba/
│       ├── agent-backend/
│       └── agent-uiux/
├── design/                     # Tài liệu thiết kế
│   ├── flows/                  # Flow diagrams (F01-F16)
│   └── screens/                # Screen specifications
├── templates/                  # Templates cho docs
│   ├── FRONTEND_SPEC.template.md
│   └── PROJECT_STATUS.template.md
├── PRD.md                      # Product Requirements Document
├── PROJECT_STATUS.md           # Trạng thái dự án
├── CLAUDE.md                   # Hướng dẫn quy trình phát triển
└── AGENT_COMMUNICATION.log     # Log giao tiếp giữa các agents
```

## Quy trình phát triển với Claude Code

### 1. Khởi tạo môi trường

```bash
# Clone repository
git clone https://github.com/tungdtfgw/pickle-ball-starter.git
cd pickle-ball-starter

# Khởi động Claude Code
claude
```

### 2. Hiểu về Custom Agents

Dự án sử dụng **3 custom agents** được định nghĩa trong `.claude/agents/`:

- **agent-ba**: Phân tích nghiệp vụ, viết PRD, thiết kế flows, database schema
- **agent-backend**: Implement backend, API, database, integration
- **agent-uiux**: Thiết kế UI/UX, implement frontend prototype

**Cách hoạt động:**
- Các agents được **agent chính tự động gọi** theo quy trình trong CLAUDE.md
- Bạn chỉ cần chat với agent chính, nó sẽ điều phối các custom agents
- Ví dụ: "Tôi muốn xây dựng app hẹn hò cho pickleball" → agent chính sẽ tự động gọi agent-ba → agent-uiux → agent-backend theo workflow

### 3. Workflow phát triển (Prototype-Driven Development)

Dự án tuân theo quy trình **4 giai đoạn** được định nghĩa trong `CLAUDE.md`:

#### Giai đoạn 1: Requirement Analysis
```
You: "Tôi muốn xây dựng [mô tả feature/app]"
```
- Agent chính → gọi agent-ba
- Agent-ba phân tích yêu cầu, tạo `PRD.md`
- Bạn review và approve PRD

#### Giai đoạn 2: Design
```
[Sau khi PRD được approve]
```
- Agent chính → gọi agent-ba thiết kế activity flows
- Agent chính → gọi agent-uiux thiết kế screens (từng screen một)
- Bạn approve từng screen design trong `design/screens/`

#### Giai đoạn 3: Frontend Prototype
```
[Sau khi design được approve]
```
- Agent chính → gọi agent-uiux implement toàn bộ UI với mock data
- Agent-uiux tạo `FRONTEND_SPEC.md`
- Bạn test prototype và approve UI/UX

#### Giai đoạn 4: Backend Development
```
[Sau khi frontend prototype được approve]
```
- Agent chính → gọi agent-ba thiết kế database schema
- Agent chính → gọi agent-backend implement backend + integration
- Bạn test toàn bộ app với real data

## Tài liệu quan trọng

### Product & Design
- **PRD.md**: Yêu cầu sản phẩm chi tiết
- **PROJECT_STATUS.md**: Trạng thái phát triển hiện tại
- **design/flows/**: flows nghiệp vụ
- **design/screens/**: Specs chi tiết từng màn hình

### Development
- **CLAUDE.md**: Hướng dẫn chi tiết sử dụng Claude Code
- **templates/**: Templates cho docs và specs

## Tips & Best Practices

### Làm việc với Claude Code CLI

1. **Mô tả rõ ràng ý tưởng/yêu cầu**
   ```
   ❌ "Làm màn hình đăng nhập"
   ✅ "Tôi muốn xây dựng màn hình đăng nhập cho app pickleball dating,
       có email/password và social login (Google, Facebook)"
   ```

2. **Để agent chính điều phối workflow**
   - Không cần chỉ định agent cụ thể
   - Agent chính sẽ tự động gọi agent-ba → agent-uiux → agent-backend
   - Bạn chỉ cần approve/feedback ở mỗi checkpoint

3. **Theo dõi tiến trình**
   - Check `PROJECT_STATUS.md` để biết giai đoạn hiện tại
   - Check `AGENT_COMMUNICATION.log` để xem lịch sử giao tiếp giữa agents

4. **Iterative development**
   - Approve từng giai đoạn trước khi chuyển sang giai đoạn tiếp theo
   - Feedback cụ thể nếu cần điều chỉnh
   - Test kỹ ở Giai đoạn 3 (Frontend Prototype) trước khi invest vào backend
---

**Lưu ý**: Đây là dự án phát triển với AI-assisted development (Claude Code). Luôn review và test code được generate trước khi commit.

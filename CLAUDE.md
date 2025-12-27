# Quy trình phát triển ứng dụng với Claude Code

Tài liệu này mô tả quy trình phát triển ứng dụng **PickleBallDating** sử dụng phương pháp **Prototype-Driven Development** với 4 giai đoạn chính: **Requirement → Design → Frontend Prototype → Backend Development**.

## Tổng quan

Dự án sử dụng 3 custom agents chuyên biệt:
- **agent-ba** (Business Analyst) - Phân tích yêu cầu, thiết kế flows và database
- **agent-uiux** (UI/UX Designer) - Thiết kế giao diện và implement frontend prototype
- **agent-backend** (Backend Developer) - Triển khai backend và integration

Agent chính (main) đóng vai trò điều phối và quản lý trạng thái dự án qua các giai đoạn.

## Đặc điểm của Prototype-Driven Development

**Triết lý**: Build toàn bộ frontend prototype với mock data trước, sau đó mới thiết kế và implement backend.
---

## Giai đoạn 1: Requirement (Phân tích yêu cầu)

### Mục tiêu
Thu thập và tài liệu hóa yêu cầu dự án thành **Product Requirements Document (PRD)**.

### Quy trình

1. **Agent chính** nhận ý tưởng/yêu cầu dự án từ người dùng
2. **Agent chính** gọi **agent-ba** để:
   - Phân tích yêu cầu chi tiết
   - Khám phá các yêu cầu ngầm định và edge cases
   - Định nghĩa user stories và acceptance criteria
   - Xác định yêu cầu phi chức năng (performance, security, scalability)
3. **Agent-ba** cộng tác với người dùng để:
   - Làm rõ các mơ hồ, giả định
   - Đặt câu hỏi sâu về tầm nhìn sản phẩm
   - Ưu tiên tính năng theo MoSCoW
4. **Agent-ba** tạo file **PRD.md** với cấu trúc:
   - Executive Summary
   - Feature Table (features có đánh số và có xác định mối quan hệ phụ thuộc)
   - Acceptance Criteria
   - Non-functional Requirements
   - Assumptions & Constraints

### Checkpoint
- ✅ Người dùng xác nhận file **PRD.md**
- ✅ Agent chính cập nhật trạng thái dự án: `Requirement ✓ → Design`

---

## Giai đoạn 2: Design (Thiết kế luồng và giao diện)

### Mục tiêu
Thiết kế luồng nghiệp vụ và mô tả chi tiết tất cả screens của ứng dụng.

**LƯU Ý QUAN TRỌNG**: Giai đoạn này KHÔNG thiết kế database. DB design sẽ được thực hiện ở Giai đoạn 4 (Backend Development), sau khi frontend prototype hoàn thành.

### Quy trình

#### 2.1. Activity Diagrams (Agent-ba)

1. **Agent chính** gọi **agent-ba** để thiết kế activity diagrams:

   **A. Activity Diagrams**
   Mỗi diagram sẽ:
   - Mô tả chi tiết về tính năng, mô tả cách người dùng sẽ tương tác trên ứng dụng để hoàn thành tính năng
   - Luồng nghiệp vụ chính của các tính năng
   - Decision points, parallel processes
   - Error handling flows
   - Lưu vào: `design/flows/[feature-number]-[short-name].md`

2. **Agent-ba** làm việc với người dùng để:
   - Xác nhận các quyết định thiết kế
   - Giải thích trade-offs giữa các phương án
   - Điều chỉnh thiết kế dựa trên feedback

#### 2.2. Screen Descriptions (Agent-uiux) - Tạo từng Screen riêng

**Sau khi agent-ba hoàn thành TẤT CẢ activity diagrams:**

**Quy trình:** Tạo từng screen thành file riêng lẻ (không tạo 1 file chứa tất cả screens)

1. **Agent chính** tạo folder `/design/screens/`

2. **Agent chính** gọi **agent-uiux** để tạo **TỪNG SCREEN MỘT**, theo thứ tự ưu tiên:
   - Có thể bắt đầu từ screens quan trọng nhất (Auth, Profile, Discovery)
   - Hoặc theo logic flow (Login → Profile → Home → Features)

3. **Với mỗi screen:**
   - **Agent-uiux** đọc PRD + Activity diagram liên quan
   - **Tạo file:** `/design/screens/[NN]-[screen-name].md`
   - Ví dụ:
     - `01-login-register.md` (F01)
     - `02-user-profile-player.md` (F02)
     - `03-court-discovery.md` (F06)
     - `04-book-court.md` (F07)
     - `05-find-opponent.md` (F09)
     - v.v...

4. **Format mỗi file screen:**

   ```markdown
   # [Screen Name]

   ## Screen Overview
   [Mô tả tổng quan 2-3 dòng]

   ## Mục đích
   [Mục đích của screen]

   ## Các Section/Components Chính
   ### 1. [Section Name]
   - Mô tả
   - Tương tác
   - Validations (nếu có)
   - Hiệu ứng

   ### 2. [Section Name]
   - ...

   ## Navigation
   - Đến screen này từ: [...]
   - Từ screen này đến: [...]

   ## States
   - Default state
   - Loading state
   - Error state
   - Edge cases

   ## Ghi chú
   [UX considerations, validations, error handling]
   ```

5. **Workflow chi tiết:**

   A. **Agent-uiux tạo screen 1**
      - Tạo file chi tiết đầy đủ
      - Báo cáo hoàn thành
      - **DỪNG LẠI** (KHÔNG tạo screen 2)

   B. **User xác nhận screen 1**
      - Approve → Tiếp tục screen 2
      - Sửa → Yêu cầu chỉnh sửa
      - Dừng → Review lại

   C. **Agent-uiux tạo screen 2** (khi user approve)
      - Tạo file chi tiết
      - Báo cáo hoàn thành
      - **DỪNG LẠI**

   D. **Lặp lại** cho tất cả screens

7. **Checkpoint:**
   - ✅ Người dùng xác nhận activity diagrams
   - ✅ Người dùng xác nhận **từng screen** trước khi qua screen tiếp theo
   - ✅ Tất cả screens được approve trong `/design/screens/[NN]-[screen-name].md`
   - ✅ Agent chính cập nhật trạng thái dự án: `Design ✓ → Frontend Prototype`

---

## Giai đoạn 3: Frontend Prototype (Xây dựng giao diện hoàn chỉnh)

### Mục tiêu
Implement TẤT CẢ screens của ứng dụng với mock data, tạo prototype hoàn chỉnh để user test UI/UX trước khi invest vào backend.

### Quy trình

#### 3.1. Setup Mock Data Structure

1. **Agent chính** gọi **agent-uiux** để bắt đầu frontend prototype

2. **Agent-uiux** thực hiện:
   - Phân tích tất cả screens trong `design/screens.md`
   - Xác định data structure cần thiết cho toàn bộ app
   - Tạo file **`data/mockData.ts`** với centralized mock data:
     ```typescript
     // data/mockData.ts
     export const MOCK_USERS = [...];
     export const MOCK_COURTS = [...];
     export const MOCK_MATCHES = [...];
     export const MOCK_MESSAGES = [...];
     ```

3. **Agent-uiux** sử dụng **MCP Image Search** để:
   - Tìm và tải ảnh phù hợp cho mock data (courts, avatars, etc.)
   - Lưu ảnh vào `assets/images/` hoặc sử dụng image URLs
   - Populate mock data với image references

#### 3.2. Implement All Screens

1. **Agent-uiux** implement TẤT CẢ screens theo thiết kế:
   - Xây dựng component structure theo atomic design
   - Implement styling với design tokens
   - Implement navigation flows (React Navigation)
   - Implement animations và interactions (React Native Reanimated)
   - Sử dụng mock data từ `data/mockData.ts`
   - Focus vào **happy paths** (không xử lý error phức tạp)

2. **Agent-uiux** tạo reusable components:
   - Button, Input, Card, Avatar, etc.
   - Đảm bảo consistency across screens
   - Document component props và usage

3. **Agent-uiux** implement basic state management:
   - Local state với useState/useReducer
   - Context API cho global state (nếu cần)
   - Mock authentication flow
   - Mock data fetching (simulate loading states)

#### 3.3. Create Frontend Specification

1. **Agent-uiux** tạo file **FRONTEND_SPEC.md** để document:
   - Danh sách tất cả screens implemented
   - Navigation structure
   - Component library
   - Mock data structure và location
   - Dependencies đã thêm
   - Known limitations (mock behaviors)
   - Handoff notes cho backend phase

2. File này sẽ là input quan trọng cho agent-backend ở giai đoạn tiếp theo

### Checkpoint
- ✅ Người dùng test toàn bộ prototype trên simulator/device
- ✅ Người dùng approve UI/UX experience
- ✅ Agent chính xác nhận **FRONTEND_SPEC.md** đã được tạo
- ✅ Agent chính cập nhật trạng thái dự án: `Frontend Prototype ✓ → Backend Development`

---

## Giai đoạn 4: Backend Development (Thiết kế DB và Integration)

### Mục tiêu
Thiết kế database, implement backend APIs, và integrate với frontend prototype đã có sẵn.

### Quy trình

#### 4.1. Database Design (Agent-ba)

**SAU KHI frontend prototype được approve:**

1. **Agent chính** gọi **agent-ba** để thiết kế database:

   **Input cho agent-ba**:
   - PRD.md (requirements)
   - Activity diagrams từ `design/flows/`
   - **FRONTEND_SPEC.md** (mock data structure từ frontend)
   - Code của frontend prototype (để hiểu data requirements)

   **Agent-ba thiết kế**:
   - Entity-Relationship Diagrams (ERD) bằng Mermaid
   - Table schemas (fields, data types, constraints, relationships)
   - Indexing strategy cho performance
   - Migration plan
   - Lưu vào: `design/database/schema.md`

2. **LƯU Ý QUAN TRỌNG**: Database schema phải MATCH với mock data structure trong frontend:
   - Field names tương thích
   - Data types phù hợp
   - Relationships giữa entities rõ ràng
   - Đảm bảo frontend không cần redesign khi chuyển sang real data

3. **Agent-ba** làm việc với người dùng để:
   - Xác nhận database schema
   - Giải thích indexing strategy
   - Thảo luận về data migration và seeding

#### 4.2. API Design (Agent-ba)

1. **Agent-ba** thiết kế API endpoints dựa trên:
   - Frontend needs (từ FRONTEND_SPEC.md)
   - Database schema
   - Activity diagrams

2. **Agent-ba** tạo file **design/api/endpoints.md**:
   - Danh sách tất cả API endpoints
   - Request/Response schemas
   - Authentication/Authorization requirements
   - Error handling strategies

#### 4.3. Backend Implementation (Agent-backend)

1. **Agent chính** gọi **agent-backend** để implement backend:

   **Input cho agent-backend**:
   - Database schema từ `design/database/schema.md`
   - API specs từ `design/api/endpoints.md`
   - FRONTEND_SPEC.md (handoff notes)
   - Frontend code (để hiểu integration points)

2. **Agent-backend** thực hiện:
   - Setup database (SQLite/PostgreSQL/Firebase)
   - Implement database migrations
   - Seed database với sample data
   - Build API endpoints (REST/GraphQL)
   - Implement authentication/authorization
   - Add error handling và validation
   - Write API documentation

#### 4.4. Frontend-Backend Integration (Agent-backend)

1. **Agent-backend** integrate với frontend:
   - Replace mock data imports với API calls
   - Implement data fetching logic
   - Add loading/error states
   - Implement state persistence (AsyncStorage/SecureStore)
   - Handle offline scenarios (optional)

2. **Agent-backend** làm việc với **agent-uiux** nếu cần:
   - Request UI changes cho error states
   - Clarify data binding requirements
   - Fix UI issues phát sinh từ real data

#### 4.5. Testing & Validation

1. **Agent-backend** đảm bảo:
   - Tất cả screens hoạt động với real data
   - Authentication flow hoàn chỉnh
   - CRUD operations đúng đắn
   - Error handling proper
   - Performance acceptable

2. **Agent chính** tóm tắt:
   - Backend components đã implement
   - API endpoints available
   - Integration status
   - Known issues (nếu có)

### Checkpoint
- ✅ Người dùng test toàn bộ app với real data
- ✅ Tất cả features hoạt động end-to-end
- ✅ Người dùng approve final app
- ✅ Agent chính cập nhật trạng thái dự án: `Backend Development ✓ → Complete`

---

## Quản lý trạng thái dự án

### File tracking: `PROJECT_STATUS.md`

Agent chính duy trì file này với format:

```markdown
# Project Status

## Current Phase: [Requirement|Design|Frontend Prototype|Backend Development|Complete]

## Progress

### ✓ Completed Phases
- [x] Requirement - PRD confirmed on [date]
- [x] Design - Activity flows and screens confirmed on [date]
- [x] Frontend Prototype - UI/UX approved on [date]

### → Current Phase
- [ ] Backend Development - In progress

## Deliverables

### Phase 1: Requirement
- [x] PRD.md

### Phase 2: Design
- [x] design/flows/*.md (Activity diagrams)
- [x] design/screens.md (Screen descriptions)

### Phase 3: Frontend Prototype
- [x] All screens implemented
- [x] data/mockData.ts
- [x] FRONTEND_SPEC.md
- [x] Prototype approved by user

### Phase 4: Backend Development
- [ ] design/database/schema.md
- [ ] design/api/endpoints.md
- [ ] Backend implementation
- [ ] Frontend-backend integration
- [ ] End-to-end testing

## Last Updated
[Date and time]
```

---

## Agent Communication Logging

### Mục đích
Tracking và audit trail cho mọi giao tiếp giữa các agents để:
- Theo dõi luồng công việc giữa các agents
- Debug khi có vấn đề
- Review lịch sử collaboration
- Đảm bảo transparency trong quy trình

### File log: `AGENT_COMMUNICATION.log`

Tất cả agents (kể cả agent chính) phải log mọi communication vào file này.

### Format log entry

```
[YYYY-MM-DD HH:MM:SS] SENDER → RECEIVER | REQUEST_BRIEF
```

**Chi tiết:**
- **Time**: ISO format `YYYY-MM-DD HH:MM:SS` (local time)
- **SENDER**: Tên agent gửi (main, agent-ba, agent-uiux, agent-backend)
- **RECEIVER**: Tên agent nhận
- **REQUEST_BRIEF**: Mô tả ngắn gọn (1 dòng, tối đa 100 ký tự) về yêu cầu/thông tin trao đổi

### Ví dụ log entries

```log
[2025-12-27 15:30:15] main → agent-ba | Phân tích yêu cầu: PickleBall Dating App
[2025-12-27 15:45:22] agent-ba → main | Hoàn thành PRD.md với 12 tính năng chính
[2025-12-27 16:10:03] main → agent-ba | Thiết kế activity flows cho matching feature
[2025-12-27 16:35:41] agent-ba → main | Hoàn thành activity diagrams cho 12 features
[2025-12-27 17:00:12] main → agent-uiux | Tạo screen descriptions cho toàn bộ app
[2025-12-27 17:30:22] agent-uiux → main | Hoàn thành design/screens.md với 18 screens
[2025-12-27 18:00:05] main → agent-uiux | Implement frontend prototype với mock data
[2025-12-27 20:15:30] agent-uiux → main | Hoàn thành prototype và FRONTEND_SPEC.md
[2025-12-27 20:30:10] main → agent-ba | Thiết kế database schema dựa trên frontend
[2025-12-27 21:00:45] agent-ba → main | Hoàn thành schema.md và API endpoints design
[2025-12-27 21:15:20] main → agent-backend | Implement backend và integrate với frontend
[2025-12-27 23:45:10] agent-backend → main | Hoàn thành backend integration
```

### Quy tắc logging

#### 1. Khi nào phải log

**BẮT BUỘC log trong các trường hợp sau:**

- Agent chính gọi custom agent (main → agent-*)
- Custom agent báo cáo kết quả cho agent chính (agent-* → main)
- Custom agent gọi custom agent khác (agent-* → agent-*)
- Agent yêu cầu thông tin từ agent khác
- Agent chuyển giao công việc (handoff)
- Agent báo lỗi/vấn đề cho agent khác

#### 2. Không cần log

- Agent tương tác với user (đã có trong chat transcript)
- Agent đọc/ghi file (đã có tool logs)
- Agent tự thực hiện công việc internal

#### 3. Cách implement logging

**Sử dụng Bash tool để append vào log file:**

```bash
echo "[$(date '+%Y-%m-%d %H:%M:%S')] SENDER → RECEIVER | REQUEST_BRIEF" >> AGENT_COMMUNICATION.log
```

**Ví dụ cụ thể:**

```bash
# Agent chính gọi agent-ba
echo "[$(date '+%Y-%m-%d %H:%M:%S')] main → agent-ba | Phân tích yêu cầu: PickleBall Dating App" >> AGENT_COMMUNICATION.log

# Agent-ba báo cáo cho main
echo "[$(date '+%Y-%m-%d %H:%M:%S')] agent-ba → main | Hoàn thành PRD.md với 12 features" >> AGENT_COMMUNICATION.log

# Agent-uiux chuyển giao cho agent-backend
echo "[$(date '+%Y-%m-%d %H:%M:%S')] agent-uiux → agent-backend | Handoff: Frontend prototype hoàn thành" >> AGENT_COMMUNICATION.log
```

#### 4. Best practices cho REQUEST_BRIEF

- **Ngắn gọn**: Tối đa 100 ký tự
- **Mô tả rõ ràng**: Ai đọc cũng hiểu ngay
- **Tập trung vào action**: Dùng động từ (Phân tích, Thiết kế, Implement, Fix, Yêu cầu, Cung cấp)
- **Bao gồm context key**: Feature name, screen name, hoặc task name

**Tốt:**
- `Phân tích yêu cầu: PickleBall Dating App`
- `Thiết kế activity flows cho matching feature`
- `Implement frontend prototype với mock data`
- `Thiết kế database schema dựa trên frontend`

**Không tốt:**
- `Làm việc` (quá chung chung)
- `Agent-ba please analyze the requirements for the pickleball dating app with...` (quá dài)
- `???` (không có thông tin)

### Trách nhiệm logging

#### Agent chính (Main Agent)
- Log **TRƯỚC** khi gọi custom agent (main → agent-*)
- Log **SAU** khi nhận kết quả từ custom agent (agent-* → main)

#### Custom Agents (agent-ba, agent-uiux, agent-backend)
- Log **NGAY** khi bắt đầu nhận task từ agent khác
- Log **TRƯỚC** khi gọi/yêu cầu agent khác (agent-* → agent-*)
- Log **SAU** khi hoàn thành và trả kết quả

### Xem log

```bash
# Xem toàn bộ log
cat AGENT_COMMUNICATION.log

# Xem 20 log entries gần nhất
tail -20 AGENT_COMMUNICATION.log

# Tìm tất cả communication từ main agent
grep "main →" AGENT_COMMUNICATION.log

# Tìm tất cả communication liên quan đến agent-ba
grep "agent-ba" AGENT_COMMUNICATION.log

# Xem log trong khoảng thời gian cụ thể
grep "2025-12-27" AGENT_COMMUNICATION.log
```

---

## Vai trò và trách nhiệm

### Agent chính (Main Agent)
- Điều phối workflow giữa các agents
- Quản lý trạng thái dự án qua các giai đoạn
- Tổng hợp kết quả và báo cáo cho người dùng
- Đảm bảo các checkpoint được hoàn thành trước khi chuyển giai đoạn

### Agent-ba (Business Analyst)
- **Giai đoạn Requirement**: Tạo PRD, phân tích yêu cầu
- **Giai đoạn Design**: Thiết kế activity diagrams (KHÔNG thiết kế DB)
- **Giai đoạn Backend Development**: Thiết kế DB schema và API endpoints (SAU KHI frontend prototype hoàn thành)

### Agent-uiux (UI/UX Designer)
- **Giai đoạn Design**: Tạo mô tả screens (design/screens.md) dựa trên activity diagrams
- **Giai đoạn Frontend Prototype**:
  - Implement TẤT CẢ screens với mock data
  - Tạo centralized mock data file
  - Sử dụng MCP Image Search để lấy ảnh mock
  - Tạo FRONTEND_SPEC.md

### Agent-backend (Backend Developer)
- **Giai đoạn Backend Development**:
  - Implement database theo schema từ agent-ba
  - Build API endpoints
  - Integrate frontend với backend
  - Replace mock data bằng real data
  - Collaborate với agent-uiux nếu cần UI adjustments

---

## Nguyên tắc làm việc

1. **Không skip giai đoạn**: Phải hoàn thành Requirement → Design → Frontend Prototype → Backend Development theo thứ tự
2. **User approval required**: Mỗi checkpoint cần xác nhận từ người dùng
3. **Frontend-first approach**: Validate UI/UX trước khi invest vào backend
4. **Backend based on frontend**: DB và API design phải match với frontend requirements thực tế
5. **Collaboration over handoff**: Các agents trao đổi với nhau, không chỉ chuyển giao một chiều
6. **Document everything**: PRD, designs, diagrams, specs phải được lưu file
7. **Iterative refinement**: Chấp nhận feedback và iterate cho đến khi đạt yêu cầu
8. **Quality over speed**: Focus vào code quality, maintainability, best practices

---

## Ví dụ workflow đầy đủ

```
User: "Tôi muốn xây dựng app hẹn hò cho người chơi pickleball"

[Giai đoạn 1: Requirement]
Main → agent-ba: Phân tích requirements
agent-ba ↔ User: Clarify vision, features, priorities
agent-ba: Tạo PRD.md
User: ✓ Approve PRD
Main: Update status → Design phase

[Giai đoạn 2: Design]
Main → agent-ba: Design activity flows (KHÔNG thiết kế DB)
agent-ba: Tạo design/flows/*.md (12 features)
User: ✓ Approve activity flows
Main → agent-uiux: Tạo screen descriptions
agent-uiux: Tạo design/screens.md (18 screens)
User: ✓ Approve screen descriptions
Main: Update status → Frontend Prototype phase

[Giai đoạn 3: Frontend Prototype]
Main → agent-uiux: Implement ALL screens với mock data
agent-uiux: Setup data/mockData.ts (centralized mock)
agent-uiux: Use MCP Image Search để lấy ảnh courts, avatars
agent-uiux: Implement 18 screens với navigation
agent-uiux: Tạo FRONTEND_SPEC.md
User: ✓ Test prototype, approve UI/UX
Main: Update status → Backend Development phase

[Giai đoạn 4: Backend Development]
Main → agent-ba: Thiết kế DB schema dựa trên frontend
agent-ba: Review FRONTEND_SPEC.md và mock data structure
agent-ba: Tạo design/database/schema.md (match với frontend)
agent-ba: Tạo design/api/endpoints.md
User: ✓ Approve DB schema và API design
Main → agent-backend: Implement backend + integration
agent-backend: Setup database và migrations
agent-backend: Build API endpoints
agent-backend: Replace mock data imports với API calls
agent-backend ↔ agent-uiux: Fix UI issues nếu cần
User: ✓ Test full app với real data
Main: Update status → Complete ✓
```

---

## Lưu ý

- File này là hướng dẫn cho **agent chính** và **các custom agents**
- Người dùng có thể linh hoạt điều chỉnh quy trình nếu cần
- Trong trường hợp emergency fix, có thể skip một số bước nhưng phải document lại
- Luôn maintain PROJECT_STATUS.md để track progress
- Giai đoạn Frontend Prototype là **validation checkpoint** quan trọng - đừng rush qua giai đoạn này

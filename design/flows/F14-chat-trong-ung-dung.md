# F14: Chat trong Ung dung - Activity Diagram

## Mo ta Tinh nang

He thong chat cho phep nguoi dung da ghep doi nhan tin voi nhau. Ho tro tin nhan van ban va hinh anh.

## Phu thuoc

- F01: Dang ky va Xac thuc Nguoi dung
- Ghep doi tu: F09, F10, F11, F13 (phai co match truoc khi chat)

---

## Activity Diagram - Danh sach Cuoc hoi thoai

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi dung mo tab Chat]

    A --> B[Goi API lay danh sach cuoc hoi thoai]

    B --> C{API tra ve?}
    C -->|Loi| D[Hien thi loi ket noi]
    D --> E[Nut: Thu lai]
    E --> B

    C -->|Thanh cong| F{Co cuoc hoi thoai nao?}
    F -->|Khong| G["Hien thi:
    Chua co cuoc tro chuyen nao
    Bat dau tim kiem de ket noi voi nguoi khac!"]
    G --> End1([Ket thuc])

    F -->|Co| H[Hien thi danh sach cuoc hoi thoai]

    H --> I["Moi cuoc hoi thoai hien thi:
    - Avatar nguoi/nhom
    - Ten nguoi/nhom
    - Tin nhan cuoi
    - Thoi gian tin nhan cuoi
    - Badge so tin chua doc (neu co)
    - Trang thai online/offline"]

    I --> J[Sap xep theo thoi gian tin nhan cuoi (moi nhat len dau)]

    J --> K[Nguoi dung tuong tac]
    K --> L{Tuong tac?}

    L -->|Tap vao cuoc hoi thoai| M[Mo man hinh chat]
    L -->|Swipe trai| N[Hien thi tuy chon]
    L -->|Pull to refresh| O[Lam moi danh sach]

    N --> P["Tuy chon:
    - Xoa cuoc tro chuyen
    - Tat thong bao
    - Block/Report"]

    P --> Q{Chon?}
    Q -->|Xoa| R[Xac nhan xoa]
    Q -->|Tat thong bao| S[Toggle thong bao]
    Q -->|Block| T[Block nguoi dung]
    Q -->|Huy| K

    R --> U{Xac nhan?}
    U -->|Co| V[Xoa cuoc tro chuyen khoi danh sach]
    U -->|Khong| K
    V --> K

    S --> W[Cap nhat trang thai thong bao]
    W --> K

    T --> X[Xac nhan block]
    X --> Y{Xac nhan?}
    Y -->|Co| Z[Block nguoi dung]
    Y -->|Khong| K
    Z --> AA[Xoa cuoc tro chuyen]
    AA --> K

    O --> B

    M --> End2([Ket thuc - Mo chat])
```

---

## Activity Diagram - Chat Chi tiet

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi dung mo cuoc hoi thoai]

    A --> B[Goi API lay lich su tin nhan]
    B --> C[Hien thi header voi thong tin nguoi/nhom]

    C --> D["Header:
    - Avatar
    - Ten
    - Trang thai (Online/Offline/Dang go...)
    - Nut quay lai
    - Nut menu (...)"]

    D --> E{Co lich su tin nhan?}
    E -->|Khong| F[Hien thi trang trong]
    E -->|Co| G[Hien thi tin nhan]

    F --> H[Placeholder: Bat dau cuoc tro chuyen!]

    G --> I["Moi tin nhan:
    - Noi dung (text/hinh)
    - Thoi gian gui
    - Trang thai (Da gui/Da nhan/Da doc)
    - Avatar nguoi gui (neu nhom)"]

    I --> J[Tin nhan minh gui: ben phai, mau xanh]
    J --> K[Tin nhan nguoi khac: ben trai, mau xam]

    K --> L[Nguoi dung tuong tac]
    H --> L

    L --> M{Tuong tac?}
    M -->|Go tin nhan| N[Nhap van ban vao input]
    M -->|Chon hinh anh| O[Mo picker chon anh]
    M -->|Tap tin nhan| P[Hien thi menu tin nhan]
    M -->|Cuon len| Q[Tai them tin nhan cu]
    M -->|Tap header| R[Xem ho so]

    %% Nhanh gui tin nhan van ban
    N --> S[Nguoi dung nhap noi dung]
    S --> T{Noi dung hop le?}
    T -->|Trong| U[Vo hieu hoa nut Gui]
    T -->|Qua dai > 1000 ky tu| V[Thong bao: Tin nhan qua dai]
    T -->|Hop le| W[Kich hoat nut Gui]

    U --> L
    V --> S

    W --> X[Nguoi dung tap Gui]
    X --> Y[Hien thi tin nhan voi trang thai Dang gui...]
    Y --> Z[Gui tin nhan len server]

    Z --> AA{Gui thanh cong?}
    AA -->|Co| AB[Cap nhat trang thai: Da gui]
    AA -->|Loi mang| AC[Cap nhat trang thai: Gui that bai]

    AB --> AD[Doi server xac nhan nguoi nhan da nhan]
    AD --> AE[Cap nhat trang thai: Da nhan]
    AE --> AF[Doi nguoi nhan doc]
    AF --> AG[Cap nhat trang thai: Da doc]
    AG --> L

    AC --> AH[Hien thi icon ! va Tap de gui lai]
    AH --> AI{Nguoi dung tap?}
    AI -->|Co| Z
    AI -->|Khong| L

    %% Nhanh gui hinh anh
    O --> AJ{Kiem tra}
    AJ -->|Qua 5 anh| AK[Thong bao: Toi da 5 anh/lan]
    AJ -->|Anh qua 5MB| AL[Thong bao: Anh qua lon]
    AJ -->|Hop le| AM[Hien thi preview anh]

    AK --> L
    AL --> O

    AM --> AN[Nguoi dung tap Gui]
    AN --> AO[Hien thi anh voi progress upload]
    AO --> AP{Upload thanh cong?}
    AP -->|Co| AQ[Hien thi anh da gui]
    AP -->|Loi| AR[Hien thi loi upload]

    AQ --> L
    AR --> AS[Nut: Thu lai / Huy]
    AS --> L

    %% Nhanh menu tin nhan
    P --> AT["Menu:
    - Copy (voi text)
    - Luu anh (voi hinh)
    - Xoa (tin nhan minh gui)
    - Reply (optional)"]
    AT --> L

    %% Nhanh tai them tin nhan
    Q --> AU[Hien thi loading]
    AU --> AV[Goi API lay tin nhan cu hon]
    AV --> AW{Con tin nhan cu?}
    AW -->|Co| AX[Them vao dau danh sach]
    AW -->|Khong| AY[Hien thi: Da tai het tin nhan]
    AX --> L
    AY --> L

    %% Nhanh xem ho so
    R --> AZ{Loai cuoc tro chuyen?}
    AZ -->|1-1| BA[Mo ho so nguoi kia]
    AZ -->|Nhom| BB[Mo danh sach thanh vien]
    BA --> L
    BB --> L
```

---

## Activity Diagram - Nhan tin nhan (Realtime)

```mermaid
flowchart TD
    Start([Nguoi gui gui tin nhan]) --> A[Server nhan tin nhan]

    A --> B[Server luu tin nhan]
    B --> C[Server gui tin nhan den nguoi nhan qua WebSocket]

    C --> D{Nguoi nhan dang mo app?}
    D -->|Khong| E[Gui Push Notification]
    D -->|Co| F{Dang o man hinh chat nay?}

    E --> G[Nguoi nhan nhan thong bao]
    G --> H[Tap thong bao -> Mo chat]

    F -->|Khong| I[Cap nhat badge tin chua doc]
    F -->|Co| J[Hien thi tin nhan moi]

    I --> K[Hien thi so tin chua doc tren tab Chat]

    J --> L[Tu dong scroll xuong tin moi]
    L --> M[Gui xac nhan Da doc len server]
    M --> N[Server cap nhat trang thai tin nhan]
    N --> O[Thong bao cho nguoi gui: Da doc]
```

---

## Activity Diagram - Chat Nhom (4 nguoi - Doi vs Doi)

```mermaid
flowchart TD
    Start([Ghep doi Doi vs Doi thanh cong]) --> A[He thong tao phong chat nhom]

    A --> B["Thanh vien nhom:
    - Nguoi 1 Doi A
    - Nguoi 2 Doi A
    - Nguoi 1 Doi B
    - Nguoi 2 Doi B"]

    B --> C[Hien thi thong bao tao nhom cho ca 4 nguoi]

    C --> D[Nguoi dung mo chat nhom]
    D --> E["Header nhom:
    - Avatar 4 nguoi (2x2 grid)
    - Ten nhom (Ten doi A vs Ten doi B)
    - So thanh vien"]

    E --> F[Hien thi tin nhan nhom]
    F --> G["Moi tin nhan co:
    - Avatar nguoi gui
    - Ten nguoi gui
    - Noi dung
    - Thoi gian"]

    G --> H[Nguoi dung gui tin nhan]
    H --> I[Tin nhan gui den CA 3 nguoi con lai]
    I --> J[3 nguoi nhan thong bao]
```

---

## Trang thai Tin nhan

```mermaid
stateDiagram-v2
    [*] --> DangGui: Nguoi dung tap Gui

    DangGui --> DaGui: Server xac nhan nhan
    DangGui --> ThatBai: Loi mang/server

    DaGui --> DaNhan: Nguoi nhan online, nhan tin
    DaNhan --> DaDoc: Nguoi nhan mo va doc tin

    ThatBai --> DangGui: Nguoi dung tap Thu lai

    DaDoc --> [*]
```

### Icon Trang thai

| Trang thai | Icon | Mau |
|------------|------|-----|
| Dang gui | Dong ho | Xam |
| Da gui | 1 dau tick | Xam |
| Da nhan | 2 dau tick | Xam |
| Da doc | 2 dau tick | Xanh |
| That bai | Dau cham than | Do |

---

## Truong hop Dac biet

### 1. Mat mang khi gui tin nhan

```mermaid
flowchart TD
    A[Nguoi dung tap Gui] --> B[Kiem tra ket noi mang]
    B --> C{Co mang?}
    C -->|Khong| D[Luu tin nhan vao hang doi local]
    D --> E[Hien thi tin nhan voi trang thai Cho gui]
    E --> F[Khi co mang lai]
    F --> G[Tu dong gui cac tin nhan trong hang doi]

    C -->|Co| H[Gui binh thuong]
```

### 2. Nguoi nhan block hoac report

```mermaid
flowchart TD
    A[Nguoi A gui tin cho Nguoi B] --> B{B da block A?}
    B -->|Co| C[Tin nhan khong gui duoc]
    C --> D[Hien thi: Khong the gui tin nhan]

    B -->|Chua| E[Gui binh thuong]
```

### 3. Hinh anh chua upload xong

```mermaid
flowchart TD
    A[Nguoi dung chon anh] --> B[Bat dau upload]
    B --> C[Hien thi progress bar]
    C --> D{Nguoi dung dong man hinh?}
    D -->|Co| E[Tiep tuc upload trong background]
    E --> F{Upload xong?}
    F -->|Co| G[Gui tin nhan anh]
    F -->|Loi| H[Thong bao loi khi quay lai]
```

---

## Giao dien Chat

### Danh sach cuoc hoi thoai
```
+----------------------------------+
|         TIN NHAN                 |
+----------------------------------+
| [Avatar] Nguyen Van A            |
|          Chao ban!       10:30   |
|                          • 2     |
+----------------------------------+
| [Avatar] Nhom: Doi A vs Doi B    |
|          A: OK, hen gap    09:15 |
+----------------------------------+
| [Avatar] HLV Tran Van B          |
|          Tuan sau hoc nhe  Hom qua|
+----------------------------------+
```

### Man hinh chat chi tiet
```
+----------------------------------+
| <  Nguyen Van A           Online |
+----------------------------------+
|                                  |
|              Chao ban!     10:30 |
|              [tin nhan minh gui] |
|                                  |
| [Avatar]                         |
| Chao, ban khoe khong?      10:31 |
| [tin nhan nguoi khac]            |
|                                  |
|              Minh khoe!    10:32 |
|              [2 dau tick xanh]   |
+----------------------------------+
| [+] [_____Nhap tin nhan_____] [>]|
+----------------------------------+
```

---

## Acceptance Criteria

- [ ] Chi mo chat giua nhung nguoi da ghep doi
- [ ] Gui va nhan tin nhan van ban
- [ ] Gui hinh anh (toi da 5 anh/lan, moi anh toi da 5MB)
- [ ] Hien thi trang thai tin nhan: Da gui, Da nhan, Da doc
- [ ] Hien thi thoi gian gui tin nhan
- [ ] Thong bao day khi co tin nhan moi (khi ung dung o nen)
- [ ] Hien thi so tin nhan chua doc tren bieu tuong chat

---

## Ghi chu Ky thuat

1. **WebSocket**: Su dung WebSocket de nhan tin nhan realtime
2. **Offline queue**: Luu tin nhan chua gui vao local, tu dong gui khi co mang
3. **Image compression**: Nen anh truoc khi upload (max 1MB sau nen)
4. **Pagination**: Tai 20 tin nhan moi lan, cuon len de tai them
5. **Read receipts**: Gui read receipt khi nguoi dung scroll den tin nhan
6. **Typing indicator**: Hien thi "Dang go..." khi nguoi kia dang go (optional)

# F16: Bang Thong ke - Activity Diagram

## Mo ta Tinh nang

Bang dieu khien hien thi cac so lieu thong ke cho chu san: so luot dat san, ty le lap day, doanh thu uoc tinh, xu huong.

## Phu thuoc

- F07: Dat San (can co du lieu dat san)
- F08: Quan ly Dat san (du lieu xac nhan/tu choi)

---

## Activity Diagram - Xem Thong ke

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Chu san mo tab Thong ke]

    A --> B{Co san nao khong?}
    B -->|Khong| C[Hien thi: Ban chua tao san nao]
    C --> D[Nut: Tao san ngay]
    D --> E[Chuyen den F03 - Tao san]
    E --> End1([Ket thuc])

    B -->|Co| F[Goi API lay du lieu thong ke]

    F --> G{API tra ve?}
    G -->|Loi| H[Hien thi loi ket noi]
    H --> I[Nut: Thu lai]
    I --> F

    G -->|Thanh cong| J{Co du lieu dat san?}
    J -->|Khong| K["Hien thi: Chua co du lieu thong ke
    Du lieu se duoc cap nhat khi co dat san"]
    K --> L[Hien thi cac chi so = 0]

    J -->|Co| M[Hien thi dashboard thong ke]
    L --> M

    M --> N["Dashboard bao gom:
    1. Bo chon khoang thoi gian
    2. Tong quan (Summary Cards)
    3. Bieu do xu huong
    4. Chi tiet theo san con
    5. Khung gio pho bien"]

    N --> O[Chu san tuong tac]

    O --> P{Tuong tac?}
    P -->|Doi khoang thoi gian| Q[Chon thoi gian moi]
    P -->|Xem chi tiet| R[Tap vao so lieu/bieu do]
    P -->|Doi san| S[Chon san khac tu dropdown]
    P -->|Lam moi| T[Pull to refresh]

    Q --> U["Tuy chon:
    - Hom nay
    - 7 ngay qua
    - Thang nay
    - Thang truoc
    - Tuy chon (chon ngay)"]
    U --> V[Goi API voi khoang thoi gian moi]
    V --> W[Cap nhat dashboard]
    W --> O

    R --> X{Loai chi tiet?}
    X -->|Tong dat san| Y[Mo danh sach dat san trong khoang thoi gian]
    X -->|Doanh thu| Z[Mo chi tiet doanh thu theo ngay]
    X -->|Bieu do| AA[Mo bieu do lon hon voi chi tiet]

    Y --> O
    Z --> O
    AA --> O

    S --> AB[Goi API cho san duoc chon]
    AB --> W

    T --> F
```

---

## Cac Chi so Thong ke

### 1. Summary Cards (Tong quan)

```mermaid
flowchart LR
    A["Card 1: Tong Dat san
    - Con so chinh: 45 luot
    - So sanh: +12% so voi ky truoc
    - Icon: Calendar"]

    B["Card 2: Ty le Lap day
    - Con so chinh: 68%
    - So sanh: +5% so voi ky truoc
    - Icon: Pie chart"]

    C["Card 3: Doanh thu Uoc tinh
    - Con so chinh: 4,500,000 VND
    - So sanh: +15% so voi ky truoc
    - Icon: Money"]

    D["Card 4: San duoc dat nhieu nhat
    - Noi dung: San A - 20 luot
    - Icon: Trophy"]
```

### 2. Bieu do Xu huong

```mermaid
flowchart TD
    A[Bieu do Duong] --> B["Truc X: Ngay/Tuan/Thang
    Truc Y: So luot dat san
    Duong 1: Ky hien tai
    Duong 2: Ky truoc (optional)"]

    C[Bieu do Cot] --> D["Truc X: San con
    Truc Y: So luot dat
    Mau: Khac nhau moi san"]
```

### 3. Chi tiet theo San con

| San con | So luot dat | Doanh thu | Ty le lap day |
|---------|-------------|-----------|---------------|
| San A | 20 | 2,000,000 VND | 75% |
| San B | 15 | 1,500,000 VND | 60% |
| San C | 10 | 1,000,000 VND | 50% |

### 4. Khung gio Pho bien

```mermaid
flowchart LR
    A["Bang xep hang:
    1. 18:00 - 19:00: 15 luot
    2. 19:00 - 20:00: 12 luot
    3. 17:00 - 18:00: 10 luot
    4. 20:00 - 21:00: 8 luot"]
```

---

## Activity Diagram - Tinh toan Thong ke

```mermaid
flowchart TD
    Start([Yeu cau thong ke]) --> A[Nhan tham so: San ID, Khoang thoi gian]

    A --> B[Query dat san trong khoang thoi gian]
    B --> C[Loc chi lay dat san Da xac nhan]

    C --> D[Tinh Tong so dat san]
    D --> E["COUNT(bookings) WHERE status = 'confirmed'"]

    E --> F[Tinh Ty le lap day]
    F --> G["Ty le = (So khung gio da dat / Tong khung gio kha dung) x 100%"]

    G --> H[Tinh Doanh thu Uoc tinh]
    H --> I["Doanh thu = SUM(gia khung gio cua moi dat san)"]

    I --> J[Tinh So lieu theo San con]
    J --> K["GROUP BY sub_court_id"]

    K --> L[Tinh Khung gio pho bien]
    L --> M["GROUP BY time_slot
    ORDER BY COUNT DESC"]

    M --> N[Tinh Xu huong theo ngay]
    N --> O["GROUP BY DATE(booking_date)"]

    O --> P[Tra ve ket qua tong hop]
    P --> End([Ket thuc])
```

---

## Cong thuc Tinh toan

### Ty le Lap day

```
Ty le lap day = (So khung gio da dat / Tong khung gio kha dung) x 100%

Trong do:
- So khung gio da dat: COUNT bookings co status = 'confirmed'
- Tong khung gio kha dung: SUM tat ca khung gio cua cac san con trong khoang thoi gian
```

**Vi du:**
- San A co 10 khung gio/ngay, trong 7 ngay = 70 khung gio kha dung
- Da dat duoc 50 khung gio
- Ty le lap day = 50/70 x 100% = 71.4%

### Doanh thu Uoc tinh

```
Doanh thu = SUM(gia cua moi khung gio da dat va xac nhan)

Luu y:
- Chi tinh dat san Da xac nhan
- Khong tinh dat san Cho xac nhan/Tu choi/Huy
```

### So sanh voi Ky truoc

```
Thay doi (%) = ((Gia tri ky nay - Gia tri ky truoc) / Gia tri ky truoc) x 100%

Vi du:
- Thang nay: 45 dat san
- Thang truoc: 40 dat san
- Thay doi = ((45 - 40) / 40) x 100% = +12.5%
```

---

## Giao dien Dashboard

```
+----------------------------------+
|     THONG KE         [San: A ▼]  |
|     [Thang nay ▼]                |
+----------------------------------+
| +------+  +------+  +------+     |
| |  45  |  | 68%  |  | 4.5M |     |
| |dat san|  |lap day|  | VND  |     |
| | +12% |  | +5%  |  | +15% |     |
| +------+  +------+  +------+     |
+----------------------------------+
|    [Bieu do xu huong dat san]    |
|    ___/\___/\___/\               |
|   /                              |
+----------------------------------+
|  THEO SAN CON                    |
|  San A: ████████ 20 (45%)        |
|  San B: ██████ 15 (33%)          |
|  San C: ████ 10 (22%)            |
+----------------------------------+
|  KHUNG GIO PHO BIEN              |
|  1. 18:00-19:00  15 luot         |
|  2. 19:00-20:00  12 luot         |
|  3. 17:00-18:00  10 luot         |
+----------------------------------+
```

---

## Truong hop Dac biet

### 1. San moi tao, chua co du lieu

```mermaid
flowchart TD
    A[Chu san mo Thong ke] --> B{Co du lieu?}
    B -->|Khong| C[Hien thi thong bao]
    C --> D["Chua co du lieu thong ke
    Du lieu se hien thi khi ban co dat san dau tien"]
    D --> E[Hien thi cac chi so = 0]
    E --> F[Van hien thi layout dashboard]
```

### 2. Du lieu qua nhieu

```mermaid
flowchart TD
    A[Query du lieu] --> B{So luong ban ghi?}
    B -->|> 10000| C[Su dung pagination]
    C --> D[Tinh toan tung trang]
    D --> E[Aggregate ket qua]

    B -->|< 10000| F[Tinh toan truc tiep]
```

### 3. Nhieu san

```mermaid
flowchart TD
    A[Chu san co 5 san] --> B[Dropdown chon san]
    B --> C["Tuy chon:
    - Tat ca san (Tong hop)
    - San 1
    - San 2
    - ..."]

    C --> D{Chon?}
    D -->|Tat ca| E[Tinh tong hop cac san]
    D -->|1 san cu the| F[Chi tinh cho san do]
```

---

## Acceptance Criteria

- [ ] Tong so luot dat san (theo thang/tuan)
- [ ] Ty le san duoc dat (ty le lap day)
- [ ] Doanh thu uoc tinh (dua tren gia khung gio)
- [ ] San con duoc dat nhieu nhat
- [ ] Khung gio duoc dat nhieu nhat
- [ ] Bieu do xu huong theo thoi gian

---

## Ghi chu Ky thuat

1. **Caching**: Cache ket qua thong ke, refresh moi 15 phut hoac khi co dat san moi
2. **Background job**: Tinh toan thong ke tong hop moi ngay vao luc 00:00
3. **Indexing**: Index theo court_id, booking_date, status de query nhanh
4. **Aggregation**: Su dung database aggregation thay vi tinh toan trong app
5. **Export**: Ho tro xuat bao cao ra file (optional - Could have)
6. **Real-time update**: Cap nhat khi co dat san moi duoc xac nhan

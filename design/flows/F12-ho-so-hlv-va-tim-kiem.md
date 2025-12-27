# F12: Ho so HLV va Tim kiem - Activity Diagram

## Mo ta Tinh nang

Huan luyen vien tao ho so voi thong tin chuyen mon. Nguoi choi co the tim kiem va xem ho so HLV.

## Phu thuoc

- F01: Dang ky va Xac thuc Nguoi dung (HLV phai dang ky vai tro HLV)
- F02: Quan ly Ho so Nguoi dung (thong tin co ban)

---

## Activity Diagram - HLV Tao/Cap nhat Ho so

```mermaid
flowchart TD
    Start([Bat dau]) --> A[HLV mo tab Ho so cua toi]

    A --> B{Da tao ho so HLV chua?}
    B -->|Chua| C[Hien thi form tao ho so HLV]
    B -->|Da tao| D[Hien thi ho so hien tai]

    C --> E["Form thong tin:
    1. Gioi thieu ban than (textarea)
    2. So nam kinh nghiem
    3. Chuyen mon (multi-select)
    4. Gia/gio (VND)
    5. Dia diem day (chon tren ban do)
    6. Lich trinh day
    7. Video/Hinh anh minh hoa"]

    E --> F[HLV dien thong tin]

    F --> G{Thong tin hop le?}
    G -->|Thieu truong bat buoc| H[Highlight truong thieu]
    H --> F

    G -->|Hop le| I[HLV tap Luu]
    I --> J[Gui du lieu len server]

    J --> K{Luu thanh cong?}
    K -->|Loi| L[Hien thi thong bao loi]
    L --> F

    K -->|Thanh cong| M[Hien thi: Ho so da duoc tao]
    M --> D

    D --> N["Hien thi ho so:
    - Anh dai dien
    - Gioi thieu
    - Kinh nghiem
    - Chuyen mon
    - Gia/gio
    - Dia diem day
    - Lich trinh
    - Media (video/anh)"]

    N --> O[Nut: Chinh sua / Xem truoc]

    O --> P{HLV chon?}
    P -->|Chinh sua| Q[Mo form chinh sua]
    P -->|Xem truoc| R[Xem ho so nhu nguoi choi thay]

    Q --> S[HLV cap nhat thong tin]
    S --> T{Luu thay doi?}
    T -->|Co| U[Gui cap nhat len server]
    T -->|Huy| D

    U --> V{Cap nhat thanh cong?}
    V -->|Co| W[Hien thi: Da cap nhat ho so]
    V -->|Loi| X[Hien thi loi]
    W --> D
    X --> Q

    R --> Y[Hien thi giao dien preview]
    Y --> Z[Nut: Quay lai]
    Z --> D
```

---

## Activity Diagram - HLV Quan ly Media

```mermaid
flowchart TD
    Start([Bat dau]) --> A[HLV vao phan Media trong ho so]

    A --> B[Hien thi media hien co]
    B --> C["Danh sach:
    - Video (toi da 3)
    - Hinh anh (toi da 10)"]

    C --> D{HLV chon action?}
    D -->|Them video| E[Mo picker chon video]
    D -->|Them hinh anh| F[Mo picker chon anh]
    D -->|Xoa media| G[Chon media de xoa]
    D -->|Sap xep| H[Keo tha de sap xep]

    E --> I{Kiem tra video}
    I -->|Qua lon > 50MB| J[Thong bao: Video qua lon]
    I -->|Dinh dang sai| K[Thong bao: Dinh dang khong ho tro]
    I -->|Da du 3 video| L[Thong bao: Da du so luong video]
    I -->|Hop le| M[Upload video]

    J --> D
    K --> D
    L --> D

    M --> N[Hien thi progress upload]
    N --> O{Upload thanh cong?}
    O -->|Co| P[Them video vao danh sach]
    O -->|Loi| Q[Thong bao loi upload]

    P --> D
    Q --> D

    F --> R{Kiem tra hinh anh}
    R -->|Qua lon > 5MB| S[Thong bao: Anh qua lon]
    R -->|Da du 10 anh| T[Thong bao: Da du so luong anh]
    R -->|Hop le| U[Upload hinh anh]

    S --> D
    T --> D

    U --> V[Hien thi progress]
    V --> W{Upload thanh cong?}
    W -->|Co| X[Them anh vao danh sach]
    W -->|Loi| Y[Thong bao loi]
    X --> D
    Y --> D

    G --> Z[Xac nhan xoa]
    Z --> AA{Xac nhan?}
    AA -->|Co| AB[Xoa media]
    AA -->|Khong| D
    AB --> D

    H --> AC[Luu thu tu moi]
    AC --> D
```

---

## Activity Diagram - Nguoi choi Tim kiem HLV

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi choi mo tab Tim HLV]

    A --> B[Hien thi ban do voi HLV gan]

    B --> C["Hien thi:
    - Ban do voi marker cac HLV
    - Danh sach HLV (co the cuon)
    - Bo loc"]

    C --> D{Nguoi choi tuong tac?}
    D -->|Tap marker tren ban do| E[Hien thi preview HLV]
    D -->|Cuon danh sach| F[Xem danh sach HLV]
    D -->|Dung bo loc| G[Mo panel bo loc]
    D -->|Tap vao 1 HLV| H[Mo chi tiet HLV]

    E --> I["Preview card:
    - Anh, Ten
    - Kinh nghiem
    - Gia/gio
    - Khoang cach"]
    I --> J[Tap de xem chi tiet]
    J --> H

    F --> K["Moi item:
    - Anh dai dien
    - Ten
    - Kinh nghiem
    - Chuyen mon (tags)
    - Gia/gio
    - Khoang cach"]
    K --> D

    G --> L["Bo loc:
    - Khoang cach (1-20km)
    - Muc gia (min-max)
    - Chuyen mon"]
    L --> M[Nguoi choi thiet lap bo loc]
    M --> N[Ap dung bo loc]
    N --> O[Cap nhat danh sach HLV]
    O --> C

    H --> P["Chi tiet HLV:
    - Anh dai dien lon
    - Gioi thieu
    - Kinh nghiem
    - Chuyen mon
    - Gia/gio
    - Dia diem day (ban do nho)
    - Lich trinh day
    - Video/Hinh anh minh hoa
    - Nut: Thich / Bo qua"]

    P --> Q{Nguoi choi action?}
    Q -->|Thich| R[Chuyen sang luong F13]
    Q -->|Bo qua| S[Quay lai danh sach]
    Q -->|Xem media| T[Mo gallery xem video/anh]
    Q -->|Xem ban do| U[Mo ban do day du]

    R --> End1([Ket thuc - Chuyen F13])
    S --> C
    T --> V[Xem gallery]
    V --> P
    U --> W[Xem ban do lon]
    W --> P
```

---

## Cau truc Du lieu Ho so HLV

```mermaid
erDiagram
    USER ||--o| COACH_PROFILE : has

    COACH_PROFILE {
        string id PK
        string user_id FK
        text bio
        int experience_years
        array specialties
        decimal hourly_rate
        json teaching_locations
        json availability
        array media_urls
        datetime created_at
        datetime updated_at
    }
```

### Chi tiet Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| bio | Text | No | Gioi thieu ban than (max 1000 ky tu) |
| experience_years | Integer | No | So nam kinh nghiem (0-50) |
| specialties | Array[String] | No | Chuyen mon: Ky thuat co ban, Chien thuat, The luc... |
| hourly_rate | Decimal | No | Gia/gio (VND) |
| teaching_locations | Array[GeoPoint] | No | Cac dia diem day |
| availability | JSON | No | Lich trinh day theo ngay/gio |
| media | Array[URL] | No | Video (max 3) + Hinh anh (max 10) |

---

## Truong hop Dac biet

### 1. HLV chua hoan thien ho so

```mermaid
flowchart TD
    A[Nguoi choi tim kiem HLV] --> B{HLV co ho so day du?}
    B -->|Chua| C[Khong hien thi trong ket qua tim kiem]
    B -->|Day du| D[Hien thi trong ket qua]

    C --> E[HLV can hoan thien:]
    E --> F["- Gioi thieu (min 50 ky tu)
    - Gia/gio
    - It nhat 1 dia diem day"]
```

### 2. Khong tim thay HLV

```mermaid
flowchart TD
    A[Tim kiem HLV] --> B{Ket qua?}
    B -->|Khong co| C[Hien thi thong bao]
    C --> D["Khong tim thay HLV trong khu vuc cua ban
    Goi y:
    - Mo rong pham vi tim kiem
    - Thay doi bo loc"]
```

---

## Acceptance Criteria

### HLV
- [ ] HLV co the tao ho so voi: Gioi thieu, Kinh nghiem, Chuyen mon, Gia/gio, Dia diem day
- [ ] HLV co the tai len video/hinh anh minh hoa
- [ ] HLV co the thiet lap lich trinh day

### Nguoi choi
- [ ] Nguoi choi co the tim HLV theo vi tri
- [ ] Nguoi choi co the xem chi tiet ho so HLV

---

## Ghi chu Thiet ke

1. **Validation ho so**: HLV can hoan thien ho so truoc khi hien thi trong tim kiem
2. **Media optimization**: Nen video/anh truoc khi upload
3. **Cache**: Cache danh sach HLV, refresh khi thay doi vi tri hoac bo loc
4. **Map clustering**: Nhom cac HLV gan nhau khi zoom out

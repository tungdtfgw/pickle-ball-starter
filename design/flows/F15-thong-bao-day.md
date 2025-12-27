# F15: Thong bao Day - Activity Diagram

## Mo ta Tinh nang

He thong gui thong bao day cho cac su kien quan trong: ghep doi, tin nhan, dat san, nhac lich.

## Phu thuoc

- F01: Dang ky va Xac thuc Nguoi dung

---

## Cac Loai Thong bao

| Ma | Loai | Nguoi nhan | Su kien kich hoat | Uu tien |
|----|------|------------|-------------------|---------|
| N01 | GHEP_DOI_MOI | Nguoi choi/HLV | 2 nguoi ghep doi thanh cong | Cao |
| N02 | TIN_NHAN_MOI | Tat ca | Nhan tin nhan moi | Cao |
| N03 | DAT_SAN_MOI | Chu san | Co yeu cau dat san moi | Cao |
| N04 | DAT_SAN_XAC_NHAN | Nguoi choi | Dat san duoc xac nhan | Cao |
| N05 | DAT_SAN_TU_CHOI | Nguoi choi | Dat san bi tu choi | Cao |
| N06 | NHAC_LICH_DANH | Nguoi choi | 1 gio truoc gio danh | Trung binh |
| N07 | DONG_DOI_HUY | Nguoi choi | Dong doi huy ket doi | Cao |

---

## Activity Diagram - Gui Thong bao

```mermaid
flowchart TD
    Start([Su kien xay ra]) --> A{Loai su kien?}

    A -->|Ghep doi moi| B[Tao thong bao N01]
    A -->|Tin nhan moi| C[Tao thong bao N02]
    A -->|Dat san moi| D[Tao thong bao N03]
    A -->|Xac nhan dat san| E[Tao thong bao N04]
    A -->|Tu choi dat san| F[Tao thong bao N05]
    A -->|Nhac lich danh| G[Tao thong bao N06]
    A -->|Dong doi huy| H[Tao thong bao N07]

    B --> I[Xac dinh nguoi nhan]
    C --> I
    D --> I
    E --> I
    F --> I
    G --> I
    H --> I

    I --> J{Nguoi nhan da bat thong bao loai nay?}
    J -->|Khong| K[Khong gui push notification]
    J -->|Co| L[Tiep tuc xu ly]

    L --> M[Luu thong bao vao database]

    M --> N{Nguoi nhan dang online trong app?}
    N -->|Co| O[Gui thong bao qua WebSocket]
    N -->|Khong| P[Gui Push Notification]

    O --> Q[Cap nhat badge trong app]
    Q --> R[Hien thi thong bao in-app]

    P --> S{Nen tang?}
    S -->|iOS| T[Gui qua APNs]
    S -->|Android| U[Gui qua FCM]

    T --> V[Hien thi notification tren thiet bi]
    U --> V

    V --> W[Nguoi dung tuong tac voi notification]
    W --> X{Hanh dong?}
    X -->|Tap| Y[Mo app va di den man hinh lien quan]
    X -->|Bo qua| Z[Dismiss notification]
    X -->|Swipe actions| AA[Thuc hien quick action]

    K --> End1([Ket thuc - Khong gui])
    R --> End2([Ket thuc - Da gui in-app])
    Y --> End3([Ket thuc - Da mo app])
    Z --> End4([Ket thuc - Da dismiss])
    AA --> End5([Ket thuc - Da xu ly quick action])
```

---

## Activity Diagram - Nguoi dung Quan ly Thong bao

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi dung mo Cai dat > Thong bao]

    A --> B[Hien thi danh sach cac loai thong bao]

    B --> C["Danh sach:
    - Ghep doi moi: [Toggle]
    - Tin nhan moi: [Toggle]
    - Dat san moi: [Toggle] (chi Chu san)
    - Trang thai dat san: [Toggle] (chi Nguoi choi)
    - Nhac lich danh: [Toggle]"]

    C --> D[Nguoi dung tap vao toggle]

    D --> E{Toggle nao?}

    E --> F[Cap nhat trang thai trong Cai dat]
    F --> G[Gui cap nhat len server]

    G --> H{Cap nhat thanh cong?}
    H -->|Co| I[Luu trang thai moi]
    H -->|Loi| J[Khoi phuc trang thai cu]
    J --> K[Hien thi loi]

    I --> L[Hien thi thong bao: Da cap nhat]

    L --> End([Ket thuc])
    K --> End
```

---

## Activity Diagram - Nhan Thong bao trong App

```mermaid
flowchart TD
    Start([Thong bao moi den]) --> A{App dang o foreground?}

    A -->|Co| B[Nhan qua WebSocket]
    A -->|Khong| C[Nhan qua Push Notification]

    B --> D{Nguoi dung dang o man hinh lien quan?}
    D -->|Co - VD: dang o Chat| E[Khong hien thi banner]
    D -->|Khong| F[Hien thi in-app notification banner]

    E --> G[Chi cap nhat du lieu]

    F --> H["Banner hien thi 3 giay:
    - Icon loai thong bao
    - Tieu de
    - Noi dung tom tat
    - Thoi gian"]

    H --> I{Nguoi dung tap banner?}
    I -->|Co| J[Di den man hinh lien quan]
    I -->|Khong| K[Banner tu dong an]

    C --> L[Hien thi system notification]
    L --> M{Nguoi dung tap?}
    M -->|Co| N[Mo app va di den man hinh]
    M -->|Khong| O[Notification nam trong tray]

    G --> P[Cap nhat badge cac tab]
    J --> P
    K --> P
    N --> P
    O --> P

    P --> End([Ket thuc])
```

---

## Chi tiet Noi dung Thong bao

### N01: Ghep doi Moi

```mermaid
flowchart LR
    A["Tieu de: Ghep doi thanh cong!
    Noi dung: Ban va [Ten] da ghep doi. Bat dau tro chuyen!
    Action: Mo man hinh Chat voi nguoi do"]
```

### N02: Tin nhan Moi

```mermaid
flowchart LR
    A["Tieu de: [Ten nguoi gui]
    Noi dung: [Preview tin nhan - max 50 ky tu]
    Action: Mo man hinh Chat"]
```

### N03: Dat san Moi (Chu san)

```mermaid
flowchart LR
    A["Tieu de: Yeu cau dat san moi
    Noi dung: [Ten nguoi dat] muon dat [Ten san con] luc [Gio]
    Action: Mo man hinh Quan ly Dat san"]
```

### N04: Dat san Xac nhan

```mermaid
flowchart LR
    A["Tieu de: Dat san thanh cong!
    Noi dung: Dat san [Ten san] luc [Gio] ngay [Ngay] da duoc xac nhan
    Action: Mo man hinh Chi tiet Dat san"]
```

### N05: Dat san Tu choi

```mermaid
flowchart LR
    A["Tieu de: Dat san bi tu choi
    Noi dung: Yeu cau dat san [Ten san] da bi tu choi. Ly do: [Ly do]
    Action: Mo man hinh Chi tiet Dat san"]
```

### N06: Nhac Lich danh

```mermaid
flowchart LR
    A["Tieu de: Sap den gio choi!
    Noi dung: 1 gio nua ban co lich danh tai [Ten san] luc [Gio]
    Action: Mo man hinh Chi tiet Dat san"]
```

### N07: Dong doi Huy

```mermaid
flowchart LR
    A["Tieu de: Thay doi dong doi
    Noi dung: [Ten] da huy ket doi voi ban
    Action: Mo man hinh Tim Ban choi"]
```

---

## Luong Scheduler - Nhac Lich danh

```mermaid
flowchart TD
    Start([Moi 15 phut]) --> A[Scheduler chay job kiem tra]

    A --> B[Query dat san trong 60-75 phut toi]
    B --> C{Co dat san nao?}

    C -->|Khong| D[Ket thuc job]
    C -->|Co| E[Lap qua tung dat san]

    E --> F{Da gui nhac chua?}
    F -->|Da gui| G[Bo qua]
    F -->|Chua| H[Tao thong bao N06]

    H --> I[Gui thong bao cho nguoi dat]
    I --> J[Danh dau da gui nhac]

    G --> K{Con dat san khac?}
    J --> K
    K -->|Co| E
    K -->|Khong| D

    D --> End([Ket thuc])
```

---

## Truong hop Dac biet

### 1. Nguoi dung tat thong bao

```mermaid
flowchart TD
    A[Su kien xay ra] --> B{Nguoi dung bat thong bao loai nay?}
    B -->|Khong| C[Khong gui push notification]
    C --> D[Van luu vao lich su thong bao trong app]
    D --> E[Nguoi dung co the xem trong Thong bao tab]
```

### 2. Gui nhieu thong bao cung luc

```mermaid
flowchart TD
    A[Nhieu su kien cung luc] --> B{Cung nguoi nhan?}
    B -->|Co| C[Nhom thong bao]
    C --> D["VD: Ban co 3 tin nhan moi"]

    B -->|Khong| E[Gui rieng tung thong bao]
```

### 3. App bi kill/Thiet bi tat

```mermaid
flowchart TD
    A[Thong bao den] --> B{App state?}
    B -->|Killed| C[Hien thi system notification]
    B -->|Background| C
    B -->|Foreground| D[Hien thi in-app banner]

    C --> E[Nguoi dung tap]
    E --> F[Cold start app]
    F --> G[Di den man hinh lien quan]
```

---

## Cau truc Du lieu Thong bao

```mermaid
erDiagram
    NOTIFICATION {
        string id PK
        string user_id FK
        string type
        string title
        string body
        json data
        boolean is_read
        datetime created_at
    }

    NOTIFICATION_SETTINGS {
        string user_id PK
        boolean ghep_doi_moi
        boolean tin_nhan_moi
        boolean dat_san_moi
        boolean dat_san_trang_thai
        boolean nhac_lich_danh
    }
```

---

## Acceptance Criteria

- [ ] Thong bao khi co ghep doi moi
- [ ] Thong bao khi co tin nhan moi
- [ ] Thong bao khi co yeu cau dat san moi (cho chu san)
- [ ] Thong bao khi dat san duoc xac nhan/tu choi (cho nguoi choi)
- [ ] Thong bao nhac lich danh truoc 1 gio
- [ ] Nguoi dung co the bat/tat tung loai thong bao trong Cai dat

---

## Ghi chu Ky thuat

1. **APNs/FCM**: Dung Firebase Cloud Messaging cho Android, APNs cho iOS
2. **Token management**: Luu device token khi dang nhap, xoa khi dang xuat
3. **Background processing**: Su dung background service de xu ly notification
4. **Deep linking**: Su dung deep link de navigate den man hinh cu the
5. **Rate limiting**: Gioi han so notification/phut de tranh spam
6. **Batching**: Gop nhieu thong bao cung loai thanh 1 (VD: 5 tin nhan moi)

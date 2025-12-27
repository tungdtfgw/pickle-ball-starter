# F11: Ghep doi Nguoi choi - Tim Doi Thi dau (Doi vs Doi) - Activity Diagram

## Mo ta Tinh nang

Sau khi co dong doi (F10), doi co the tim doi thu khac de danh doi. Tuong tu F09 nhung ghep doi giua 2 doi.

## Phu thuoc

- F02: Quan ly Ho so Nguoi dung
- F10: Ghep doi Nguoi choi - Tim Ban choi (phai co dong doi)
- F07: Dat San (sau khi ghep doi thanh cong)

---

## Activity Diagram Chinh

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi choi mo tab Tim Doi Thi dau]

    A --> B{Nguoi choi da co dong doi?}
    B -->|Chua| C[Hien thi thong bao]
    C --> D["Noi dung: Ban can co dong doi truoc khi tim doi thi dau
    Nut: Tim dong doi ngay"]
    D --> E[Chuyen den F10 - Tim Ban choi]
    E --> End1([Ket thuc - Chuyen den F10])

    B -->|Co| F[Hien thi thong tin doi cua minh]
    F --> G["Thong tin doi:
    - Anh 2 nguoi
    - Ten doi (hoac Ten 2 nguoi)
    - Trinh do trung binh"]

    G --> H[Goi API lay danh sach doi phu hop]

    H --> I{API tra ve ket qua?}
    I -->|Loi| J[Hien thi loi ket noi]
    J --> K[Nut: Thu lai]
    K --> H

    I -->|Thanh cong| L{Co doi phu hop?}
    L -->|Khong| M[Hien thi: Hien tai khong co doi phu hop]
    M --> N[Goi y: Thu lai sau hoac mo rong lich trinh]
    N --> End2([Ket thuc])

    L -->|Co| O[Hien thi the doi dau tien]

    O --> P["Thong tin tren the doi:
    - Anh 2 nguoi cua doi
    - Ten doi / Ten 2 nguoi
    - Trinh do trung binh
    - Khoang cach trung binh
    - So khung gio trung"]

    P --> Q[Nguoi choi thuc hien swipe]

    Q --> R{Thao tac?}
    R -->|Swipe trai| S[Bo qua doi nay]
    R -->|Swipe phai| T[Thich doi nay]
    R -->|Tap the| U[Xem chi tiet doi]

    S --> V[Luu vao lich su]
    V --> W{Con doi khac?}
    W -->|Co| O
    W -->|Khong| X[Het goi y]
    X --> End3([Ket thuc])

    T --> Y[Gui Thich den server]
    Y --> Z{Doi kia da Thich doi minh?}
    Z -->|Chua| V

    Z -->|Da Thich - MATCH| AA[Ghep doi thanh cong!]
    AA --> AB["Hien thi animation:
    - 4 nguoi (2 doi)
    - Chuc mung! Da tim duoc doi thu!"]

    AB --> AC[Tinh toan khung gio trung cua 4 nguoi]
    AC --> AD{So khung gio trung?}

    AD -->|Khong co khung gio trung| AE["Thong bao:
    Hien tai lich cua 2 doi khong trung khop
    Hay chat de thoa thuan lich"]
    AE --> AF[Chuyen den Chat nhom]

    AD -->|Dung 1 khung gio| AG[Hien thi khung gio trung]
    AG --> AH[Nut: Dat san ngay / Chat truoc]

    AD -->|Nhieu khung gio| AI[Hien thi danh sach khung gio]
    AI --> AJ[Chon 1 khung gio]
    AJ --> AH

    AH --> AK{Chon?}
    AK -->|Dat san| AL[Chuyen den man hinh Dat san]
    AK -->|Chat| AM[Chuyen den Chat nhom 4 nguoi]
    AK -->|Dong| AN[Dong, tiep tuc swipe]
    AN --> W

    AL --> End4([Ket thuc - Dat san])
    AM --> End5([Ket thuc - Chat])
    AF --> End6([Ket thuc - Chat])

    U --> AO["Hien thi chi tiet doi:
    Nguoi 1:
    - Anh, Ten, Tuoi, Trinh do
    Nguoi 2:
    - Anh, Ten, Tuoi, Trinh do
    Thong tin chung:
    - Trinh do doi (trung binh)
    - Lich trung voi doi minh"]

    AO --> AP[Nut: Thich / Bo qua / Dong]
    AP --> AQ{Chon?}
    AQ -->|Thich| T
    AQ -->|Bo qua| S
    AQ -->|Dong| Q
```

---

## Thuat toan Goi y Doi Thi dau

```mermaid
flowchart TD
    A[Lay danh sach cac doi] --> B[Loc doi con hoat dong]
    B --> C["Loai doi da swipe"]

    C --> D["Tinh lich trinh doi minh:
    Giao cua lich A va lich B"]

    D --> E["Voi moi doi khac:
    Tinh lich trinh doi ho (giao C va D)"]

    E --> F["Tim khung gio trung:
    Giao cua (lich doi minh) va (lich doi ho)"]

    F --> G{Co khung gio trung?}
    G -->|Khong| H[Loai khoi danh sach goi y]
    G -->|Co| I[Tinh diem uu tien]

    I --> J["Diem =
    (So khung trung x 40) +
    (Khoang cach gan x 30) +
    (Trinh do tuong duong x 30)"]

    J --> K[Sap xep theo diem]
    K --> L[Tra ve danh sach goi y]
```

### Tinh Trinh do Doi

```mermaid
flowchart LR
    A["Trinh do nguoi 1: L1
    Trinh do nguoi 2: L2"] --> B["Trinh do doi = (L1 + L2) / 2"]

    B --> C["VD: Nguoi 1: 3, Nguoi 2: 4
    Trinh do doi = 3.5"]
```

### Tinh Khoang cach Doi

```mermaid
flowchart LR
    A["Vi tri nguoi 1: P1
    Vi tri nguoi 2: P2"] --> B["Diem trung tam doi = (P1 + P2) / 2"]

    B --> C["Khoang cach giua 2 doi =
    Distance(Trung tam doi A, Trung tam doi B)"]
```

---

## Xu ly Thong bao Ghep doi

```mermaid
flowchart TD
    A[Doi 1 swipe phai Doi 2] --> B{Doi 2 da swipe phai Doi 1?}

    B -->|Chua| C[Luu cho xu ly sau]
    C --> D[Khong thong bao]

    B -->|Da swipe - Match!| E[Tao ban ghi Ghep doi Doi vs Doi]
    E --> F[Tinh khung gio trung cua 4 nguoi]
    F --> G[Luu vao Ghep doi]

    G --> H[Gui push notification cho CA 4 NGUOI]
    H --> I["Noi dung:
    Doi cua ban da tim duoc doi thu!
    [Ten Doi 2]
    Tap de xem chi tiet"]
```

---

## Giao dien The Doi

```
+----------------------------------+
|  [Avatar A]     [Avatar B]       |
|      \             /             |
|       \           /              |
|        [Ten Doi]                 |
+----------------------------------+
|  ★★★★☆ Trinh do 3.5              |
|  📍 5 km                         |
|  🕐 2 khung gio chung            |
+----------------------------------+
|                                  |
|   [X Bo qua]    [❤ Thich]       |
|                                  |
+----------------------------------+
```

---

## Truong hop Dac biet

### 1. Mot nguoi trong doi khong ranh khung gio da chon

```mermaid
flowchart TD
    A[Ghep doi thanh cong] --> B[Hien thi khung gio trung]
    B --> C[4 nguoi thao luan trong chat]
    C --> D{Moi nguoi dong y khung gio?}
    D -->|Co| E[Dat san]
    D -->|Khong| F[Tiep tuc thao luan hoac huy]
```

### 2. Dong doi huy ket doi giua chung

```mermaid
flowchart TD
    A[Doi A dang swipe] --> B[Nguoi trong Doi A huy ket doi]
    B --> C[He thong thong bao]
    C --> D["Thong bao cho nguoi con lai:
    Dong doi da huy ket doi"]

    D --> E[Tu dong thoat khoi F11]
    E --> F[Chuyen ve trang thai khong co dong doi]

    F --> G{Co ghep doi dang cho xu ly?}
    G -->|Co| H[Thong bao cho doi kia]
    H --> I["Doi [Ten] da huy
    Match bi huy"]
    G -->|Khong| J[Ket thuc]
```

### 3. Chat nhom 4 nguoi

```mermaid
flowchart TD
    A[Ghep doi thanh cong] --> B[Tao phong chat nhom]
    B --> C["Thanh vien:
    - Nguoi 1 Doi A
    - Nguoi 2 Doi A
    - Nguoi 1 Doi B
    - Nguoi 2 Doi B"]

    C --> D[Ca 4 nguoi co the chat]
    D --> E[Thoa thuan lich va san]
    E --> F[Bat ky ai cung co the dat san]
```

---

## Luong Trang thai Ghep doi Doi vs Doi

```mermaid
stateDiagram-v2
    [*] --> ChuaCoDoiThu: Co dong doi

    ChuaCoDoiThu --> DangTimDoiThu: Bat dau swipe
    DangTimDoiThu --> DaGhepDoi: Match thanh cong
    DangTimDoiThu --> ChuaCoDoiThu: Het goi y

    DaGhepDoi --> DaDatSan: Dat san thanh cong
    DaGhepDoi --> ChuaCoDoiThu: Match het han/Huy

    DaDatSan --> HoanTat: Choi xong

    note right of DaGhepDoi: 4 nguoi co the chat\nva thoa thuan lich
```

---

## Acceptance Criteria

- [ ] Chi kha dung khi nguoi choi da co dong doi
- [ ] Hien thi the ho so cua doi: Anh dai dien 2 nguoi, Ten doi/Ten 2 nguoi, Trinh do trung binh
- [ ] Swipe de tim doi thu
- [ ] Khi ghep doi:
  - Neu trung 1 khung gio -> Dat san
  - Neu trung nhieu khung gio -> Chon khung gio roi dat san
- [ ] Ca 4 nguoi deu nhan thong bao khi ghep doi

---

## Ghi chu Thiet ke

1. **Dong bo lich**: Lich doi = Giao lich cua 2 thanh vien
2. **Chat nhom**: Sau khi match, tao chat nhom 4 nguoi tu dong
3. **Quyen dat san**: Bat ky ai trong 4 nguoi cung co the dat san
4. **Huy match**: Neu 1 nguoi huy ket doi, match voi doi kia cung bi huy
5. **Thong bao**: Gui thong bao cho ca 4 nguoi cung luc

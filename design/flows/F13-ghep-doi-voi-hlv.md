# F13: Ghep doi voi HLV - Activity Diagram

## Mo ta Tinh nang

Nguoi choi tim HLV bang cach swipe. Khi ghep doi, ca 2 co the chat de sap xep lich hoc.

## Phu thuoc

- F12: Ho so HLV va Tim kiem (HLV phai co ho so)
- F02: Quan ly Ho so Nguoi dung

---

## Activity Diagram - Nguoi choi Tim HLV (Swipe)

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Nguoi choi mo tab Tim HLV]

    A --> B{Che do xem?}
    B -->|Danh sach/Ban do| C[Chuyen sang F12 - Tim kiem HLV]
    B -->|Swipe| D[Che do swipe tim HLV]

    D --> E[Goi API lay danh sach HLV goi y]

    E --> F{API tra ve?}
    F -->|Loi| G[Hien thi loi ket noi]
    G --> H[Nut: Thu lai]
    H --> E

    F -->|Thanh cong| I{Co HLV phu hop?}
    I -->|Khong| J[Hien thi: Khong tim thay HLV gan ban]
    J --> K[Goi y mo rong pham vi hoac doi]
    K --> End1([Ket thuc])

    I -->|Co| L[Hien thi the HLV dau tien]

    L --> M["Thong tin tren the:
    - Anh dai dien (lon)
    - Ten
    - So nam kinh nghiem
    - Chuyen mon (tags)
    - Gia/gio
    - Khoang cach
    - Preview video/anh (optional)"]

    M --> N[Nguoi choi thao tac]

    N --> O{Thao tac?}
    O -->|Swipe trai| P[Bo qua HLV nay]
    O -->|Swipe phai| Q[Quan tam HLV nay]
    O -->|Tap the| R[Xem chi tiet ho so]

    P --> S[Luu vao lich su]
    S --> T{Con HLV khac?}
    T -->|Co| L
    T -->|Khong| U[Het goi y]
    U --> End2([Ket thuc])

    Q --> V[Gui thong tin Quan tam den server]
    V --> W{HLV da Thich nguoi choi nay?}
    W -->|Chua| X[Luu cho xu ly sau]
    X --> S

    W -->|Da Thich - MATCH| Y[Ghep doi thanh cong!]
    Y --> Z["Hien thi animation:
    - Anh nguoi choi va HLV
    - Chuc mung! Ban va [Ten HLV] da ket noi"]

    Z --> AA["Tuy chon:
    - Chat ngay
    - Dong, tiep tuc swipe"]

    AA --> AB{Chon?}
    AB -->|Chat| AC[Mo man hinh Chat voi HLV]
    AB -->|Dong| T

    AC --> End3([Ket thuc - Chat])

    R --> AD["Chi tiet ho so HLV:
    - Tat ca thong tin tu F12
    - Nut: Quan tam / Bo qua"]
    AD --> AE{Chon?}
    AE -->|Quan tam| Q
    AE -->|Bo qua| P
    AE -->|Dong| N
```

---

## Activity Diagram - HLV Tim Hoc vien (Swipe)

```mermaid
flowchart TD
    Start([Bat dau]) --> A[HLV mo tab Tim Hoc vien]

    A --> B[Goi API lay danh sach nguoi choi quan tam]

    B --> C{API tra ve?}
    C -->|Loi| D[Hien thi loi]
    D --> E[Nut: Thu lai]
    E --> B

    C -->|Thanh cong| F{Co nguoi choi quan tam?}
    F -->|Khong| G["Hien thi: Chua co nguoi choi nao quan tam den ban
    Goi y: Hoan thien ho so de thu hut hoc vien"]
    G --> End1([Ket thuc])

    F -->|Co| H[Hien thi the nguoi choi]

    H --> I["Thong tin:
    - Anh dai dien
    - Ten, Tuoi
    - Trinh do hien tai
    - Khoang cach
    - Muc tieu hoc (neu co)"]

    I --> J[HLV thao tac]

    J --> K{Thao tac?}
    K -->|Swipe trai| L[Bo qua nguoi nay]
    K -->|Swipe phai| M[Chap nhan nguoi nay]
    K -->|Tap the| N[Xem chi tiet ho so]

    L --> O[Luu vao lich su]
    O --> P{Con nguoi khac?}
    P -->|Co| H
    P -->|Khong| Q[Het danh sach]
    Q --> End2([Ket thuc])

    M --> R[Ghep doi thanh cong!]
    R --> S["Hien thi:
    - Animation ket noi
    - Chat de trao doi lich hoc"]

    S --> T{HLV chon?}
    T -->|Chat ngay| U[Mo man hinh Chat]
    T -->|Dong| P

    U --> End3([Ket thuc - Chat])

    N --> V[Xem chi tiet ho so nguoi choi]
    V --> W{Chon?}
    W -->|Chap nhan| M
    W -->|Bo qua| L
    W -->|Dong| J
```

---

## Thuat toan Goi y HLV cho Nguoi choi

```mermaid
flowchart TD
    A[Lay danh sach HLV] --> B[Loc HLV co ho so hoan thien]
    B --> C[Loc theo khoang cach]

    C --> D["Tieu chi sap xep:
    1. Khoang cach (trong ban kinh 15km)
    2. Muc gia phu hop (neu co preference)
    3. Chuyen mon phu hop (neu nguoi choi co nhu cau)"]

    D --> E[Loai HLV da swipe]
    E --> F[Tra ve danh sach]
```

---

## Luong Ghep doi HLV - Nguoi choi

```mermaid
sequenceDiagram
    participant NC as Nguoi choi
    participant SV as Server
    participant HLV as HLV

    NC->>SV: Swipe phai (Quan tam HLV X)
    SV->>SV: Luu: NC quan tam HLV X
    SV->>HLV: Push: Co nguoi quan tam den ban

    HLV->>SV: Mo tab Tim Hoc vien
    SV->>HLV: Tra ve danh sach nguoi quan tam (co NC)

    HLV->>SV: Swipe phai (Chap nhan NC)
    SV->>SV: Tao Match
    SV->>NC: Push: Ban va HLV X da ket noi!
    SV->>HLV: Hien thi Match thanh cong

    Note over NC,HLV: Ca 2 co the chat tu do
```

---

## Khac biet voi F09 (Tim Doi thu)

| Tieu chi | F09 - Tim Doi thu | F13 - Tim HLV |
|----------|-------------------|---------------|
| Doi tuong swipe | Nguoi choi <-> Nguoi choi | Nguoi choi -> HLV |
| Hai chieu | Ca 2 swipe nhau | NC swipe truoc, HLV xem va chap nhan |
| Sau match | Dat san | Chat de thoa thuan |
| Lich trinh | Tu dong matching | Tu thoa thuan |
| Muc tieu | Thi dau | Hoc |

---

## Truong hop Dac biet

### 1. HLV khong phan hoi sau khi ghep doi

```mermaid
flowchart TD
    A[Ghep doi thanh cong] --> B[Nguoi choi gui tin nhan]
    B --> C{HLV phan hoi?}
    C -->|Co| D[Tiep tuc chat binh thuong]
    C -->|Khong sau 7 ngay| E[Hien thi goi y cho nguoi choi]
    E --> F["HLV nay chua phan hoi
    Ban co the:
    - Cho them
    - Tim HLV khac"]
```

### 2. HLV muon tu choi sau khi da match

```mermaid
flowchart TD
    A[Da match voi nguoi choi] --> B[HLV muon huy]
    B --> C[HLV co the block/report]
    C --> D[Match bi vo hieu hoa]
    D --> E[Nguoi choi khong the lien lac nua]
```

---

## Giao dien The HLV

```
+----------------------------------+
|                                  |
|        [Anh dai dien HLV]        |
|                                  |
+----------------------------------+
|  Nguyen Van A                    |
|  ⏱ 5 nam kinh nghiem            |
|  📍 3.2 km                       |
|  💰 300,000 VND/gio              |
+----------------------------------+
|  #Ky thuat  #Chien thuat        |
+----------------------------------+
|                                  |
|   [X Bo qua]    [❤ Quan tam]    |
|                                  |
+----------------------------------+
```

---

## Acceptance Criteria

- [ ] Hien thi the HLV voi: Anh dai dien, Ten, Kinh nghiem, Gia/gio, Khoang cach
- [ ] Swipe phai = Quan tam, Swipe trai = Bo qua
- [ ] Ghep doi khi ca Nguoi choi va HLV cung Thich nhau
- [ ] Sau khi ghep doi, mo khoa chat de trao doi chi tiet
- [ ] Khong tu dong dat san (tu thoa thuan)

---

## Ghi chu Thiet ke

1. **Uu tien HLV**: HLV la ben cung cap dich vu, nen HLV co quyen xem ai quan tam truoc
2. **Khong ep dat san**: Nguoi choi va HLV tu thoa thuan lich hoc qua chat
3. **Profile match**: Hien thi thong tin phu hop (trinh do nguoi choi, chuyen mon HLV)
4. **Notification**: Thong bao cho HLV khi co nguoi quan tam moi

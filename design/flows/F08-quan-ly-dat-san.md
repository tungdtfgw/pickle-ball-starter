# F08: Quan ly Dat san - Activity Diagram

## Mo ta Tinh nang

Chu san quan ly cac yeu cau dat san: xem danh sach, xac nhan hoac tu choi. Co the xem lich dat san theo ngay/tuan va loc theo san con.

## Phu thuoc

- F07: Dat San (phai co yeu cau dat san de quan ly)

---

## Activity Diagram

```mermaid
flowchart TD
    Start([Bat dau]) --> A[Chu san mo tab Quan ly Dat san]

    A --> B{Co thong bao dat san moi?}
    B -->|Co| C[Hien thi badge so luong moi]
    B -->|Khong| D[Hien thi danh sach dat san]
    C --> D

    D --> E[Chu san chon che do xem]

    E --> F{Che do xem?}
    F -->|Danh sach| G[Hien thi danh sach theo trang thai]
    F -->|Lich| H[Hien thi dang lich ngay/tuan]

    %% Nhanh Danh sach
    G --> I[Chu san chon bo loc trang thai]
    I --> J{Trang thai nao?}
    J -->|Cho xac nhan| K[Loc chi hien thi Cho xac nhan]
    J -->|Da xac nhan| L[Loc chi hien thi Da xac nhan]
    J -->|Tat ca| M[Hien thi tat ca trang thai]

    K --> N[Chu san co the loc theo san con]
    L --> N
    M --> N

    N --> O{Loc theo san con?}
    O -->|Co| P[Chon san con tu dropdown]
    O -->|Khong| Q[Giu nguyen danh sach]
    P --> Q

    %% Nhanh Lich
    H --> R[Hien thi lich voi cac slot da dat]
    R --> S[Moi slot hien thi mau theo trang thai]
    S --> T[Chu san co the chuyen ngay/tuan]
    T --> Q

    Q --> U[Chu san chon 1 dat san de xem chi tiet]

    U --> V[Hien thi chi tiet dat san]
    V --> W["Thong tin hien thi:
    - Thong tin nguoi dat (Ten, SDT, Avatar)
    - San con
    - Khung gio va ngay
    - Ghi chu cua nguoi dat
    - Trang thai hien tai
    - Thoi gian tao yeu cau"]

    W --> X{Trang thai hien tai?}

    X -->|Cho xac nhan| Y[Hien thi 2 nut: Xac nhan / Tu choi]
    X -->|Da xac nhan| Z[Hien thi thong tin - Khong co action]
    X -->|Bi tu choi| AA[Hien thi thong tin va ly do tu choi]
    X -->|Da huy| AB[Hien thi thong tin - Da huy boi nguoi dat]

    Y --> AC{Chu san chon action?}
    AC -->|Xac nhan| AD[Hien thi xac nhan: Ban co chac muon xac nhan?]
    AC -->|Tu choi| AE[Hien thi form nhap ly do tu choi]
    AC -->|Quay lai| Q

    AD --> AF{Xac nhan?}
    AF -->|Co| AG[Gui request xac nhan den server]
    AF -->|Khong| Y

    AG --> AH{Server xu ly thanh cong?}
    AH -->|Co| AI[Cap nhat trang thai thanh Da xac nhan]
    AH -->|Khong| AJ[Hien thi loi: Khong the xac nhan]

    AI --> AK[Gui thong bao den nguoi dat]
    AK --> AL[Cap nhat khung gio - Da co nguoi dat]
    AL --> AM[Hien thi thong bao thanh cong]
    AM --> End([Ket thuc])

    AJ --> AN{Ly do loi?}
    AN -->|Khung gio da duoc dat| AO[Hien thi: Khung gio nay da co nguoi dat khac]
    AN -->|Loi mang| AP[Hien thi: Loi ket noi, vui long thu lai]
    AN -->|Loi khac| AQ[Hien thi: Da xay ra loi, vui long thu lai]
    AO --> Y
    AP --> Y
    AQ --> Y

    %% Nhanh Tu choi
    AE --> AR[Chu san nhap ly do tu choi]
    AR --> AS{Ly do hop le?}
    AS -->|Khong - Trong| AT[Hien thi: Vui long nhap ly do tu choi]
    AS -->|Co| AU[Gui request tu choi den server]
    AT --> AE

    AU --> AV{Server xu ly thanh cong?}
    AV -->|Co| AW[Cap nhat trang thai thanh Bi tu choi]
    AV -->|Khong| AX[Hien thi loi]

    AW --> AY[Gui thong bao tu choi den nguoi dat kem ly do]
    AY --> AZ[Hien thi thong bao: Da tu choi dat san]
    AZ --> End

    AX --> AE

    Z --> BA{Chu san muon lam gi?}
    BA -->|Xem thong tin nguoi dat| BB[Mo ho so nguoi dat]
    BA -->|Quay lai| Q
    BB --> Q

    AA --> Q
    AB --> Q
```

---

## Cac Truong hop Dac biet

### 1. Nhieu dat san cho cung khung gio

```mermaid
flowchart TD
    A[2+ yeu cau cho cung khung gio] --> B[Chu san xem danh sach cho xac nhan]
    B --> C[Highlight cac yeu cau xung dot]
    C --> D[Chu san chon 1 yeu cau de xac nhan]
    D --> E[He thong xac nhan yeu cau nay]
    E --> F[Tu dong tu choi cac yeu cau khac]
    F --> G["Gui thong bao tu choi voi ly do:
    Khung gio da duoc nguoi khac dat truoc"]
```

### 2. Chu san khong truc tuyen

```mermaid
flowchart TD
    A[Yeu cau dat san moi] --> B{Chu san online?}
    B -->|Khong| C[Yeu cau o trang thai Cho xac nhan]
    C --> D[Luu vao danh sach cho xu ly]
    D --> E[Gui push notification cho chu san]
    E --> F{Chu san mo app?}
    F -->|Co| G[Hien thi danh sach cho xu ly]
    F -->|Chua| H[Tiep tuc cho]
    H --> I{Qua thoi gian X gio?}
    I -->|Khong| F
    I -->|Co - Could have| J[Tu dong huy yeu cau]
    J --> K[Thong bao cho nguoi dat]
```

### 3. Xem lich dat san dang Calendar

```mermaid
flowchart TD
    A[Che do xem Lich] --> B[Hien thi lich theo ngay/tuan]
    B --> C[Moi khung gio la 1 o trong lich]

    C --> D[Ma mau trang thai:]
    D --> E["Xanh la: Da xac nhan
    Vang: Cho xac nhan
    Xam: Trong
    Do: Da huy/Tu choi"]

    E --> F[Chu san tap vao 1 slot]
    F --> G{Slot co dat san?}
    G -->|Co| H[Mo chi tiet dat san]
    G -->|Khong| I[Khong co action]

    H --> J[Thuc hien Xac nhan/Tu choi]
```

---

## Luu do Trang thai Dat san (Tu goc nhin Chu san)

```mermaid
stateDiagram-v2
    [*] --> ChoXacNhan: Nguoi choi dat san

    ChoXacNhan --> DaXacNhan: Chu san Xac nhan
    ChoXacNhan --> BiTuChoi: Chu san Tu choi
    ChoXacNhan --> DaHuy: Nguoi choi Huy

    DaXacNhan --> [*]: Hoan tat
    BiTuChoi --> [*]: Ket thuc
    DaHuy --> [*]: Ket thuc
```

---

## Ghi chu Thiet ke

1. **Hien thi trang thai ro rang**: Mau sac va icon khac nhau cho moi trang thai
2. **Uu tien Cho xac nhan**: Mac dinh hien thi danh sach Cho xac nhan truoc
3. **Thong bao real-time**: Khi co yeu cau moi, hien thi badge va push notification
4. **Ly do tu choi bat buoc**: Giup nguoi choi hieu ly do va co the dat lai
5. **Xung dot dong thoi**: Khi xac nhan 1 yeu cau, tu dong xu ly cac yeu cau xung dot

---

## Acceptance Criteria

- [ ] Chu san nhan thong bao khi co yeu cau dat san moi
- [ ] Hien thi danh sach dat san theo trang thai (Cho xac nhan/Da xac nhan/Tat ca)
- [ ] Chu san co the xem chi tiet dat san: Thong tin nguoi dat, San, Khung gio, Ghi chu
- [ ] Chu san co the Chap nhan hoac Tu choi dat san
- [ ] Khi tu choi, chu san co the nhap ly do
- [ ] Xem lich dat san dang Lich theo ngay/tuan
- [ ] Loc dat san theo san con

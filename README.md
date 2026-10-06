# Sea Battle — Battleship online 2 người

Game Battleship chạy trên trình duyệt. Hai người chơi kết nối trực tiếp với nhau qua mã phòng: không cần tài khoản, không cần cài đặt.

**▶ Chơi ngay:** https://silky-itt.github.io/battleship/

---

## 1. Cách mở game

### Cách 1: Chơi online (khuyên dùng)
1. Mở **https://silky-itt.github.io/battleship/** bằng Chrome, Edge, Safari hoặc Firefox, trên máy tính hay điện thoại đều được.
2. Xong. Không cần tải gì thêm.

### Cách 2: Chạy trên máy của bạn
Cần có Python 3 (macOS có sẵn).

```bash
git clone https://github.com/silky-itt/battleship.git
cd battleship
python3 -m http.server 8000
```

Sau đó mở **http://localhost:8000** trong trình duyệt.

> Không nên mở thẳng file `index.html` bằng cách nhấp đúp (đường dẫn `file://`), vì trình duyệt sẽ chặn tải file âm thanh. Hơn nữa, link mời khi đó chỉ dùng được trên chính máy của bạn.

Muốn chơi với người ở mạng khác thì dùng cách 1, hoặc tự đưa thư mục này lên một host tĩnh bất kỳ (GitHub Pages, Netlify, Cloudflare Pages…).

---

## 2. Chơi với bạn bè

**Người tạo phòng (host):**
1. Nhập tên và chọn chân dung chỉ huy.
2. Chọn **Mode** (Classic hoặc Commander) và **Map** (Open Sea, Archipelago hoặc Fjord).
3. Bấm **Create Room**. Màn hình hiện mã phòng 6 ký tự.
4. Bấm **Copy** rồi gửi link cho bạn, hoặc chỉ cần đọc mã phòng.

**Người vào phòng:**
1. Mở link mời (mã phòng sẽ tự điền), hoặc mở game rồi gõ mã vào ô **ROOM CODE**.
2. Nhập tên và bấm **Join**.

**Vào trận:**
1. Hai bên xếp hạm đội: kéo thả tàu vào bàn cờ, hoặc bấm **Random**.
2. Bấm **Ready**. Khi cả hai cùng sẵn sàng thì trận đấu bắt đầu.
3. Mỗi lần đổi lượt sẽ có băng rôn **YOUR TURN** hoặc **ENEMY TURN** chạy ngang màn hình.
4. Hết ván thì bấm **Rematch** để đấu tiếp. Tỉ số được giữ ở góc trên.

Host đóng tab thì phòng biến mất. Lần sau cần tạo phòng mới.

---

## 3. Luật chơi

- Mỗi bên có 5 tàu: **Carrier (5 ô), Battleship (4), Cruiser (3), Submarine (3), Destroyer (2)**.
- Hai bên thay phiên bắn vào vùng biển của đối phương. Chốt trắng là trượt, chốt đỏ là trúng.
- **Bắn thường mà trúng thì được bắn tiếp.** Trượt thì mất lượt.
- Ai đánh chìm toàn bộ hạm đội đối phương trước sẽ thắng.

### Chế độ
| Mode | Mô tả |
|---|---|
| **Classic** | Luật gốc như trên. |
| **Commander** | Mỗi lượt +1 ⚡, mỗi phát bắn thường trúng thêm +1 ⚡ (tối đa 10). Dùng ⚡ cho kỹ năng; dùng kỹ năng sẽ kết thúc lượt. |

### Kỹ năng (chế độ Commander)
| Kỹ năng | ⚡ | Tác dụng |
|---|---|---|
| **Fire** | 0 | Bắn 1 ô |
| **Radar** | 3 | Quét vùng 3×3, đánh dấu vòng xanh lên các ô có tàu địch |
| **Cluster Bomb** | 5 | Bắn 5 ô hình chữ thập |
| **Airstrike** | 8 | Bắn toàn bộ một hàng hoặc một cột |

### Bản đồ
| Map | Mô tả |
|---|---|
| **Open Sea** | Lưới 10×10 trống |
| **Archipelago** | Đảo rải rác; không đặt tàu hay bắn vào đảo được |
| **Fjord** | Bờ biển khúc khuỷu ở các góc |

---

## 4. Điều khiển

| Thao tác | Máy tính | Điện thoại |
|---|---|---|
| Đặt tàu | Kéo tàu thả vào bàn cờ | Kéo bằng ngón tay, hoặc chạm vào tàu trong danh sách để đặt ngẫu nhiên |
| Xoay tàu | Bấm vào tàu đã đặt, hoặc nhấn `R` khi đang kéo | Chạm vào tàu đã đặt |
| Bắn | Bấm vào ô trên vùng biển địch | Chạm vào ô |
| Dùng kỹ năng | Chọn ô hình thoi, rê chuột để xem vùng bắn, bấm để bắn | Chọn kỹ năng, chạm ô 1 lần để xem, chạm lần nữa để bắn |
| Đổi hàng/cột (Airstrike) | Nhấn `R`, chuột phải, hoặc nút ↔/↕ | Nút ↔ Row / ↕ Column |
| Huỷ kỹ năng | `Esc` hoặc nút ✕ | Nút ✕ |
| Nhạc, âm thanh, rời phòng | Nút bánh răng ⚙ | Nút bánh răng ⚙ |

---

## 5. Gặp sự cố?

| Vấn đề | Cách xử lý |
|---|---|
| "Room not found" | Kiểm tra lại mã; host phải còn mở tab. |
| Kết nối mãi không được / "Connection timed out" | Một số mạng (wifi công ty, trường học, vài mạng 4G) chặn kết nối WebRTC trực tiếp. Thử đổi mạng khác, ví dụ phát wifi từ điện thoại. |
| Báo "different game version" | Cả hai tải lại trang (`Cmd/Ctrl + Shift + R`) để cùng dùng bản mới nhất. |
| Không có tiếng | Bấm vào trang một lần (trình duyệt chỉ phát âm thanh sau thao tác đầu tiên), rồi kiểm tra ⚙ Settings. |
| Vừa cập nhật mà không thấy thay đổi | GitHub Pages mất khoảng 1 phút để cập nhật; tải lại hẳn trang bằng `Cmd/Ctrl + Shift + R`. |

---

## 6. Cấu trúc thư mục

```
battleship/
├── index.html          # Toàn bộ game (HTML + CSS + JS)
├── assets/
│   ├── sfx/            # Hiệu ứng âm thanh (.m4a)
│   └── music/          # Nhạc nền (.m4a)
└── docs/
    ├── RESEARCH.md     # Research về game, âm thanh, thiết kế các phiên bản
    └── UI-GUIDE.md     # Quy tắc giao diện: màu, font, component, chuyển động
```

- Kết nối: [PeerJS](https://peerjs.com/) (WebRTC), dùng máy chủ kết nối miễn phí của PeerJS.
- Deploy: push lên nhánh `main` là GitHub Pages tự cập nhật.

## 7. Ghi công

Âm thanh đều là **CC0 (public domain)**: Thimras ("Battle at sea"), Kenney ("Impact Sounds"), ezwa/qubodup ("6 short water splashes"), yd ("Enemy Ship Approaching"), beardalaxy ("Pirate Ship Theme Loop"). Nguồn chi tiết xem `docs/RESEARCH.md` mục 5.

Font: Lilita One và Nunito (Google Fonts, SIL Open Font License).

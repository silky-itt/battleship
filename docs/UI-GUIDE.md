# Hải Chiến — UI Guide (tông "Biển hoàng hôn")

Đây là bộ quy tắc giao diện cho mọi thay đổi UI sau này của game. Mục tiêu: **ấm, vàng, dễ đọc, không quá tối mà cũng không quá sáng**. Giao diện trong game dùng **tiếng Anh**.

Nếu sửa UI mà khác tài liệu này, hãy cập nhật tài liệu trước rồi mới sửa code.

---

## 1. Nguyên tắc (rút ra từ research)

1. **Rõ ràng trên hết.** Người chơi phải đọc được ngay mình đang ở lượt nào, còn bao nhiêu tàu, có bao nhiêu ⚡. Nếu không đọc ngay được là UI thất bại. ([virtuall.pro][virtuall])
2. **Thứ bậc thị giác.** Thông tin quan trọng đặt ở nơi mắt nhìn tới tự nhiên: bàn cờ ở giữa, chỉ huy và năng lượng ở góc trái, tàu địch ở cạnh phải. ([virtuall.pro][virtuall])
3. **Màu mang nghĩa nhất quán.** Xanh lá là tích cực, đỏ là nguy hiểm/bị trúng. Hải Chiến quy ước thêm: **vàng hổ phách = của mình / hành động chính**, **đỏ san hô = đối thủ / nguy hiểm**. ([virtuall.pro][virtuall])
4. **Không nhồi nhét.** HUD chỉ hiện thứ cần ngay lúc đó; mọi thứ khác (âm thanh, rời phòng) nằm trong Cài đặt. ([onerain HUD guide][hud])
5. **Phản hồi có chừng mực.** Hiệu ứng ngắn, không che bàn cờ, tôn trọng `prefers-reduced-motion` (xem `RESEARCH.md` mục 4).
6. **Tương phản theo WCAG 2.2 AA:** chữ thường ≥ 4.5:1, chữ lớn (≥ 18pt, hoặc ≥ 14pt đậm) ≥ 3:1, thành phần UI và đồ hoạ quan trọng ≥ 3:1 so với nền liền kề. ([WebAIM][webaim], [MDN][mdn])
7. **Hai font:** một font display to, dày cho tiêu đề và băng rôn; một font sans dễ đọc cho chữ thường và chỉ số. Đây là cách đa số game làm. ([Made Good Designs][fonts])

Nguồn tham khảo hình ảnh nên dùng khi muốn tìm ý tưởng: [Game UI Database][gameuidb], một thư viện hơn 55.000 màn hình UI game có lọc theo màu và loại màn hình. ([AlternativeTo][gameuidb-news])

---

## 2. Bảng màu (design tokens)

Tất cả màu khai báo dưới dạng biến CSS trong `:root`. Không dùng mã màu trực tiếp trong component.

### Nền cảnh
| Token | Giá trị | Dùng cho |
|---|---|---|
| `--sky-top` | `#F3B45E` | Trời phía trên (cam mật ong) |
| `--sky-mid` | `#F6C66B` | Trời giữa |
| `--sky-low` | `#FBE3A6` | Chân trời quanh mặt trời |
| `--sun` | `#FFF1C1` | Mặt trời và quầng sáng |
| `--sea-top` | `#3A9AA6` | Biển gần chân trời |
| `--sea-mid` | `#2E8C9A` | Biển giữa |
| `--sea-deep` | `#1F6C7A` | Biển gần người xem |
| `--cliff-lit` / `--cliff` / `--cliff-shade` | `#E2B07A` / `#A9876A` / `#6E5442` | Vách đá: cạnh được nắng chiếu, thân, bóng |

### Giao diện
| Token | Giá trị | Dùng cho |
|---|---|---|
| `--panel` | `rgba(255,244,220,.9)` (≈ `#FFF4DC`) | Thẻ, panel, modal |
| `--panel-border` | `#E7C98A` | Viền panel |
| `--ink` | `#3B2A12` | Chữ chính |
| `--ink-soft` | `#6E5230` | Chữ phụ |
| `--amber` → `--amber-dk` | `#F2B230` → `#E09A1A` | Nút chính, viền chọn, "của mình" |
| `--gold-hi` | `#FFC845` | Băng rôn YOUR TURN, ⚡ |
| `--wood` | `#5A3E1B` | Viền đậm, nhãn bàn cờ |
| `--teal` → `--teal-dk` | `#1E5560` → `#123E46` | Thân cờ chỉ huy, banner bàn cờ, nút phụ |
| `--coral` | `#C2412D` | Đối thủ, ENEMY TURN, nguy hiểm |
| `--hit` | `#D93A2B` | Chốt trúng |
| `--success` | `#23805A` | Sẵn sàng, đánh chìm tàu địch |
| `--coast` | `#B4531A` | Viền bờ biển quanh vùng chơi |
| `--grid` | `rgba(185,138,78,.55)` | Đường kẻ ô (trang trí) |

### Độ tương phản đã kiểm tra (công thức WCAG)
| Cặp màu | Tỉ lệ | Kết quả |
|---|---|---|
| `--ink` trên `--panel` | 12.60:1 | AAA |
| `--ink-soft` trên `--panel` | 6.60:1 | AA |
| `--ink` trên nút `--amber` | 7.33:1 | AAA |
| Kem `#FFF4DC` trên `--teal` | 7.62:1 | AAA |
| `--ink` trên băng rôn `--gold-hi` | 8.91:1 | AAA |
| Trắng trên băng rôn `--coral` | 5.14:1 | AA |
| Trắng trên `--success` | 4.88:1 | AA |
| `--coast` trên ô `--panel` | 4.59:1 | Đạt ≥ 3:1 cho đồ hoạ |
| Chốt `--hit` trên ô | 4.19:1 | Đạt ≥ 3:1 cho đồ hoạ |
| `--grid` trên ô | ≈ 2.3:1 | Chỉ để trang trí; vị trí ô được xác định bằng nhãn A–J / 1–10 |

**Quy tắc độ sáng:** cảnh nền nằm ở mức sáng vừa (trời cam-vàng, biển xanh ngọc trầm). Panel kem sáng hơn nền một bậc để nổi lên. Mảng tối duy nhất là thân cờ chỉ huy và banner màu teal, dùng làm điểm nhấn chứ không làm nền.

---

## 3. Typography

| Vai trò | Font | Cỡ (desktop / mobile) |
|---|---|---|
| Logo, tiêu đề lớn, băng rôn lượt | **Lilita One** (Google Fonts) | 48–64px / 34–40px |
| Banner bàn cờ, nhãn nút lớn | Lilita One, chữ hoa, letter-spacing .04em | 15–18px |
| Chữ thường, mô tả, chỉ số | **Nunito** 600–900 | 14–16px; chỉ số 28–36px |
| Nhãn bàn cờ (A–J, 1–10) | Nunito 900 | 11px / 9px |

- Tiêu đề lớn có viền chữ nâu `--wood` và đổ bóng nâu để nổi trên trời vàng.
- Số liệu (⚡, tỉ số) dùng `font-variant-numeric: tabular-nums`.

---

## 4. Component

### Panel / thẻ
Nền `--panel`, viền 2px `--panel-border`, bo góc 18px, bóng ấm `0 10px 28px rgba(90,62,27,.22)`, `backdrop-filter: blur(10px)`.

### Nút
- **Primary:** gradient `--amber` → `--amber-dk`, chữ `--ink` đậm, viền 2px `--wood`, bóng đáy 3px `--wood` (kiểu nút nổi). Khi bấm: lún xuống 2px.
- **Secondary:** teal, chữ kem.
- **Danger:** coral, chữ trắng.
- **Disabled:** opacity .45, không có bóng.

### Cờ chỉ huy (pennant)
Thân teal, viền vàng 3px, chân dung có vòng kem. Đang tới lượt thì viền phát sáng vàng (`--gold-hi`). Trên mobile cờ thu gọn thành thẻ ngang.

### Bàn cờ
- Ô nước: kem trong suốt `rgba(255,244,220,.72)` trên nền biển (đủ đục để lưới đều màu khi nằm vắt qua cả trời lẫn biển), kẻ `--grid`.
- Viền bờ biển 2px `--coast` quanh vùng chơi và quanh đảo.
- Đảo: xanh lá ấm `#9CC46B` → `#6E9E4A`, viền cát `#F3DDA0`.
- Chốt trượt: trắng kem; chốt trúng: `--hit`, ô tô `rgba(217,58,43,.22)`.
- Banner trên bàn cờ: teal, chữ kem, font Lilita One. Bàn cờ mình đang bị bắn thì banner chuyển coral.

### Kỹ năng (hình thoi)
Mặt đá xám ấm. Khi được chọn: gradient amber, viền `--gold-hi`, phát sáng. Nhãn chi phí là cờ nhỏ màu teal.

### Thanh tip
Nền teal đậm, viền amber, chữ kem; tên kỹ năng tô `--gold-hi`.

### Băng rôn báo lượt (turn announcement)
- Hiện mỗi khi lượt đổi chủ, kể cả lượt đầu tiên.
- **YOUR TURN:** dải `--gold-hi` → `--amber`, chữ `--ink`. **ENEMY TURN:** dải `--coral` → `#9E2F1F`, chữ trắng.
- Dải nằm ngang giữa màn hình, cao khoảng 88px (mobile 68px), hai đầu cắt hình đuôi cờ. Có dòng phụ nhỏ (ví dụ "Fire at will!" / "Brace for impact!").
- Chuyển động 1,4 s: trượt vào từ trái (0,25 s, ease-out) → dừng 0,9 s → trượt ra phải (0,25 s). Có một vệt sáng lướt qua chữ.
- `pointer-events: none`: không chặn thao tác. Với reduced-motion thì chỉ hiện rồi tắt.
- Âm thanh: lượt mình là tiếng chuông (`bell`), lượt địch là tiếng kim loại trầm (`ready` với cao độ thấp).

### Toast
Nền teal, viền amber, chữ kem. Loại tốt: success; loại xấu: coral. Hiện ở dưới cùng màn hình (để không che banner bàn cờ), tối đa khoảng 2,6 s.

### Modal
Nền mờ nâu `rgba(59,42,18,.45)`, thẻ panel.

---

## 5. Chuyển động & âm thanh

| Sự kiện | Thời lượng | Easing |
|---|---|---|
| Hover nút | 120 ms | ease |
| Băng rôn lượt | 1.4 s | ease-out vào, ease-in ra |
| Đổi bàn cờ lớn/nhỏ | sau 0,8 s kể từ khi đổi lượt | — |
| Toast | 2.6 s | — |

Mọi animation trang trí (mây, sóng, nhấp nhô) phải tắt được bằng `prefers-reduced-motion`.

---

## 6. Ngôn ngữ (UI tiếng Anh)

| Khái niệm | Chữ hiển thị |
|---|---|
| Tàu | Carrier, Battleship, Cruiser, Submarine, Destroyer |
| Chế độ | Classic, Commander |
| Bản đồ | Open Sea, Archipelago, Fjord |
| Kỹ năng | Fire, Radar, Cluster Bomb, Airstrike |
| Lượt | YOUR TURN, ENEMY TURN |
| Nút | Create Room, Join, Ready, Random, Rotate, Clear, Rematch, Leave Room |

Giọng văn: ngắn, chủ động, kiểu mệnh lệnh hải quân ("Deploy your fleet", "Fire at will!", "Brace for impact!").

---

## 7. Checklist khi làm UI

- [x] Mọi màu lấy từ token ở mục 2
- [x] Chữ đạt ≥ 4.5:1, chữ lớn và đồ hoạ quan trọng đạt ≥ 3:1
- [x] Font Lilita One + Nunito
- [x] Toàn bộ chữ trong game là tiếng Anh, `<html lang="en">`
- [x] Băng rôn YOUR TURN / ENEMY TURN mỗi khi đổi lượt
- [x] Không chặn thao tác bằng hiệu ứng; có reduced-motion
- [x] Kiểm tra ở 1366×860 và 390×844

[virtuall]: https://virtuall.pro/blog/game-interface-design
[hud]: https://db-01-us-west-2.aws.onerain.com/hud-elements
[webaim]: https://webaim.org/articles/contrast/
[mdn]: https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_WCAG/Perceivable/Color_contrast
[fonts]: https://madegooddesigns.com/?p=6586
[gameuidb]: https://www.gameuidatabase.com/
[gameuidb-news]: https://alternativeto.net/news/2024/8/game-ui-database-2-0-launches-with-over-55-500-screens-and-enhanced-tools-for-ui-designers/

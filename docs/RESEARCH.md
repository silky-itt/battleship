# Hải Chiến — Research & Bản thiết kế v2

Tài liệu này tổng hợp research về tựa game Battleship và chốt bản thiết kế cho phiên bản 2 của Hải Chiến. Code trong `index.html` làm theo phần **4. Thiết kế v2** và **6. Checklist**.

---

## 1. Lịch sử tựa game

| Mốc | Sự kiện | Nguồn |
|---|---|---|
| Trước Thế chiến I | Sĩ quan Nga được cho là đã chơi các phiên bản đầu. Nhật ký năm 1907 của nhà thơ Ryurik Ivnev có ghi lại một ván chơi. | [Wikipedia][wiki] |
| 1931 | Bản thương mại đầu tiên: *Salvo* do Starex phát hành tại Mỹ, dạng giấy và bút chì. | [Wikipedia][wiki] |
| 1930–1940s | Nhiều nhà phát hành ra biến thể, trong đó có *Broadsides* của Milton Bradley. | [Wikipedia][wiki] |
| 1967 | Milton Bradley ra bản bàn nhựa có cắm chốt và tàu mô hình, là phiên bản phổ biến nhất. | [Wikipedia][wiki], [Toy Tales][toytales] |
| 1977 | *Electronic Battleship*, đồ chơi chạy vi xử lý, "có thể phát nhiều loại âm thanh". | [Wikipedia][wiki] |
| 1979 | Bản video game đầu tiên trên Z80 Compucolor. | [Wikipedia][wiki] |
| 2012 | Phim điện ảnh *Battleship*. | [Wikipedia][wiki] |

**Rút ra cho thiết kế:** ngay từ bản 1977, âm thanh đã là "điểm ăn tiền" của game. Bản 2 phải coi âm thanh và phản hồi khi bắn là trọng tâm.

## 2. Luật & biến thể

- **Lưới:** 10×10, cột đánh chữ A–J, hàng đánh số 1–10. Mỗi người có 2 lưới: một lưới cho hạm đội của mình, một lưới để theo dõi các phát bắn. ([Wikipedia][wiki])
- **Hạm đội chuẩn (Milton Bradley 1990):** Carrier 5 ô, Battleship 4, Cruiser 3, Submarine 3, Destroyer 2. Năm 2002 Hasbro đổi Cruiser thành Destroyer và thêm Patrol Boat 2 ô. Hải Chiến giữ bộ 1990 (5-4-3-3-2). ([Wikipedia][wiki])
- **Salvo:** mỗi lượt bắn số phát bằng số tàu còn sống. ([Wikipedia][wiki])
- **Luật nhà phổ biến ở VN:** bắn trúng được bắn tiếp. Hải Chiến v1 đã áp dụng và v2 giữ nguyên.

## 3. Các loại tàu (tham khảo để vẽ, nhìn từ trên xuống)

| Tàu | Ô | Đặc điểm nhận dạng khi nhìn từ trên |
|---|---|---|
| Tàu sân bay (Carrier) | 5 | Sàn phẳng hình chữ nhật, đường băng có vạch đứt ở giữa, đảo chỉ huy nằm lệch một bên mạn, vài máy bay đậu trên sàn |
| Thiết giáp hạm (Battleship) | 4 | Thân dài, mũi nhọn; 2 tháp pháo lớn phía trước, 1 tháp phía sau, mỗi tháp 3 nòng; cụm cầu tàu và ống khói ở giữa |
| Tuần dương hạm (Cruiser) | 3 | Giống thiết giáp hạm nhưng nhỏ hơn: 1 tháp pháo trước, 1 tháp sau, cầu tàu và ống khói ở giữa |
| Tàu ngầm (Submarine) | 3 | Thân hình điếu xì gà, bo tròn hai đầu, màu tối; tháp chỉ huy nhỏ nằm lệch về phía trước, có cánh lặn |
| Khu trục hạm (Destroyer) | 2 | Thân thon và nhọn, 1 tháp pháo nhỏ ở mũi, cầu tàu nhỏ |

**Màu:** xám hải quân (haze gray). Sàn tàu sân bay màu xám đậm, vạch vàng và trắng. Tàu ngầm màu than chì. Khi trúng đạn, tàu bị cháy sém đen dần; khi chìm, toàn thân tối lại, nghiêng và lún xuống nước.

## 4. Game feel — "juice"

Bài nói *Juice it or lose it* (GDC 2012, Martin Jonasson & Petri Purho) cho thấy một game Breakout bình thường trở nên vui hẳn nhờ thêm **flash, rung, chữ nổi, âm thanh, hạt (particle)**. Các yếu tố này không đổi luật chơi nhưng tạo cảm giác thoả mãn. ([eastondev][juice1], [RPG Playground][juice2])

Cũng có ý kiến phản biện rằng "juice" quá tay sẽ làm giảm sự nhập tâm ([RPG Playground][juice2]). Vì vậy hiệu ứng phải **ngắn (≤ 1 giây), không che bàn cờ, và tôn trọng `prefers-reduced-motion`**.

Áp dụng cho Hải Chiến:

| Sự kiện | Hình | Âm thanh | Rung |
|---|---|---|---|
| Bắn | Đạn bay theo đường cong từ phía người bắn tới ô, có vệt khói | Tiếng pháo | — |
| Trượt | Cột nước bắn tung, gợn sóng tròn, giọt nước văng ra | Tiếng đạn rơi xuống nước | — |
| Trúng | Chớp sáng, quả cầu lửa, mảnh vỡ và tia lửa văng ra, ô bị trúng cháy liên tục kèm khói | Tiếng nổ trúng thân tàu | Nhẹ (khi mình bị trúng) |
| Chìm tàu | Nổ lớn ở mọi ô của tàu, tàu cháy đen, nghiêng rồi lún xuống | Tiếng tàu bị phá huỷ | Mạnh |
| Thắng | Pháo hoa và confetti | Chuông + fanfare | — |
| Thua | Màn hình tối nhẹ | Giai điệu đi xuống | — |
| Đặt/xoay tàu | Tàu "nảy" nhẹ, gợn sóng | Tiếng gỗ va (place / rotate) | — |

**Biển sống động:** gradient nước nhiệt đới, sóng lăn tăn chuyển động, ánh nắng lấp lánh (caustics), vệt sóng trắng quanh mũi tàu.

## 5. Âm thanh — nguồn và giấy phép

Tất cả đều là **CC0 (public domain)**: dùng tự do, kể cả thương mại, không bắt buộc ghi công. Hải Chiến vẫn ghi công trong game để cảm ơn tác giả.

| File trong game | Nguồn gốc | Tác giả | Link |
|---|---|---|---|
| `sfx/fire.m4a` | cannon_fire_1.ogg (cắt 1,9 s) | Thimras | [Battle at sea][thimras] |
| `sfx/miss.m4a` | cannon_miss_1.ogg | Thimras | [Battle at sea][thimras] |
| `sfx/hit.m4a` | cannon_hit_ship_short.ogg (cắt 2,8 s) | Thimras | [Battle at sea][thimras] |
| `sfx/hit2.m4a` | cannon_hit_1.ogg (cắt 3,6 s) | Thimras | [Battle at sea][thimras] |
| `sfx/sunk.m4a` | ship_destroyed_short.ogg (cắt 5,5 s) | Thimras | [Battle at sea][thimras] |
| `sfx/splash1.m4a`, `splash2.m4a` | water_splash-02/05.flac | ezwa / qubodup | [6 short water splashes][splash] |
| `sfx/place`, `rotate`, `click`, `ready`, `bell` | Impact Sounds (impactWood, impactGeneric, impactMetal, impactBell) | Kenney | [kenney.nl][kenney] |
| `music/battle.m4a` | *Enemy Ship Approaching* (esa_0.ogg) | yd | [OpenGameArt][esa] |
| `music/lobby.m4a` | *Pirate Ship Theme Loop* | beardalaxy | [OpenGameArt][pirate] |

**Định dạng:** file gốc là OGG Vorbis, đã chuyển sang **AAC (.m4a)** bằng ffmpeg để chạy được trên Safari/iPhone. Hiệu ứng là mono 80 kbps, nhạc là stereo 72 kbps. Tổng khoảng 0,8 MB.

**Cách phát:** dùng Web Audio API (`decodeAudioData` → `AudioBufferSourceNode`) để nhiều âm chồng lên nhau mà không trễ. Mỗi lần phát đổi cao độ ngẫu nhiên ±6% để không bị lặp nhàm. Có hai nút tắt riêng: **nhạc** và **hiệu ứng**. Âm thanh chỉ bật sau cú chạm đầu tiên, vì trình duyệt chặn tự phát.

**Nhạc:** `lobby` phát ở sảnh và khi xếp tàu, `battle` phát khi vào trận. Chuyển nhạc bằng crossfade 1,2 s, âm lượng nhạc khoảng 35% để không át hiệu ứng.

## 6. Thiết kế v2 — checklist thực hiện

### Hình ảnh
- [x] Theme sáng: biển nhiệt đới (xanh ngọc → xanh dương), nền trời và cát nhạt. Bỏ dark mode tự động vì yêu cầu là "màu sáng hơn".
- [x] 5 tàu vẽ bằng SVG nhìn từ trên theo bảng mục 3, mỗi loại một hình riêng, xoay 90° khi đặt dọc.
- [x] Vệt sóng trắng quanh tàu; tàu nhấp nhô nhẹ.
- [x] Biển: sóng chuyển động, caustics lấp lánh (CSS, không tốn CPU).

### Hiệu ứng (canvas overlay toàn màn hình)
- [x] Đạn bay theo đường cong bậc hai, có vệt khói.
- [x] Trượt: cột nước, vòng gợn sóng, giọt nước.
- [x] Trúng: chớp sáng, cầu lửa, tia lửa, mảnh vỡ; ô trúng có lửa cháy và khói bay liên tục.
- [x] Chìm: nổ dây chuyền dọc thân tàu, tàu sạm đen, nghiêng và lún xuống (CSS transform).
- [x] Rung màn hình khi mình bị trúng (nhẹ) và khi tàu chìm (mạnh).
- [x] Thắng: pháo hoa và confetti khoảng 4 giây.
- [x] Tắt bớt hiệu ứng khi người dùng bật `prefers-reduced-motion`.

### Âm thanh
- [x] Web Audio loader cho 12 hiệu ứng và 2 bản nhạc, đổi cao độ ngẫu nhiên.
- [x] Hai nút: 🎵 nhạc / 🔊 hiệu ứng, nhớ lựa chọn bằng localStorage.

### Gameplay
- [x] Emote: 6 icon (😂 😱 🔥 👏 😎 🙏), bong bóng nổi trên màn hình cả hai bên, chống spam bằng cooldown 1,5 s.
- [x] Giữ toàn bộ luật và giao thức P2P của v1. Message mới `{t:'emote', e}` được kiểm tra theo danh sách cho phép.

### Kiểm thử
- [x] Test tự động 2 trình duyệt: tạo phòng → vào phòng → xếp → bắn đến hết ván → đấu lại → emote → rời phòng.
- [x] Chụp màn hình desktop và mobile để kiểm tra giao diện.
- [x] Đảm bảo file asset tải được qua GitHub Pages (đường dẫn tương đối).

---

[wiki]: https://en.wikipedia.org/wiki/Battleship_(game)
[toytales]: https://toytales.ca/battleship-from-milton-bradley-1967/
[juice1]: https://eastondev.com/blog/en/posts/dev/20260521-game-feedback-feel/
[juice2]: https://rpgplayground.com/research-making-a-juicy-game/
[thimras]: https://opengameart.org/node/136787
[splash]: https://opengameart.org/content/6-short-water-splashes
[kenney]: https://kenney.nl/assets/impact-sounds
[esa]: https://opengameart.org/node/15203
[pirate]: https://opengameart.org/content/pirate-ship-theme-loop

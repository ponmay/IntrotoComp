# IntrotoComp — Mô phỏng Breadboard, VOM, Kit FPGA & Kit Vi Xử Lý ATmega324PA

Ứng dụng mô phỏng thực hành môn **Nhập môn Điện toán / Kỹ thuật Số / Vi xử lý** dành cho sinh viên **Trường Đại học Bách Khoa — ĐHQG-HCM**, chạy trực tiếp trên **Windows 10/11** và **macOS (Apple Silicon M1/M2/M3/M4 & Intel)** dưới dạng gói **Portable** thuần Offline không cần cài đặt Python hay Node.js.

---

## 1. Tải và Chạy Ngay (Windows & macOS)

Mở mục **[Releases](https://github.com/ponmay/IntrotoComp/releases)** và tải gói tương ứng với hệ điều hành của bạn:

### A. Trên Windows 10 / 11
1. Tải về duy nhất tệp **`IntrotoComp.exe`**.
2. Nhấn đúp chuột vào **`IntrotoComp.exe`** để chạy ngay (nếu Windows SmartScreen hiện cảnh báo tệp tải từ Internet, chọn **More info** → **Run anyway**).

### B. Trên macOS (MacBook Air / Pro chip M1, M2, M3, M4 hoặc Intel)
1. Tải về tệp **`IntrotoComp-macOS.zip`** và nhấn đúp để giải nén ra **`IntrotoComp.app`** (có thể kéo vào thư mục `Applications`).
2. Ở lần mở đầu tiên, do ứng dụng giáo dục không đăng ký chứng chỉ Apple trả phí, mở **Terminal** và chạy 1 lệnh gỡ cờ cách ly trình duyệt:
   ```bash
   xattr -cr ~/Downloads/IntrotoComp.app
   ```
   *(Nếu bạn đã kéo vào Applications thì thay bằng `xattr -cr /Applications/IntrotoComp.app`; hoặc vào **System Settings → Privacy & Security → nhấn Open Anyway**).*
3. Nhấn đúp vào **`IntrotoComp.app`** để sử dụng bình thường từ các lần sau.

> Lưu ý: Bản phát hành chỉ cung cấp tệp thực thi hoàn chỉnh (đã đóng gói sẵn giao diện và lõi mô phỏng bên trong), không yêu cầu tải hay biên dịch mã nguồn.

---

## 2. Tính Năng Chính

### A. Phòng Thí Nghiệm Breadboard MB-102 & VOM DT-9205A
- **Nguồn 5V / GND / CLK độc lập**: Cắm dây từ khối nguồn bên trái vào thanh nguồn Breadboard; hỗ trợ cả 2 nửa thanh nguồn trên/dưới bị tách giữa cột `30` và `34` giống MB-102 ngoài đời. Có thể nhấn trực tiếp vào nhãn **`✂ HỞ GIỮA`** trên thanh nguồn để tự động nối/tháo cặp dây cầu **Đỏ (`+`)** và **Đen (`-`)** qua khe giữa.
- **Đồng hồ đếm ngược chung & Kiểm tra cập nhật**: Thanh trên cùng tích hợp đồng hồ đếm ngược dùng chung cho cả 2 chế độ **Breadboard** và **Kit FPGA** (khi hết giờ `00:00`, toàn bộ nền chuyển sang màu đỏ để báo hiệu ngay); tự động kiểm tra bản phát hành mới trên GitHub Releases khi có mạng và cho phép kiểm tra thủ công trong mục **Cài đặt (`⚙`)** (vẫn hoạt động hoàn toàn bình thường khi phòng máy chạy Offline).
- **Linh kiện chuẩn thực hành**: Đầy đủ nhóm IC số `74LS/74HC` (`74LS00`, `74LS02`, `74LS04`, `74LS08`, `74LS32`, `74LS47`, `74LS74`, `74LS86`, `74LS90`, `74LS138`, `74LS283`, ...), DIP Switch 4/8, Điện trở `330Ω / 1kΩ / 10kΩ`, LED đơn Đỏ/Xanh/Vàng, LED 7 đoạn Common Anode, dây nối nhiều màu với hiệu ứng kéo cắm trực quan.
- **Chế độ Lý tưởng & Thực tế**:
  - **Lý tưởng**: Linh kiện và lỗ cắm luôn tiếp xúc tốt.
  - **Thực tế**: Cho phép tùy chỉnh tỉ lệ lỗi ngẫu nhiên (`%`) cho IC, LED, điện trở, DIP, dây nối và lỗ cắm Breadboard để luyện tập kỹ năng **đo kiểm VOM DT-9205A** (`DCV`, `ACV`, `LOGIC`, `Ω`, `BEEP`, `DIODE`) và dò lỗi như mạch thật. Máy đo VOM không hiển thị gợi ý lỗ hỏng sẵn trên màn hình, sinh viên cần tự đo thông mạch hoặc điện áp giữa các điểm để tự xác định vị trí lỗi.
- **Lưu & Mở Mạch Breadboard (`.json` / `.ktsbb`)**:
  - Lần đầu bấm **Lưu mạch** (hoặc `Ctrl + S`): Cho phép chọn thư mục cụ thể và đặt tên tệp mạch.
  - Các lần **Lưu** / `Ctrl + S` tiếp theo khi đang mở tệp: Ghi đè trực tiếp vào đúng tệp hiện tại.
  - Giữ `Shift` + bấm **Lưu** (hoặc `Ctrl + Shift + S`): Lưu sang một tệp mới ở vị trí tùy chọn.
- **Cầu nối FPGA IO (`io-0..io-13`) trên Breadboard**:
  - Chọn nhanh 1 trong 3 Kit (**`DE10-Std`**, **`DE23-Lite`**, **`Nexys A7`**) ngay dưới Breadboard, đồng bộ 2 chiều với tab **Kit FPGA**.
  - Hiển thị tên tín hiệu và mã chân thực tế (`GPIO[0..13]` hoặc `PMOD JA/JB`), đèn báo **● ĐANG HOẠT ĐỘNG** chuyển sang **xanh lá** khi Kit FPGA đã cấp nguồn và nạp bitstream.

### B. Mô Phỏng 3 Kit FPGA (`DE10-Standard`, `DE23-Lite`, `Nexys A7-100T`)
- **Chế độ Chuẩn (Bitstream) & Chế độ Bypass (Code + Chân)**:
  - **Chuẩn (`.sof` / `.bit`)**: Yêu cầu file bitstream đã biên dịch từ Quartus Prime / Vivado kèm mã nguồn HDL và file gán chân (`.qsf`/`.pin` hoặc `.xdc`) để kiểm tra định dạng nhị phân, chip ID và dấu thời gian.
  - **Bypass (Code + Chân)** *(khóa bằng mật khẩu giảng viên)*: Giúp chạy thử nhanh mà **không cần biên dịch bitstream**; ẩn nút chọn file `.sof`/`.bit` và chỉ nhận **Chọn thư mục**. Khi được mở khóa và dùng chế độ này, người dùng **phải tạo một thư mục riêng** chứa đủ cả mã nguồn HDL (`.v`, `.sv`, `.vhd`) và file gán chân (`.qsf`/`.pin` hoặc `.xdc`) gán đủ tất cả cổng top-level đúng với kit đang chọn, rồi trỏ đúng vào thư mục đó.
- **Mô phỏng thao tác phần cứng đúng thực tế từng Kit**:
  - `DE10-Standard`: Cấp nguồn DC 12V và cáp USB-Blaster II tách biệt 2 dây.
  - `DE23-Lite` & `Nexys A7-100T`: Chỉ cần gắn 1 dây USB để vừa cấp nguồn vừa nạp JTAG.
- **Nạp & Kiểm Tra Dự Án RTL**: Hỗ trợ tải tệp `.sof` / `.bit` kèm mã nguồn Verilog (`.v`), SystemVerilog (`.sv`), VHDL (`.vhd`) và tệp ràng buộc chân (`.qsf`, `.xdc`). Có tab kiểm tra map chân theo từng kit. Xung nhịp mô phỏng chạy đúng tần số phần cứng của kit (`50 MHz` / `100 MHz`).

### C. Mô Phỏng Kit Thí Nghiệm Vi Xử Lý `ATmega324PA` (3D WebGL, VOM, Oscilloscope & Cầu Nối `UART0`)
- **Bo mạch thực hành 3D WebGL & 2D trực quan sát thực tế**: Tái hiện đầy đủ khối phần cứng 3D trên Kit Vi xử lý (`8 MHz` / `1 MHz`): 4 cổng `PORT A/B/C/D` kèm công cụ cắm **Cáp Bus bẹ 16 sợi `AWM 2651` (`8×2`)** và **Dây Jumper đơn** trực tiếp trên mạch, `BARLED`, `RGB + LED đơn`, `8 DIP Switch`, `8 nút nhấn SW0..SW7` (có rung dội tiếp điểm cơ học thực tế), `Keypad 4×4`, cụm `4 LED 7 đoạn` (`74HC573`), `Ma trận LED 8×8` (`74HC595` + `ULN2803`), màn hình `LCD 16×2`, biến trở `VR1/VR2` xoay trực tiếp trên board, cảm biến nhiệt độ `MCP9701`, ánh sáng `TEPT5700`, `Buzzer` và động cơ `DC Motor L298N + Encoder`.
- **Thiết bị đo kiểm tích hợp ngay trên Kit (`📟 VOM` & `📈 OSC`)**:
  - **`📟 VOM` (`DT-9205A`)**: Đo áp DC/PWM trung bình, áp xoay chiều `True-RMS`, điện trở biến trở, kiểm tra thông mạch `BEEP`, sụt áp thuận LED và tần số/`Duty %` bằng cách chọn chân hoặc chấm trực tiếp que đo lên bo 2D/3D.
  - **`📈 OSC` (`DSO-2024A` — Máy hiện sóng số 2 kênh)**: Quan sát thời gian thực dạng sóng `PWM`/`CTC` (`OC0`, `OC1`, `OC2`), khung truyền nối tiếp `UART0 8N1`, hai pha vuông góc `90°` `Encoder A/B` và xung dội cơ học với đầy đủ `Time/div`, `Volts/div`, `Trigger`, `SINGLE` và `⚡ AUTOSET`.
- **2 chế độ nạp chương trình (tương tự Kit FPGA)**:
  - **Chuẩn (`.hex` / `.bin`)**: Nạp tệp `.hex`, `.elf` hoặc `.bin` biên dịch từ Microchip Studio / AVR-GCC qua cáp `MPLAB PICkit 4`.
  - **Bypass (Folder Code)** *(khóa bằng mật khẩu giảng viên)*: Cho phép chọn trực tiếp thư mục dự án chứa mã nguồn hợp ngữ AVR (`.asm`/`.s`) hoặc C (`.c`/`.h`) mà không cần tệp `.hex`/`.bin`.
- **Cầu nối cổng `COM` ảo tự động sang Hercules & PuTTY**: Bấm **`🔌 Kết nối`** bên dưới Kit để tự động tạo/ghép cặp cổng Serial `COM` ảo nối chéo (driver ký số WHQL trên Windows 10/11 hoặc `PTY` trên macOS) và hiện đúng tên cổng `COMx` để mở trực tiếp trong **Hercules SETUP Utility (tab `Serial`)** hoặc **PuTTY (`Serial`)**.

---

## 3. Phím Tắt Nhanh (Breadboard)

| Phím tắt | Chức năng |
| --- | --- |
| `W` | Chọn công cụ đi dây (Wire) |
| `1` – `6` | Đổi màu dây (Đỏ, Xanh dương, Xanh lá, Vàng, Đen, Tím) |
| `V` | Bật / tắt công cụ que đo VOM |
| `M` | Xoay thang đo VOM |
| `X` | Công cụ Xóa linh kiện / dây |
| `P` | Bật / tắt nguồn 5V DC |
| `Ctrl + S` | Lưu / Ghi đè mạch hiện tại |
| `Ctrl + Shift + S` | Lưu sang tệp `.json` / `.ktsbb` mới |
| `?` | Mở bảng phím tắt đầy đủ |
| `Esc` | Hủy thao tác đang đặt / đóng hộp thoại |

---

## 4. Tác Giả, Điều Khoản Sử Dụng & Miễn Trừ Bản Quyền

- **Tác giả**: **Ly & Phu** — Faculty of Electrical and Electronics Engineering, Ho Chi Minh City University of Technology, VNU-HCM.
- **Lời cảm ơn**: Cảm ơn **Gemini 4 Carbon** đã xây dựng, chỉnh sửa và phát triển ứng dụng này.
- **Mục đích sử dụng**: Sản phẩm này chỉ phục vụ cho mục đích giảng dạy và học tập, **không** dùng vào mục đích mua bán, kinh doanh hay thương mại hóa dưới bất kỳ hình thức nào.
- **Tuyên bố miễn trừ nhãn hiệu (Nominative Fair Use)**:
  - Phần mềm tự thiết kế toàn bộ đồ họa vector SVG và bộ mô phỏng logic **clean-room** phục vụ giảng dạy.
  - Tên bo mạch, mã vi mạch và tên chuẩn chân (như *DE10-Standard*, *DE23-Lite*, *Nexys A7-100T*, *ATmega324PA*, *MPLAB PICkit 4*, *Terasic*, *Digilent*, *Intel/Altera*, *AMD/Xilinx*, *Microchip/Atmel*) chỉ được nhắc đến để mô tả khả năng tương thích kỹ thuật với tệp dự án do sinh viên tự biên dịch.
  - Mọi nhãn hiệu đều thuộc quyền sở hữu của các hãng tương ứng. Dự án này là công cụ giáo dục độc lập, **không** trực thuộc và **không** được tài trợ hay ủy quyền bởi Terasic, Digilent, Intel, AMD hay Microchip.

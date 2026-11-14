# IntrotoComp — Mô phỏng Breadboard, VOM & Kit FPGA

Ứng dụng mô phỏng thực hành môn **Nhập môn Điện toán / Kỹ thuật Số** dành cho sinh viên **Trường Đại học Bách Khoa — ĐHQG-HCM**, chạy trực tiếp trên Windows 10/11 dưới dạng **1 file Portable duy nhất** (không cần cài đặt, không cần Python/Node.js).

---

## 1. Tải và Chạy Ngay (Bản Portable)

1. Mở mục **[Releases](https://github.com/ponmay/IntrotoComp/releases)** bên phải (hoặc trên thanh điều hướng).
2. Tải về duy nhất tệp **`IntrotoComp.exe`** ở bản phát hành mới nhất.
3. Nhấn đúp chuột vào **`IntrotoComp.exe`** để chạy ngay.

> Lưu ý: Bản phát hành chỉ cung cấp tệp thực thi `.exe` portable hoàn chỉnh (đã đóng gói sẵn giao diện và lõi mô phỏng bên trong), không yêu cầu tải hay biên dịch mã nguồn. Nếu Windows SmartScreen hiện cảnh báo tệp tải từ Internet, chọn **More info** → **Run anyway**.

---

## 2. Tính Năng Chính

### A. Phòng Thí Nghiệm Breadboard MB-102 & VOM DT-9205A
- **Nguồn 5V / GND / CLK độc lập**: Cắm dây từ khối nguồn bên trái vào thanh nguồn Breadboard; hỗ trợ cả 2 nửa thanh nguồn trên/dưới bị tách giữa cột `30` và `34` giống MB-102 ngoài đời.
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
  - Tên bo mạch, mã chip và tên chuẩn chân (như *DE10-Standard*, *DE23-Lite*, *Nexys A7-100T*, *Terasic*, *Digilent*, *Intel/Altera*, *AMD/Xilinx*) chỉ được nhắc đến để mô tả khả năng tương thích kỹ thuật với tệp dự án do sinh viên tự biên dịch trên Quartus/Vivado.
  - Mọi nhãn hiệu đều thuộc quyền sở hữu của các hãng tương ứng. Dự án này là công cụ giáo dục độc lập, **không** trực thuộc và **không** được tài trợ hay ủy quyền bởi Terasic, Digilent, Intel hay AMD.

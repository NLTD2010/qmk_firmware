# Hướng Dẫn Cài Đặt QMK/VIA Trên Aukey KM-G14

## 1. Giới thiệu

Aukey KM-G14 là bàn phím cơ layout TKL ANSI với RGB matrix và ba đèn LED indicator: Caps Lock, Scroll Lock và Win Lock. Bàn phím này sử dụng vi điều khiển VS11K09A-1, hỗ trợ flash firmware tùy chỉnh bằng QMK/VIA.

## 2. Cài Đặt Môi Trường QMK

### 2.1 Cài đặt môi trường QMK

Trước tiên, bạn cần cài đặt môi trường QMK bằng cách làm theo hướng dẫn chính thức tại:
[Setting Up QMK Environment](https://docs.qmk.fm/newbs_getting_started)

Tuy nhiên, khi chạy lệnh `qmk setup`, hãy sử dụng lệnh sau thay vì lệnh mặc định:

```sh
qmk setup NLTD2010/qmk_firmware
```

Lệnh này sẽ thiết lập firmware phù hợp với bàn phím Aukey KM-G14.

## 3. Chỉnh Sửa Keymap/Config

Sau khi thiết lập xong, nếu bạn muốn chỉnh sửa keymap hoặc cấu hình bàn phím, hãy điều hướng đến thư mục firmware của bàn phím bằng lệnh sau:

```sh
cd qmk_firmware/keyboards/aukey/kmg14
```

Ở đây, bạn có thể chỉnh sửa keymap bằng cách mở tệp `keymap.c` trong thư mục `keymaps/default/` hoặc tạo một keymap mới theo ý muốn:
Bạn có thể thay đổi các phím hoặc bổ sung các chức năng như macro, layer.

## 4. Biên Dịch và Flash Firmware

Sau khi đã chỉnh sửa keymap theo ý muốn, tiến hành biên dịch firmware bằng lệnh:

```sh
qmk compile -kb aukey/kmg14 -km default
```

Nếu quá trình biên dịch hoàn tất mà không có lỗi, firmware sẽ được tạo dưới dạng tệp `.hex` hoặc `.bin` trong thư mục `qmk_firmware/.build`.

### 4.1 Đưa bàn phím vào chế độ bootloader

Để flash firmware, bạn cần đưa bàn phím vào chế độ bootloader bằng cách **kéo điểm bootpin về GND**.
![](https://github.com/user-attachments/assets/707d5097-1e72-47e1-a9b8-3a0f62d57552)

### 4.2 Flash firmware với Sonix Flasher

Để flash firmware, sử dụng công cụ [Sonix Flasher](https://github.com/SonixQMK/sonix-flasher/).

Mở Sonix Flasher và thực hiện các bước sau:

1. Chọn **SN32F24x**.
2. Chọn **SN32F248B (bootloader)** từ danh sách.
3. Đặt `qmk offset` thành **0x00**.
4. Nhấn vào nút **Flash QMK...**.
5. Chọn tệp `.bin` mà bạn đã biên dịch (tìm trong `qmk_firmware/.build`).
6. Nhấn **Open** và đợi quá trình flash hoàn tất.
![image](https://github.com/user-attachments/assets/9495c69d-d18f-49f2-9bfc-c97ac4d46054)

Chúc các bạn thành công!


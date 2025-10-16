# Hướng dẫn cài đặt Klipper

Cài đặt Klipper bằng [KIAUH](https://github.com/dw-0/kiauh)

KIAUH là script giúp bạn **cài đặt và quản lý Klipper, Moonraker** cùng các giao diện web như **Fluidd** hoặc **Mainsail** chỉ với vài thao tác đơn giản.  

---

> ⚠️ **Lưu ý hệ thống hỗ trợ**  
> - KIAUH yêu cầu hệ điều hành Linux có **systemd** (ví dụ: Raspberry Pi OS, Debian, Ubuntu, Armbian...).  
> - Hoạt động ổn định nhất trên **Raspberry Pi OS Lite (32-bit hoặc 64-bit)**.  
> - Các bản **Ubuntu Server 20.04 / 22.04 / Armbian / Debian 11, 12** cũng tương thích tốt.  
> - Không hoạt động trên các hệ không dùng **systemd** (ví dụ: Alpine Linux, OpenWRT).  
> - KIAUH hỗ trợ cài, cập nhật và gỡ: **Klipper**, **Moonraker**, **Fluidd / Mainsail**.

---

## 1. Chuẩn bị thiết bị và hệ điều hành

### Giới thiệu

KIAUH là một script hỗ trợ bạn cài đặt Klipper trên **hệ điều hành Linux** đã được cài sẵn trên thẻ SD của **Raspberry Pi (hoặc SBC khác)**.  
Do đó, bạn cần đảm bảo rằng mình **đã có một hệ thống Linux hoạt động bình thường**.  
Đối với Raspberry Pi, bản Linux được khuyến nghị là **Raspberry Pi OS Lite (32-bit hoặc 64-bit)**.

Cách dễ nhất để ghi (flash) hệ điều hành này vào thẻ SD là sử dụng công cụ **Raspberry Pi Imager** chính thức.

---

### Cài đặt hệ điều hành cho Raspberry Pi

1. **Tải, cài đặt và mở Raspberry Pi Imager.**  
   Sau khi mở phần mềm, chọn **Choose OS → Raspberry Pi OS (other)**.

   <p align="center">
     <img src="https://github.com/seprinder/seprinder_cai_dat_klipper/blob/main/Image/pi-imager-os.png" alt="Chọn hệ điều hành Raspberry Pi OS Lite trong Imager" width="600">
   </p>

2. **Chọn phiên bản hệ điều hành:**  
   Chọn **Raspberry Pi OS Lite (32-bit)**  
   (hoặc chọn bản **64-bit** nếu bạn muốn dùng phiên bản 64-bit).

    <p align="center">
     <img src="https://github.com/seprinder/seprinder_cai_dat_klipper/blob/main/Image/pi-imager-lite.png" alt="Chọn Raspberry Pi OS Lite 32bit" width="600">
   </p>

3. **Quay lại menu chính của Raspberry Pi Imager**, chọn đúng **thẻ SD** bạn muốn ghi hệ điều hành vào.

4. **Vào mục Advanced Options (biểu tượng bánh răng ⚙️ ở góc trái dưới)**  
   - Bật **Enable SSH** (cho phép kết nối từ xa).  
   - Thiết lập **Wi-Fi SSID / Password** nếu dùng Wi-Fi.  
   - Tùy chọn: đặt tên thiết bị và mật khẩu mới nếu muốn.

    <p align="center">
     <img src="https://github.com/seprinder/seprinder_cai_dat_klipper/blob/main/Image/pi-imager-advanced.png" alt="Bật SSH và cấu hình Wi-Fi trong Raspberry Pi Imager" width="600">
   </p>

5. Nhấn **Write** để bắt đầu ghi hệ điều hành.  
   Sau khi hoàn tất, tháo thẻ SD và gắn vào **Raspberry Pi**, bật nguồn để khởi động.

> Nếu cần thêm hướng dẫn chi tiết về **raspberry Pi Imager**, hãy xem tài liệu chính thức tại trang [Raspberry Pi](https://www.raspberrypi.com/software/).

---

### Ghi chú cho thiết bị khác (Orange Pi, Banana Pi, SBC khác)

Các bước trên **chỉ áp dụng cho Raspberry Pi**.  
Nếu bạn sử dụng SBC khác (như Orange Pi hoặc các dòng Pi tương tự), hãy tìm hiểu cách **ghi hệ điều hành Linux phù hợp** lên thẻ SD (thường dùng **Balena Etcher** hoặc **rufus** để ghi).

Đảm bảo rằng hệ điều hành bạn chọn có thể chạy được **KIAUH**.  
Các bản phân phối dựa trên **Debian 11 (Bullseye)** thường hoạt động ổn định nhất.

> ⚠️ Trước khi tiếp tục, hãy xác nhận rằng thiết bị của bạn có thể khởi động được và bạn **có thể đăng nhập SSH hoặc mở terminal trực tiếp.**

---

## 2. Cài đặt KIAUH

Sau khi thiết bị của bạn đã khởi động và kết nối mạng ổn định, mở terminal hoặc SSH (bằng [PUTTY](https://putty.org/index.html) vào thiết bị và chạy tuần tự các lệnh sau:

```bash
sudo apt-get update && sudo apt-get install git -y
cd ~
git clone https://github.com/dw-0/kiauh.git
./kiauh/kiauh.sh
```

Sau khi lệnh cuối cùng chạy xong, bạn sẽ thấy menu KIAUH hiển thị như sau:

<p align="center">
  <img src="https://github.com/seprinder/seprinder_cai_dat_klipper/blob/main/Image/kiauh-menu.png" alt="Giao diện menu KIAUH" width="600">
</p>

Đây là giao diện chính để bạn cài đặt, cập nhật hoặc gỡ Klipper và các thành phần khác.

---

## 3. Cài Klipper, Moonraker và Giao diện Web

Trong menu KIAUH:

1. Chọn **1 (Install)**  
2. Chọn các thành phần muốn cài:
   - **Klipper** – phần mềm điều khiển máy in 3D.  
   - **Moonraker** – giao tiếp giữa Klipper và trình duyệt web.  
   - **Fluidd** hoặc **Mainsail** – giao diện web điều khiển máy in.

> 💡 Bạn chỉ cần chọn **một giao diện web** (Fluidd nhẹ hơn, Mainsail nhiều tùy chỉnh hơn).

Sau khi chọn, KIAUH sẽ tự động tải và cài tất cả gói cần thiết.  
Thời gian cài đặt: khoảng **5–15 phút** (tùy tốc độ mạng và thiết bị).

Hoàn tất, truy cập giao diện web bằng trình duyệt:

```
http://<địa_chỉ_IP_của_thiết_bị>
```
Ví dụ:
```
http://192.168.1.45
```
---

## 4. Build và nạp firmware cho bo mạch (MCU)

Để Klipper điều khiển được bo mạch máy in, bạn cần biên dịch và nạp firmware.

### Mở lại KIAUH
```bash
cd ~/kiauh
./kiauh.sh
```

### Build firmware
1. Trong menu, chọn **[4] Advanced → [1] Build Firmware**  
2. Chọn loại vi điều khiển (VD: STM32, LPC1768, ATmega...).  
3. Chọn giao tiếp (thường là **USB**).  
4. Sau khi hoàn tất, firmware nằm tại:
   ```
   ~/klipper/out/klipper.bin
   ```

### Nạp firmware
- Nếu bo mạch hỗ trợ USB → KIAUH có thể flash trực tiếp.  
- Nếu không → copy file `firmware.bin` vào thẻ SD → gắn vào bo → bật nguồn để tự nạp.

> ⚠️ Một số bo (VD: SKR Mini E3, MKS Robin Nano) chỉ hỗ trợ **nạp qua thẻ SD**.

---

## 5. Cấu hình và kiểm tra lần đầu

1 – Mở giao diện Klipper  
Trên máy tính hoặc điện thoại cùng mạng với Pi, mở trình duyệt và gõ:  
```
http://<địa_chỉ_IP_của_máy>
```
(ví dụ: `http://192.168.1.45`)  
→ Giao diện **Fluidd** hoặc **Mainsail** sẽ hiện ra.

---

2 – Tạo file cấu hình  
Vào menu **Configuration → printer.cfg → Add/Edit**  
→ Tải về tai [đây](https://github.com/Klipper3d/klipper/tree/master/config), tạo file mới hoặc dùng mẫu có sẵn trong:  
```
/home/pi/klipper/config/
```

---

3 – Gán cổng MCU  
Trong file `printer.cfg`, tìm đoạn:
```ini
[mcu]
serial: /dev/serial/by-id/usb-Klipper_...
```
Để biết đúng đường dẫn, gõ trong terminal:
```bash
ls /dev/serial/by-id/*
```
→ Sao chép đường dẫn đó vào dòng `serial:`.

---

4 – Lưu và khởi động lại  
Nhấn **Save & Restart**.

---

5 – Kiểm tra hoạt động  
Trong giao diện web:  
- Nhấn **Home All (G28)** → máy di chuyển về gốc.  
- Thử tăng nhiệt đầu phun trong tab **Temperature**.  
Nếu không báo lỗi → Klipper đã cài thành công.

**Tham khảo:**  
- [KIAUH GitHub](https://github.com/dw-0/kiauh)  
- [Tài liệu Klipper chính thức](https://www.klipper3d.org/)

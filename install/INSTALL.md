Hướng dẫn cài đặt hệ thống **Home Network Monitoring & DNS Security Lab**.

Hệ thống gồm các thành phần:

* Pi-hole DNS Filtering Server
* PRTG Network Monitoring
* Telegram Alert Notification

---

# 1. Chuẩn bị hệ thống

Thiết bị cần thiết:

| Thiết bị                       | Mục đích                |
| ------------------------------ | ----------------------- |
| Raspberry Pi 3 Model B trở lên | Chạy Pi-hole DNS server |
| Máy Windows                    | Chạy PRTG Monitoring    |
| Router                         | Quản lý mạng nội bộ     |
| Máy client                     | Kiểm tra hệ thống       |


* Raspberry Pi đã được cài hệ điều hành và kết nối mạng
* Có thể truy cập Raspberry Pi bằng SSH

---

# 2. Kết nối vào Raspberry Pi

SSH vào thiết bị:
Có thể dung IPScanner để dò IP của Raspberry

Ví dụ:

```
ssh pi@192.168.1.10
```

Sau khi đăng nhập thành công sẽ truy cập vào terminal của Raspberry Pi.

---

# 3. Cập nhật hệ thống

Trước khi cài đặt nên cập nhật hệ thống:

```
sudo apt update
sudo apt upgrade -y
```

---

# 4. Cài đặt Pi-hole

Chạy script cài đặt:

```
curl -sSL https://install.pi-hole.net | bash
```

Trong quá trình cài đặt:

Chọn các cấu hình sau:

* Upstream DNS provider (Google hoặc Cloudflare)
* Static IP address
* Enable Web Admin Interface

Sau khi hoàn thành sẽ hiển thị thông tin truy cập.

Ví dụ:

```
Admin Web Interface:
http://192.168.1.10/admin
```

---

# 5. Truy cập giao diện quản lý Pi-hole

Mở trình duyệt và truy cập:

```
http://IP-Pi-hole/admin
```

Ví dụ:

```
http://192.168.1.10/admin
```

Nếu cần đặt lại mật khẩu:

```
pihole -a -p
```

---

# 6. Cấu hình DNS cho mạng

Để các thiết bị trong mạng sử dụng Pi-hole, cần cấu hình DNS trong router.

```
Primary DNS: 192.168.1.10
```

Sau khi cấu hình:

Tất cả DNS request sẽ đi qua Pi-hole.

---

# 7. Cài đặt PRTG Network Monitor

Cài đặt trên máy Windows.

Các bước:

1. Tải file cài đặt PRTG
2. Chạy installer
3. Accept license
4. Hoàn tất cài đặt

Sau khi cài xong truy cập dashboard:

```
http://IP-monitoring-server
```

---

# 8. Thêm thiết bị monitoring

Trong giao diện PRTG:

1. Chọn **Add Device**
2. Nhập IP thiết bị

Ví dụ:

| Device  | IP           |
| ------- | ------------ |
| Router  | 192.168.1.1  |
| Pi-hole | 192.168.1.10 |

---

# 9. Thêm Sensors

Thêm các sensor để giám sát:

Ping Sensor
Kiểm tra thiết bị có hoạt động hay không.

HTTP Sensor
Kiểm tra web interface.

DNS Sensor
Kiểm tra DNS server hoạt động.

CPU Load
Giám sát CPU server.

---

# 10. Cấu hình Telegram Alert

## Tạo Telegram Bot

Mở Telegram và tìm:

BotFather

Gõ lệnh:

```
/newbot
```

Sau khi tạo bot sẽ nhận được:

```
BOT TOKEN
```

---

## Lấy Chat ID

Mở trình duyệt:

```
https://api.telegram.org/bot<TOKEN>/getUpdates
```

Sẽ hiển thị thông tin:

```
chat_id
```

---

## Test gửi message

Ví dụ:

```
https://api.telegram.org/bot<TOKEN>/sendMessage?chat_id=<CHAT_ID>&text=TestAlert
```

Nếu thành công bot sẽ gửi tin nhắn Telegram.

---

# 11. Tạo Alert trong PRTG

Trong PRTG:

1. Vào **Notification Templates**
2. Tạo template mới

Ví dụ nội dung cảnh báo:

```
⚠ Network Alert

Device: %device
Status: DOWN
Time: %datetime
```

Sau đó tạo trigger khi sensor bị lỗi.

---

# 12. Kiểm tra hệ thống

Thử tắt Raspberry Pi hoặc ngắt mạng.

PRTG sẽ:

1. Phát hiện Ping failed
2. Trigger alert
3. Gửi cảnh báo Telegram

Ví dụ thông báo:

```
⚠ Network Alert

Device: Pi-hole Server
Status: DOWN
Time: 22:40
```

---

# 13. Kiểm tra DNS Filtering

Truy cập một số website để kiểm tra quảng cáo.

Dashboard Pi-hole sẽ hiển thị:

* Total Queries
* Queries Blocked
* Top Clients
* Top Domains

---

# 14. Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống sẽ:

* Lọc quảng cáo bằng DNS filtering
* Giám sát thiết bị mạng
* Hiển thị dashboard monitoring
* Gửi cảnh báo khi hệ thống gặp sự cố

# Home-Network-Monitoring-DNS-Security-Lab
Triển khai hệ thống giám sát mạng gia đình, lọc DNS và cảnh báo sự cố qua Telegram.

### Giới thiệu dự án

Dự án này xây dựng một hệ thống giám sát và bảo mật mạng gia đình bằng cách kết hợp các công cụ monitoring, DNS filtering và hệ thống cảnh báo tự động.

Lab được triển khai trên máy ảo nhằm mô phỏng một hệ thống monitoring nhỏ giống môi trường doanh nghiệp.

Mục tiêu của dự án:

Giám sát trạng thái thiết bị mạng

Phát hiện sự cố hệ thống

Chặn quảng cáo và domain tracking ở cấp DNS

Hiển thị dashboard giám sát trực quan

Gửi cảnh báo tự động khi có sự cố

## Công nghệ sử dụng

Pi-hole — chặn quảng cáo và lọc DNS trong mạng nội bộ

PRTG Network Monitor — giám sát thiết bị mạng

Grafana — tạo dashboard giám sát hệ thống

Telegram Bot — gửi thông báo cảnh báo

VMware / VirtualBox — môi trường ảo hóa

## Môi trường Lab

Hệ thống được triển khai bằng 2 máy ảo.

Máy ảo	Hệ điều hành	Mục đích
Ubuntu Server	Linux	chạy Pi-hole và Grafana
Windows	Windows 10	chạy PRTG Monitoring

Tài nguyên sử dụng:

Tài nguyên	Dung lượng
RAM	~4GB
Disk	~35GB
Số VM	2
## Kiến trúc hệ thống
Internet
   │
Home Router
   │
Virtual Network
   │
 ┌───────────────┬───────────────┐
 │               │
Ubuntu Server   Windows Machine
│               │
├─ Pi-hole      └─ PRTG Network Monitor
└─ Grafana
        │
        ▼
   Telegram Alert
### Chức năng hệ thống
## Giám sát mạng (Network Monitoring)

PRTG được sử dụng để giám sát:

trạng thái server

độ trễ mạng (latency)

CPU và RAM

thời gian phản hồi DNS

Các sensor được sử dụng:

Ping Sensor

CPU Sensor

Memory Sensor

DNS Sensor

Bandwidth Sensor

## Lọc DNS và chặn quảng cáo

Pi-hole hoạt động như DNS server nội bộ giúp:

chặn quảng cáo toàn mạng

chặn domain tracking

ghi log truy vấn DNS

Ví dụ domain bị chặn:

ads.google.com
doubleclick.net
tracking.facebook.com
## Dashboard giám sát

Grafana được sử dụng để tạo dashboard trực quan cho hệ thống.

Dashboard hiển thị:

trạng thái thiết bị mạng

DNS queries

blocked domains

độ trễ mạng

Điều này giúp dễ dàng quan sát và phân tích hệ thống.

## Hệ thống cảnh báo

Khi PRTG phát hiện sự cố:

Trigger alert

Chạy script cảnh báo

Telegram Bot gửi thông báo

Ví dụ thông báo:
⚠ Network Alert

Device: Pi-hole Server
Status: DOWN
Time: 22:40

## Demo
1️. Thiết bị bị tắt

Tắt server Pi-hole.

Kết quả:

PRTG phát hiện thiết bị offline

Telegram gửi cảnh báo ngay lập tức

2. Test chặn quảng cáo

Truy cập website có quảng cáo.

Kết quả:

Pi-hole chặn domain quảng cáo

log DNS hiển thị domain bị block

## Quan sát dashboard

Mở dashboard Grafana để xem:

DNS traffic

trạng thái thiết bị

độ trễ mạng

### Cấu trúc project
home-network-monitoring-lab
│
├── README.md
│
├── architecture
│   └── network-diagram.png
│
├── screenshots
│   ├── grafana-dashboard.png
│   ├── pihole-dashboard.png
│   └── prtg-dashboard.png
│
├── scripts
│   └── telegram-alert.ps1
│
└── docs
    └── setup-guide.md

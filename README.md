Home-Network-Monitoring-DNS-Security-Lab

Dự án triển khai hệ thống giám sát mạng gia đình, lọc DNS và cảnh báo sự cố qua Telegram.

Giới thiệu dự án

Dự án này xây dựng một hệ thống giám sát và bảo mật mạng gia đình bằng cách kết hợp các công cụ monitoring, DNS filtering và hệ thống cảnh báo tự động.

Lab được triển khai trên máy ảo nhằm mô phỏng một hệ thống monitoring nhỏ tương tự môi trường doanh nghiệp.

Mục tiêu của dự án

Giám sát trạng thái thiết bị mạng

Phát hiện sự cố hệ thống

Chặn quảng cáo và domain tracking ở cấp DNS

Hiển thị dashboard giám sát trực quan

Gửi cảnh báo tự động khi có sự cố

Công nghệ sử dụng

Pi-hole – chặn quảng cáo và lọc DNS trong mạng nội bộ

PRTG Network Monitor – giám sát thiết bị mạng

Grafana – tạo dashboard giám sát hệ thống

Telegram Bot – gửi thông báo cảnh báo

VMware / VirtualBox – môi trường ảo hóa

Cấu trúc repository

diagrams/ : Sơ đồ kiến trúc hệ thống

configs/ : File cấu hình hệ thống monitoring

docs/ : Tài liệu tổng quan hệ thống

install/ : Hướng dẫn cài đặt và cấu hình

Môi trường Lab

Hệ thống được triển khai bằng 2 máy ảo.

Máy ảo	Hệ điều hành	Mục đích
Ubuntu Server	Linux	Chạy Pi-hole và Grafana
Windows	Windows 10	Chạy PRTG Monitoring
Tài nguyên sử dụng
Tài nguyên	Dung lượng
RAM	~4GB
Disk	~35GB
Số VM	2
Kiến trúc hệ thống

Hệ thống được thiết kế theo mô hình giám sát mạng đơn giản gồm các thành phần:

Internet

Home Router

Virtual Network

Monitoring Server

DNS Filtering Server

Alert System

Sơ đồ kiến trúc được lưu tại:

diagrams/network_architecture.png

Pi-hole hoạt động như DNS server nội bộ trong mạng.

Chức năng:

chặn quảng cáo toàn mạng

chặn domain tracking

ghi log DNS query

Ví dụ các domain bị block:

ads.google.com
doubleclick.net
tracking.facebook.com
PRTG Network Monitor

PRTG được sử dụng để giám sát trạng thái thiết bị mạng và server.

Các thông tin được theo dõi:

trạng thái server

độ trễ mạng (latency)

CPU usage

RAM usage

DNS response time

bandwidth

Các sensor được sử dụng:

Ping Sensor

CPU Sensor

Memory Sensor

DNS Sensor

Bandwidth Sensor

Grafana Dashboard

Grafana được sử dụng để tạo dashboard giám sát trực quan.

Dashboard hiển thị:

trạng thái thiết bị mạng

DNS queries

blocked domains

network latency

Điều này giúp dễ dàng quan sát và phân tích hệ thống.

Telegram Alert System

Hệ thống cảnh báo được tích hợp với Telegram Bot.

Khi PRTG phát hiện sự cố:

Trigger alert

Chạy script cảnh báo

Telegram Bot gửi thông báo

Ví dụ thông báo:

⚠ Network Alert

Device: Pi-hole Server
Status: DOWN
Time: 22:40
Demo hệ thống
Thiết bị bị tắt

Tắt server Pi-hole.

Kết quả:

PRTG phát hiện thiết bị offline

Telegram gửi cảnh báo ngay lập tức

Test chặn quảng cáo

Truy cập website có quảng cáo.

Kết quả:

Pi-hole chặn domain quảng cáo

DNS log hiển thị domain bị block

Quan sát dashboard

Mở dashboard Grafana để xem:

DNS traffic

trạng thái thiết bị

độ trễ mạng

Dashboard giúp theo dõi hệ thống mạng một cách trực quan và dễ dàng phân tích sự cố.

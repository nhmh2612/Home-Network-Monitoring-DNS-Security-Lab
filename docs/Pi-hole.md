# Pi-hole DNS Configuration Guide

## Đăng nhập

![Login](../diagrams/login.png)

---

## Dashboard

Sau khi đăng nhập thành công, ta sẽ vào trang **Dashboard** của Pi-hole để theo dõi tình trạng DNS, số lượng truy vấn và các domain bị chặn.

![Dashboard](../diagrams/dashboard.png)

---

# 1. Upstream DNS Servers

Khuyến nghị sử dụng **Cloudflare DNS** hoặc **Quad9 DNS**.

## Cấu hình phổ biến (khuyên dùng)

Tick:

Cloudflare (DNSSEC)

IPv4 DNS:

1.1.1.1
1.0.0.1

### Lý do

- tốc độ rất nhanh
- bảo vệ quyền riêng tư tốt
- độ ổn định cao

---

## Cấu hình bảo mật cao hơn

Tick:

Quad9 (filtered, DNSSEC)

DNS:

9.9.9.9
149.112.112.112

Quad9 có **malware filtering** giúp chặn domain độc hại.

![Upstream DNS](../diagrams/upstream.png)

### Lưu ý

Không nên chọn quá nhiều upstream DNS cùng lúc.

Khuyến nghị:

1 – 2 upstream DNS server

---

# 2. Pi-hole Domain Name

Giữ mặc định:

lan

Thiết bị trong mạng sẽ có dạng:

laptop.lan  
phone.lan  
printer.lan  

Điều này giúp dễ dàng quản lý và quan sát các thiết bị trong mạng nội bộ.

![Domain Name](../diagrams/domain.png)

---

# 3. Expand Hostnames

Bật:

Enable

Pi-hole sẽ tự động hiển thị hostname dạng:

hostname.lan

Thay vì chỉ hiển thị địa chỉ IP.

---

# 4. Rate Limiting

Giữ cấu hình mặc định:

1000 queries  
60 seconds  

### Mục đích

- chống spam DNS
- tránh DNS flooding
- bảo vệ server khỏi quá tải

Thông thường **không cần thay đổi cấu hình này**.

![Rate Limiting](../diagrams/ratelimit.png)

---

# 5. Interface Settings

Chọn:

Allow only local requests

Đây là **cấu hình an toàn nhất cho homelab**.

Không nên chọn:

Permit all origins

Vì sẽ biến Pi-hole thành:

Open DNS Resolver

→ dễ bị lạm dụng cho DNS amplification attack.

![Interface Settings](../diagrams/is.png)

---

# 6. Advanced DNS Settings

Khuyến nghị bật các tùy chọn sau:

Never forward non-FQDN queries  
Never forward reverse lookups for private IP ranges  

### Lợi ích

- tăng quyền riêng tư
- giảm truy vấn DNS không cần thiết
- tối ưu quá trình phân giải DNS

---

# 7. DNSSEC

Bật:

Enable DNSSEC

DNSSEC giúp:

- chống **DNS Spoofing**
- xác thực **DNS response**
- tăng độ tin cậy của hệ thống DNS

Lưu ý: chỉ bật khi upstream DNS hỗ trợ DNSSEC.

Các DNS hỗ trợ:

- Cloudflare
- Quad9

![DNSSEC](../diagrams/DNSSEC.png)

---

# 8. Query Log

Ví dụ một số truy vấn DNS trong Pi-hole:

doubleclick.net  → blocked  
google.com       → allowed  
facebook.com     → allowed  

![Query Log](../diagrams/querylog.png)

---

# 9. Network Clients

Ví dụ các thiết bị trong mạng nội bộ:

192.168.1.5   laptop.lan  
192.168.1.6   phone.lan  
192.168.1.7   tv.lan  

Tính năng này giúp:

- theo dõi thiết bị trong mạng
- kiểm tra DNS traffic của từng client
- phát hiện thiết bị bất thường

![Network Clients](../diagrams/client.png)

---

# Kết luận

Hệ thống **Pi-hole DNS Filtering** mang lại nhiều lợi ích cho mạng gia đình:

- chặn quảng cáo và tracker
- tăng bảo mật DNS
- giám sát hoạt động mạng
- quản lý thiết bị trong LAN

"""


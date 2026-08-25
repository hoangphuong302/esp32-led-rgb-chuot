# ESP32 LED RGB chuột

Firmware ESPHome độc lập cho LED RGB chuột BLE của Nhà Sam. Thiết bị này chỉ làm ba việc: giữ kết nối BLE với LED, nhận lệnh từ `nhasam.id.vn`, và hỗ trợ OTA. Nó không điều khiển điều hòa hay Cozy Life.

## Phần cứng đã khóa

- Board: ESP32-C3 4 MB
- MAC Wi-Fi: `70:AF:09:3A:EB:F0`
- LED BLE MAC: `FF:FF:DE:0D:04:AF`
- GATT write: service `FFE5`, characteristic `FFE9`
- GATT status notify: service `FFE0`, characteristic `FFE4`

## Giao thức LED

- Bật: `CC 23 33`
- Tắt: `CC 24 33`
- Màu: `56 RR GG BB 00 F0 AA`
- Hỏi trạng thái: `EF 01 77`

Lệnh chỉ được ACK về server sau khi LED trả gói trạng thái hợp lệ và trạng thái nguồn khớp. Lệnh màu luôn gửi gói bật trước để tương thích với controller Triones clone.

## Build / nạp lần đầu

1. Sao chép `secrets.yaml.example` thành `secrets.yaml` và điền bí mật.
2. Chạy `esphome run esp32-led-rgb-chuot.yaml --device COM3`.
3. Các lần sau dùng `esphome run esp32-led-rgb-chuot.yaml --device esp32-led-rgb-chuot.local` hoặc IP đã đối chiếu với MAC.

Không commit `secrets.yaml` hoặc file firmware nhị phân.

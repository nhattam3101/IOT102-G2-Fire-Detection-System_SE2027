# FireSafe System

**IOT102 · SE2027 · Group 2**  
IoT-based fire detection and warning prototype / Mô hình phát hiện và cảnh báo cháy ứng dụng IoT

[English](#english) · [Tiếng Việt](#tiếng-việt)

---

## English

FireSafe uses an ESP32 to read temperature, flame and smoke/gas sensors, display the system state and control local alarms and a model door. The firmware also connects to Blynk for monitoring, threshold settings and door control.

### System diagrams

These images are the diagrams used in the group's report. Select an image to view it at full size.

| Diagram | Purpose |
| --- | --- |
| [Block diagram](diagrams/block-diagram.png) | Overview of system components and their connections. |
| [Circuit schematic](diagrams/circuit-schematic.png) | Hardware connections for the prototype. |
| [Flowchart](diagrams/flowchart.png) | Main system logic and operating flow. |

### Operation

- **SAFE:** green LED; buzzer off.
- **WARNING:** temperature reaches the warning threshold; yellow LED and intermittent buzzer.
- **DANGER:** flame or smoke/gas is detected, or temperature reaches the danger threshold; red LED, continuous buzzer and door opens.
- The default temperature thresholds are 40 °C and 45 °C. Blynk can adjust them within the limits in the firmware. The door cannot be closed by the button or Blynk during DANGER.
- Local sensing and warning are processed before the Wi-Fi/Blynk connection is serviced.

### Hardware and pins

| Component | ESP32 GPIO |
| --- | --- |
| Flame sensor, digital output | 19 |
| MQ-2 sensor, digital output | 18 |
| LM35 temperature sensor | 34 |
| Buzzer | 15 |
| Green / yellow / red LEDs | 25 / 26 / 27 |
| I²C LCD SDA / SCL | 21 / 22 |
| Servo / push button | 32 / 33 |

Check the circuit schematic and the actual components before wiring. Flame and MQ-2 inputs are configured active LOW; the button uses the internal pull-up.

### Getting started

1. Install Arduino IDE, the ESP32 board package, and the **Blynk** and **ESP32Servo** libraries.
2. Copy `secrets.example.h` to `secrets.h` in the sketch directory. Set `WIFI_SSID`, `WIFI_PASSWORD` and `BLYNK_AUTH_TOKEN` for your own 2.4 GHz network and Blynk device. Keep `secrets.h` private.
3. Configure the Blynk template and datastreams shown below. The sketch contains the template ID and name; use the matching template or update these values for your own template.
4. Open `FireDetectionWithBlynk.ino` in Arduino IDE, select the ESP32 board and port, then verify and upload. If prompted, allow Arduino IDE to put the sketch in a same-named folder and place `secrets.h` there too.
5. Open Serial Monitor at **115200 baud**. See [hardware log test](DATALOG_HARDWARE_TEST.md) for the event and dashboard checks.

| Blynk pin | Data / control |
| --- | --- |
| V0 | Temperature |
| V1 | Flame detection |
| V2 | Smoke/gas detection |
| V3 | System status |
| V4 / V5 | Warning / danger temperature thresholds |
| V6 | Door status |
| V7 | Door control and state feedback |

The firmware uses event codes `fire_warning`, `fire_danger` and `system_safe`; configure these in Blynk if event logging is required.

### Repository contents

```text
FireSafe-System/
├── diagrams/                    # Report diagrams
├── FireDetectionWithBlynk.ino   # ESP32 firmware
├── secrets.example.h            # Credentials template
├── DATALOG_HARDWARE_TEST.md     # Blynk hardware test guide
└── README.md
```

This is an educational prototype and is not a certified fire alarm system.

---

## Tiếng Việt

FireSafe sử dụng ESP32 để đọc cảm biến nhiệt độ, lửa và khói/khí, hiển thị trạng thái, điều khiển cảnh báo tại chỗ và cửa mô hình. Firmware cũng kết nối Blynk để giám sát, chỉnh ngưỡng và điều khiển cửa.

### Sơ đồ hệ thống

Đây là các hình sơ đồ được sử dụng trong báo cáo của nhóm. Chọn tên sơ đồ để xem ảnh kích thước đầy đủ.

| Sơ đồ | Nội dung |
| --- | --- |
| [Sơ đồ khối](diagrams/block-diagram.png) | Tổng quan các thành phần và kết nối của hệ thống. |
| [Sơ đồ mạch](diagrams/circuit-schematic.png) | Các kết nối phần cứng của mô hình. |
| [Lưu đồ](diagrams/flowchart.png) | Luồng xử lý và hoạt động chính của hệ thống. |

### Nguyên lý hoạt động

- **SAFE:** LED xanh sáng, còi tắt.
- **WARNING:** nhiệt độ đạt ngưỡng cảnh báo; LED vàng sáng và còi kêu ngắt quãng.
- **DANGER:** phát hiện lửa hoặc khói/khí, hoặc nhiệt độ đạt ngưỡng nguy hiểm; LED đỏ sáng, còi kêu liên tục và cửa mở.
- Ngưỡng nhiệt độ mặc định là 40 °C và 45 °C; có thể điều chỉnh qua Blynk trong giới hạn của firmware. Nút nhấn và Blynk không thể đóng cửa khi đang ở trạng thái DANGER.
- Việc đọc cảm biến và cập nhật cảnh báo tại chỗ được xử lý trước kết nối Wi-Fi/Blynk.

### Phần cứng và chân kết nối

| Thành phần | GPIO ESP32 |
| --- | --- |
| Cảm biến lửa, ngõ ra số | 19 |
| Cảm biến MQ-2, ngõ ra số | 18 |
| Cảm biến nhiệt độ LM35 | 34 |
| Còi | 15 |
| LED xanh / vàng / đỏ | 25 / 26 / 27 |
| LCD I²C SDA / SCL | 21 / 22 |
| Servo / nút nhấn | 32 / 33 |

Đối chiếu sơ đồ mạch với linh kiện thực tế trước khi đấu nối. Ngõ vào Flame và MQ-2 được cấu hình kích hoạt mức LOW; nút nhấn dùng điện trở kéo lên nội bộ.

### Hướng dẫn sử dụng

1. Cài Arduino IDE, bộ hỗ trợ board ESP32 và các thư viện **Blynk**, **ESP32Servo**.
2. Sao chép `secrets.example.h` thành `secrets.h` trong thư mục sketch. Điền `WIFI_SSID`, `WIFI_PASSWORD` và `BLYNK_AUTH_TOKEN` của mạng 2.4 GHz và thiết bị Blynk. Giữ kín `secrets.h`.
3. Cấu hình template và các datastream Blynk theo bảng bên dưới. Code đã có template ID và tên; dùng template tương ứng hoặc cập nhật các giá trị này theo template của bạn.
4. Mở `FireDetectionWithBlynk.ino` bằng Arduino IDE, chọn board ESP32 và cổng, sau đó kiểm tra và nạp. Nếu IDE yêu cầu đưa sketch vào thư mục cùng tên, đặt cả `secrets.h` vào thư mục đó.
5. Mở Serial Monitor với tốc độ **115200 baud**. Xem [hướng dẫn kiểm tra log phần cứng](DATALOG_HARDWARE_TEST.md) để kiểm tra event và dashboard.

| Chân Blynk | Dữ liệu / điều khiển |
| --- | --- |
| V0 | Nhiệt độ |
| V1 | Phát hiện lửa |
| V2 | Phát hiện khói/khí |
| V3 | Trạng thái hệ thống |
| V4 / V5 | Ngưỡng nhiệt độ cảnh báo / nguy hiểm |
| V6 | Trạng thái cửa |
| V7 | Điều khiển và phản hồi trạng thái cửa |

Firmware sử dụng các event code `fire_warning`, `fire_danger` và `system_safe`; cấu hình các event này trên Blynk nếu cần ghi log.

### Cấu trúc thư mục

```text
FireSafe-System/
├── diagrams/                    # Các sơ đồ trong báo cáo
├── FireDetectionWithBlynk.ino   # Firmware ESP32
├── secrets.example.h            # Mẫu cấu hình thông tin kết nối
├── DATALOG_HARDWARE_TEST.md     # Hướng dẫn kiểm tra Blynk
└── README.md
```

Đây là mô hình phục vụ học tập, chưa phải hệ thống báo cháy được chứng nhận.

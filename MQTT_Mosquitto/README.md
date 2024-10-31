## Bố trí thí nghiệm
  Cài đặt https://mosquitto.org/ borker và MQTTX trên máy
  Thử nghiệm với localhost: Mở Admintrator:Command Prompt
    + Dùng lệnh 'net start mosquitto' để bắt đầu khởi động mosquitto broker
    + DÙng lệnh 'mosquitto -v' để theo dõi chi tiết về quá trình kết nối, các sự kiện xuất bản và đăng ký của các client
    + Cấu hình listener 1883, listener 8883, username, password cho localhost; với listener 8883 cần tạo self-signed certificate
  Sử dụng phần mềm MQTTX để kiểm tra kết nối với localhost port 1883 và 8883 (Ngoài ra, có thể sử dụng 1 MQTT broker công khai test.mosquitto.org do Eclipse Mosquitto cung cấp)
## Kịch bản thí nghiệm
  Kiểm tra các trạng thái kết nối thành công
  Thiết lập một client để publish tin nhắn lên topic esp32/echo_test
  Dùng MQTTX kiểm tra tin nhắn được gửi và nhận trong thời gian thực.
  Thử nghiệm với các chủ đề khác nhau và xác nhận hoạt động ổn định của broker, bao gồm cả cổng 1883 và 8883
## Mục đích
  Đánh giá tính ổn định và hiệu suất của Mosquitto broker trên các cổng.
  Xác nhận tính chính xác của dữ liệu truyền qua MQTT: Đảm bảo tin nhắn được gửi và nhận đúng nội dung, không bị mất mát.
## Kết quả
  Dùng MQTTX kiểm tra kết nối thành công
  Hình 1: Cấu hình hoàn thiện cho cổng 1883
  ![Hình 1](https://github.com/user-attachments/assets/cbfafe0a-bf65-4c75-a3d5-9ec17670aa2a)
  **Hình 1**
  Hinh 2 và 3: Cấu hình hoàn thiện cho cổng 8883 trên MQTTX với Broker localhost
  ![Hình 2](https://github.com/user-attachments/assets/5b2d4c23-cc89-4984-8e03-1accceba6eae)
**Hình 2**
  ![Hình 3](https://github.com/user-attachments/assets/16f3d029-bdd9-463c-98e1-d18b48c69fc6)
**Hình 3**
Hình 4 và 5: Kiểm tra tin nhắn gửi nhận (Hình 4 thể hiện cổng 8883 và Hình 5 thể hiện cổng 1883)
![Hình 4](https://github.com/user-attachments/assets/1492ee26-b1a3-4d43-805b-dda7652c2061)
**Hình 4**
![Hình 5](https://github.com/user-attachments/assets/ec59752d-c021-4cf4-b959-d2d71e3895a4)
**Hình 5**
## Kết luận 
  Kết quả thu được từ việc sử dụng MQTTX để kiểm tra kết nối, gửi và nhận tin nhắn cho thấy Mosquitto broker đáp ứng tốt yêu cầu về độ tin cậy và hiệu suất, kể cả khi sử dụng các cấu hình bảo mật như TLS.
  Thông qua việc cấu hình và thử nghiệm với localhost (có thể thử nghiệm thêm broker công khai test.mosquitto.org), ta thấy tính bảo mật và chính xác khi dùng Mosquitto trong việc giao tiếp qua các cổng khác nhau. 

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
  ![image](https://github.com/user-attachments/assets/1492ee26-b1a3-4d43-805b-dda7652c2061)

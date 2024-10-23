## Kịch bản

- Dùng thư viện PubSubClient trên ESP32
- Kết nối với một MQTT Broker (ở đây là EMQX cloud server), ESP32 là một client. 
- ESP32 MQTT Client publish 10 thông điệp lên broker mỗi giây một lần với nội dung là số đếm từ 0 đến 9. 
- Trong quá trình publish 10s kể trên, sẽ ngắt kết nối WiFi của ESP32, bằng một trong 2 cách:
    1. Tắt WiFi router rồi bật lại (có thể dùng điểm phát wifi AP trên điện thoại thông minh để tiện ngắt kết nối và bật lại)
    2. Dùng mô phỏng phần cứng ESP32 bằng Wokwi extension trên VS Code: ngắt kết nối internet của máy PC đang dùng rồi bật lại. 
- Bật lại kết nối WiFi (bằng 1 trong hai cách kể trên) trong quá trình publishing 10 thông điệp. Ví dụ: tiến hành ngắt wifi từ thông điệp thứ 3, sau đó bật lại vào thông điệp thứ 7. 
- Sau đó ESP32 in ra các thông điệp `echo` từ chính topic trên (mà nó đã subscribe trước khi publish) để xem có trả về các thông điệp đã publish, quan sát xem các thông điệp bị trống ở giữa trong quá trình ngắt kết nối WiFi ở giữa.

## Mục đích 
- Xem việc ngắt kết nối từ bên dưới chồng Internet Protocol có ảnh hưởng tới lớp trên không. Ở đây là lớp WiFi (link layer) bị ngắt --> lớp TCP/IP bị ngắt --> có ảnh hưởng tới lớp ứng dụng MQTT trên cùng hay không? ESP core lib sẽ in ra thông điệp lỗi như nào (có báo lỗi từ lớp dưới lên lớp bên trên hay không?)
- Quan sát sự bỏ mặc việc mất thông điệp trong QoS = 0. 

## Kết quả
- Không thực hiện được việc ngắt kết nối Internet khi mô phỏng bằng Wokwi trên VS Code: "Wokwi required internet connection, ... please paid version!"
- Thư viện PubSubClient có thể gọi hàm publish trước khi thiết lập kết nối thành công với broker ở xa (xem hình 1) là không báo lỗi gì.
- Các thông điệp Publish ban đầu với QoS 0 được bỏ qua hoàn toàn (khi chưa thiết lập kết nối với broker như nói ở trên): trên hình 1 các thông điệp 0, 1, 2 bị bỏ qua. Lưu ý: thư viện PubSubClient chỉ hỗ trợ publish với QoS = 0 cho nên không test được cơ chế retry của QoS 1 và QoS 2.
- Khi vừa mới kết nối thành công thì phía client nhận được đầu tiên là thông điệp Retained từ thí nghiệm trước đó (số 99) gửi về từ Broker (hình 1), do trong chương trình chúng ta thực hiện việc đăng ký `mqttClient.subscribe(echo_topic);` ngay sau khi kết nối thành công ở dòng 55 file main.cpp.
- Các thông điệp publish sau khi kết nối với broker thành công từ số 3 trở đi đều được gửi/nhận (echo) đều đặn không mất thông điệp nào, mặc cho việc publish và subcribe ở đây đều ở mức QoS = 0 và retained = false. 

Todos: để mai làm:
- Kết quả hình 2
- Kết quả hình 3
- Nghiên cứu kỹ hơn về "clean session"

## Kết luận 


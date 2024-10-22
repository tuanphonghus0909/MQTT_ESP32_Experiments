# Các dự án thực hành với giao thức MQTT trên ESP32

Đầu tiên nên cài đặt một client trên PC như EMQX client (MQTTX) và thử kết nối với các dịch vụ MQTT miễn phí để test thử trên PC trước.
Sử dụng thư viện PubSubClient by Nick O’Leary trên ESP32/PIO 

- Thí nghiệm với các mức chất lượng dịch vụ QoS 0, 1, 2 
- Retained vs Non-Retained message (Publish)
- Thí nghiệm về LWT 
- Thí nghiệm về keep alive 

Gợi ý nâng cao:
- Thiết lập kết nối TLS với một trong các MQTT broker (cổng 8883 thay vì 1883). 
- Nghĩ ra một thử nghiệm với giao thức MQTT trên con chip ESP32: độc đáo sáng tạo. 

---



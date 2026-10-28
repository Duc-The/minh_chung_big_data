# Nhật ký bổ sung ngày 21/10/2026

- Tinh gọn tài liệu và công cụ dựng báo cáo; giữ CSV, chỉ mục, model, cube và Docker volumes để tiếp tục demo.
- Chạy kiểm thử trong container Spark: 20/20 đạt. Log: outputs/logs/submission_tests_20261021.log.
- Spark đọc trực tiếp HDFS và đếm 1.300.086 record. Log: outputs/logs/cleanup_spark_inspect.log.
- Kiểm tra HDFS HEALTHY, Airflow không có lỗi import DAG, khởi động lại dashboard và kiểm tra bộ lọc/Clear/tra cứu/dự đoán. Kết quả: outputs/logs/cleanup_validation.json.
- Đóng ZIP source, kiểm checksum và thử giải nén, tạo môi trường cục bộ, kiểm cấu hình Compose; push mã nguồn lên GitHub tại commit dd8165d.
- Đại diện nhóm xác nhận phân công thực hiện; cập nhật báo cáo và bổ sung gói minh chứng riêng. Các tác vụ tự động hóa và lần chạy kiểm chứng được giữ đúng dấu vết thực tế, không tạo commit cá nhân hồi tố.

Các snapshot ngày 15/10/2026 trong báo cáo được giữ nguyên. Kiểm tra ngày 21/10 là lần kiểm tra bổ sung, không phải lần huấn luyện lại toàn bộ pipeline.

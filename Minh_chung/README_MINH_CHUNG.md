# Minh chứng đồ án ReviewLens

Gói này đi kèm báo cáo và ReviewLens_Source.zip. Các ảnh/bảng chính dùng snapshot ngày 15/10/2026; kết quả kiểm tra sau tinh gọn ngày 21/10/2026 được lưu riêng. Không dùng số liệu live hiện tại thay cho số trong ảnh lịch sử.

## Mã nguồn và cách đọc đường dẫn

- Repository: https://github.com/trongvi0807/BigData-PRO
- Mã nguồn nộp: nhánh master, commit dd8165d4d01315e4ff8ca17f3d53a278775bcad3.
- Snapshot gốc của báo cáo: commit 0fbabf67fa1a3a5526a75090a76d3484088a2190. GitHub giữ lịch sử này.
- Giải nén ZIP source và đọc README để tải dữ liệu, khởi động Docker và tái chạy pipeline. Gói minh chứng không thay thế dữ liệu vận hành của dashboard.
- Đường dẫn jobs/, src/, dags/, scripts/, config/ và dashboard/ nằm trong mã nguồn. Đường dẫn outputs/, docs/, artifacts/ và output/docx/ bên dưới nằm trong gói minh chứng này.

## Đối chiếu từng yêu cầu

| Nội dung | Mã nguồn | Minh chứng trong gói |
| --- | --- | --- |
| Nguồn/schema/quy mô | scripts/audit_dataset.py; jobs/batch_pipeline.py | artifacts/audit/dataset_profile.json; outputs/raw_inspection.json |
| HDFS raw và block | scripts/bootstrap_hdfs.py; infra/hadoop/ | outputs/logs/hdfs_ls_20261015.txt; hdfs_blocks_20261015.txt; hdfs_report_20261015.txt; hdfs_raw_sha256_20261015.txt |
| Làm sạch và SQL | jobs/batch_pipeline.py; src/review_analytics/spark_ops.py | outputs/data_quality.json; persisted_validation.json; spark_query_plan.txt; platform_summary.csv; monthly_summary.csv; outputs/logs/batch_20261015.log |
| Phân tích và biểu đồ | jobs/batch_pipeline.py | outputs/aspect_mentions.csv; unmatched_low_ratings.csv; outputs/report_charts/ |
| ML và nhãn thay thế | jobs/train_sentiment.py; src/review_analytics/sentiment.py | outputs/sentiment_evaluation.json; sentiment_model.json; outputs/logs/sentiment_train_20261015.log |
| Kafka replay | jobs/replay_kafka.py; jobs/stream_reviews.py | outputs/logs/kafka_topic_20261015.txt; kafka_producer_20261015.log; kafka_consumer_20261015.log; outputs/stream_batch_*.json |
| Thu thập thật | jobs/collect_live_reviews.py; jobs/publish_live_dashboard.py | outputs/logs/live_kafka_topic_20261015.txt; outputs/live/generations/5bf111f038694040a540af00fc0d109f/ |
| Airflow batch | dags/ecommerce_pipeline.py | outputs/demo_evidence.json; outputs/logs/airflow_tasks/run_id=validation_20261015/ |
| Airflow live đúng snapshot trong bảng | dags/live_reviews_pipeline.py | outputs/logs/live_airflow_tasks/run_id=scheduled__2026-10-15T01-00-00_UTC/; outputs/live_dashboard_validation.json |
| Dashboard đọc đầu ra Spark | jobs/prepare_dashboard.py; scripts/build_dashboard_index.py; dashboard/ | outputs/dashboard_preparation.json; dashboard_validation.json; combined_source_validation.json; clear_filters_validation.json; outputs/screenshots/11-clear-all-data-20261015.png |
| Replay và đồ thị nguồn thật | jobs/prepare_replay.py; jobs/replay_months.py; dashboard/web/replay.js | outputs/replay/; replay_browser_validation.json; replay_restart_validation.json; outputs/screenshots/14-four-platform-replay-20261015.png; 15-live-source-growth-20261015.png |
| Kiểm tra sau tinh gọn | tests/; scripts/validate_dashboard.py | outputs/logs/submission_tests_20261021.log; cleanup_spark_inspect.log; cleanup_validation.json |
| Nhật ký, Git và thành viên | lịch sử repository | GIT_HISTORY.txt; docs/IMPLEMENTATION_JOURNAL.md; BO_SUNG_NHAT_KY_20261021.md; PHAN_CONG_THUC_HIEN.md |

Các tên tệp rút gọn trong cùng ô bảng dùng chung thư mục với đường dẫn đứng trước khi ngữ cảnh rõ ràng. Báo cáo Word cũng ghi đầy đủ các nhóm đường dẫn.

## Kiểm toàn vẹn

SOURCE_REFERENCE.json ghi SHA-256 của ZIP source và commit. REPORT_REFERENCE.json ghi SHA-256 bản Word đã hoàn thiện. MANIFEST_SHA256.json ghi hash các tệp trong gói; SHA256SUMS.txt có thể kiểm trong WSL tại thư mục gốc gói:

```bash
sha256sum -c SHA256SUMS.txt
```

26 artifact của bản Word gốc đã được đối chiếu trùng SHA-256 với output/docx/word_report_manifest.json. Manifest gốc mô tả snapshot cũ; REPORT_REFERENCE.json nhận diện bản Word cập nhật. Tên thư mục log có dấu hai chấm được đổi thành dấu gạch để giải nén được trên Windows; PATH_ALIASES.json giữ ánh xạ, nội dung log và run ID không bị sửa.

## Phạm vi và giới hạn

Không có .env, mật khẩu cục bộ, CSV gốc, SQLite hoặc Docker volumes. Gói không chứa nhãn khía cạnh do người đọc đã hoàn thành. Phân công được đại diện nhóm xác nhận ngày 21/10/2026; lịch sử Git giữ nguyên tác giả thực tế Codex-Automation. Log có thể chứa các attempt lỗi và attempt khôi phục, cần chọn đúng run ID và attempt thành công thay vì chỉ tìm một dòng success.

# Reliability Checklist — FIT4110 Lab 03

Điền checklist này trước khi nộp Lab 03.

## 1. Functional tests

- [x] Có test cho endpoint health.
- [x] Có test happy path cho endpoint chính.
- [x] Có kiểm tra status code 2xx.
- [x] Có kiểm tra field quan trọng trong response.
- [x] Có ít nhất 1 test đọc dữ liệu danh sách hoặc chi tiết.

## 2. Auth tests

- [x] Có test thiếu token.
- [x] Có test sai token hoặc token rỗng.
- [x] Endpoint public được khai báo rõ nếu không cần auth.
- [x] Test thể hiện đúng expected status 401/403.

## 3. Negative tests

- [x] Có test thiếu field bắt buộc.
- [x] Có test sai kiểu dữ liệu.
- [x] Có test sai enum hoặc giá trị ngoài miền.
- [x] Lỗi trả về theo cùng một error model.

## 4. Boundary tests

- [x] Có test min/max hoặc dữ liệu sát ngưỡng.
- [x] Có test limit/pagination nếu endpoint có danh sách.
- [x] Có test payload lớn hoặc metadata thiếu.
- [x] Có ghi chú kỳ vọng xử lý dữ liệu biên.

## 5. Reliability tests cơ bản

- [x] Có kiểm tra response time.
- [x] Có mô tả timeout mong muốn.
- [x] Có test hoặc ghi chú retry/idempotency nếu phù hợp.
- [x] Có consumer-side smoke test với ít nhất 1 mock của nhóm khác.

## 6. Evidence

- [x] Collection export JSON.
- [x] Environment mock export JSON.
- [x] Environment local export JSON.
- [x] Newman report XML/HTML.
- [x] Test-case matrix đã điền.
- [x] Biên bản handshake đã điền.

## 7. Ghi chú local environment

- Collection đã chuẩn bị sẵn local environment tại `http://localhost:8000`.
- Ở thời điểm nộp Lab 03, service thật chưa được triển khai trong repo này nên evidence chính là Newman chạy trên Prism mock.
- Request trong folder `06_Local_only_NonFunctional` chỉ kiểm response time khi `env=local`; khi chạy mock, test được skip có kiểm soát để không dùng latency mock làm bằng chứng cho service thật.

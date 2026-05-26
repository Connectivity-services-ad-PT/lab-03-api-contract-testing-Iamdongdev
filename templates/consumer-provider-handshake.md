# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-26
- Provider team: Nhóm 8
- Consumer team: Core Business / Analytics
- Provider service: IoT Ingestion
- Consumer service: Core Business, Analytics

## Contract

- Contract file: `contracts/iot-ingestion.openapi.yaml`
- Mock base URL: `http://localhost:4010`
- Auth method: `Authorization: Bearer {{authToken}}`
- Endpoint được test:
  - `POST /telemetry/readings`
  - `GET /telemetry/readings/{readingId}`
  - `GET /devices/{deviceId}/latest`
  - `POST /events/sensor`

## Smoke test

### Request

```http
POST /events/sensor
Authorization: Bearer lab-token
Content-Type: application/json
```

```json
{
  "eventType": "telemetry.ingested",
  "eventId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2b555",
  "correlationId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2babc",
  "deviceId": "SENSOR-001",
  "locationId": "ROOM-A101",
  "sensorType": "temperature",
  "value": 30.5,
  "unit": "celsius",
  "timestamp": "2026-05-19T04:33:00Z"
}
```

### Expected response

```json
{
  "eventId": "0196fb3d-4ad7-7d1e-9f49-5d5148d2b555",
  "acceptedAt": "2026-05-19T04:33:02Z"
}
```

## Kết quả

- [x] Consumer gọi mock thành công.
- [x] Consumer parse được field cần dùng: `eventId`, `acceptedAt`.
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về qua `Problem` schema.
- [x] Có Newman report hoặc screenshot sau khi chạy `npm run test:mock`.

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| Contract Lab 3 | Dùng template `/readings`, `device_id`, `metric` | Dùng contract Lab 2 `/telemetry/readings`, `deviceId`, `sensorType` | Nhóm 8 |
| Event cho Analytics | Chưa có variant riêng `telemetry.ingested` trong mock Lab 3 | Bổ sung `TelemetryIngestedEvent` vào `SensorEvent.oneOf` | Nhóm 8 |
| Rate limit | Chưa có response `429` trong contract Lab 2 | Bổ sung `TooManyRequests` để phục vụ reliability test Lab 3 | Nhóm 8 |

## Xác nhận

- Provider representative: Dương Ngọc Đông - Nhóm 8 - IoT Ingestion
- Consumer representative: Core Business / Analytics theo user story Pair 05/06

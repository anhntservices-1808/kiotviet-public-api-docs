# Webhooks — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.11 — Webhook

Webhook cho phép KiotViet gửi thông báo real-time đến URL của bạn khi có sự kiện xảy ra.

---

## 2.11.1 — Lấy danh sách webhook

**Phương thức:** `GET https://public.kiotapi.com/webhooks`

### Response

```json
[
  {
    "id": 1,
    "url": "https://your-server.com/webhook",
    "type": "product",
    "isActive": true,
    "createdDate": "2024-01-01T00:00:00"
  }
]
```

---

## 2.11.2 — Tạo mới webhook

**Phương thức:** `POST https://public.kiotapi.com/webhooks`

### Request Body

```json
{
  "url": "https://your-server.com/webhook",
  "type": "product",
  "isActive": true
}
```

### Các loại webhook (type)

| Type | Mô tả |
|---|---|
| `product` | Sự kiện hàng hóa (tạo, cập nhật, xóa) |
| `order` | Sự kiện đặt hàng |
| `invoice` | Sự kiện hóa đơn |
| `customer` | Sự kiện khách hàng |
| `stocktake` | Sự kiện kiểm kho |
| `purchaseorder` | Sự kiện phiếu đặt hàng nhà cung cấp |

---

## 2.11.3 — Cập nhật webhook

**Phương thức:** `PUT https://public.kiotapi.com/webhooks/{id}`

---

## 2.11.4 — Xóa webhook

**Phương thức:** `DELETE https://public.kiotapi.com/webhooks/{id}`

---

## Định dạng dữ liệu gửi đến webhook

Khi có sự kiện, KiotViet sẽ gửi POST request đến URL đã đăng ký:

### Webhook hàng hóa

```json
{
  "Notifications": [
    {
      "Action": "update",
      "Data": {
        "id": 1001,
        "code": "SP001",
        "name": "iPhone 15",
        "modifiedDate": "2024-01-01T10:00:00"
      }
    }
  ]
}
```

### Webhook đặt hàng / hóa đơn

```json
{
  "Notifications": [
    {
      "Action": "create",
      "Data": {
        "id": 10001,
        "code": "DH001",
        "total": 25000000,
        "status": 1,
        "modifiedDate": "2024-01-01T10:00:00"
      }
    }
  ]
}
```

### Giá trị Action

| Action | Mô tả |
|---|---|
| `create` | Tạo mới |
| `update` | Cập nhật |
| `delete` | Xóa |

# Invoices (Hóa đơn) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.12.1 — Lấy danh sách hóa đơn

**Phương thức:** `GET https://public.kiotapi.com/invoices`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `branchIds` | int[]? | ID chi nhánh |
| `customerIds` | long[]? | ID khách hàng |
| `customerCode` | string | Mã khách hàng |
| `status` | int[]? | Tình trạng hóa đơn |
| `includePayment` | Boolean | Có lấy thông tin thanh toán |
| `includeInvoiceDelivery` | Boolean | Có lấy thông tin giao hàng |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật từ |
| `toDate` | datetime? | Thời gian đến |
| `pageSize` | int? | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |
| `orderBy` | string | Sắp xếp theo trường |
| `orderDirection` | string | `Asc` hoặc `Desc` |
| `createdDate` | datetime? | Thời gian tạo |
| `saleChannelId` | int? | ID kênh bán hàng |

### Trạng thái hóa đơn (status)

| Giá trị | Mô tả |
|---|---|
| 1 | Đang xử lý |
| 2 | Hoàn thành |
| 3 | Hủy |

### Response

```json
{
  "total": 50,
  "pageSize": 20,
  "data": [
    {
      "id": 20001,
      "code": "HD001",
      "purchaseDate": "2024-01-01T10:00:00",
      "branchId": 1,
      "branchName": "Chi nhánh 1",
      "soldById": 100,
      "soldByName": "Nhân viên A",
      "customerId": 500,
      "customerCode": "KH001",
      "customerName": "Nguyễn Văn A",
      "orderId": 10001,
      "orderCode": "DH001",
      "total": 25000000,
      "totalPayment": 25000000,
      "discountRatio": 0,
      "discount": 0,
      "status": 2,
      "statusValue": "Hoàn thành",
      "description": "Ghi chú hóa đơn",
      "usingCod": false,
      "totalTax": 0,
      "payments": [],
      "invoiceDetails": [],
      "invoiceDelivery": null,
      "retailerId": 100,
      "modifiedDate": "2024-01-01T10:00:00",
      "createdDate": "2024-01-01T10:00:00",
      "saleChannelId": null
    }
  ]
}
```

---

## 2.12.2 — Lấy chi tiết hóa đơn

**Phương thức:**
- Theo ID: `GET https://public.kiotapi.com/invoices/{id}`
- Theo Code: `GET https://public.kiotapi.com/invoices/code/{code}`

### Response (chi tiết)

Bao gồm đầy đủ `invoiceDetails`, `invoiceDelivery`, `payments`, `invoiceOrderSurcharges`.

---

## 2.12.3 — Tạo mới hóa đơn

**Phương thức:** `POST https://public.kiotapi.com/invoices`

> **Ghi chú:** Khi thêm mới hóa đơn từ MyKiot hoặc KV Sync sẽ thêm param Partner vào header:
> - Từ MyKiot: `Partner: MyKiot`
> - Từ KV Sync: `Partner: KVSync`

### Request Body

```json
{
  "isApplyVoucher": false,
  "purchaseDate": "2024-01-01T10:00:00",
  "branchId": 1,
  "soldById": 100,
  "cashierId": null,
  "discount": 0,
  "description": "Ghi chú hóa đơn",
  "method": "Cash",
  "totalPayment": 25000000,
  "accountId": null,
  "saleChannelId": null,
  "invoiceDetails": [
    {
      "productId": 1001,
      "productCode": "SP001",
      "productName": "iPhone 15",
      "quantity": 1.0,
      "price": 25000000,
      "discount": 0,
      "discountRatio": 0,
      "note": "",
      "usePoint": false,
      "InvoiceDetailTaxs": [
        {
          "TaxId": 4
        }
      ]
    }
  ],
  "invoiceDelivery": {
    "deliveryCode": "",
    "type": 1,
    "price": 30000,
    "receiver": "Nguyễn Văn A",
    "contactNumber": "0901234567",
    "address": "123 Lê Lợi",
    "locationId": 1,
    "locationName": "TP.HCM - Quận 1",
    "weight": 0.5,
    "expectedDelivery": "2024-01-03T10:00:00"
  },
  "customer": {
    "id": 500,
    "code": "KH001",
    "name": "Nguyễn Văn A",
    "contactNumber": "0901234567"
  },
  "surchages": [],
  "Payments": []
}
```

---

## 2.12.4 — Cập nhật hóa đơn

**Phương thức:** `PUT https://public.kiotapi.com/invoices/{id}`

### Request Body

Tương tự POST, kèm `id` trong path.

---

## 2.12.5 — Hủy hóa đơn

**Phương thức:** `DELETE https://public.kiotapi.com/invoices/{id}`

### Response (200 OK)

```json
{
  "message": "Hủy hóa đơn thành công"
}
```

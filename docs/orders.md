# Orders (Đặt hàng) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## Lưu ý cài đặt

- Cần bật **"Cho phép đặt hàng"** trong Thiết lập → nếu tắt, API trả lỗi: `"Thiết lập 'Cho phép đặt hàng' đang không được bật."`
- Cần bật **"Sử dụng tính năng giao hàng"** để dùng các API giao hàng
- Cần bật **"Không cho phép thay đổi thời gian bán hàng"** để POST/PUT thời gian bán hàng

---

## 2.5.1 — Lấy danh sách đặt hàng

**Phương thức:** `GET https://public.kiotapi.com/orders`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `branchIds` | int[]? | ID chi nhánh |
| `customerIds` | long[]? | ID khách hàng |
| `customerCode` | string | Mã khách hàng |
| `status` | int[]? | Tình trạng đặt hàng |
| `includePayment` | Boolean | Có lấy thông tin thanh toán |
| `includeOrderDelivery` | Boolean | Có lấy thông tin giao hàng |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật từ |
| `toDate` | datetime? | Thời gian cập nhật đến |
| `pageSize` | int? | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |
| `orderBy` | string | Sắp xếp theo trường |
| `orderDirection` | string | `Asc` hoặc `Desc` |
| `createdDate` | datetime? | Thời gian tạo |
| `saleChannelId` | int? | ID kênh bán hàng |

### Response

```json
{
  "total": 50,
  "pageSize": 20,
  "data": [
    {
      "id": 10001,
      "code": "DH001",
      "purchaseDate": "2024-01-01T10:00:00",
      "branchId": 1,
      "branchName": "Chi nhánh 1",
      "soldById": 100,
      "soldByName": "Nhân viên A",
      "customerId": 500,
      "customerCode": "KH001",
      "customerName": "Nguyễn Văn A",
      "total": 25000000,
      "totalPayment": 25000000,
      "discountRatio": 0,
      "discount": 0,
      "status": 1,
      "statusValue": "Đang xử lý",
      "description": "Ghi chú đơn hàng",
      "usingCod": false,
      "totalTax": 0,
      "payments": [],
      "orderDetails": [],
      "orderDelivery": null,
      "retailerId": 100,
      "modifiedDate": "2024-01-01T10:00:00",
      "createdDate": "2024-01-01T10:00:00",
      "saleChannelId": null
    }
  ]
}
```

---

## 2.5.2 — Lấy chi tiết đặt hàng

**Phương thức:**
- Theo ID: `GET https://public.kiotapi.com/orders/{id}`
- Theo Code: `GET https://public.kiotapi.com/orders/code/{code}`

### Response (chi tiết)

Bao gồm đầy đủ `orderDetails`, `orderDelivery`, `payments`, `invoiceOrderSurcharges`.

Cấu trúc `orderDetails`:
```json
{
  "productId": 1001,
  "productCode": "SP001",
  "productName": "iPhone 15 - 256GB",
  "isMaster": true,
  "quantity": 2.0,
  "price": 25000000,
  "discountRatio": 0,
  "discount": 0,
  "note": "",
  "orderDetailTaxs": []
}
```

Cấu trúc `orderDelivery`:
```json
{
  "deliveryCode": "VD001",
  "type": 1,
  "price": 30000,
  "receiver": "Nguyễn Văn A",
  "contactNumber": "0901234567",
  "address": "123 Lê Lợi",
  "locationId": 1,
  "locationName": "TP.HCM - Quận 1",
  "weight": 0.5,
  "length": 20.0,
  "width": 15.0,
  "height": 10.0,
  "partnerDeliveryId": null,
  "partnerDelivery": null
}
```

---

## 2.5.3 — Tạo mới đặt hàng

**Phương thức:** `POST https://public.kiotapi.com/orders`

> **Ghi chú:** Khi tạo từ MyKiot thêm header `Partner: MyKiot`; từ KV Sync thêm `Partner: KVSync`

### Request Body

```json
{
  "isApplyVoucher": false,
  "purchaseDate": "2024-01-01T10:00:00",
  "branchId": 1,
  "soldById": 100,
  "cashierId": null,
  "discount": 0,
  "description": "Ghi chú đơn hàng",
  "method": "Cash",
  "totalPayment": 25000000,
  "accountId": null,
  "makeInvoice": false,
  "saleChannelId": null,
  "orderDetails": [
    {
      "productId": 1001,
      "productCode": "SP001",
      "productName": "iPhone 15",
      "quantity": 1.0,
      "price": 25000000,
      "discount": 0,
      "discountRatio": 0,
      "note": "",
      "OrderDetailTaxs": [
        {
          "TaxId": 4
        }
      ]
    }
  ],
  "orderDelivery": {
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

### Thanh toán bằng Voucher

```json
"Payments": [
  {
    "Method": "Voucher",
    "MethodStr": "Voucher",
    "Amount": 50000,
    "Id": -1,
    "AccountId": null,
    "VoucherId": 30996,
    "VoucherCampaignId": 30087
  }
]
```

### Mã Tax (TaxId)

**Thuế khấu trừ:** `1`=VAT 0%, `2`=VAT 5%, `3`=VAT 8%, `4`=VAT 10%, `5`=KCT, `12`=KKKNT

**Thuế trực tiếp:** `6`=VAT 1%, `7`=VAT 2%, `8`=VAT 3%, `9`=VAT 5%, `64`=0% VAT 5% TNCN, `65`=0% VAT 1.5% TNCN, `66`=0% VAT 2% TNCN

---

## 2.5.4 — Cập nhật đặt hàng

**Phương thức:** `PUT https://public.kiotapi.com/orders/{id}`

### Request Body

Tương tự POST, kèm `id` trong path.

---

## 2.5.5 — Hủy đặt hàng

**Phương thức:** `DELETE https://public.kiotapi.com/orders/{id}`

### Response (200 OK)

```json
{
  "message": "Hủy đơn hàng thành công"
}
```

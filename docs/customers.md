# Customers (Khách hàng) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.6.1 — Lấy danh sách khách hàng

**Phương thức:** `GET https://public.kiotapi.com/customers`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `code` | string | Mã khách hàng |
| `name` | string | Tên khách hàng |
| `contactNumber` | string | Số điện thoại |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật từ |
| `pageSize` | int | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |
| `orderBy` | string | Sắp xếp theo trường |
| `orderDirection` | string | `Asc` (mặc định) hoặc `Desc` |
| `includeRemoveIds` | bool | Có lấy ID bị xóa dựa trên lastModifiedFrom |
| `customerGroupId` | int? | ID nhóm khách hàng |
| `birthDate` | datetime? | Ngày sinh |
| `includeCustomerGroup` | bool | Có lấy thông tin nhóm khách hàng |
| `gender` | bool? | Giới tính |

### Response

```json
{
  "total": 100,
  "pageSize": 20,
  "data": [
    {
      "id": 500,
      "code": "KH001",
      "name": "Nguyễn Văn A",
      "gender": true,
      "birthDate": "1990-01-01T00:00:00",
      "contactNumber": "0901234567",
      "address": "123 Lê Lợi, TP.HCM",
      "locationName": "TP.HCM - Quận 1",
      "wardName": "Phường Bến Nghé",
      "email": "nguyenvana@example.com",
      "comment": "Khách VIP",
      "retailerId": 100,
      "groups": [
        {
          "id": 1,
          "name": "Khách VIP"
        }
      ],
      "debt": 0,
      "totalInvoiced": 25000000,
      "totalPoint": 100,
      "totalRevenue": 25000000,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00",
      "type": 0,
      "organization": null,
      "taxCode": null,
      "isActive": true
    }
  ],
  "removeIds": []
}
```

---

## 2.6.2 — Lấy chi tiết khách hàng

**Phương thức:**
- Theo ID: `GET https://public.kiotapi.com/customers/{id}`
- Theo Code: `GET https://public.kiotapi.com/customers/code/{code}`

---

## 2.6.3 — Tạo mới khách hàng

**Phương thức:** `POST https://public.kiotapi.com/customers`

### Request Body

```json
{
  "code": "KH001",
  "name": "Nguyễn Văn A",
  "gender": true,
  "birthDate": "1990-01-01T00:00:00",
  "contactNumber": "0901234567",
  "address": "123 Lê Lợi",
  "locationId": 1,
  "wardId": 101,
  "email": "nguyenvana@example.com",
  "comment": "Khách VIP",
  "debt": 0,
  "organization": null,
  "taxCode": null,
  "groups": [
    {
      "id": 1
    }
  ]
}
```

### Response

Trả về object khách hàng vừa tạo.

---

## 2.6.4 — Cập nhật khách hàng

**Phương thức:** `PUT https://public.kiotapi.com/customers/{id}`

### Request Body

Tương tự POST.

---

## 2.6.5 — Xóa khách hàng

**Phương thức:** `DELETE https://public.kiotapi.com/customers/{id}`

### Response (200 OK)

```json
{
  "message": "Xóa dữ liệu thành công"
}
```

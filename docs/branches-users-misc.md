# Branches, Users, Bank Accounts, Surcharges — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.7 — Danh sách chi nhánh

**Phương thức:** `GET https://public.kiotapi.com/branches`

### Response

```json
{
  "total": 3,
  "pageSize": 20,
  "data": [
    {
      "id": 1,
      "branchName": "Chi nhánh chính",
      "address": "123 Lê Lợi, TP.HCM",
      "contactNumber": "0901234567",
      "wardName": "Phường Bến Nghé",
      "locationName": "TP.HCM - Quận 1",
      "isActive": true,
      "retailerId": 100,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00"
    }
  ]
}
```

---

## 2.8 — Danh sách người dùng

**Phương thức:** `GET https://public.kiotapi.com/users`

### Response

```json
{
  "total": 5,
  "pageSize": 20,
  "data": [
    {
      "id": 100,
      "userName": "admin",
      "givenName": "Admin",
      "branchId": 1,
      "isActive": true,
      "retailerId": 100,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00"
    }
  ]
}
```

---

## 2.9 — Danh sách tài khoản ngân hàng

**Phương thức:** `GET https://public.kiotapi.com/bankaccounts`

### Response

```json
{
  "total": 2,
  "pageSize": 20,
  "data": [
    {
      "id": 1,
      "bankName": "Vietcombank",
      "accountNumber": "1234567890",
      "accountHolder": "Nguyen Van A",
      "bankCode": "VCB",
      "isActive": true,
      "retailerId": 100
    }
  ]
}
```

---

## 2.10 — Danh sách thu khác (Surcharges)

**Phương thức:** `GET https://public.kiotapi.com/surcharges`

### Response

```json
{
  "total": 3,
  "pageSize": 20,
  "data": [
    {
      "id": 1,
      "code": "PHC01",
      "name": "Phí vận chuyển",
      "value": 30000,
      "isActive": true,
      "retailerId": 100
    }
  ]
}
```

---

## 2.13 — Nhóm khách hàng

**Phương thức:** `GET https://public.kiotapi.com/customergroups`

### Response

```json
{
  "total": 3,
  "pageSize": 20,
  "data": [
    {
      "id": 1,
      "name": "Khách VIP",
      "discount": 5.0,
      "retailerId": 100,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00"
    }
  ]
}
```

---

## 2.14 — Sổ quỹ (Cash Book)

**Phương thức:** `GET https://public.kiotapi.com/cashbooks`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `branchId` | int? | ID chi nhánh |
| `fromDate` | datetime? | Từ ngày |
| `toDate` | datetime? | Đến ngày |
| `pageSize` | int | Số items/trang |
| `currentItem` | int | Lấy từ bản ghi thứ N |

### Response

```json
{
  "total": 50,
  "pageSize": 20,
  "data": [
    {
      "id": 1,
      "code": "PT001",
      "type": 1,
      "typeName": "Thu",
      "amount": 25000000,
      "description": "Thu tiền hóa đơn HD001",
      "branchId": 1,
      "branchName": "Chi nhánh 1",
      "createdDate": "2024-01-01T10:00:00",
      "retailerId": 100
    }
  ]
}
```

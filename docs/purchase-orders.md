# Purchase Orders (Phiếu nhập hàng) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.15 — Phiếu nhập hàng

---

## 2.15.1 — Lấy danh sách phiếu nhập

**Phương thức:** `GET https://public.kiotapi.com/purchaseorders`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `branchIds` | int[]? | ID chi nhánh |
| `supplierIds` | long[]? | ID nhà cung cấp |
| `status` | int[]? | Tình trạng phiếu nhập |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật từ |
| `toDate` | datetime? | Thời gian đến |
| `pageSize` | int? | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |
| `orderBy` | string | Sắp xếp theo trường |
| `orderDirection` | string | `Asc` hoặc `Desc` |

### Response

```json
{
  "total": 20,
  "pageSize": 20,
  "data": [
    {
      "id": 30001,
      "code": "PN001",
      "purchaseDate": "2024-01-01T10:00:00",
      "branchId": 1,
      "branchName": "Chi nhánh 1",
      "supplierId": 200,
      "supplierCode": "NCC001",
      "supplierName": "Nhà cung cấp A",
      "discount": 0,
      "total": 20000000,
      "totalPayment": 20000000,
      "status": 2,
      "statusValue": "Đã nhập hàng",
      "description": "Nhập hàng tháng 1",
      "retailerId": 100,
      "modifiedDate": "2024-01-01T10:00:00",
      "createdDate": "2024-01-01T10:00:00",
      "purchaseOrderDetails": [
        {
          "productId": 1001,
          "productCode": "SP001",
          "productName": "iPhone 15",
          "quantity": 10.0,
          "price": 20000000,
          "discount": 0
        }
      ]
    }
  ]
}
```

---

## 2.15.2 — Lấy chi tiết phiếu nhập

**Phương thức:**
- Theo ID: `GET https://public.kiotapi.com/purchaseorders/{id}`
- Theo Code: `GET https://public.kiotapi.com/purchaseorders/code/{code}`

---

## 2.16 — Nhà cung cấp (Suppliers)

**Phương thức:** `GET https://public.kiotapi.com/suppliers`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `code` | string | Mã nhà cung cấp |
| `name` | string | Tên nhà cung cấp |
| `contactNumber` | string | Số điện thoại |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật |
| `pageSize` | int | Số items/trang |
| `currentItem` | int | Lấy từ bản ghi thứ N |

### Response

```json
{
  "total": 10,
  "pageSize": 20,
  "data": [
    {
      "id": 200,
      "code": "NCC001",
      "name": "Nhà cung cấp A",
      "contactNumber": "0901234567",
      "email": "ncc@example.com",
      "address": "456 Nguyễn Trãi, TP.HCM",
      "organization": "Công ty A",
      "taxCode": "0123456789",
      "comment": "NCC chính",
      "retailerId": 100,
      "debt": 0,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00"
    }
  ]
}
```

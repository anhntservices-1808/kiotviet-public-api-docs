# Products (Hàng hóa) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.4.1 — Lấy danh sách hàng hóa

**Phương thức:** `GET https://public.kiotapi.com/products`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `orderBy` | string? | Sắp xếp theo trường (Ví dụ: `Name`) |
| `orderDirection` | string? | `Asc` (mặc định) hoặc `Desc` |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật |
| `pageSize` | int | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |
| `includeInventory` | Boolean | Có lấy thông tin tồn kho? |
| `includePricebook` | Boolean | Có lấy thông tin bảng giá? |
| `IncludeSerials` | Boolean | Lấy thông tin serial/IMEI |
| `IncludeBatchExpires` | Boolean | Lấy thông tin lô, hạn sử dụng |
| `includeWarranties` | Boolean | Lấy thông tin bảo hành |
| `masterUnitId` | long? | ID hàng hóa đơn vị cần filter |
| `masterProductId` | long? | ID hàng hóa cùng loại cần filter |
| `categoryId` | int? | ID nhóm hàng cần filter |
| `BranchIds` | []int | ID chi nhánh cần xem tồn kho |
| `includeRemoveIds` | bool | Có lấy danh sách ID bị xóa dựa trên lastModifiedFrom |
| `includeQuantity` | bool | Có lấy thông tin định mức tồn |
| `productType` | int? | Loại hàng hóa: `1`=combo, `2`=thông thường, `3`=dịch vụ |
| `includeMaterial` | bool | Có lấy danh sách hàng thành phần |
| `isActive` | bool? | Hàng đang kinh doanh |
| `name` | string | Tìm kiếm theo tên hàng hóa |
| `includeSoftDeletedAttribute` | bool | Lấy thuộc tính đã xóa mềm (mặc định `true`) |
| `tradeMarkId` | int? | ID thương hiệu cần filter |
| `IncludeProductShelves` | boolean? | Có lấy thông tin vị trí sản phẩm |

### Response

```json
{
  "removeId": [],
  "total": 100,
  "pageSize": 20,
  "data": [
    {
      "id": 1001,
      "code": "SP001",
      "barCode": "8935001234567",
      "retailerId": 100,
      "allowsSale": true,
      "name": "iPhone 15",
      "categoryId": 5,
      "categoryName": "Điện thoại",
      "tradeMarkId": 10,
      "tradeMarkName": "Apple",
      "fullName": "iPhone 15 - 256GB - Xanh",
      "description": "Mô tả sản phẩm",
      "hasVariants": true,
      "attributes": [
        {
          "productId": 1001,
          "attributeName": "Dung lượng",
          "attributeValue": "256GB"
        }
      ],
      "unit": "Cái",
      "masterUnitId": null,
      "masterProductId": null,
      "conversionValue": 1.0,
      "units": [],
      "images": [],
      "inventories": [
        {
          "productId": 1001,
          "productCode": "SP001",
          "productName": "iPhone 15",
          "branchId": 1,
          "branchName": "Chi nhánh 1",
          "onHand": 50.0,
          "cost": 20000000,
          "onOrder": 0,
          "reserved": 5.0,
          "minQuality": 10,
          "maxQuality": 100
        }
      ],
      "priceBooks": [
        {
          "priceBookId": 1,
          "priceBookName": "Bảng giá chung",
          "productId": 1001,
          "isActive": true,
          "startDate": null,
          "endDate": null,
          "price": 25000000
        }
      ],
      "productFormulas": [],
      "productSerials": [],
      "productBatchExpires": [],
      "productWarranties": [],
      "basePrice": 25000000,
      "weight": 0.174,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00",
      "orderTemplate": "",
      "minQuantity": 10,
      "maxQuantity": 100,
      "productShelves": [],
      "taxType": "khau_tru",
      "taxRate": "10",
      "taxRateDirect": null,
      "productTaxs": [],
      "purchaseTax": null
    }
  ]
}
```

---

## 2.4.2 — Lấy chi tiết hàng hóa

**Phương thức:**
- Theo ID: `GET https://public.kiotapi.com/products/{id}`
- Theo Code: `GET https://public.kiotapi.com/products/code/{code}`
- Kèm thuộc tính đã xóa mềm: `GET https://public.kiotapi.com/products/{id}?includeSoftDeletedAttribute=true`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `id` | long | ID hàng hóa |
| `code` | string | Mã hàng hóa |
| `includeSoftDeletedAttribute` | bool | Lấy cả thuộc tính đã xóa mềm |

---

## 2.4.3 — Tạo mới hàng hóa

**Phương thức:** `POST https://public.kiotapi.com/products`

### Request Body

```json
{
  "name": "Tên hàng hóa",
  "code": "SP001",
  "barCode": "8935001234567",
  "fullName": "Tên đầy đủ",
  "categoryId": 5,
  "allowsSale": true,
  "description": "Mô tả",
  "hasVariants": false,
  "isProductSerial": false,
  "attributes": [
    {
      "attributeName": "Màu sắc",
      "attributeValue": "Đỏ"
    }
  ],
  "unit": "Cái",
  "masterProductId": null,
  "masterUnitId": null,
  "conversionValue": 1.0,
  "inventories": [
    {
      "branchId": 1,
      "branchName": "Chi nhánh 1",
      "onHand": 100.0,
      "cost": 10000000
    }
  ],
  "basePrice": 15000000,
  "weight": 0.5,
  "images": ["https://example.com/image.jpg"],
  "productTaxs": [{"taxId": 4}],
  "purchaseTax": {"taxId": 4}
}
```

### Response

Trả về object hàng hóa vừa tạo với đầy đủ thông tin.

---

## 2.4.4 — Cập nhật hàng hóa

**Phương thức:** `PUT https://public.kiotapi.com/products/{id}`

### Request

Path: `id` (long) — ID hàng hóa

Query: `branchId` (int) — ID chi nhánh hiện tại

### Request Body

```json
{
  "name": "Tên mới",
  "code": "SP001",
  "barCode": "8935001234567",
  "categoryId": 5,
  "allowsSale": true,
  "description": "Mô tả mới",
  "hasVariants": false,
  "attributes": [],
  "unit": "Cái",
  "masterUnitId": null,
  "conversionValue": 1,
  "inventories": [],
  "basePrice": 16000000,
  "weight": 0.5,
  "isActive": true,
  "isRewardPoint": true,
  "productTaxs": [{"taxId": 4}],
  "purchaseTax": {"taxId": 4}
}
```

---

## 2.4.5 — Xóa hàng hóa

**Phương thức:** `DELETE https://public.kiotapi.com/products/{id}`

### Request

Path: `id` (long) — ID hàng hóa

### Response (200 OK)

```json
{
  "message": "Xóa dữ liệu thành công"
}
```

---

## 2.4.6 — Lấy toàn bộ thuộc tính sản phẩm

**Phương thức:** `GET https://public.kiotapi.com/attributes/allwithdistinctvalue`

### Response

```json
[
  {
    "name": "Màu sắc",
    "id": 1,
    "attributeValues": [
      {"value": "Đỏ", "attributeId": 1},
      {"value": "Xanh", "attributeId": 1}
    ]
  }
]
```

---

## 2.4.7 — Tạo mới danh sách hàng hóa (Bulk)

**Phương thức:** `POST https://public.kiotapi.com/listaddproducts`

### Request Body

```json
{
  "listProducts": [
    {
      "name": "Sản phẩm 1",
      "code": "SP001",
      "categoryId": 5,
      "allowsSale": true,
      "hasVariants": false,
      "unit": "Cái",
      "basePrice": 10000000
    }
  ]
}
```

### Response

```json
{
  "message": "Thêm mới danh sách sản phẩm thành công"
}
```

---

## 2.4.8 — Cập nhật danh sách hàng hóa (Bulk)

**Phương thức:** `PUT https://public.kiotapi.com/listupdatedproducts`

### Request Body

```json
{
  "listProducts": [
    {
      "id": 1001,
      "name": "Sản phẩm 1",
      "code": "SP001",
      "categoryId": 5,
      "allowsSale": true,
      "basePrice": 11000000
    }
  ]
}
```

### Response

```json
{
  "message": "Cập nhật danh sách sản phẩm thành công"
}
```

---

## 2.4.9 — Lấy thông tin tồn kho (productOnHands)

**Phương thức:** `GET https://public.kiotapi.com/productOnHands`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `orderBy` | string? | Sắp xếp (Ví dụ: `Code`) |
| `lastModifiedFrom` | datetime? | Thời gian cập nhật |
| `branchIds` | [int] | Danh sách chi nhánh |
| `pageSize` | int | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N |

### Response

```json
{
  "total": 50,
  "pageSize": 20,
  "data": [
    {
      "id": 1001,
      "code": "SP001",
      "createdDate": "2023-01-01T00:00:00",
      "modifiedDate": "2024-01-01T00:00:00",
      "inventories": [
        {
          "branchId": 1,
          "onhand": 50.0,
          "reserved": 5.0
        }
      ]
    }
  ]
}
```

---

## Ghi chú về Tax (Thuế)

### Thuế khấu trừ (`taxType = "khau_tru"`)

| TaxId | Giá trị |
|---|---|
| 1 | VAT 0% |
| 2 | VAT 5% |
| 3 | VAT 8% |
| 4 | VAT 10% |
| 5 | KCT |
| 12 | KKKNT |

### Thuế trực tiếp (`taxType = "truc_tiep"`)

| TaxId | Giá trị |
|---|---|
| 6 | VAT 1% |
| 7 | VAT 2% |
| 8 | VAT 3% |
| 9 | VAT 5% |
| 64 | 0% VAT 5% TNCN |
| 65 | 0% VAT 1.5% TNCN |
| 66 | 0% VAT 2% TNCN |

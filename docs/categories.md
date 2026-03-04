# Categories (Nhóm hàng hóa) — KiotViet Public API

**Base URL:** `https://public.kiotapi.com`

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

---

## 2.3.1 — Lấy danh sách nhóm hàng

Trả về toàn bộ danh mục hàng hóa. Danh sách sắp xếp theo bảng chữ cái (a-z).

- Tối đa 3 cấp nhóm hàng
- Không xóa nhóm cha khi còn nhóm con
- Không xóa nhóm con khi đang được sử dụng

**Phương thức:** `GET https://public.kiotapi.com/categories`

### Request Parameters

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `lastModifiedFrom` | datetime? | Thời gian cập nhật |
| `pageSize` | int? | Số items/trang, mặc định 20, tối đa 100 |
| `currentItem` | int | Lấy từ bản ghi thứ N, mặc định 0 |
| `orderBy` | string | Sắp xếp theo trường (Ví dụ: `name`) |
| `orderDirection` | string | `Asc` (mặc định) hoặc `Desc` |
| `hierachicalData` | Boolean | `true`: lấy theo cấp; `false`: list phẳng theo lastModifiedFrom |

### Response (khi `hierachicalData = true`)

```json
{
  "total": 10,
  "pageSize": 20,
  "data": [
    {
      "categoryId": 1,
      "parentId": null,
      "categoryName": "Điện thoại",
      "retailerId": 100,
      "hasChild": true,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00",
      "children": []
    }
  ],
  "removedIds": [],
  "timestamp": "2024-01-01T00:00:00"
}
```

### Response (khi `hierachicalData = false`)

```json
{
  "total": 10,
  "pageSize": 20,
  "data": [
    {
      "categoryId": 1,
      "parentId": null,
      "categoryName": "Điện thoại",
      "retailerId": 100,
      "hasChild": true,
      "modifiedDate": "2024-01-01T00:00:00",
      "createdDate": "2023-01-01T00:00:00"
    }
  ],
  "removedIds": [],
  "timestamp": "2024-01-01T00:00:00"
}
```

---

## 2.3.2 — Lấy chi tiết nhóm hàng theo ID

**Phương thức:** `GET https://public.kiotapi.com/categories/{id}`

### Request

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `id` | long | ID của nhóm hàng (path param) |

### Response

```json
{
  "data": {
    "categoryId": 1,
    "parentId": null,
    "categoryName": "Điện thoại",
    "retailerId": 100,
    "hasChild": true,
    "modifiedDate": "2024-01-01T00:00:00",
    "createdDate": "2023-01-01T00:00:00",
    "children": []
  }
}
```

---

## 2.3.3 — Tạo mới nhóm hàng

**Phương thức:** `POST https://public.kiotapi.com/categories`

### Request Body

```json
{
  "categoryName": "Tên nhóm hàng",
  "parentId": 5
}
```

| Tham số | Kiểu | Mô tả |
|---|---|---|
| `categoryName` | string | Tên nhóm hàng hóa (bắt buộc) |
| `parentId` | int | ID nhóm cha (nếu có, tối đa 3 cấp) |

### Response

```json
{
  "message": "Cập nhật dữ liệu thành công",
  "data": {
    "categoryId": 10,
    "parentId": 5,
    "categoryName": "Tên nhóm hàng",
    "retailerId": 100,
    "hasChild": false,
    "modifiedDate": "2024-01-01T00:00:00",
    "createdDate": "2024-01-01T00:00:00",
    "children": []
  }
}
```

---

## 2.3.4 — Cập nhật nhóm hàng

**Phương thức:** `PUT https://public.kiotapi.com/categories/{id}`

### Request

Path: `id` (long) — ID nhóm hàng

### Request Body

```json
{
  "parentId": 5,
  "categoryName": "Tên nhóm hàng mới"
}
```

### Response

```json
{
  "message": "Cập nhật dữ liệu thành công",
  "data": {
    "categoryId": 10,
    "parentId": 5,
    "categoryName": "Tên nhóm hàng mới",
    "retailerId": 100,
    "hasChild": false,
    "modifiedDate": "2024-01-01T00:00:00",
    "createdDate": "2023-01-01T00:00:00",
    "children": []
  }
}
```

---

## 2.3.5 — Xóa nhóm hàng

**Phương thức:** `DELETE https://public.kiotapi.com/categories/{id}`

### Request

Path: `id` (long) — ID nhóm hàng cần xóa

### Response (200 OK)

```json
{
  "message": "Xóa dữ liệu thành công"
}
```

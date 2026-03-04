# KiotViet Public API Documentation

> **⚠️ Unofficial Mirror** | Crawled from [kiotviet.vn](https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/) for AI coding agents & developers.
> All content © KiotViet. This repo is for reference only.

---

## 🇻🇳 Tiếng Việt

KiotViet Public API là REST API cho phép tích hợp và trao đổi dữ liệu giữa **KiotViet POS** và các nền tảng bên ngoài (website, thương mại điện tử, CRM, ERP...).

### Xác thực nhanh

1. Lấy `ClientId` và `client_secret` từ **Thiết lập cửa hàng → Thiết lập kết nối API**

2. Lấy Access Token:
```bash
curl -X POST https://id.kiotviet.vn/connect/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "scopes=PublicApi.Access&grant_type=client_credentials&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET"
```

3. Dùng token trong tất cả request:
```
Retailer: ten-gian-hang
Authorization: Bearer YOUR_ACCESS_TOKEN
```

---

## 🇺🇸 English

KiotViet Public API is a REST API for integrating and exchanging data between **KiotViet POS** and external platforms (websites, e-commerce, CRM, ERP...).

### Quick Authentication

1. Get `ClientId` and `client_secret` from **Store Settings → API Connection Settings**

2. Get Access Token:
```bash
curl -X POST https://id.kiotviet.vn/connect/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "scopes=PublicApi.Access&grant_type=client_credentials&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET"
```

3. Use token in all requests:
```
Retailer: your-store-name
Authorization: Bearer YOUR_ACCESS_TOKEN
```

---

## API Reference

| Section | File | Description |
|---|---|---|
| 🔐 Authentication | [docs/authentication.md](docs/authentication.md) | OAuth 2.0, lấy token, headers bắt buộc |
| 📦 Categories | [docs/categories.md](docs/categories.md) | Nhóm hàng hóa (CRUD) |
| 🛍️ Products | [docs/products.md](docs/products.md) | Hàng hóa, tồn kho, thuộc tính (CRUD) |
| 📋 Orders | [docs/orders.md](docs/orders.md) | Đặt hàng (CRUD) |
| 🧾 Invoices | [docs/invoices.md](docs/invoices.md) | Hóa đơn (CRUD) |
| 👥 Customers | [docs/customers.md](docs/customers.md) | Khách hàng (CRUD) |
| 📦 Purchase Orders | [docs/purchase-orders.md](docs/purchase-orders.md) | Phiếu nhập hàng + Nhà cung cấp |
| 🔔 Webhooks | [docs/webhooks.md](docs/webhooks.md) | Webhooks real-time events |
| 🏪 Branches & Users | [docs/branches-users-misc.md](docs/branches-users-misc.md) | Chi nhánh, người dùng, ngân hàng, nhóm KH |

---

## Base URLs

| Service | URL |
|---|---|
| **API Base** | `https://public.kiotapi.com` |
| **Auth** | `https://id.kiotviet.vn/connect/token` |

---

## Key Rules & Limits

- **Rate Limit:** GET APIs — 5,000 requests/hour
- **Token Expiry:** 86,400 seconds (24 hours)
- **Pagination:** `pageSize` (max 100) + `currentItem`
- **Required Headers:** `Retailer` + `Authorization: Bearer {token}`
- **Product Types:** `1`=Combo, `2`=Standard, `3`=Service
- **Tax IDs (khấu trừ):** `1`=VAT 0%, `2`=VAT 5%, `3`=VAT 8%, `4`=VAT 10%, `5`=KCT, `12`=KKKNT
- **Tax IDs (trực tiếp):** `6`=VAT 1%, `7`=VAT 2%, `8`=VAT 3%, `9`=VAT 5%

---

## Supported Features

- ✅ Nhóm hàng hóa (Categories) — GET, POST, PUT, DELETE
- ✅ Hàng hóa (Products) — GET, POST, PUT, DELETE, Bulk add/update
- ✅ Tồn kho (Inventory) — GET
- ✅ Đặt hàng (Orders) — GET, POST, PUT, DELETE
- ✅ Hóa đơn (Invoices) — GET, POST, PUT, DELETE
- ✅ Khách hàng (Customers) — GET, POST, PUT, DELETE
- ✅ Phiếu nhập hàng (Purchase Orders) — GET
- ✅ Nhà cung cấp (Suppliers) — GET
- ✅ Chi nhánh (Branches) — GET
- ✅ Người dùng (Users) — GET
- ✅ Tài khoản ngân hàng (Bank Accounts) — GET
- ✅ Nhóm khách hàng (Customer Groups) — GET
- ✅ Sổ quỹ (Cash Book) — GET
- ✅ Thu khác / Phụ thu (Surcharges) — GET
- ✅ Webhooks — GET, POST, PUT, DELETE

---

## Official Documentation

- 📖 [KiotViet Public API Docs](https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/)
- 🏬 [KiotViet Website](https://www.kiotviet.vn)

---

## Disclaimer

This is an **unofficial mirror** of KiotViet's public documentation, created for use with AI coding agents (Context7, Cursor, Claude, etc.). All intellectual property belongs to KiotViet. For the most up-to-date and authoritative documentation, please refer to the official source.

*Crawled: March 2026*

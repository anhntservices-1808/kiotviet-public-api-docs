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
| 🔐 2.1–2.2 Authentication | [docs/authentication.md](docs/authentication.md) | OAuth 2.0, lấy token, headers bắt buộc |
| 🗂️ 2.3 Categories | [docs/categories.md](docs/categories.md) | Nhóm hàng hóa (CRUD) |
| 🛍️ 2.4 Products | [docs/products.md](docs/products.md) | Hàng hóa, tồn kho, thuộc tính (CRUD + bulk) |
| 📋 2.5 Orders | [docs/orders.md](docs/orders.md) | Đặt hàng (CRUD) |
| 👥 2.6 Customers | [docs/customers.md](docs/customers.md) | Khách hàng (CRUD + bulk) |
| 🏪 2.7–2.8 Branches & Users | [docs/branches.md](docs/branches.md) | Chi nhánh, người dùng |
| 🏦 2.9 Bank Accounts | [docs/bank-accounts.md](docs/bank-accounts.md) | Tài khoản ngân hàng |
| 💰 2.10 Surcharges | [docs/surcharges.md](docs/surcharges.md) | Thu khác / phụ thu (CRUD) |
| 🔔 2.11 Webhooks | [docs/webhooks.md](docs/webhooks.md) | Webhooks + real-time events (12 event types) |
| 🧾 2.12 Invoices | [docs/invoices.md](docs/invoices.md) | Hóa đơn (CRUD) |
| 👤 2.13 Customer Groups | [docs/customer-groups.md](docs/customer-groups.md) | Nhóm khách hàng |
| 📒 2.14 Cash Book | [docs/cash-book.md](docs/cash-book.md) | Sổ quỹ, thanh toán hóa đơn |
| 📦 2.15 Purchase Orders | [docs/purchase-orders.md](docs/purchase-orders.md) | Phiếu nhập hàng (CRUD) |
| 🚚 2.16 Transfers | [docs/transfers.md](docs/transfers.md) | Chuyển hàng giữa chi nhánh (CRUD) |
| 💲 2.17 Price Books | [docs/price-books.md](docs/price-books.md) | Bảng giá (GET + UPDATE) |
| 🛒 2.18 Sales Channels | [docs/sales-channels.md](docs/sales-channels.md) | Kênh bán hàng |
| 🔄 2.19 Returns | [docs/returns.md](docs/returns.md) | Trả hàng (GET) |
| 📥 2.20 Purchase Requisitions | [docs/purchase-requisitions.md](docs/purchase-requisitions.md) | Đặt hàng nhập (GET) |
| 📍 2.21 Locations | [docs/locations.md](docs/locations.md) | Danh sách Location |
| ⚙️ 2.22 Settings | [docs/settings.md](docs/settings.md) | Thiết lập cửa hàng |
| 🎫 2.23 Coupons | [docs/coupons.md](docs/coupons.md) | Cập nhật trạng thái Coupon |
| 🎟️ 2.24 Vouchers | [docs/vouchers.md](docs/vouchers.md) | Voucher (CRUD + phát hành + hủy) |
| 🏷️ 2.25 Brands | [docs/brands.md](docs/brands.md) | Thương hiệu |
| 🏭 2.26 Suppliers | [docs/suppliers.md](docs/suppliers.md) | Nhà cung cấp (GET) |
| 📄 Overview | [docs/overview.md](docs/overview.md) | Giới thiệu tổng quan, danh mục |

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

## Official Documentation

- 📖 [KiotViet Public API Docs](https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/)
- 🏬 [KiotViet Website](https://www.kiotviet.vn)

---

## Disclaimer

This is an **unofficial mirror** of KiotViet's public documentation, created for use with AI coding agents (Context7, Cursor, Claude, etc.). All intellectual property belongs to KiotViet. For the most up-to-date and authoritative documentation, please refer to the official source.

*Crawled: March 2026*

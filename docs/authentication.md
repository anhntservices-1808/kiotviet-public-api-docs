# Authentication — KiotViet Public API

**Source:** https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-ket-noi-api/public-api/

## 2.1 — Tổng quan xác thực

KiotViet API xác thực dựa trên cơ chế **OAuth 2.0**. Để kết nối, cần có 2 thông tin:
- `ClientId`
- `client_secret` (Mã bảo mật)

Lấy thông tin từ: **Thiết lập cửa hàng** (tài khoản admin) → **Thiết lập kết nối API**

### Thư viện OAuth theo ngôn ngữ

- **C#:** https://www.nuget.org/packages/OAuth2Client/
- **PHP:** https://github.com/thephpleague/oauth2-client

### Endpoints xác thực

| Endpoint | URL |
|---|---|
| Authorization Endpoint | `http://id.kiotviet.vn/connect/authorize` |
| Token Endpoint | `http://id.kiotviet.vn/connect/token` |

---

## 2.2 — Lấy Access Token

**Phương thức:** `POST https://id.kiotviet.vn/connect/token`

### Request Headers

```
Content-Type: application/x-www-form-urlencoded
```

### Request Body

```
scopes=PublicApi.Access&grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}
```

| Tham số | Giá trị |
|---|---|
| `scopes` | `PublicApi.Access` |
| `grant_type` | `client_credentials` |
| `client_id` | ClientId của cửa hàng |
| `client_secret` | Mã bảo mật của cửa hàng |

### Response

```json
{
  "access_token": "eyJhbGciOiJSU0...",
  "expires_in": 86400,
  "token_type": "Bearer"
}
```

> **Lưu ý:** `expires_in` = 86400 giây (24 giờ). Cần refresh token khi hết hạn.

---

## Header bắt buộc cho tất cả API (trừ lấy token)

```
Retailer: {tên_gian_hàng}
Authorization: Bearer {access_token}
```

**Ví dụ:**
```
Retailer: taphoaxyz
Authorization: Bearer eyJhbGciOiJSU0EtT0FFUCIsImVu...Z31gSjq6REOpMUj3hBYBojekzw
```

---

## Giới hạn tốc độ

- **GET APIs:** Giới hạn **5000 request/giờ**

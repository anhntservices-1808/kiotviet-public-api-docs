### **2.26. Nhà cung cấp**

#### **2.26.1. Lấy danh sách nhà cung cấp**

**– Mục đích sử dụng**: Trả về danh sách nhà cung cấp của cửa hàng.

**– Phương thức và URL: GET**[https://public.kiotapi.com/suppliers](https://internal.kiotapi.com/vouchercampaign "https://internal.kiotapi.com/vouchercampaign")

– **Request:** Sử dụng hàm GET với tham số

|  |
| --- |
| {    “pageSize”: int?, // Số bản ghi trong 1 trang, mặc định 20 bản ghi, tối đa 100 bản ghi    “currentItem”: int?, // Vị trí bắt đầu lấy dữ liệu, mặc định lấy từ bản ghi số 1    “orderDirection”: string?, // Sắp xếp kết quả trả về (Asc: tăng dần, mặc định | Desc: giảm dần)    “code”: string?, // Tìm kiếm theo mã nhà cung cấp    “name”: string?, // Tìm kiếm theo tên nhà cung cấp    “contactNumber”: string?, // Tìm kiếm theo điện thoại nhà cung cấp    “lastModifiedFrom”: datetime?, // Tìm kiếm theo khoảng thời gian cập nhật    “includeRemoveIds”: boolean?, // Có lấy thông tin danh sách ID nhà cung cấp bị xóa dựa trên modifiedDate    “includeTotal”: boolean?, // Có lấy thông tin totalInvoiced, totalInvoicedWithoutReturn    “includeSupplierGroup”: boolean? // Có lấy thông tin Groups  } |

– **Respones:**

|  |
| --- |
| {  “removedId”: int [], // Danh sách ID nhà cung cấp bị xóa dựa trên modifiedDate  “total”: int, // Tổng số nhà cung cấp    “pageSize”: int, // Số bản ghi trong 1 trang, mặc định 20 bản ghi, tối đa 100 bản ghi    “data”: [        {        “id”: long, // ID nhà cung cấp        “code”: string, // Mã nhà cung cấp        “name”: string, // Tên nhà cung cấp        “contactNumber”: string, // Điện thoại        “email”: string, // Email        “address”: string, // Địa chỉ        “locationName”: string, // Khu vực        “wardName”: string, // Phường xã        “organization”: strting, // Tên công ty        “taxCode”: string, // Mã số thuế        “comments”: string, // Ghi chú        “groups”: “string”, // Danh sách nhóm nhà cung cấp ngăn cách bởi dấu phẩy        “isActive”: boolean, // Trạng thái hoạt động (true: đang hoạt động | false: ngừng hoạt động)        “modifiedDate”: datetime, // Thời gian cập nhật thông tin nhà cung cấp gần nhất        “createdDate”: datetime, // Thời gian tạo nhà cung cấp        “retailerId”: long, // ID gian hàng        “branchId”: long, // ID chi nhánh tạo nhà cung cấp        “createdBy”: string, // Tên người tạo nhà cung cấp        “debt”: decimal, // Nợ cần trả hiện tại        “totalInvoiced”: decimal, // Tổng mua        “totalInvoicedWithoutReturn”: decimal // Tổng mua trừ trả hàng        }    ]  } |

#### **2.26.2. Lấy chi tiết nhà cung cấp**

**– Mục đích sử dụng**: Trả về thông tin chi tiết của 1 nhà cung cấp theo ID nhà cung cấp hoặc theo mã nhà cung cấp (code).

**– Phương thức và URL: GET**

- **Theo ID:** [https://public.kiotapi.com/suppliers/{id}](https://internal.kiotapi.com/vouchercampaign "https://internal.kiotapi.com/vouchercampaign")
- **Theo code:** [https://public.kiotapi.com/suppliers/{code}](https://internal.kiotapi.com/vouchercampaign "https://internal.kiotapi.com/vouchercampaign")

– **Request:** Sử dụng hàm GET với tham số

|  |
| --- |
| “id”: long // ID của nhà cung cấp  “code”: string // Mã của nhà cung cấp |

– **Response****:**

|  |
| --- |
| {  “id”: long, // ID nhà cung cấp    “code”: string, // Mã nhà cung cấp    “name”: string, // Tên nhà cung cấp    “contactNumber”: string, // Điện thoại    “email”: string, // Email    “address”: string, // Địa chỉ    “locationName”: string, // Khu vực    “wardName”: string, // Phường xã    “organization”: strting, // Tên công ty    “taxCode”: string, // Mã số thuế    “comments”: string, // Ghi chú    “groups”: “string”, // Danh sách nhóm nhà cung cấp ngăn cách bởi dấu phẩy    “isActive”: boolean, // Trạng thái hoạt động (true: đang hoạt động | false: ngừng hoạt động)    “modifiedDate”: datetime, // Thời gian cập nhật thông tin nhà cung cấp gần nhất    “createdDate”: datetime, // Thời gian tạo nhà cung cấp    “retailerId”: long, // ID gian hàng    “branchId”: long, // ID chi nhánh tạo nhà cung cấp    “createdBy”: string, // Tên người tạo nhà cung cấp    “debt”: decimal, // Nợ cần trả hiện tại    “totalInvoiced”: decimal, // Tổng mua    “totalInvoicedWithoutReturn”: decimal // Tổng mua trừ trả hàng  } |

***Cảm ơn bạn đã theo dõi bài viết!***

- Để tìm hiểu thêm về các nghiệp vụ quản lý bán hàng, mời bạn xem bài viết:
  [**Tổng quan Các nhóm Giải pháp của KiotViet**](https://www.kiotviet.vn/huong-dan-su-dung-kiotviet/retail-lam-quen-voi-kiotviet/tong-quan-cac-nhom-giai-phap-kiotviet/)
- Để tham khảo thêm các video hướng dẫn sử dụng, mời bạn theo dõi kênh YouTube:
  [**HDSD – Phần mềm KiotViet**](https://www.youtube.com/@HDSDPhanmemKiotViet)

***Chúc bạn kinh doanh hiệu quả cùng KiotViet!***

*Tài liệu được cập nhật mới nhất ngày 23/01/2026*

![]()

Đang tải ảnh...

### Mục lục

- [1. Giới thiệu](#heading-0)
- [2. Chức năng](#heading-1)
- [2.1. Authenticate](#heading-2)
- [2.2. Lấy thông tin Access Token](#heading-3)
- [2.3. Nhóm hàng](#heading-4)
- [2.3.1. Lấy danh sách nhóm hàng](#heading-5)
- [2.3.2. Lấy chi tiết nhóm hàng](#heading-6)
- [2.3.4. Cập nhật nhóm hàng](#heading-7)
- [2.3.5. Xóa nhóm hàng](#heading-8)
- [2.4. Hàng hóa](#heading-9)
- [2.4.1. Lấy danh sách hàng hóa](#heading-10)
- [2.4.2. Lấy chi tiết hàng hóa](#heading-11)
- [2.4.3. Thêm mới hàng hóa](#heading-12)
- [2.4.4. Cập nhật hàng hóa](#heading-13)
- [2.4.5. Xóa hàng hóa](#heading-14)
- [2.4.6. Lấy thông tin thuộc tính sản phẩm](#heading-15)
- [2.4.7. Thêm mới danh sách hàng hóa](#heading-16)
- [2.4.9. Lấy danh sách tồn kho hàng hóa](#heading-17)
- [2.5. Đặt hàng](#heading-18)
- [2.5.1. Lấy danh sách đặt hàng](#heading-19)
- [2.5.2. Lấy chi tiết đặt hàng](#heading-20)
- [2.5.3. Thêm mới đặt hàng](#heading-21)
- [2.5.4. Cập nhật đặt hàng](#heading-22)
- [2.5.5. Xóa đặt hàng](#heading-23)
- [2.6. Khách hàng](#heading-24)
- [2.6.1. Lấy danh sách khách hàng](#heading-25)
- [2.6.2. Lấy chi tiết khách hàng](#heading-26)
- [2.6.3. Thêm mới khách hàng](#heading-27)
- [2.6.4. Cập nhật khách hàng](#heading-28)
- [2.6.5. Xóa khách hàng](#heading-29)
- [2.6.6. Thêm mới danh sách khách hàng](#heading-30)
- [2.6.7. Cập nhật danh sách khách hàng](#heading-31)
- [2.7. Lấy danh sách chi nhánh](#heading-32)
- [2.8. Lấy danh sách người dùng](#heading-33)
- [2.9. Lấy danh sách tài khoản ngân hàng](#heading-34)
- [2.10. Thu khác](#heading-35)
- [2.10.1. Lấy danh sách thu khác](#heading-36)
- [2.10.2. Thêm mới thu khác](#heading-37)
- [2.10.3. Cập nhật thu khác](#heading-38)
- [2.10.4. Ngừng hoạt động thu khác](#heading-39)
- [2.11. Webhook](#heading-40)
- [2.11.1. Đăng ký Webhook](#heading-41)
- [2.11.2. Hủy đăng ký Webhook](#heading-42)
- [2.11.3. Khách hàng](#heading-43)
- [2.11.4. Hàng hóa](#heading-44)
- [2.11.5. Tồn kho](#heading-45)
- [2.11.6. Đặt hàng](#heading-46)
- [2.11.7. Hóa đơn](#heading-47)
- [2.11.8. Bảng giá](#heading-48)
- [2.11.9. Danh mục hàng hóa](#heading-49)
- [2.11.10. Chi nhánh](#heading-50)
- [2.11.11. Danh sách webhook](#heading-51)
- [2.11.12. Chi tiết webhook](#heading-52)
- [2.12. Hóa đơn](#heading-53)
- [2.12.1. Lấy danh sách hóa đơn](#heading-54)
- [2.12.2. Lấy chi tiết hóa đơn](#heading-55)
- [2.12.3. Thêm mới hóa đơn](#heading-56)
- [2.12.4. Cập nhật hóa đơn](#heading-57)
- [2.12.5. Xóa hóa đơn](#heading-58)
- [2.13. Nhóm khách hàng](#heading-59)
- [2.13.1. Lấy danh sách nhóm khách hàng](#heading-60)
- [2.14. Sổ quỹ](#heading-61)
- [2.14.1. Lấy danh sách sổ quỹ](#heading-62)
- [2.14.2. Thanh toán hóa đơn](#heading-63)
- [2.15. Nhập hàng](#heading-64)
- [2.15.1. Lấy danh sách nhập hàng](#heading-65)
- [2.15.2. Lấy chi tiết nhập hàng](#heading-66)
- [2.15.3. Thêm mới nhập hàng](#heading-67)
- [2.15.4. Cập nhật nhập hàng](#heading-68)
- [2.15.5. Xóa nhập hàng](#heading-69)
- [2.16. Chuyển hàng](#heading-70)
- [2.16.1. Lấy danh sách chuyển hàng](#heading-71)
- [2.16.2. Lấy chi tiết chuyển hàng](#heading-72)
- [2.16.3. Thêm mới chuyển hàng](#heading-73)
- [2.16.4. Cập nhật chuyển hàng](#heading-74)
- [2.16.5. Xóa phiếu chuyển hàng](#heading-75)
- [2.17. Bảng giá](#heading-76)
- [2.17.1. Lấy danh sách bảng giá](#heading-77)
- [2.17.2. Lấy chi tiết bảng giá](#heading-78)
- [2.17.3. Cập nhật chi tiết bảng giá](#heading-79)
- [2.18. Kênh bán hàng](#heading-80)
- [2.18.1. Lấy danh sách kênh bán hàng](#heading-81)
- [2.19. Trả hàng](#heading-82)
- [2.19.1. Lấy danh sách trả hàng](#heading-83)
- [2.19.2. Lấy chi tiết phiếu trả hàng](#heading-84)
- [2.20. Đặt hàng nhập](#heading-85)
- [2.20.1. Lấy danh sách đặt hàng nhập](#heading-86)
- [2.20.2. Lấy chi tiết đặt hàng nhập](#heading-87)
- [2.21. Lấy danh sách Location](#heading-88)
- [2.22. Thiết lập cửa hàng](#heading-89)
- [2.23. Cập nhật trạng thái Coupon](#heading-90)
- [2.24. Voucher](#heading-91)
- [2.24.1. Lấy danh sách đợt phát hành](#heading-92)
- [2.24.2. Lấy danh sách voucher trong đợt phát hành](#heading-93)
- [2.24.3. Tạo mới voucher](#heading-94)
- [2.24.4. Phát hành voucher](#heading-95)
- [2.24.5. Hủy voucher](#heading-96)
- [2.25. Thương hiệu](#heading-97)
- [2.25.1. Lấy danh sách thương hiệu](#heading-98)
- [2.26. Nhà cung cấp](#heading-99)
- [2.26.1. Lấy danh sách nhà cung cấp](#heading-100)
- [2.26.2. Lấy chi tiết nhà cung cấp](#heading-101)

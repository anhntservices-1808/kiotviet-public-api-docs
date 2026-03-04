### **2.10. Thu khác**

– Mô tả chi tiết cho các thông tin liên quan đến thu khác như sau:

#### **2.10.1. Lấy danh sách thu khác**

–**Mục đích sử dụng:** Trả lại toàn bộ danh sách thu khác của cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/surchages>

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“branchId”*: int?, // Id chi nhánh
*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int?,
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc,

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [  {  “id”: long, // Id thu khác   “surchargeCode”: string, // Mã thu khác  “surchargeName”: string, // Tên thu khác  “valueRatio”: double, // Phần trăm thu khác  “value”: decimal? // Giá trị thu khác  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime? // thời gian cập nhật  “createDate”: datetime  }]  } |

**Lưu ý*****:*** Hiện tại KiotViet hỗ trợ các thiết lập cho tính năng thu khác như sau:

 Trong trường hợp người dùng **không** tích chọn thiết lập “Hỗ trợ các khoản thu khác khi bán hàng”, khi gọi các API danh sách thu khác, API sẽ **trả lại** thông báo exception “Chưa bật thu khác trong thiết lập cửa hàng”.

#### **2.10.2. Thêm mới thu khác**

**–** **Mục đích sử dụng**: Thêm mới một thu khác

**– Phương thức và URL: POST** <https://public.kiotapi.com/surchages>

**– Request:** JSON mã hóa yêu cầu gồm 1 object nhóm hàng riêng biệt với nhưng tham số sau:

**– Body**

|  |
| --- |
| {                      “name”: string // tên thu khác                      “code”: string // mã thu khác (nếu không truyền lên, hệ thống sẽ tự động sinh mã code)                      “value”: decimal? // giá trị thu khác  } |

**– Response:**

|  |
| --- |
| {  “message”: “Thông tin thu khác được cập nhật thành công”,  “data”: {  “id”: long, // Id thu khác  “surchargeCode”: string, // Mã thu khác  “surchargeName”: string, // Tên thu khác  “valueRatio”: double, // Phần trăm thu khác  “value”: decimal? // Giá trị thu khác  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime? // thời gian cập nhật  “createDate”: datetime  }  } |

#### **2.10.3. Cập nhật thu khác**

**–** **Mục đích sử dụng**: Cập nhật một thu khác

**– Phương thức và URL: PUT** <https://public.kiotapi.com/surchages>/id

**–** **Request:** JSON mã hóa yêu cầu gồm 1 object nhóm hàng riêng biệt với nhưng tham số sau:

***“id”***: long // ID thu khác

**– Body**

|  |
| --- |
| {  “name”: string // tên thu khác  “code”: string // mã thu khác  “value”: decimal // giá trị thu khác  } |

**– Response:**

|  |
| --- |
| {  “message”: “Thông tin thu khác được cập nhật thành công”,  “data”: {  “id”: long, // Id thu khác  “surchargeCode”: string, // Mã thu khác  “surchargeName”: string, // Tên thu khác  “valueRatio”: double, // Phần trăm thu khác  “value”: decimal? // Giá trị thu khác  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime? // thời gian cập nhật  “createDate”: datetime  } |

#### **2.10.4. Ngừng hoạt động thu khác**

–**Mục đích sử dụng**: Ngừng/cho phép hoạt động 1 thu khác

**– Phương thức và URL: POST** <https://public.kiotapi.com/surchages>/id/activesurchage

**– Request:** JSON mã hóa yêu cầu gồm 1 object nhóm hàng riêng biệt với nhưng tham số sau:

***“id”:*** long // ID thu khác

**– Body:**

|  |
| --- |
| {  “isActive”: bool// true: cho phép hoạt động; false : ngừng hoạt động  } |

**– Response:**

|  |
| --- |
| {  “message”: “Cập nhật dữ liệu thành công”,  } |

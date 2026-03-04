### **2.7. Lấy danh sách chi nhánh**

**– Mục đích sử dụng**: Trả lại danh sách toàn bộ chi nhánh của cửa hàng đã được xác nhận

– **Phương thức và URL**: **GET** <https://public.kiotapi.com/branches>

– **Request:** Sử dụng hàm **GET** với tham số:

*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int?,
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc, *“includeRemoveIds”*: boolean, //Có lấy thông tin danh sách Id bị xoá dựa trên lastModifiedFrom

**– Response:**

|  |
| --- |
| {  “removedIds”: int [], // chi nhánh ngừng hoạt động  “total”: int,  “pageSize”: int,  “data”: [  {  “id”: int, // Id chi nhánh  “branchName”: string,  “branchCode”: string,  “contactNumber”: string,  “retailerId”: int, // Id cửa hàng  “email”: string,  “address”: string,  “modifiedDate”: datetime?  “createdDate”: datetime  }  “timestamp”: datetime  } |

### **2.8. Lấy danh sách người dùng**

–**Mục đích sử dụng**: Trả lại danh sách toàn bộ người dùng của cửa hàng đã được xác nhận và không cho thấy thông tin Super Admin (isAdmin = true).

**– Phương thức và URL: GET** <https://public.kiotapi.com/users>

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int?,
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc, *“includeRemoveIds”*: boolean //Có lấy thông tin danh sách Id bị xoá dựa trên lastModifiedFrom

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [  {  “id”: long, // ID người dùng  “userName”: string, // Tên đăng nhập  “givenName”: string, // Họ tên  “address”: string, // Địa chỉ  “mobilePhone”: string // Điện thoại  “email”: string, // Email  “description”: string, // ghi chú  “retailerId”: int, // Id cửa hàng  “birthDate”: date // Ngày sinh  “createdDate”: datetime  }],  “removeIds”: int [] // danh sách khách hàng bị xóa và ngừng hoạt động dựa trên ModifiedDate  } |

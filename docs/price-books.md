### **2.17. Bảng giá**

Mô tả chi tiết cho các API hỗ trợ Bảng giá như sau:

#### **2.17.1. Lấy danh sách bảng giá**

–**Mục đích sử dụng:** Trả về danh sách bảng giá

**– Phương thức và URL: GET** https://public.kiotapi.com/pricebooks

**– Request:** Sử dụng hàm **GET** với tham số:

*“includePriceBookBranch”*: Boolean, optional // Có lấy thông tin danh sách chi nhánh áp dụng bảng giá
*“includePriceBookCustomerGroups”*: Boolean, optional // Có lấy thông tin danh sách nhóm KH áp dụng bảng giá
*“includePriceBookUsers”*: Boolean, optional // Có lấy thông tin danh sách người dùng áp dụng bảng giá
*“orderBy”:* string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc
*“currentItem”*: int?,
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“lastModifiedFrom”*: datetime? // thời gian cập nhật

**– Response:**

|  |
| --- |
| {  “total”: int, tổng  “pageSize”: int, bao nhiêu dòng / 1 trang dữ liệu  “data”: [{  “id”: long // id bảng giá  “name”: string // tên bảng giá  “isActive”: boolean // trạng thái hoạt động hay không  “isGlobal”: boolean, // có phải là bảng giá chung không  “startDate”: datetime, // ngày bắt đầu áp dụng  “endDate”: datetime, // ngày hết hạn  “forAllCusGroup”: boolean // áp dụng cho tất cả nhóm khách hàng  “forAllUser”: boolean, // áp dụng cho tất cả user  “priceBookBranches” ://  [{  “id”: long, //Id quan hệ bảng giá – chi nhánh  “priceBookId”: long,//ID bảng giá “branchId”: long, //ID chi nhánh áp dụng  }],  “priceBookCustomerGroups” :// [{  “customerGroupName”: string,  “id”: long, //Id quan hệ bảng giá – nhóm khách hàng  “priceBookId”: long,//ID bảng giá  “customerGroupId”: long,//ID nhóm khách hàng  }],  “priceBookUsers” :[{  “userName”: string,//Tên người dùng  “id”: long, //Id quan hệ  “priceBookId”: long, //ID bảng giá  “userId”: long,//ID người dùng  }],  }]  } |

#### **2.17.2. Lấy chi tiết bảng giá**

**–** **Mục đích sử dụng**: Trả về thông tin chi tiết của bảng giá theo ID

**–** **Phương thức và URL**: theo Id : **GET** [https://public.kiotapi.com/pricebooks/{id}](https://public.kiotapi.com/pricebooks/%7bid%7d)

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“id”*: long // ID của bảng giá
*“orderBy”*:  string,  //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc
*“currentItem”*: int? // lấy dữ liệu từ bản ghi hiện tại, nếu không nhập thì mặc định là 0
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“lastModifiedFrom”*: datetime? // thời gian cập nhật

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items  “data”: [{  “productId”: long //ID của hàng hóa  “productCode”: string // code của hàng hóa  “price”: decimal // giá  }]} |

#### **2.17.3. Cập nhật chi tiết bảng giá**

**– Mục đích sử dụng**: Cập nhật thông tin giá bán của hàng hóa trong bảng giá

**– Phương thức và URL:** **POST** [https://public.kiotapi.com/pricebooks/](https://public.kiotapi.com/pricebooks/%7bid%7d)detail

**– Request:** Sử dụng hàm POST với tham số:

|  |
| --- |
| {      “pricebookId”: long, //ID của bảng giá, mặc định là 0 (Bảng giá chung)      “productId”: long, //ID của hàng hóa      “price”: decimal //Giá của hàng hóa  } |

**– Response:**

|  |
| --- |
| {      “message”: string, //Nội dung thông báo      “isSuccess”: boolean //Thành công không  } |

### **2.6. Khách hàng**

– Mô tả chi tiết cho các thông tin liên quan đến khách hàng như sau:

#### **2.6.1. Lấy danh sách khách hàng**

– **Mục đích sử dụng**: Trả lại danh sách khách hàng theo cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/customers>

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“code”*: string, optional // nếu có mã code, cho phép tìm kiếm khách hàng theo mã khách hàng
*“name”*: string, optional // tìm kiếm theo tên khách hàng
*“contactNumber”*: string, optional // tìm kiếm theo số điện thoại khách hàng
*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int?,
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc
*“includeRemoveIds”*: boolean, //Có lấy thông tin danh sách Id bị xoá dựa trên lastModifiedFrom
*“includeTotal”*: boolean, //Có lấy thông tin TotalInvoice, TotalPoint, TotalRevenue
*“includeCustomerGroup”*: boolean, //Có lấy thông tin nhóm khách hàng hay không
*“birthDate”*: string //filter khách hàng theo ngày sinh nhật
*“groupId”*: int, //filter theo nhóm khách hàng
*“includeCustomerSocial”*: boolean, // Có lấy thông tin Psid facebook fanpage của khách hàng hay không

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [  {  “id”: long, // ID khách hàng  “code”: string, // Mã khách hàng  “name”: string, // Tên khách hàng  “gender”: Boolean?, // Giới tính (true: nam, false: nữ)  “birthDate”: date?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “organization”: string, // Công ty  “comments”: string, // Ghi chú  “taxCode”: string, // Mã số thuế  “debt”: decimal, // Nợ hiện tại  “totalInvoiced”: decimal?, // Tổng bán  “totalPoint”: double?, // Tổng điểm  “totalRevenue”: decimal?,  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime? // thời gian cập nhật  “createdDate”: datetime,  “rewardPoint”: long?// Điểm hiện tại  “psidFacebook”: long?// Psid facebook fanpage  }],  “removeId”: int [] // danh sách Id khách hàng bị xóa dựa trên ModifiedDate  } |

#### **2.6.2. Lấy chi tiết khách hàng**

**– Mục đích sử dụng**: Trả lại thông tin chi tiết của khách hàng theo ID, theo Code

**– Phương thức và URL:**

- Theo Id : **GET** [https://public.kiotapi.com/customers/{id}](https://public.kiotapi.com/customers/%7bid%7d)
- Theo Code : **GET** [https://public.kiotapi.com/customers/code/{code}](https://public.kiotapi.com/customers/code/%7bcode%7d)

**– Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID của khách hàng
***“code”***: string // Mã của khách hàng

**– Response:**

|  |
| --- |
| {  “id”: long, // ID khách hàng  “code”: string, // Mã khách hàng  “name”: string, // Tên khách hàng  “gender”: Boolean?, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “organization”: string, // Công ty  “comments”: string, // Ghi chú  “taxCode”: string, // Mã số thuế  “retailerId”: int, // Id cửa hàng  “debt”: decimal, // Nợ hiện tại  “totalInvoiced”: decimal?, // Tổng bán  “totalPoint”: double?, // Tổng điểm  “totalRevenue”: decimal?,  “modifiedDate”: datetime? // thời gian cập nhật  “createdDate”: datetime  “groups”: string // danh sách tên nhóm khách hàng,  “rewardPoint”: long?// Điểm hiện tại  “psidFacebook”: long?// Psid facebook fanpage  } |

#### **2.6.3. Thêm mới khách hàng**

–**Mục đích sử dụng**: Tạo mới khách hàng

**– Phương thức và URL: POST** <https://public.kiotapi.com/customer>s

**–** **Request:** JSON mã hóa yêu cầu gồm 1 object khách hàng:

|  |
| --- |
| {  “code”: string, // Ma khach hang  “name”: string, // Tên khách hàng  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “subNumber”: string, // Số điện thoại khách hàng thứ hai  “IdentificationNumber”: string, // Số CCCD/CMND khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “comments”: string, // Ghi chú  “groupIds”: int[] // Danh sách Id nhóm khách hàng  “branchId”: int[] // ID chi nhánh tạo khách hàng  } |

**–  Response:**

|  |
| --- |
| {  “id”: long, // ID khách hàng (với id=-1 là bản ghi đầu tiên chứa thông tin tổng quan)  “code”: string, // Mã khách hàng  “name”: string, // Tên khách hàng  “type”: int, // Loại khách hàng ( 0 : Cá nhân, 1 : Công ty )  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “subNumber”: string, // Số điện thoại khách hàng thứ hai  “IdentificationNumber”: string, // Số CCCD/CMND khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “email”: string, // Email của khách hàng  “organization”: string, // Tên công ty của khách hàng (nếu là khách hàng công ty)  “comments”: string, // Ghi chú  “taxCode”: string, // Mã số thuế  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime?, // Thời gian cập nhật  “createdDate”: datetime  “customerGroupDetails”: [  {  “id”: long // Id Chi tiết nhóm khách hàng  “customerId”: long // Id khách hàng  “groupId”: int // Id nhóm khách hàng  }  ],  } |

#### **2.6.4. Cập nhật khách hàng**

– **Mục đích sử dụng**: Cập nhật thông tin khách hàng theo ID

**– Phương thức và URL: PUT** <https://public.kiotapi.com/customers/Id>

**– Request:** Sử dụng hàm PUT với ID khách hàng qua 1 object JSON.

***“id”***: long // ID khách hàng

**– Body**

|  |
| --- |
| {  “code”: string, // Mã khách hàng  “name”: string, // Tên khách hàng  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “subNumber”: string, // Số điện thoại khách hàng thứ hai  “IdentificationNumber”: string, // Số CCCD/CMND khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “comments”: string, // Ghi chú  “groupIds”: int[] // Danh sách Id nhóm khách hàng  “taxCode”: string // Mã số thuế  } |

**– Response:**

|  |
| --- |
| {  “id”: long, // ID khách hàng (với id=-1 là bản ghi đầu tiên chứa thông tin tổng quan)  “code”: string, // Mã khách hàng  “name”: string, // Tên khách hàng  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “subNumber”: string, // Số điện thoại khách hàng thứ hai  “IdentificationNumber”: string, // Số CCCD/CMND khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “email”: string, // Email của khách hàng  “organization”: string, // Tên công ty của khách hàng (nếu là khách hàng công ty)  “comments”: string, // Ghi chú  “taxCode”: string, // Mã số thuế  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime?, // Thời gian cập nhật  “createdDate”: datetime,  “groups”: string, // danh sách tên nhóm  } |

#### **2.6.5. Xóa khách hàng**

– **Mục đích sử dụng**: Xóa khách hàng theo ID

**– Phương thức và URL: DELETE** [https://public.kiotapi.com/customers/{id}](https://public.kiotapi.com/customers/%7bid%7d)

**–** **Request:** Gồm Id của khách hàng trong URL:

***“id”***: long // ID của khách hàng

**–** **Response:** Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

#### **2.6.6. Thêm mới danh sách khách hàng**

–**Mục đích sử dụng**: Thêm mới danh sách khách hàng

**– Phương thức và URL: POST** https://public.kiotapi.com/listaddcutomers

**–** **Request:** JSON mã hóa yêu cầu gồm 1 danh sách object khách hàng riêng biệt với nhưng tham số sau:

|  |
| --- |
| { “listCustomers”:[  {  “code”: string, // Ma khach hang  “name”: string, // Tên khách hàng  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “comments”: string, // Ghi chú  },  …]        } |

**– Response:**

|  |
| --- |
| {  “message”: “Thêm mới danh sách khách hàng thành công”  } |

#### **2.6.7. Cập nhật danh sách khách hàng**

– **Mục đích sử dụng**: Cập nhật danh sách khách hàng

**– Phương thức và URL: PUT** https://public.kiotapi.com/listupdatecustomers

**–** **Request:** JSON mã hóa yêu cầu gồm 1 danh sách object khách hàng riêng biệt với nhưng tham số sau:

|  |
| --- |
| { “listCustomers”:[ // danh sách khách hàng  {  “id”: long, //Id khách hàng  “code”: string, // Ma khach hang  “name”: string, // Tên khách hàng  “gender”: Boolean, // Giới tính (true: nam, false: nữ)  “birthDate”: datetime?, // Ngày sinh khách hàng  “contactNumber”: string, // Số điện thoại khách hàng  “address”: string, // Địa chỉ khách hàng  “locationName”: string, // Khu vực  “wardName”: string, // Phường xã  “email”: string, // Email của khách hàng  “comments”: string, // Ghi chú  },  …]        } |

**– Response:**

|  |
| --- |
| {  “message”: “Cập nhật danh sách khách hàng thành công”  } |

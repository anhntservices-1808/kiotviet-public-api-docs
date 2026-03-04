### **2.18. Kênh bán hàng**

Mô tả chi tiết cho các API hỗ trợ Kênh bán hàng như sau:

#### **2.18.1. Lấy danh sách kênh bán hàng**

**– Mục đích sử dụng**: Trả về danh sách hóa đơn theo cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/salechannel>

**– Request:** Sử dụng hàm **GET** với tham số:

*“orderBy”*:string,//Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc
*“currentItem”*: int?// lấy dữ liệu từ bản ghi hiện tại, nếu không nhập thì mặc định là 0
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“lastModifiedFrom”*: datetime? // thời gian cập nhật

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items  “data”: [{  “id”: long // Id kênh bán hàng  “name”: string // tên kênh bán hàng  “isActive”: boolean // còn sử dụng không  “img”: string // đường dẫn ảnh đại diện  “isNotDelete” : boolean // true = không thể xóa  }]} |

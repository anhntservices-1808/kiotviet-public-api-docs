### **2.9. Lấy danh sách tài khoản ngân hàng**

– **Mục đích sử dụng:** Trả lại toàn bộ danh sách tài khoản ngân hàng của cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/BankAccounts>

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int?,
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc, *“includeRemoveIds”*: boolean, //Có lấy thông tin danh sách Id bị xoá dựa trên lastModifiedFrom

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [  {  “id”: int, // ID tài khoản ngân hàng  “bankName”: string, // Tên tài khoản ngân hàng  “accountNumber”: string, // Số tài khoản ngân hàng  “description”: string, // ghi chú  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime? // thời gian cập nhật,  “createdDate”: datatime  }],  “removeIds”: int [] // danh sách khách hàng bị xóa dựa trên ModifiedDate  } |

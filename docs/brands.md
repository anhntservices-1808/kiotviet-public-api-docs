### **2.25. Thương hiệu**

#### **2.25.1. Lấy danh sách thương hiệu**

**– Mục đích sử dụng**: Trả về toàn bộ danh mục thương hiệu của hàng hóa. Danh sách này được sắp xếp theo thứ tự bảng chữ cái (a-z).

**– Phương thức và URL: GET**[https://public.kiotapi.com/trademark](https://internal.kiotapi.com/vouchercampaign "https://internal.kiotapi.com/vouchercampaign")

– **Request:** Sử dụng hàm GET với tham số

|  |
| --- |
| {                      “lastModifiedFrom”: datetime? // thời gian cập nhật                      “pageSize”: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items                      “currentItem”: int, // lấy dữ liệu từ bản ghi hiện tại, nếu không nhập thì mặc định là 0                      “orderBy”: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)                      “orderDirection”: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc  } |

– **Respones:**

|  |
| --- |
| {                      “total”: int, //tổng                      “pageSize”: int,                      “data”: [{                                           “tradeMarkId”: int, // ID thương hiệu                                           “tradeMarkName”: int, // ID thương hiệu                                           “createdDate”: datetime, // thời gian tạo thương hiệu                                           “modifiedDate”: datetime, // thời gian cập nhật thương hiệu, nếu chưa từng   cập nhật thì bằng thời gian tạo }]  } |

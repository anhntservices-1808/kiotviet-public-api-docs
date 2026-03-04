### **2.13. Nhóm khách hàng**

Mô tả chi tiết cho các API hỗ trợ Nhóm khách hàng như sau:

#### **2.13.1. Lấy danh sách nhóm khách hàng**

**–** **Mục đích sử dụng**: lấy danh sách nhóm khách hàng

**– Phương thức và URL**: **GET** <https://public.kiotapi.com/customers/group>

**– Response:**

|  |
| --- |
| {  “total”: int // Tổng danh sách nhóm  “data”: [  {  “id”: int // Id nhóm khách hàng  “name”: string // Tên nhóm khách hàng,  “description”: string // Ghi chú,  “createdDate”: DateTime // Ngày tạo,  “createdBy”: long // Id người tạo,  “retailerId”: int // Id chi nhánh,  “discount”: decimal? // Giảm giá,  “customerGroupDetails”: [  {  “id”: long // Id Chi tiết nhóm khách hàng  “customerId”: long // Id khách hàng  “groupId”: int // Id nhóm khách hàng  }  ]  }]  } |

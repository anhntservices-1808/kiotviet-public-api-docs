### **2.21. Lấy danh sách Location**

**–** **Mục đích sử dụng**: Trả về thông tin location

**– Phương thức và URL**: **GET** https://public.kiotapi.com/locations

**–** **Request:** Không có tham số

**–** **Response**

|  |
| --- |
| {  “total”: int,  “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items  “data”: [{  “id”: long, //Id location  “name”: string, //Tên location  “normalName”: string //Tên không dấu  }]  } |

### **2.22. Thiết lập cửa hàng**

**– Mục đích sử dụng**: Trả về danh sách thiết lập cửa hàng

**– Phương thức và URL: GET** https://public.kiotapi.com/settings

**–** **Request:** Sử dụng hàm **GET**

**– Response**

|  |
| --- |
| {  “ManagerCustomerByBranch” : bool, // Quản lí khách hàng theo chi nhánh  “AllowOrderWhenOutStock” : bool, // Cho phép đặt hàng khi hết tồn kho  “AllowSellWhenOrderOutStock” : bool, // Bán hàng, chuyển hàng khi sản phẩm đã được đặt hàng  “AllowSellWhenOutStock“: bool // Bán hàng, Chuyển hàng, Trả hàng nhập, Sản xuất, Xuất hủy khi hết tồn kho  } |

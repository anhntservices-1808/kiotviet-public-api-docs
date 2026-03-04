### **2.23. Cập nhật trạng thái Coupon**

– **Mục đích sử dụng**: Cập nhật trạng thái mã Coupon về “Đã sử dụng”

– **Phương thức và URL:** **POST** <https://public.kiotapi.com/coupons/setused>

– **Request:**Sử dụng hàm POST

– **Body:**

|  |
| --- |
| {    “coupons”:[{          “code”: “string”  //Mã coupon: require          }]   } |

**– Response:**

|  |
| --- |
| {      “message”: string, // nội dung thông báo      “dataError”:[{                          “code”: “string” // thông báo lỗi tương ứng                           }]  } |

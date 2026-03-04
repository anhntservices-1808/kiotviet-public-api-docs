### **2.14. Sổ quỹ**

Mô tả chi tiết cho các API hỗ trợ Sổ quỹ như sau:

#### **2.14.1. Lấy danh sách sổ quỹ**

–**Mục đích sử dụng**: Trả về danh sách phiếu thu chi trong sổ quỹ theo cửa hàng đã được xác nhận

**– Phương thức và URL: GET** https://public.kiotapi.com/cashflow

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“branchIds”*: int[], optional // ID chi nhánh
*“code”*: string[] //Danh sách mã code của phiếu
*“userId”*: long? //Id người tạo
*“accountId”*: int? //Tài khoản nhận
*“partnerType”*: srting //Loại người nộp/nhận: A: tất cả, C: khách hàng, S: nhà cung cấp, U: nhân viên, D: tối tác giao hàng, O: khác
*“method”*: string[] //Danh sách phương thức thanh toán
*“cashFlowGroupId”*: int?[] //Loại thu/chi
*“usedForFinancialReporting”*: int? //Lọc theo kết qua kinh doanh: 0: không hoạch toán, 1: đưa vào hoạch toán
*“partnerName”*: string //Tên người nộp/nhận
*“contactNumber”*: string//Số điện thoại người nộp/nhận
*“isReceipt”*: bool? //Theo phiếu thu/chi; True: thu, false: chi
*“includeAccount”*: bool //Lấy thông tin tài khoản ngân hàng hay không
*“includeBranch”*: bool? //Lấy tên chi nhánh hay không
*“includeUser”*: bool? //Lấy tên người tạo hay không
*“startDate”*: datetime? // thời gian bắt đầu
*“endDate”*: datetime? // thời gian kết thúc
*“status”*: int? // trạng thái phiếu; 0: Đã thanh toán, 1: Đã hủy, không truyền: tất cả
*“ids”*: long?[] // Id phiếu thu/chi
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [{  “id”: long //Id phiếu  “code”: string //Mã phiếu  “address”: string // Địa chỉ  “branchId”: int, //Id chi nhánh  “wardName”: string, //Tên phường  “contactNumber”: string, // Số điện thoại  “createdBy”: long // Id người tạo  “usedForFinancialReporting”: int,  “cashFlowGroupId”: int?, Id loại thu chi  “method”: string, // phương thức thanh toán  “partnerType”: string, // Người nộp/nhận  “partnerId”: long?, // Id người nộp/nhận  “status”: int, // trạng thái phiếu  “statusValue”: string, // trạng thái phiếu bằng chữ  “transDate”: datetime, //Ngày tạo  “amount”: decimal, // Giá trị  “partnerName”: string, //tên người nộp/nhận  “user”: string, // tên người tạo  “AccountId”:int? // Id tài khoản ngân hàng  “Description”:string //Ghi chú  }]  } |

#### **2.14.2. Thanh toán hóa đơn**

–**Mục đích sử dụng**: Thu tiền hóa đơn đơn nợ

– **Phương thức**: POST

– **URL**: https://public.kiotapi.com/payments

– **Request**:

|  |
| --- |
| {      “amount”: decimal, //Số tiền      “method”: string, //Phương thức thanh toán (Cash, Card, Transfer)      “accountId”: int?, optional //ID tài khoản ngân hàng, truyền nếu phương thức thanh toán là Card, Transfer       “invoiceId”: long //ID hóa đơn  } |

– **Response**: 

|  |
| --- |
| {      “paymentId”: int, //ID phiếu thanh toán      “paymentCode”: string, //Mã phiếu thanh toán      “amount”: decimal, //Số tiền      “method”: string, //Phương thức thanh toán (Cash, Card, Transfer)      “accountId”: int?, //ID số tài khoản ngân hàng, truyền nếu phương thức thanh toán là Card, Transfer      “invoiceId”: long, //ID hóa đơn      “DocumentCode”: long //Mã hóa đơn  } |

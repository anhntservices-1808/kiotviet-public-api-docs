### **2.15. Nhập hàng**

Mô tả chi tiết cho các API hỗ trợ Nhập hàng như sau:

#### **2.15.1. Lấy danh sách nhập hàng**

**–** **Mục đích sử dụng**: Trả về danh sách nhập hàng

**– Phương thức và URL: GET** https://public.kiotapi.com/purchaseorders

**–** **Request:** Sử dụng hàm **GET** với tham số sau:

*“branchIds”*: int[], optional // ID chi nhánh
*“status”*: int[], optional // Tình trạng đặt hàng
*“includePayment”*: Boolean, // có lấy thông tin thanh toán
*“includeOrderDelivery”*: Boolean,

“fromPurchaseDate”: “date”, optinal // từ ngày nhập hàng

“toPurchaseDate”: “date”, optinal // đến ngày nhập hàng
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items

“TaxIds”: int[], optional // ID thuế

**– Response:**

|  |
| --- |
| “total”: int, “pageSize”: int, “data”: [{  “id”: long //Id phiếu  “code”: string //Mã phiếu  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “purchaseDate”: datetime, // Ngày nhập hàng  “discountRatio”: long // Giảm giá phần trăm  “total”: int, // Giá trị nhập hàng “supplierId”: long, //Id nhà cung cấp  “supplierName”: string, // Tên nhà cung cấp  “supplierCode”: string, // Mã nhà cung cấp  “partnerType”: string, // Người nộp/nhận  “purchaseById”: long?, // Id người nhập  “purchaseName”: int, // tên người nhập  “totalTax”: “decimal?”, // Tổng thuế  “purchaseOrderDetails” :[{  “productId”: long, // Id hàng hóa  “ProductCode”: string, // mã hàng hóa  “productName”: string, // Tên hàng hóa  “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discount”: string,// Giảm giá  “serialNumbers”: string, // Danh sách imei  “productBatchExpire”: {  “id”: long, // Id lô  “productId” long, // ID sản phẩm  “batchName”: string, // Tên  “fullNameVirgule”: string, // Tên đầy đủ  “createdDate”: DateTime, // Ngày tạo lô  “expireDate”: DateTime // Ngày hết hạn lô  }  “purchaseOrderDetailTaxes”: [  {  “id”: “int”,  “detailId”: “long”, // ID chi tiết nhập hàng  “retailerId”: “int”, // ID gian hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?” // Giá trị thuế  }  ]  }  ]// Thông tin nhập hàng chi tiết  }  ]  } |

#### **2.15.2. Lấy chi tiết nhập hàng**

– **Mục đích sử dụng**: Trả lại chi tiết của một sản phẩm cụ thể theo ID

**– Phương thức và URL: GET** [https://public.kiotapi.com/purchaseorders/{id}](https://public.kiotapi.com/purchaseorders/%7bid%7d)

**–** **Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID của của nhập hàng

**– Response:**

|  |
| --- |
| {  “id”: long //Id phiếu  “retailerId”: long // Id shope  “code”: string //Mã phiếu  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “purchaseDate”: datetime, // Ngày nhập hàng  “discountRatio”: long // Giảm giá phần trăm  “total”: int, // Giá trị nhập hàng “supplierId”: long, //Id nhà cung cấp  “supplierName”: string, // Tên nhà cung cấp  “supplierCode”: string, // Mã nhà cung cấp  “partnerType”: string, // Người nộp/nhận  “purchaseById”: long?, // Id người nhập  “purchaseName”: int, // tên người nhập  “totalTax”: “decimal?”, // Tổng thuế  “purchaseOrderDetails”: [  {  “productId”: long, // Id hàng hóa  “ProductCode”: string, // mã hàng hóa  “productName”: string, // Tên hàng hóa  “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discount”: string,// Giảm giá  “serialNumbers”: string, // Danh sách imei  “productBatchExpire”: {  “id”: long, // Id lô  “productId” long, // ID sản phẩm  “batchName”: string, // Tên  “fullNameVirgule”: string, // Tên đầy đủ  “createdDate”: DateTime, // Ngày tạo lô  “expireDate”: DateTime // Ngày hết hạn lô  },  “purchaseOrderDetailTaxes”: [  {  “id”: “int”,  “detailId”: “long”, // ID chi tiết nhập hàng  “retailerId”: “int”, // ID gian hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?” // Giá trị thuế  }  ]  }  ]// Thông tin nhập hàng chi tiết  “payments” :[  {  “id”: long, // Id thanh toán  “code”: string, // mã thanh toán  “method”: string, // phương thức thanh toán  “status”: int, // trạng thái  “statusValue”: string, //tên trạng thái  “transDate”: DateTime,// ngày Thanh toán  }  ]// Thông tin thanh toán  } |

#### **2.15.3. Thêm mới nhập hàng**

**–** **Mục đích sử dụng:** Tạo mới phiếu nhập hàng

**– Phương thức và URL**: **POST** https://public.kiotapi.com/purchaseorders

**– Request:** JSON mã hóa yêu cầu gồm 1 object nhập hàng

|  |
| --- |
| {  “purchaseDate”: datetime,   // Ngày nhập hàng  “branchId”: int,   // Id chi nhánh  “supplier”: {  “code”: string,  “name”: string,  “contactNumber”: string,  “address”: string, “email”: string,  “comment”: string  }, // Thông tin Nhà cung cấp      “description”: string             //    Ghi chú phiếu nhập  “isDraft”: int                         //    Trạng thái của phiếu nhập  “discount”: decimal?           //    Số tiền giảm giá  “discountRatio”: double?    //    Phần trăm giảm giá  “paidAmount”: decimal,      //    Tiền trả trước cho NCC  “paymentMethod”: string,   //    Phương thức thanh toán cho NCC (Cash, Transfer, Card)  “accountId” : long              //     Id của tài khoản ngân hàng nếu phương thức thanh toán là TRANSFER, CARD (lấy thông tin từ https://public.kiotapi.com/BankAccounts)  “isApplyPurchaseTax”: “bool”, // Có áp dụng VAT nhập hàng hay không?  “surcharges” : [{  “code”: string,                        // Mã chi phí  “name”: string,                      // Tên chi phí  “value”: decimal?,                // Số tiền thu  “valueRatio”: decimal?,       // Phần trăm thu (nếu truyền cả 2 giá trị value và valueRatio thì sẽ lấy valueRatio)  “isSupplierExpense”: bool, // Hoàn lại khi trả hàng nhập  “type”: int,                           // Hình thức, chi phí nhập trả nhà cung cấp?  }] // Danh sách thu khác, bao gồm chi phí trả nhà cung cấp hoặc không trả nhà cung cấp.  “purchaseOrderDetails” :[{  “productCode”: string,              //  Mã hàng hóa  “description”: string,                //   Ghi chú  “quantity”: double,                 //    Số lượng hàng hóa  “price”: decimal,                   //     Giá nhập  “discount”: decimal?,          //      Giảm giá  “discountRatio”: double?,// Giảm giá  “productTax”: {  “taxId”: “int”, // ID thuế  “productId”: “long” // ID hàng hóa  }  ] // Thông tin nhập hàng chi tiết  } |

**– Response:**

|  |
| --- |
| {  “id”: long                 //   Id phiếu  “retailerId”: long    //    Id shop  “code”: string       //    Mã phiếu  “branchId”: int,    //    Id chi nhánh  “branchName”: string,            //    Tên chi nhánh  “purchaseDate”: datetime,    //     Ngày nhập hàng  “discount”: decimal              //      Số tiền giảm giá  “discountRatio”: long          //       Phần trăm giảm giá  “total”: int,                          //        Giá trị nhập hàng  “supplierId”: long,             //    Id nhà cung cấp  “supplierName”: string,    //    Tên nhà cung cấp  “supplierCode”: string,    //    Mã nhà cung cấp  “partnerType”: string,    //    Người nộp/nhận  “purchaseById”: long?,    //    Id người nhập  “purchaseName”: int,    //    Tên người nhập  “totalTax”: “decimal?”, // Tổng thuế  “purchaseOrderDetails” :[{  “productId”: long,    //   Id hàng hóa  “productCode”: string,    //    Mã hàng hóa  “productName”: string,    //    Tên hàng hóa  “quantity”: double,    //    Số lượng hàng hóa  “price”: decimal,    //    Giá nhập  “discount”: decimal, // Giảm giá  “discountRatio”: double?,// Giảm giá  “serialNumbers”: “string”, // Danh sách imei  “productBatchExpire”: {  “id”: “long”, // Id lô  “productId”: “long”, // ID sản phẩm  “batchName”: “string”, // Tên  “fullNameVirgule”: “string”, // Tên đầy đủ  “createdDate”: “DateTime”, // Ngày tạo lô  “expireDate”: “DateTime” // Ngày hết hạn lô  },  “purchaseOrderDetailTaxes”: [  {  “id”: “int”,  “detailId”: “long”, // ID chi tiết nhập hàng  “retailerId”: “int”, // ID gian hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?” // Giá trị thuế  }  ]  }  ] // Thông tin nhập hàng chi tiết “payments” :[{  “id”: long, // Id thanh toán  “code”: string, // Mã thanh toán  “method”: string,   // Phương thức thanh toán,  “amount”: decimal,  // Phương thức thanh toán,  “status”: int, // Trạng thái  “statusValue”: string, // Tên trạng thái  “transDate”: DateTime, // Ngày Thanh toán  }]// Thông tin thanh toán      } |

#### **2.15.4. Cập nhật nhập hàng**

**–** **Mục đích sử dụng:** Cập nhật phiếu nhập hàng theo ID

**– Phương thức và URL:** PUT https://public.kiotapi.com/purchaseorders/Id

**– Request:** Sử dụng hàm PUT với ID phiếu nhập hàng qua 1 object JSON.

***“id”***: long // ID phiếu nhập hàng

**– Body**

|  |
| --- |
| {  “purchaseDate”: datetime,   // Ngày nhập hàng  “branchId”: int,                      // Id chi nhánh  “supplier”: {  “code”: string,  “name”: string,  “contactNumber”: string,  “address”: string,  “email”: string,  “comment”: string  }, // Thông tin Nhà cung cấp  “description”: string    //    Ghi chú phiếu nhập  “isDraft”: int                //    Trạng thái của phiếu nhập  “discount”: decimal?  //    Số tiền giảm giá  “discountRatio”: double?    //    Phần trăm giảm giá  “paidAmount”: decimal,      //    Tiền trả trước cho NCC  “paymentMethod”: string,   //    Phương thức thanh toán cho NCC (Cash, Transfer, Card)  “accountId” : long    // Id của tài khoản ngân hàng nếu phương thức thanh toán là TRANSFER, CARD (lấy thông tin từ https://public.kiotapi.com/BankAccounts)  “isApplyPurchaseTax”: “bool”, // Có áp dụng VAT nhập hàng hay không?  “surcharges” : [{  “code”: string,    // Mã chi phí  “name”: string,    // Tên chi phí  “value”: decimal?,// Số tiền thu  “valueRatio”: decimal?,    // Phần trăm thu  “isSupplierExpense”: bool, // Hoàn lại khi trả hàng nhập  “type”: int,    // Hình thức, chi phí nhập trả nhà cung cấp?  }] // Danh sách thu khác, bao gồm chi phí trả nhà cung cấp hoặc không trả nhà cung cấp.  “purchaseOrderDetails” :[  {  “productCode”: string,    // Mã hàng hóa  “description”: string,    // Ghi chú  “quantity”: double,    // Số lượng hàng hóa  “price”: decimal,    // Giá nhập  “discount”: “decimal?”, // Số tiền giảm giá  “discountRatio”: “double?”, // Phần trăm giảm giá  “productTax”: {  “taxId”: “int”, // ID thuế  “productId”: “long” // ID hàng hóa  }  }  ] // Thông tin nhập hàng chi tiết  } |

**– Response:**

|  |
| --- |
| {  “id”: long    //    Id    phiếu  “retailerId”: long    //    Id    shop  “code”: string    //    Mã    phiếu  “branchId”: int,    //    Id    chi nhánh  “branchName”: string,    //    Tên chi nhánh  “purchaseDate”: datetime,    //    Ngày nhập hàng  “discount”: decimal    //    Số tiền giảm giá  “discountRatio”: long    //    Phần trăm giảm giá  “total”: int,    //    Giá trị nhập hàng  “supplierId”: long,    //    Id nhà cung cấp  “supplierName”: string,    //    Tên nhà cung cấp  “supplierCode”: string,    //    Mã nhà cung cấp  “partnerType”: string,    //    Người nộp/nhận  “purchaseById”: long?,    //    Id người nhập  “purchaseName”: int,    //    Tên người nhập  “totalTax”: decimal?,        // Tổng thuế  “purchaseOrderDetails” :[  {  “productId”: long,    //    Id hàng hóa  “productCode”: string,    //    Mã hàng hóa  “productName”: string,    //    Tên hàng hóa  “quantity”: double,    //    Số lượng hàng hóa  “price”: decimal,    //    Giá nhập  “discount”: decimal,    //    Giảm giá  “discountRatio”: double?,// Giảm giá  “serialNumbers”: string,    // Danh sách imei  “productBatchExpire”: {  “id”: long,               // Id lô  “productId”: long,        // ID sản phẩm  “batchName”: string,      // Tên  “fullNameVirgule”: string,// Tên đầy đủ  “createdDate”: DateTime,  // Ngày tạo lô  “expireDate”: DateTime    // Ngày hết hạn lô  },  “purchaseOrderDetailTaxes”: [  {  “id”: int,  “detailId”: long,       // ID chi tiết nhập hàng  “retailerId”: int,      // ID gian hàng  “taxId”: int,           // ID thuế  “detailTax”: decimal?   // Giá trị thuế  }  ]  }  ] // Thông tin nhập hàng chi tiết “payments” :[{  “id”: long, // Id thanh toán  “code”: string, // Mã thanh toán  “method”: string,    // Phương thức thanh toán,  “amount”: decimal,    // Phương thức thanh toán,  “status”: int,// Trạng thái  “statusValue”: string, // Tên trạng thái  “transDate”: DateTime, // Ngày Thanh toán  }]// Thông tin thanh toán  } |

#### **2.15.5. Xóa nhập hàng**

–**Mục đích sử dụng:** Xóa đơn đặt hàng theo ID

**– Phương thức và URL:** DELETE https://public.kiotapi.com/purchaseorders?id={Id}&IsVoidPayment=true

**– Request:** Gồm Id của phiếu nhập hàng trong URL**:**

***“id”***: long // ID của phiếu nhập hàng
***“IsVoidPayment”*:** bool // Hủy phiếu thanh toán, nếu không truyền tham số này thì mặc định không hủy phiếu thanh toán gắn kèm đặt hàng

**– Response:**

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

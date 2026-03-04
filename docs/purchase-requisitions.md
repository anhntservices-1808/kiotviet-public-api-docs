### **2.20. Đặt hàng nhập**

Mô tả chi tiết cho các API hỗ trợ Đặt hàng nhập như sau:

#### **2.20.1. Lấy danh sách đặt hàng nhập**

**– Mục đích sử dụng**: Trả về danh sách đặt hàng nhập

**– Phương thức và URL: GET** https://public.kiotapi.com/ordersuppliers

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“branchId”*: int? // Id chi nhánh
*“status”*: int? // Trạng thái đặt hàng nhập
*“productKey”*: string, //Mã nhập hàng
*“supplierKey”*: string, // Mã nhà cung cấp
*“userNamKey”*: string, // Mã người tạo
*“userNamCreatedKey”*: string, // Mã người đặt
*“expensesOthersIds”*: string, // Chi phí nhập trả nhà cung cấp
*“descriptionKey”*: string, // Ghi chú
*“codeKey”*: string, // Mã phiếu đặt hàng nhập
*“purchaseOrderCode”*: string, // Mã phiếu nhập hàng

**– Response**

|  |
| --- |
| {  “total”: int,  “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items  “data”: [{  “id”: long, //Id nhập hàng  “code”: string, //Mã đặt hàng  “invoiceId”: long?,//Id nhập hàng  “orderDate”: datetime, // Ngày đặt  “branchId”: int, //Id chi nhánh  “retailerId”: int, //Id cửa hàng  “userId”: long, //Id người dùng  “description”: string, // Ghi chú  “status”: int, // Trạng thái  “discountRatio”: string, // Giảm giá theo %  “productQty”: double?, // Số lương  “discount”: decimal?,// Giảm giá  “createdDate”: datetime, // Ngày tạo  “createdBy”: long, // Id người tạo  “totalTax”: “decimal?”, // Tổng thuế  “orderSupplierDetails”: [  {  “id”: long,  “orderSupplierId”: long,  “productId”: long,  “quantity”: double,  “price”: decimal,  “discount”: decimal,  “allocation”: decimal,  “createdDate”: datime,  “description”: string,  “orderByNumber”: int?,  “allocationSuppliers”: decimal?,  “allocationThirdParty”: decimal?,  “orderQuantity”: double,  “subTotal”: decimal,  “orderSupplierDetailTaxes”: [  {  “id”: “int”,  “detailId”: “long”, // ID chi tiết đặt hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?” // Giá trị thuế chi tiết  }  ]  }  ],  “OrderSupplierExpensesOthers”:[  {  “id”:  long,  “form”:  int?,  “expensesOtherOrder”:  byte?,  “expensesOtherCode”:  string,  “expensesOtherName”:  string,  “expensesOtherId”:  int,  “orderSupplierId”:  long?,  “price”:  decimal,  “isReturnAuto”:  bool?,  “exValue”:  decimal?,  “createdDate”:  datetime  }  ],  “total”: decimal,  “exReturnSuppliers”: decimal?,  “exReturnThirdParty”: decimal?,  “totalAmt”: decimal?,  “totalQty”: double?,  “totalQuantity”: double,  “subTotal”: decimal,  “paidAmount”: decimal,  “toComplete”: bool,  “statusValue”: string,  “viewPrice”: bool,  “supplierDebt”: decimal,  “supplierOldDebt”: decimal,  “purchaseOrderCodes”: string,  “supplierId”: int?,//ID nhà cung cấp  “supplierCode”: string,//Mã nhã cung cấp do người dùng tạo  “supplierName”: string//Tên nhà cung cấp  }  ]  } |

#### **2.20.2. Lấy chi tiết đặt hàng nhập**

**–** **Mục đích sử dụng**: Trả về thông tin chi tiết của phiếu đặt hàng nhập

**– Phương thức và URL**: **GET** https://public.kiotapi.com/ordersuppliers/ {id}

**–** **Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID đặt hàng nhập

– **Response**

|  |
| --- |
| {     “total”: “int”,     “pageSize”: “int”, // Số items trong 1 trang, mặc định 20 items, tối đa 100 items     “data”: [         {             “id”: “long”, // Id nhập hàng             “code”: “string”, // Mã đặt hàng             “invoiceId”: “long?”, // Id nhập hàng             “orderDate”: “datetime”, // Ngày đặt             “branchId”: “int”, // Id chi nhánh             “retailerId”: “int”, // Id cửa hàng             “userId”: “long”, // Id người dùng             “description”: “string”, // Ghi chú             “status”: “int”, // Trạng thái             “discountRatio”: “string”, // Giảm giá theo %             “productQty”: “double?”, // Số lượng             “discount”: “decimal?”, // Giảm giá             “createdDate”: “datetime”, // Ngày tạo             “createdBy”: “long”, // Id người tạo             “totalTax”: “decimal?”, // Tổng thuế             “orderSupplierDetails”: [                 {                     “id”: “long”,                     “orderSupplierId”: “long”,                     “productId”: “long”,                     “quantity”: “double”,                     “price”: “decimal”,                     “discount”: “decimal”,                     “allocation”: “decimal”,                     “createdDate”: “datetime”,                     “description”: “string”,                     “orderByNumber”: “int?”,                     “allocationSuppliers”: “decimal?”,                     “allocationThirdParty”: “decimal?”,                     “orderQuantity”: “double”,                     “subTotal”: “decimal”,                     “orderSupplierDetailTaxes”: [                         {                             “id”: “int”,                             “detailId”: “long”, // ID chi tiết đặt hàng                             “taxId”: “int”, // ID thuế                             “detailTax”: “decimal?” // Giá trị thuế chi tiết                         }                     ]                 }             ],             “orderSupplierExpensesOthers”: [                 {                     “id”: “long”,                     “form”: “int?”,                     “expensesOtherOrder”: “byte?”,                     “expensesOtherCode”: “string”,                     “expensesOtherName”: “string”,                     “expensesOtherId”: “int”,                     “orderSupplierId”: “long?”,                     “price”: “decimal”,                     “isReturnAuto”: “bool?”,                     “exValue”: “decimal?”,                     “createdDate”: “datetime”                 }             ],             “total”: “decimal”,             “exReturnSuppliers”: “decimal?”,             “exReturnThirdParty”: “decimal?”,             “totalAmt”: “decimal?”,             “totalQty”: “double?”,             “totalQuantity”: “double”,             “subTotal”: “decimal”,             “paidAmount”: “decimal”,             “toComplete”: “bool”,             “statusValue”: “string”,             “viewPrice”: “bool”,             “supplierDebt”: “decimal”,             “supplierOldDebt”: “decimal”,             “purchaseOrderCodes”: “string”,            “supplierId”: int?,//ID nhà cung cấp           “supplierCode”: string,//Mã nhã cung cấp do người dùng tạo           “supplierName”: string//Tên nhà cung cấp         }     ]  } |

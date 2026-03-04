### **2.12. Hóa đơn**

Hiện tại KiotViet hỗ trợ các thiết lập cho tính năng hóa đơn như sau:

– Trong trường hợp người dùng không tích chọn setting cho “Cho phép bán hàng khi hết tồn kho”, thì POST/PUT các API liên quan đến việc bán các sản phẩm đã hết tồn kho, trả lại thông báo “Thiết lập “Cho phép bán hàng khi hết tồn kho” đang không được bật”

– Trong trường hợp người dùng không tích chọn setting cho “Sử dụng tính năng giao hàng”, các giao dịch liên quan tới giao hàng sẽ không hiển thị trên kiotviet nữa. Vì vậy khi gọi các API liên quan tới phần giao hàng, cần trả lại thông báo “Thiết lập “Sử dụng tính năng giao hàng” đang không được bật”.

– Trong trường hợp người dùng tích chọn setting “Sử dụng ính năng giao hàng” nhưng không tích chọn setting cho “Quản lý thu hộ tiền”, các giao dịch liên quan tới thu hộ tiền sẽ không hiển thị trên kiotviet nữa. Vì vậy khi gọi các API liên quan tới phần thu hộ tiền, cần trả lại thông báo “Thiết lập “Quản lý thu hộ tiền” đang không được bật”.

– Trong trường hợp người dùng không tích chọn setting cho “Không cho phép thay đổi thời gian bán hàng”, khi Post/ Put các API liên quan thời gian bán hàng, trả lại thông báo “Thiết lập “Không cho phép thay đổi thời gian bán hàng” đang không được bật”.

Mô tả chi tiết cho các API hỗ trợ Hóa đơn như sau:

#### **2.12.1. Lấy danh sách hóa đơn**

–**Mục đích sử dụng**: Trả về danh sách hóa đơn theo cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/invoices>

**–** **Request:** Sử dụng hàm **GET** với tham số:

*“branchIds”*: int[], optional // ID chi nhánh
*“customerIds”*: long[], optional // Id khách hàng
*“customerCode”*: string //Mã khách hàng
*“status”*: int[], optional // Tình trạng đặt hàng
*“includePayment”*: Boolean, // có lấy thông tin thanh toán
 *“includeInvoiceDelivery”*: Boolean, //hóa đơn có giao hàng hay không
*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int,
*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“toDate”*: datetime? //Thời gian cập nhật cho đến thời điểm toDate
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc *“orderId”*: long?, // Lọc danh sách hóa đơn theo Id của đơn đặt hàng
*“createdDate”*: datetime? //Thời gian tạo
*“fromPurchaseDate”*: datetime? //Từ ngày giao dịch
*“toPurchaseDate”*: datetime? //Đến ngày giao dịch

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [{  “id”: long //Id đặt hàng  “code”: string //Mã đặt hàng  “purchaseDate”: datetime // Ngày đặt hàng  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “soldById”: long?,  “soldByName”: string  “customerId”: long?, // Id khách hàng  “customerCode”: string, Mã khách hàng  “customerName”: string, // Tên khách hàng  “total”: decimal, // Khách cần trả  “totalPayment”: decimal, //Khách đã trả  “status”: int, // trạng thái hóa đơn  “statusValue”: string, // trạng thái đơn đặt hàng bằng chữ  “usingCod”: boolean,  “createdDate”: datetime, //Ngày tạo  “modifiedDate”: datetime, //Ngày cập nhật  “totalTax”: decimal?,  “payments” :[{  “id”: long,  “code”: string,  “amount”: decimal,  “method”: string”,  “status”: byte?,  “statusValue”: string,  “transDate”: datetime,  “bankAccount”: string,  “accountId”: int?  }],  “invoiceOrderSurcharges”: [        {  “id”: long,  “invoiceId”:long?,  “surchargeId”: long?,  “surchargeName”: string,  “surValue”: decimal?,  “price”: decimal?,  “createdDate”: DateTime  }  ],  “invoiceDetails” :{  “productId”: long, // Id hàng hóa  “productCode”: string,  “productName”: string, //Tên hàng hóa  (bao gồm thuộc tính và đơn vị tính)  “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discountRatio”: double?, // Giảm giá trên sản phẩm theo %  “discount”: decimal?, // Giảm giá trên sản phẩm theo tiền  “note”: string // Ghi chú hàng hóa  “serialNumbers”: string, // Danh sách imei  “productBatchExpire”: {  “id”: long, // Id lô  “productId” long, // ID sản phẩm  “batchName”: string, // Tên  “fullNameVirgule”: string, // Tên đầy đủ  “createdDate”: DateTime, // Ngày tạo lô  “expireDate”: DateTime // Ngày hết hạn lô  }  “invoiceDetailTaxs”: [  {  “id”: “int”,  “detailId”: “long”,  “detailTax”: “decimal?”,  “taxId”: “int”,  “name”: “string”,  “value”: “decimal?”  }  ]  }  ],  “SaleChannel”:{  “IsNotDelete”: bool,  “RetailerId”: long,  “Position”: int,  “IsActivate”: bool,  “CreatedBy”: long,  “CreatedDate”: datetime,  “Id”: long,  “Name”: string  },// Để lấy thông tin SaleChannel thì phải truyền thêm  //SaleChannel=true  “invoiceDelivery”:{  “deliveryCode”: string,  “type”: byte?,  “status”: byte, (1: Chờ xử lý, 2: Đang giao hàng,3: Giao thành công, 4:Đang chuyển hoàn, 5:Đã chuyển hoàn, 6:Đã hủy, 7: Đang lấy hàng, 8:Chờ lấy lại, 9:Đã lấy hàng, 10:Chờ giao lại, 11:Chờ chuyển hàng, 12:Chờ chuyển hoàn lại) //trạng thái vận đơn  “statusValue”: string,  “price”: Decimal?,  “receiver”: string,  “contactNumber”: string,  “address”: string,  “locationId”: int?,  “locationName”: string,  “usingPriceCod”: bool, //Thu hộ tiền  “priceCodPayment”: decimal, //Số tiền thu hộ  “weight”: double?,  “length”:  double?,  “width”:  double?,  “height”: double?,  “partnerDeliveryId”: long?,  “partnerDelivery”:{  “code”: string,  “name”: string,  “address”: string,  “contactNumber”: string,  “email”: string  }  }  }]  } |

#### **2.12.2. Lấy chi tiết hóa đơn**

–**Mục đích sử dụng**: Trả về thông tin chi tiết của hóa đơn theo ID, theo Code

**– Phương thức và URL:**

- Theo Id : **GET** https://public.kiotapi.com/invoices/ {id}
- Theo Code : **GET** https://public.kiotapi.com/invoices/code/ {code}

**– Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID của hóa đơn
***“code”***: string // Mã của hóa đơn

**– Response:**

|  |
| --- |
| {  “id”: long //Id hóa đơn  “code”: string //Mã hóa đơn  “orderCode”: string //Mã đơn đặt hàng  “purchaseDate”: datetime // Ngày hóa đơn  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “soldById”: long?,  “soldByName”: string  “customerId”: long?, // Id khách hàng  “customerCode”: string, //Mã khách hàng  “customerName”: string, // Tên khách hàng  “total”: decimal, // Khách cần trả  “totalPayment”: decimal, //Khách đã trả  “status”: int, // trạng thái đơn hóa đơn  “statusValue”: string, // trạng thái đơn hóa đơn bằng chữ  “description”: string, // ghi chú  “usingCod”: boolean,  “createdDate”: datetime, //Ngày tạo  “modifiedDate”: datetime, //Ngày cập nhật  “totalTax”: decimal?,  “payments” :[{  “id”: long,  “code”: string,  “amount”: decimal,  “method”: string,  “status”: byte?,  “statusValue”: string,  “transDate”: datetime,  “bankAccount”: string,  “accountId”: int?  }],  “invoiceOrderSurcharges”: [                          {  “id”: long,  “invoiceId”:long?,  “surchargeId”: long?,  “surchargeName”: string,  “surValue”: decimal?,  “price”: decimal?,  “createdDate”: DateTime  }  ],  “invoiceDetails” :{  “productId”: long, // Id hàng hóa  “productCode”: string,  “productName”: string, //Tên hàng hóa  (bao gồm thuộc tính và đơn vị tính)  “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discountRatio”: double?, // Giảm giá trên sản phẩm theo %  “discount”: decimal?, // Giảm giá trên sản phẩm theo tiền  “note”: string // Ghi chú hàng hóa  “serialNumbers”: string, // Danh sách imei  “productBatchExpire”: {  “id”: long, // Id lô  “productId” long, // ID sản phẩm  “batchName”: string, // Tên  “fullNameVirgule”: string, // Tên đầy đủ  “createdDate”: DateTime, // Ngày tạo lô  “expireDate”: DateTime // Ngày hết hạn lô  }  “invoiceDetailTaxs”: [  {  “id”: “int”, // ID chi tiết thuế  “detailId”: “long”, // Id chi tiết hóa đơn  “detailTax”: “decimal?”, // Giá trị thuế cho hàng hóa này  “taxId”: “int”, // ID thuế  “name”: “string”, // Tên Thuế  “value”: “decimal?” // Mức thuế  }  ]  }  ],  “invoiceDelivery”:{  “deliveryCode”: string,  “type”: byte?,  “status”: byte, (1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy) //trạng thái vận đơn  “statusValue”: string,  “price”: Decimal?,  “receiver”: string,  “contactNumber”: string,  “address”: string,  “locationId”: int?,  “locationName”: string,  “usingPriceCod”: bool, //Thu hộ tiền  “priceCodPayment”: decimal, //Số tiền thu hộ  “weight”: double?,  “length”:  double?,  “width”:  double?,  “height”: double?,  “partnerDeliveryId”: long?,  “partnerDelivery”:{  “code”: string,  “name”: string,  “address”: string,  “contactNumber”: string,  “email”: string  },  “SaleChannel”:{  “IsNotDelete”: bool,  “RetailerId”: long,  “Position”: int,  “IsActivate”: bool,  “CreatedBy”: long,  “CreatedDate”: datetime,  “Id”: long,  “Name”: string  }  }  } |

#### **2.12.3. Thêm mới hóa đơn**

**–** **Mục đích sử dụng**: Tạo mới hóa đơn

**– Phương thức và URL: POST** <https://public.kiotapi.com/invoices>

**–** **Request:** JSON mã hóa yêu cầu gồm 1 object hóa đơn

|  |
| --- |
| {      “isApplyVoucher”: true, //Có apply voucher khi tạo hóa đơn không,      “branchId”: int,      “purchaseDate”: datetime,      “customerId”: long?,      “discount”: decimal?,      “totalPayment”: decimal,      “saleChannelId”: int? optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác      “method”: string,      “accountId”: int?,      “usingCod”: bool,      “soldById”: long,      “orderId”: long?,      “invoiceDetails”: [          {              “productId”: long,              “productCode”: string,              “productName”: string,              “quantity”: double,              “price”: decimal,              “discount”: decimal?,              “discountRatio”: decimal?,              “note”: string,              “serialNumbers”: string, // Serial Imei              “InvoiceDetailTaxs”: [                  {                      “TaxId”: int, //TaxID truyền ID của mức thuế tương ứng với phương pháp tính thuế của gian hàng đang sử dụng  // Thuế khấu trừ: 1: VAT 0%, 2: VAT 5%, 3: VAT 8%, 4: VAT 10%, 5: KCT, 12: KKKNT  // Thuế trực tiếp: 6: VAT 1%, 7: VAT 2%, 8: VAT 3%, 9: VAT 5%, 64: 0% VAT 5% TNCN, 65: 0% VAT 1,5% TNCN, 66: 0% VAT 2% TNCN                  }              ]          }      ],      “deliveryDetail”: {          “deliveryCode”: string,          “type”: byte?,          “status”: byte, // (1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy) //trạng thái vận đơn          “price”: Decimal?,          “receiver”: string,          “contactNumber”: string,          “address”: string,          “locationId”: int,          “locationName”: string,          “wardName”: string, // Tên phường          “weight”: double,          “length”: double,          “width”: double,          “usingPriceCod”: bool, //Thu hộ tiền          “height”: double,          “partnerDeliveryId”: long?,          “expectedDelivery”: datetime,          “partnerDelivery”: {              “code”: string,              “name”: string,              “address”: string,              “contactNumber”: string,              “email”: string          },          “surchages”: [              {                  “id”: int,                  “code”: string,                  “price”: decimal,              }          ],          “Payments”: [ //Thêm phương thức thanh toán bằng voucher              {                  “Method”: “Voucher”, // Giá trị mặc định là Voucher (không đổi)                  “MethodStr”: “Voucher”, // Giá trị mặc định là Voucher (không đổi)                  “Amount”: 50000, // Giá trị của voucher                  “Id”: -1, // Giá trị mặc định là -1 (không đổi)                  “AccountId”: null, // Giá trị mặc định là null (không đổi)                  “VoucherId”: 30996, // Id của voucher                  “VoucherCampaignId”: 30087 // Id của đợt phát hành voucher              }          ]      }  } |

**– Response:**

|  |
| --- |
| {      “id”: long,      “code”: string,      “purchaseDate”: datetime,      “branchId”: int,      “branchName”: string,      “soldById”: long?,      “soldByName”: string,      “customerId”: long?,      “customerName”: string,      “saleChannelId”: int?, optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác      “total”: decimal, // Khách cần trả      “totalPayment”: decimal, //Khách đã trả      “discountRatio”: double?, // Giảm giá trên đơn theo %      “discount”: decimal?, // giảm giá hóa đơn (giảm giá hóa đơn trước thuế nếu MODE là sau thuế)      “discountAfterTax”: decimal?, // giảm giá hóa đơn sau thuế      “method”: string, // Phương thức thanh toán (Cash, Card, Transfer)      “status”: int, // trạng thái hóa đơn      “statusValue”: string, // trạng thái đơn hóa đơn bằng chữ      “description”: string, // ghi chú      “usingCod”: boolean,      “pricingMode”: int?, // MODE thuế. null: trực tiếp, 0: trước thuế, 1: sau thuế      “totalTax”: decimal?, // giá trị totalTax được tính tự động      “invoiceDetails”: {          “productId”: long, // Id hàng hóa          “productName”: string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính)          “quantity”: double, // Số lượng hàng hóa          “discountRatio”: double?, // Giảm giá trên sản phẩm theo %          “price”: decimal?, // giá bán (giá bán trước thuế nếu Mode là sau thuế)          “discount”: decimal?, // giảm giá (giảm giá trước thuế nếu Mode là sau thuế)          “note”: string, // Ghi chú hàng hóa          “allocationDiscount”: decimal?, // giảm giá phân bổ (giảm giá phân bổ trước thuế nếu Mode là sau thuế)          “invoiceDetailTaxs”: [              {                  “id”: int, // ID chi tiết thuế                  “detailId”: long, // Id chi tiết hóa đơn                  “detailTax”: decimal?, // Giá trị thuế cho hàng hóa này                  “taxId”: int, // ID thuế                  “name”: string, // Tên Thuế                  “value”: decimal?, // Mức thuế                  “priceAfterTax”: decimal?, // giá bán sau thuế                  “discountAfterTax”: decimal? // giảm giá sau thuế              }          ]      },      “deliveryDetail”: {          “deliveryCode”: string,          “type”: byte?,          “status”: byte, // (1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy) //trạng thái vận đơn          “statusValue”: string,          “price”: Decimal?,          “receiver”: string,          “contactNumber”: string,          “address”: string,          “locationId”: int?,          “locationName”: string,          “usingPriceCod”: bool, //Thu hộ tiền          “priceCodPayment”: decimal, //Số tiền thu hộ                         “weight”: double?,          “length”: double?,          “width”: double?,          “height”: double?,          “partnerDeliveryId”: long?,          “partnerDelivery”: {              “code”: string,              “name”: string,              “address”: string,              “contactNumber”: string,              “email”: string          }      },      “invoiceOrderSurcharges”: [          {              “id”: long,              “invoiceId”:long?,              “surchargeId”: long?,              “surchargeName”: string,              “surValue”: decimal?,              “price”: decimal?,              “createdDate”: DateTime          }      ]  } |

#### **2.12.4. Cập nhật hóa đơn**

–**Mục đích sử dụng**: Cập nhật hóa đơn theo ID

**– Phương thức và URL: PUT** <https://public.kiotapi.com/invoices/Id>

**–** **Request:** Sử dụng hàm PUT với ID hóa đơn qua 1 object JSON.

***“id”***: long // ID hóa đơn

**– Body**

|  |
| --- |
| {    “purchaseDate”: datetime,      “status”: byte,      “soldById”: long,      “codPaymentMethod”: string, //Phương thức thanh toán thu hộ (Cash, Tranfer),      “codPaymentAccount”: int?, //Id tài khoản ngân hàng nếu thanh toán chuyển khoản, thẻ ngân hang,      “saleChannelId”: int?, //optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác      “deliveryDetail”: {          “deliveryCode”: string,          “type”: byte?,          “status”: byte, //(1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy) //trạng thái vận đơn          “price”: Decimal?,          “receiver”: string,          “contactNumber”: string,          “address”: string,          “locationId”: int,          “locationName”: string,          “wardName”: string, // Tên phường          “weight”: double,          “length”: double,          “usingPriceCod”: bool, //Thu hộ tiền          “priceCodPayment”: decimal, //Số tiền thu hộ          “width”: double,          “height”: double,          “partnerDeliveryId”: long?,          “expectedDelivery”: datetime,          “partnerDelivery”: {              “code”: string,              “name”: string,              “address”: string,              “contactNumber”: string,              “email”: string          }      },      “invoiceDetails”: {          “productId”: long, // Id hàng hóa          “productCode”: string,          “productName”: string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính)          “quantity”: double, // Số lượng hàng hóa          “price”: decimal, //Giá trị          “discountRatio”: double?, // Giảm giá trên sản phẩm theo %          “discount”: decimal?, // Giảm giá trên sản phẩm theo tiền          “note”: string, // Ghi chú hàng hóa                 “serialNumbers”: string, // Danh sách imei          “invoiceDetailTaxs”: [              {                               “taxId”: int, //TaxID truyền ID của mức thuế tương ứng với phương pháp tính thuế của gian hàng đang sử dụng  // Thuế khấu trừ: 1: VAT 0%, 2: VAT 5%, 3: VAT 8%, 4: VAT 10%, 5: KCT, 12: KKKNT  // Thuế trực tiếp: 6: VAT 1%, 7: VAT 2%, 8: VAT 3%, 9: VAT 5%, 64: 0% VAT 5% TNCN, 65: 0% VAT 1,5% TNCN, 66: 0% VAT 2% TNCN                               }          ]      }  } |

**– Response:**

|  |
| --- |
| {   ```     "id": long, ```  ```     "code": string, ```  ```     "purchaseDate": datetime, ```  ```     "branchId": int, ```  ```     "branchName": string, ```  ```     "soldById": long?, ```  ```     "soldByName": string, ```  ```     "customerId": long?, ```  ```     "customerName": string, ```  ```     "total": decimal, // Khách cần trả ```  ```     "totalPayment": decimal, //Khách đã trả ```  ```     "discountRatio": double?, // Giảm giá trên đơn theo % ```  ```     "method": string, // Phương thức thanh toán (Cash, Card, Transfer) ```  ```     "status": int, // trạng thái hóa đơn ```  ```     "statusValue": string, // trạng thái hóa đơn bằng chữ ```  ```     "description": string, // ghi chú ```  ```     "usingCod": boolean, ```  ```     "saleChannelId": int?, ```  ```     "discount": decimal?, // giảm giá hóa đơn (giảm giá hóa đơn trước thuế nếu MODE là sau thuế) ```  ```     "discountAfterTax": decimal?, // giảm giá hóa đơn sau thuế ```  ```     "pricingMode": int?, // MODE thuế. null: trực tiếp, 0: trước thuế, 1: sau thuế ```  ```     "totalTax": decimal?, // giá trị totalTax được tính tự động ```  ```     "invoiceDetails": { ```  ```         "productId": long, // Id hàng hóa ```  ```         "productName": string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính) ```  ```         "quantity": double, // Số lượng hàng hóa ```  ```         "discountRatio": double?, // Giảm giá trên sản phẩm theo % ```  ```         "price": decimal?, // giá bán (giá bán trước thuế nếu Mode là sau thuế) ```  ```         "discount": decimal?, // giảm giá (giảm giá trước thuế nếu Mode là sau thuế) ```  ```         "allocationDiscount": decimal?, // giảm giá phân bổ (giảm giá phân bổ trước thuế nếu Mode là sau thuế) ```  ```         "invoiceDetailTaxs": [ ```  ```             { ```  ```                 "DetailTax": decimal?, // Giá trị thuế ```  ```                 "id": int, // ID chi tiết thuế ```  ```                 "detailId": long, // Id chi tiết hóa đơn ```  ```                 "taxId": int, // ID thuế ```  ```                 "name": string, // Tên Thuế ```  ```                 "value": decimal?, // Mức thuế ```  ```                 "priceAfterTax": decimal?, // giá bán sau thuế ```  ```                 "discountAfterTax": decimal?, // giảm giá sau thuế ```  ```                 "discountByPromotionAfterTax": decimal?, // giảm giá khuyến mãi sau thuế ```  ```                 "allocationDiscountAfterTax": decimal? // giảm giá phân bổ sau thuế ```  ```             } ```  ```         ] ```  ```     }, ```  ```     "deliveryDetail": { ```  ```         "deliveryCode": string, ```  ```         "type": byte?, ```  ```         "status": byte, //(1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy) //trạng thái vận đơn ```  ```         "statusValue": string, ```  ```         "price": Decimal?, ```  ```         "receiver": string, ```  ```         "contactNumber": string, ```  ```         "address": string, ```  ```         "locationId": int?, ```  ```         "locationName": string, ```  ```         "usingPriceCod": bool, //Thu hộ tiền ```  ```         "priceCodPayment": decimal, //Số tiền thu hộ ```  ```         "weight": double?, ```  ```         "length": double?, ```  ```         "width": double?, ```  ```         "height": double?, ```  ```         "partnerDeliveryId": long?, ```  ```         "partnerDelivery": { ```  ```             "code": string, ```  ```             "name": string, ```  ```             "address": string, ```  ```             "contactNumber": string, ```  ```             "email": string ```  ```         } ```  ```     } ```  ``` } ``` |

#### **2.12.5. Xóa hóa đơn**

– **Mục đích sử dụng**: Xóa hóa đơn theo ID

**– Phương thức và URL: DELETE** [https://public.kiotapi.com/invoices](https://public.kiotapi.com/invoices/%7bid%7d)

**–** **Request: :** JSON mã hóa yêu cầu gồm 1 object tham số sau:

|  |
| --- |
| {  “id”: long // ID của hóa đơn  “isVoidPayment”:bool // Hủy phiếu thanh toán gắn kèm hóa đơn, nếu không truyền tham số này thì mặc định không hủy phiếu thanh toán gắn kèm hóa đơn  } |

**– Response:**

|  |
| --- |
| {  “id”: long,  “code”: string,  “purchaseDate”: datetime,  “branchId”: int,  “branchName”: string,  “soldById”: long?,  “soldByName”: string,  “customerId”: long?,  “customerName”: string,  “saleChannelId” : int?, optional // Id kênh bán hàng  “total”: decimal, // Khách cần trả  “totalPayment”: decimal, //Khách đã trả  “discountRatio”: double?, // Giảm giá trên đơn theo %  “discount”: decimal?, // Giảm giá trên đơn theo tiền  “method”: string, // Phương thức thanh toán (Cash, Card, Transfer)  “status”: 2, // trạng thái đơn  “statusValue”: “Đã hủy”, // trạng thái đơn đặt hàng bằng chữ  “description”: string, // ghi chú  “usingCod”: boolean,  “invoiceDetails” :{  “productId”: long, // Id hàng hóa  “productName”: string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính) “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discountRatio”: double?, // Giảm giá trên SP theo %  “discount”: decimal?, // Giảm giá trên SP theo tiền,  “note”: string // Ghi chú hàng hóa  },  “deliveryDetail”:{  “deliveryCode”: string,  “type”: byte?,  status”: byte, (1: Chờ xử lý, 2: Đang giao hàng,3: Giao thành công, 4:Đang chuyển hoàn, 5:Đã chuyển hoàn, 6:Đã hủy, 7: Đang lấy hàng, 8:Chờ lấy lại, 9:Đã lấy hàng, 10:Chờ giao lại, 11:Chờ chuyển hàng, 12:Chờ chuyển hoàn lại) //trạng thái vận đơn  “statusValue”: string,  “price”: Decimal?,  “receiver”: string,  “contactNumber”: string,  “address”: string,  “locationId”: int?,  “locationName”: string,  “usingPriceCod”: bool, //Thu hộ tiền  “priceCodPayment”: decimal, //Số tiền thu hộ  “weight”: double?,  “length”:  double?,  “width”:  double?,  “height”: double?,  “partnerDeliveryId”: long?,  “partnerDelivery”:{  “code”: string,  “name”: string,  “address”: string,  “contactNumber”: string,  “email”: string  }  },  “payments”:[  {  “id”: string,  “code”: string,  “amount”: decimal,  “method”: string,  “status”: byte,  “statusValue”: byte,  “transDate”: datetime  }],  “invoiceOrderSurcharges”: []  } |

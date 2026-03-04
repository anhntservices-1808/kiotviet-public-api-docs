### **2.5. Đặt hàng**

Hiện tại KiotViet hỗ trợ thiết lập cho tính năng đặt hàng như sau:

– Trong trường hợp người dùng không tích chọn setting cho “Cho phép đặt hàng”, các giao dịch liên quan tới đặt hàng sẽ không hiển thị trên Kiotviet nữa. Vì vậy, khi gọi các API liên quan tới phần đặt hàng, nếu thiết lập này đang tắt thì API sẽ trả lại thông báo “Thiết lập “Cho phép đặt hàng” đang không được bật.”.

– Trong trường hợp người dùng không tích chọn setting cho “Sử dụng tính năng giao hàng”, các giao dịch sẽ không hiển thị tính năng giao hàng nữa. Vì vậy, khi gọi các API liên quan tới phần giao hàng, nếu thiết lập này đang tắt thì API sẽ trả lại thông báo “Thiết lập “Sử dụng tính năng giao hàng.” đang không được bật”.

– Trong trường hợp người dùng không tích chọn setting cho “Không cho phép thay đổi thời gian bán hàng”, khi Post/ Put các API liên quan đến thời gian bán hàng thì API sẽ trả lại thông báo “Thiết lập “Không cho phép thay đổi thời gian bán hàng” đang không được bật.”.
– Mô tả chi tiết cho các API hỗ trợ Đặt hàng như sau:

#### **2.5.1. Lấy danh sách đặt hàng**

**– Mục đích sử dụng:** Trả về danh sách đặt hàng theo cửa hàng đã được xác nhận

**– Phương thức và URL: GET** <https://public.kiotapi.com/orders>

**– Request:** Sử dụng hàm **GET** với tham số:

|  |
| --- |
| “branchIds”: int[], optional // ID chi nhánh  “customerIds”: long[], optional // Id khách hàng  “customerCode”: string //Mã khách hàng  “status”: int[], optional // Tình trạng đặt hàng  “includePayment”: Boolean, // có lấy thông tin thanh toán  “includeOrderDelivery”: Boolean,  “lastModifiedFrom”: datetime? // thời gian cập nhật  “pageSize”: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items  “currentItem”: int,  “lastModifiedFrom”: datetime? // thời gian cập nhật  “toDate”: datetime? //Thời gian cập nhật cho đến thời điểm toDate  “orderBy”: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)  “orderDirection”: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc  “createdDate”: datetime? //Thời gian tạo  “saleChannelId” : int?, optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác |

**– Response:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [{  “id”: long //Id đặt hàng  “code”: string //Mã đặt hàng  “purchaseDate”: datetime // Ngày đặt hàng  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “soldById”: long?,  “soldByName”: string  “customerId”: long?, // Id khách hàng  “customerCode”: string, //Mã khách hàng  “customerName”: string, // Tên khách hàng  “total”: decimal, // Khách cần trả  “totalPayment”: decimal, //Khách đã trả  “discountRatio”: double?, // Giảm giá trên đơn theo %  “discount”: decimal?, // Giảm giá trên đơn theo tiền  “status”: int, // trạng thái đơn đặt hàng  “statusValue”: string, // trạng thái đơn đặt hàng bằng chữ  “description”: string, // ghi chú  “usingCod”: boolean,  “totalTax”: “decimal?”, // Tổng thuế  “payments” :[{  “id”: long,  “code”: string,  “amount”: decimal,  “method”: string”,  “status”: byte?,  “statusValue”: string,  “transDate”: datetime,  “bankAccount”: string,  “accountId”: int?  }],  “orderDetails” :{  “productId”: long, // Id hàng hóa  “productCode”:  string,  “productName”: string, //Tên hàng hóa bao gồm thuộc tính và đơn vị tính  “isMaster”: boolean, //Tính năng thêm dòng, true: hàng hóa ở dòng chính, false: hàng hóa ở dòng phụ.   “quantity”: double, // Số lượng hàng hóa  “price”: decimal, //Giá trị  “discountRatio”: double?, // Giảm giá trên sản phẩm theo %  “discount”: decimal?, // Giảm giá trên sản phẩm theo tiền  “note”: string // Ghi chú hàng hóa  },  “orderDelivery”:{  “deliveryCode”: string,  “type”: byte?,  “price”: Decimal?,  “receiver”: string,  “contactNumber”: string,  “address”: string,  “locationId”: int?,  “locationName”: string,  “weight”: double?,  “length”: double?,  “width”: double?,  “height”: double?,  “partnerDeliveryId”: long?,  “partnerDelivery”:{  “code”: string,  “name”: string,  “address”: string,  “contactNumber”: string,  “email”: string  }  “orderDetailTaxs”: [  {  “id”: “int”, // ID chi tiết thuế  “detailId”: “long”, // ID chi tiết đặt hàng  “retailerId”: “int”, // ID gian hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?”, // Giá trị thuế  “taxName”: “string”, // Tên thuế  “taxValue”: “decimal?” // Mức thuế  }  ]  }  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime // thời gian cập nhật  “createdDate”: datetime // thời gian tạo  “saleChannelId” : int?, optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác  }]  } |

#### **2.5.2. Lấy chi tiết đặt hàng**

**– Mục đích sử dụng**: Trả về thông tin chi tiết của đơn đặt hàng theo ID, theo Code

**– Phương thức và URL**:

- Theo Id : **GET** https://public.kiotapi.com/orders/ {id}
- Theo Code : **GET** https://public.kiotapi.com/orders/code/ {code}

**– Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID của đơn đặt hàng
***“code”***: code // Mã của đơn đặt hàng

**– Response:**

|  |
| --- |
| {  “id”: long //Id đặt hàng  “code”: string //Mã đặt hàng  “purchaseDate”: datetime // Ngày đặt hàng  “branchId”: int, //Id chi nhánh  “branchName”: string, //Tên chi nhánh  “soldById”: long?,  “soldByName”: string  “customerId”: long?, // Id khách hàng  “customerName”: string, // Tên khách hàng  “total”: decimal, // Khách cần trả  “totalPayment”: decimal, //Khách đã trả  “discountRatio”: double, // Giảm giá trên đơn theo %  “discount”: decimal?, // Giảm giá trên đơn theo tiền  “status”: int, // trạng thái đơn đặt hàng  “statusValue”: string, // trạng thái đơn đặt hàng bằng chữ  “description”: string, // ghi chú  “usingCod”: boolean,  “totalTax”: decimal?,//Tổng thuế  “payments” :[{  “id”: long,  “code”: string,  “amount”: decimal,  “method”: string,  “status”: byte?,  “statusValue”: string,  “transDate”: datetime,  “bankAccount”: string,  “accountId”: int?  }],  “orderDetails” :{  “productId”: long, // Id hàng hóa  “productCode”:  string,  “productName”: string, //Tên hàng hóa bao gồm thuộc tính và đơn vị tính  “quantity”: double, // Số lượng hàng hóa  “isMaster”: boolean, //Tính năng thêm dòng, true: hàng hóa ở dòng chính, false: hàng hóa ở dòng phụ.  “price”: decimal, //Giá trị  “discountRatio”: double?, // Giảm giá trên sản phẩm theo %  “discount”: decimal?, // Giảm giá trên sản phẩm theo tiền  “note”: string // Ghi chú hàng hóa  “orderDetailTaxs”: [  {  “id”: “int”, // ID chi tiết thuế  “detailId”: “long”, // ID chi tiết đặt hàng  “retailerId”: “int”, // ID gian hàng  “taxId”: “int”, // ID thuế  “detailTax”: “decimal?”, // Giá trị thuế  “taxName”: “string”, // Tên thuế  “taxValue”: “decimal?” // Mức thuế  }  ]  }  ],  “orderDelivery”:{  “deliveryCode”: string,  “type”: byte?,  “price”: Decimal?,  “receiver”: string,  “contactNumber”: string,  “address”: string,  “locationId”: int?,  “locationName”: string,  “weight”: double?,  “length”: double?,  “width”: double?,  “height”: double?,  “partnerDeliveryId”: long?,  “partnerDelivery”:{  “code”: string,  “name”: string,  “address”: string,  “contactNumber”: string,  “email”: string  }  },  “invoiceOrderSurcharges”: [{  “id”: long,  “invoiceId”:long?,  “surchargeId”: long?,  “surchargeName”: string,  “surValue”: decimal?,  “price”: decimal?,  “createdDate”: DateTime  }],  “retailerId”: int, // Id cửa hàng  “modifiedDate”: datetime // thời gian cập nhật  “createdDate”: datetime //thời gian tạo  } |

#### **2.5.3. Thêm mới đặt hàng**

**– Mục đích sử dụng**: Tạo mới đơn đặt hàng

**– Phương thức và URL: POST** <https://public.kiotapi.com/order>s

**– Request:** JSON mã hóa yêu cầu gồm 1 object đặt hàng:

**Chú ý*:*** *Khi thêm mới đơn đặt hàng từ* ***MyKiot*** *hoặc* ***KV Sync*** *sẽ thêm param* ***Partner*** *vào header:*

-Từ MyKiot :

- Partner : MyKiot

-Từ KV Sync :

- Partner : KVSync

|  |
| --- |
| {      “isApplyVoucher”: true, //Có apply voucher khi tạo đặt hàng không      “purchaseDate”: datetime,      “branchId”: int,      “soldById”: long?,      “cashierId”: long?, //Id người tạo đơn đặt hàng, nếu không truyền thì mặc định Admin là người tạo      “discount”: decimal,      “description”: string,      “method”: string,      “totalPayment”: decimal, //khách đã trả      “accountId”: int?, //Id account tài khoản ngân hàng nếu phương thức thanh toán là TRANSFER, CARD,      “makeInvoice”: bool, // Tạo hóa đơn từ đơn đặt hàng, tạo phiếu thu cho hóa đơn đó với thời điểm hiện tại ,      “saleChannelId”: int?, //optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác      “orderDetails”: [          {              “productId”: long,              “productCode”: string,              “productName”: string,              “quantity”: double,              “price”: decimal,              “discount”: decimal?,              “discountRatio”: double?,              “note”: string,              “OrderDetailTaxs”: [                  {                      “TaxId”: int, //TaxID truyền ID của mức thuế tương ứng với phương pháp tính thuế của gian hàng đang sử dụng  // Thuế khấu trừ: 1: VAT 0%, 2: VAT 5%, 3: VAT 8%, 4: VAT 10%, 5: KCT, 12: KKKNT  // Thuế trực tiếp: 6: VAT 1%, 7: VAT 2%, 8: VAT 3%, 9: VAT 5%, 64: 0% VAT 5% TNCN, 65: 0% VAT 1,5% TNCN, 66: 0% VAT 2% TNCN                  }              ]          }      ],      “orderDelivery”: {          “deliveryCode”: string,          “type”: byte?,          “price”: Decimal?,          “receiver”: string,          “contactNumber”: string,          “address”: string,          “locationId”: int?,          “locationName”: string,          “weight”: double,          “length”: double,          “width”: double,          “height”: double,          “partnerDeliveryId”: long?,          “expectedDelivery”: datetime,          “partnerDelivery”: {              “code”: string,              “name”: string,              “address”: string,              “contactNumber”: string,              “email”: string          }      },      “customer”: {          “id”: long,          “code”: string,          “name”: string,          “gender”: boolean,          “birthDate”: datetime,          “contactNumber”: string,          “address”: string,          “email”: string,          “comment”: string      },      “surchages”: [          {              “id”: int,              “code”: string,              “price”: decimal,          }      ],      “Payments”: [ //Thêm phương thức thanh toán bằng voucher          {              “Method”: “Voucher”, // Giá trị mặc định là Voucher (không đổi)              “MethodStr”: “Voucher”, // Giá trị mặc định là Voucher (không đổi)              “Amount”: 50000, // Giá trị của voucher              “Id”: -1, // Giá trị mặc định là -1 (không đổi)              “AccountId”: null, // Giá trị mặc định là null (không đổi)              “VoucherId”: 30996, // Id của voucher              “VoucherCampaignId”: 30087 // Id của đợt phát hành voucher          }      ]  } |

**– Response:**

|  |
| --- |
| {   ```     "id": long, ```  ```     "code": string, ```  ```     "purchaseDate": datetime, ```  ```     "branchId": int, ```  ```     "branchName": string, ```  ```     "soldById": long?, ```  ```     "soldByName": string, ```  ```     "customerId": long?, ```  ```     "customerName": string, ```  ```     "total": decimal, // Khách cần trả ```  ```     "totalPayment": decimal, //Khách đã trả ```  ```     "discountRatio": double?, // Giảm giá trên đơn theo % ```  ```     "method": string, // Phương thức thanh toán (Cash, Card, Transfer) ```  ```     "status": int, // trạng thái đơn đặt hàng ```  ```     "statusValue": string, // trạng thái đơn đặt hàng bằng chữ ```  ```     "description": string, // ghi chú ```  ```     "usingCod": boolean, ```  ```     "saleChannelId": int?, optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác ```  ```     "discount": decimal?, // giảm giá hóa đơn (giảm giá hóa đơn trước thuế nếu MODE là sau thuế) ```  ```     "discountAfterTax": decimal?, // giảm giá hóa đơn sau thuế ```  ```     "pricingMode": int?, // MODE thuế. null: trực tiếp, 0: trước thuế, 1: sau thuế ```  ```     "totalTax": decimal?, // giá trị totalTax được tính tự động ```  ```     "orderDetails": { ```  ```         "productId": long, // Id hàng hóa ```  ```         "productName": string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính) ```  ```         "quantity": double, // Số lượng hàng hóa ```  ```         "discountRatio": double?, // Giảm giá trên sản phẩm theo % ```  ```         "price": decimal?, // giá bán (giá bán trước thuế nếu Mode là sau thuế) ```  ```         "discount": decimal?, // giảm giá (giảm giá trước thuế nếu Mode là sau thuế) ```  ```         "note": string, // Ghi chú hàng hóa, ```  ```         "orderDetailTaxs": [ ```  ```             { ```  ```                 "id": int, // ID chi tiết thuế ```  ```                 "detailId": long, // ID chi tiết đặt hàng ```  ```                 "retailerId": int, // ID gian hàng ```  ```                 "taxId": int, // ID thuế ```  ```                 "detailTax": decimal?, // Giá trị thuế ```  ```                 "taxName": string, // Tên thuế ```  ```                 "taxValue": decimal?, // Mức thuế ```  ```                 "priceAfterTax": decimal?, // giá bán sau thuế ```  ```                 "discountAfterTax": decimal? // giảm giá sau thuế ```  ```             } ```  ```         ] ```  ```     }, ```  ```     "orderDelivery": { ```  ```         "deliveryCode": string, ```  ```         "type": byte?, ```  ```         "price": Decimal?, ```  ```         "receiver": string, ```  ```         "contactNumber": string, ```  ```         "address": string, ```  ```         "locationId": int?, ```  ```         "locationName": string, ```  ```         "weight": double?, ```  ```         "length": double?, ```  ```         "width": double?, ```  ```         "height": double?, ```  ```         "partnerDeliveryId": long?, ```  ```         "partnerDelivery": { ```  ```             "code": string, ```  ```             "name": string, ```  ```             "address": string, ```  ```             "contactNumber": string, ```  ```             "email": string ```  ```         } ```  ```     }, ```  ```     "payments": [ ```  ```         { ```  ```             "id": long, ```  ```             "code": string, ```  ```             "amount": decimal, ```  ```             "method": string, ```  ```             "status": byte?, ```  ```             "statusValue": string, ```  ```             "transDate": datetime, ```  ```             "bankAccount": string, ```  ```             "accountId": int? ```  ```         } ```  ```     ], ```  ```     "invoiceOrderSurcharges": [ ```  ```         { ```  ```             "id": long, ```  ```             "invoiceId":long?, ```  ```             "surchargeId": long?, ```  ```             "surchargeName": string, ```  ```             "surValue": decimal?, ```  ```             "price": decimal?, ```  ```             "createdDate": DateTime ```  ```         } ```  ```     ] ```  ``` } ``` |

#### **2.5.4. Cập nhật đặt hàng**

**– Mục đích sử dụng**: Cập nhật đơn đặt hàng theo ID

**– Phương thức và URL: PUT** <https://public.kiotapi.com/orders/Id>

**–** **Request:** Sử dụng hàm PUT với ID đơn đặt hàng qua 1 object JSON.

***“id”***: long // ID đơn đặt hàng

**– Body**

|  |
| --- |
| {      “purchaseDate”: datetime,      “branchId”: int,      “soldById”: long?,      “cashierId”: long?, //Id người tạo đơn đặt hàng, nếu không truyền thì mặc định Admin là người tạo      “discount”: decimal,      “description”: string,      “method”: string,      “totalPayment”: decimal, //Khách đã trả,      “accountId”: int?, //Id account tài khoản ngân hàng nếu phương thức thanh toán là TRANSFER, CARD,      “makeInvoice”: bool, // Tạo hóa đơn từ đơn đặt hàng, tạo phiếu thu cho hóa đơn đó với thời điểm hiện tại,      “saleChannelId”: int?, // optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác      “orderDetails”: [          {              “productId”: long,              “productCode”: string,              “productName”: string,              “isMaster”: boolean, // optional // sản phẩm              “quantity”: double,              “price”: decimal,              “discount”: decimal?,              “discountRatio”: double?,              “OrderDetailTaxs”: [                  {                      “TaxId”: int, //TaxID truyền ID của mức thuế tương ứng với phương pháp tính thuế của gian hàng đang sử dụng  // Thuế khấu trừ: 1: VAT 0%, 2: VAT 5%, 3: VAT 8%, 4: VAT 10%, 5: KCT, 12: KKKNT  // Thuế trực tiếp: 6: VAT 1%, 7: VAT 2%, 8: VAT 3%, 9: VAT 5%, 64: 0% VAT 5% TNCN, 65: 0% VAT 1,5% TNCN, 66: 0% VAT 2% TNCN                  }              ]          }      ],      “orderDelivery”: {          “deliveryCode”: string,          “type”: byte?,          “price”: Decimal?,          “receiver”: string,          “contactNumber”: string,          “address”: string,          “locationId”: int?,          “locationName”: string,          “weight”: double?,          “length”: double?,          “width”: double?,          “height”: double?,          “partnerDeliveryId”: long?,          “expectedDelivery”: datetime,          “partnerDelivery”: {              “code”: string,              “name”: string,              “address”: string,              “contactNumber”: string,              “email”: string          }      },      “customer”: {          “id”: long,          “code”: string,          “name”: string,          “gender”: boolean,          “birthDate”: datetime,          “contactNumber”: string,          “address”: string,          “email”: string,          “comment”: string      },      “surchages”: [          {              “id”: int,              “code”: string,              “price”: decimal,          }      ]  } |

**– Response:**

|  |
| --- |
| {   ```     "id": long, ```  ```     "code": string, ```  ```     "purchaseDate": datetime, ```  ```     "branchId": int, ```  ```     "branchName": string, ```  ```     "soldById": long?, ```  ```     "soldByName": string, ```  ```     "customerId": long, ```  ```     "customerName": string, ```  ```     "total": decimal, // Khách cần trả ```  ```     "totalPayment": decimal, //Khách đã trả ```  ```     "discountRatio": double?, // Giảm giá trên đơn theo % ```  ```     "discount": decimal?, // giảm giá hóa đơn (giảm giá hóa đơn trước thuế nếu MODE là sau thuế) ```  ```     "discountAfterTax": decimal?, // giảm giá hóa đơn sau thuế ```  ```     "method": string, // Phương thức thanh toán (Cash, Card, Transfer) ```  ```     "status": int, // trạng thái đơn đặt hàng ```  ```     "statusValue": string, // trạng thái đơn đặt hàng bằng chữ ```  ```     "description": string, // ghi chú ```  ```     "usingCod": boolean, ```  ```     "saleChannelId": int?, //optional // Id kênh bán hàng, nếu không truyền mặc định kênh khác ```  ```     "pricingMode": int?, // MODE thuế. null: trực tiếp, 0: trước thuế, 1: sau thuế ```  ```     "totalTax": decimal?, // giá trị totalTax được tính tự động ```  ```     "orderDetails": { ```  ```         "productId": long, // Id hàng hóa ```  ```         "productName": string, //Tên hàng hóa (bao gồm thuộc tính và đơn vị tính) ```  ```         "quantity": double, // Số lượng hàng hóa ```  ```         "discountRatio": double?, // Giảm giá trên sản phẩm theo % ```  ```         "price": decimal?, // giá bán (giá bán trước thuế nếu Mode là sau thuế) ```  ```         "discount": decimal?, // giảm giá (giảm giá trước thuế nếu Mode là sau thuế)   ```  ```         "orderDetailTaxs": [ ```  ```             { ```  ```                 "id": int, // ID chi tiết thuế ```  ```                 "detailId": long, // ID chi tiết đặt hàng ```  ```                 "retailerId": int, // ID gian hàng ```  ```                 "taxId": int, // ID thuế ```  ```                 "detailTax": decimal?, // Giá trị thuế ```  ```                 "taxName": string, // Tên thuế ```  ```                 "taxValue": decimal?, // Mức thuế ```  ```                 "priceAfterTax": decimal?, // giá bán sau thuế ```  ```                 "discountAfterTax": decimal? // giảm giá sau thuế ```  ```             } ```  ```         ] ```  ```     }, ```  ```     "orderDelivery": { ```  ```         "deliveryCode": string, ```  ```         "type": byte?, ```  ```         "price": Decimal?, ```  ```         "receiver": string, ```  ```         "contactNumber": string, ```  ```         "address": string, ```  ```         "locationId": int?, ```  ```         "locationName": string, ```  ```         "weight": double?, ```  ```         "length": double?, ```  ```         "width": double?, ```  ```         "height": double?, ```  ```         "partnerDeliveryId": long?, ```  ```         "partnerDelivery": { ```  ```             "code": string, ```  ```             "name": string, ```  ```             "address": string, ```  ```             "contactNumber": string, ```  ```             "email": string ```  ```         } ```  ```     }, ```  ```     "payments": [ ```  ```         { ```  ```             "id": long, ```  ```             "code": string, ```  ```             "amount": decimal, ```  ```             "method": string, ```  ```             "status": byte?, ```  ```             "statusValue": string, ```  ```             "transDate": datetime, ```  ```             "bankAccount": string, ```  ```             "accountId": int? ```  ```         } ```  ```     ], ```  ```     "invoiceOrderSurcharges": [ ```  ```         { ```  ```             "id": long, ```  ```             "invoiceId":long?, ```  ```             "surchargeId": long?, ```  ```             "surchargeName": string, ```  ```             "surValue": decimal?, ```  ```             "price": decimal?, ```  ```             "createdDate": DateTime ```  ```         } ```  ```     ] ```  ``` } ``` |

#### **2.5.5. Xóa đặt hàng**

**– Mục đích sử dụng**: Xóa đơn đặt hàng theo ID

**– Phương thức và URL: DELETE** [https://public.kiotapi.com/orders/{id}](https://public.kiotapi.com/orders/%7bid%7d) ?IsVoidPayment=true

**–** **Request:** Gồm Id của đơn đặt hàng trong URL:

***“id”***: long // ID của đơn đặt hàng
***“IsVoidPayment”***: bool // Hủy phiếu thanh toán, nếu không truyền tham số này thì mặc định không hủy phiếu thanh toán gắn kèm đặt hàng

**–** **Response:** Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

### **2.4. Hàng hóa**

Mô tả chi tiết cho các liên quan đến thông tin hàng hóa như sau:

#### **2.4.1. Lấy danh sách hàng hóa**

**– Mục đích sử dụng**: Trả về toàn bộ hàng hóa theo cửa hàng đã được xác nhận (authenticated retailer)

**–** **Phương thức và URL:** **GET** <https://public.kiotapi.com/products>

**–** **Request:** Sử dụng hàm **GET** với tham số:

|  |
| --- |
| {                      “orderBy”: string, optional //Sắp xếp dữ liệu theo trường orderBy (ví dụ: orderBy=Name)                      “lastModifiedFrom”: datetime? // thời gian cập nhật                      “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items                      “currentItem”: int, // lấy dữ liệu từ bản ghi currentItem                      “includeInventory”: Boolean, // có lấy thông tin tồn kho?                      “includePricebook”: Boolean, // có lấy thông tin bảng giá?                       “IncludeSerials”: Boolean, // lấy thông tin serial imei                      “IncludeBatchExpires”: Boolean, // lấy thông tin lô, hạn sử dụng                      “includeWarranties”: Boolean, // Lấy thông tin bảo hành                      “masterUnitId”: long?, //Id hàng hoá đơn vị cần filter                      “masterProductId”: long?, //Id hàng hoá cùng loại cần filter                      “categoryId”: int?, //Id nhóm hàng cần filter                      “BranchIds”: []int, //Id chi nhánh cần xem tồn kho                      “orderDirection”: string, optional                      “includeRemoveIds”: bool, //Có lấy thông tin danh sách Id bị xoá dựa                      “includeQuantity”: bool, //có lấy thông tin định mức tồn                      “productType”: bool, //loại hàng hóa                      “includeMaterial”: bool, //có lấy danh sách hàng thành phần                      “isActive”: bool? //Hàng đang kinh doanh,                      “name”: string //search hàng hóa theo tên                      “includeSoftDeletedAttribute”: bool //Có lấy thông tin danh sách thuộc tính bị xóa của hàng hóa (mặc định là true nếu không truyền tham số này => Nghĩa là lấy tất cả thuộc tính bao gồm thuộc tính đã bị xóa. Ngược lại nếu = false thì loại bỏ các thuộc tính đã bị xóa).                      “tradeMarkId”: int?, //Id thương hiệu cần filter                      “IncludeProductShelves”: boolean? // Có lấy thông tin vị trí sản phẩm  } |

**–** **Nếu có *“OrderDirection”*,** chọn sắp xếp kết quả về theo:

- ASC (Mặc định)​
- DESC

“includeRemoveIds”: Boolean //Có lấy thông tin danh sách Id bị xoá dựa trên lastModifiedFrom,
“productType”: int? (optional) //Loại hàng hóa

**– Nếu có *“productType”*,** giá trị thuộc :

- 1: hàng combo
- 3: hàng hóa dịch vụ
- 2: các hàng hóa còn lại

​“includeMaterial”: Boolean //Có lấy thông tin danh sách hàng thành phần hay không

**– Response:**

|  |
| --- |
| “removeId”: int [], // Danh sách Id hàng hóa bị xóa dựa trên ModifiedDate  “total”: int, // Tổng số hàng hóa  “pageSize”: int,  “data”: [{  “id”: long, // ID hàng hóa  “code”: string, // Code hàng hóa  “barCode”: string, //Mã vạch hàng hóa  “retailerId”: int, // Id cửa hàng  “allowsSale”: Boolean, // Sản phẩm được bán trực tiếp hay không  “name”: string, // Tên sản phẩm  “categoryId”: int, // Id của nhóm hàng hóa  “categoryName”: string, // Tên của nhóm hàng hóa  “tradeMarkId”: int, // Id của thương hiệu  “tradeMarkName”: string, // Tên của thương hiệu  “fullName”: string, // Tên sản phẩm bao gồm thuộc tính và đơn vị tính  “description”: string, // Mô tả sản phẩm  “hasVariants”: Boolean?, // Sản phẩm có thuộc tính hay không  “attributes”: [{  “productId”: long, // Id sản phẩm  “attributeName”: string, // tên thuộc tính  “attributeValue”: string // giá trị thuộc tính  }], // danh sách thuộc tính  “unit”: string, // đơn vị tính của 1 sản phẩm,  “masterUnitId”: long, // Id của hàng hóa đơn vị cơ bản (null)  “masterProductId”: long?,  “conversionValue”: double?, // Đơn vị quy đổi  “units”: [{  “id”: long, // ID sản phẩm  “code”: string, // Mã sản phẩm                    “name”: string, // Tên sản phẩm                                      “fullName”: string, // Tên sản phẩm                                “unit”: string, // Đơn vị tính  “conversionValue”: double, // Đơn vị quy đổi  “basePrice”: decimal, // Giá bán của sản phẩm  }], // danh sách đơn vị tính  “images”: [{“Image”: string, // ảnh sản phẩm}], // Danh sách hình ảnh của hàng hóa                                       “inventories”: [{  “productId”: long, // Id của sản phẩm  “productCode”: string, // Mã của sản phẩm  “productName”: string, // Tên của sản phẩm  “branchId”: int, // Id của chi nhánh  “branchName”: string, // Tên của chi nhánh  “onHand”: double?, // Tồn kho theo chi nhánh  “cost”: decimal?, // Giá sản phẩm  “onOrder”: double, // Số lượng đặt từ nhà cung cấp theo chi nhánh  “reserved”: double, // Đặt hàng theo chi nhánh  “minQuality”: double, // Định mức tồn thấp nhất  “maxQuality”: double, // Định mức tồn cao nhất  }], // danh sách tồn kho trên các chi nhánh  “priceBooks”: // bảng giá (mặc định là bảng giá chung)  [{  “priceBookId”: long, // ID bảng giá  “priceBookName”: string, // Tên bảng giá  “productId”: long// ID sản phẩm  “isActive”: Boolean, // Có được sử dụng?  “startDate”: datetime?, // có hiệu lực từ ngày  “endDate”: datetime?, // có hiệu lực đến ngày  “price”: decimal, // Giá bán theo bảng giá  }], // danh sách các bảng giá mà sản phẩm đang được gán  “productFormulas”: // danh sách hàng thành phần (nếu có)  [{  “materialId”: long, // ID hàng thành phần  “materialCode”: string, // Code hàng thành phần  “materialFullName”: string// tên đầy đủ hàng thành phần  “materialName”: string, // tên hàng thành phần  “quantity”: int, // số lượng  “basePrice”: decimal, // giá  “productId”: long?, // mã hàng combo chứa sản phẩm này  “product”: // chi tiết sản phẩm  {  “createdDate”: datetime?, // ngày tạo  “id”: long, // ID sản phẩm của thành phần,  “retailerId”: long, // Id cửa hàng,  “code”: string , // code sản phẩm của thành phần,  “name”: string?, // tên hàng thành phần,  “fullName”: datetime?, // tên đầy đủ hàng thành phần,  “categoryId”: int, // Id của nhóm hàng hóa,  “allowsSale”: Boolean, // Sản phẩm được bán trực tiếp hay không,  “hasVariants”: Boolean?, // Sản phẩm có thuộc tính hay không,  “basePrice”: decimal, // Giá bán của sản phẩm,  “unit”: string, // Đơn vị tính,  “conversionValue”: double?, // Đơn vị quy đổi,  “modifiedDate”: datetime?, // ngày sửa,  “isActive”: Boolean, // Có được sử dụng?,  “isRewardPoint”: bool?, // có tích điểm hay không,  “orderTemplate”: string, //Mẫu ghi chú (hóa đơn đặt hàng),  “isLotSerialControl”: bool?, //Có phải imei hay không  “isBatchExpireControl”: bool? //Có phải Hàng lô/ date hay không  },                  }],                 “productSerials”: // Danh sách Imei            [{  “productId”: long, //Id sản phẩm  “serialNumber”: string, //số serial Imei  “status”: int, // 1: còn hàng, 0: hết hàng  “branchId”: int, // id chi nhánh  “quantity”: double?, //Số lượng: 1  “createdDate”: datetime, //ngày tạo  “modifiedDate”: datetime?, //ngày sửa  }],  “productBatchExpires”: // Danh sách lô  [{  “productId”: long, //Id sản phẩm  “onHand”: double, //Tồn kho của lô  “batchName”:  string, //Tên lô  “expireDate”: datetime, //ngày hết hạn lô  “fullNameVirgule”: string, //Tên đầy đủ của lô  “branchId”: int, // id chi nhánh  }],   }],  “productWarranties”: [{  “Id”: long, // id bảo hành bảo trì  “description”: string, //mô tả  “numberTime”: int, // thời gian bảo hành  “timeType”: int, // kiểu thời gian(ngày:1 tháng:2 năm:3)  “warrantyType”: int, //kiểu bảo hành (bảo hành:1, bảo trì: 3)  “productId”: long, //productId  “retailerId”: long, //retailerId  “createdBy”: long?, // người tạo  “createdDate”: datetime?,  // thời gian tạo  “modifiedDate”: datetime?, // thời giant hay đổi  }]  “basePrice”: decimal?, // giá sản phẩm  “weight”: double?, // trọng lượng sản phẩm  “modifiedDate”: datetime // thời gian cập nhật  “createdDate”: datetime, // thời gian tạo,  “orderTemplate”: string //Mẫu ghi chú (hóa đơn đặt hàng),  “minQuantity” : int  //Định mức tồn nhỏ nhất  “maxQuantity” : int  //Định mức tồn nhiều nhất,  “productShelves”: // Danh sách vị trí sản phẩm trên các chi nhánh  [{  “branchId”: long, // Id của chi nhánh  “branchName”: string, // Tên của chi nhánh  “ProductShelves”: string // Vị trí sản phẩm (Vị trí 1 | Vị trí 2)   ``` }] ```   “taxType”: string, // Loại thuế của sản phẩm (“khau\_tru” hoặc “truc\_tiep”)  “taxRate”: string, // Mức thuế khấu trừ tương ứng (Cho phép các giá trị: 0, 5, 8, 10, “KCT”, “KKKNT”) (áp dụng nếu taxType = “khau\_tru”)  “taxRateDirect”: decimal? // Tỷ lệ tính thuế trực tiếp (%) (Cho phép các giá trị: 1, 2, 3, 5, null) (áp dụng nếu taxType = “truc\_tiep”)  “productTaxs”: [                 {                     “id”: “long”,                     “productId”: “long”, // ID hàng hóa                     “taxId”: “int”, // ID thuế                     “value”: “decimal?”, // Mức thuế                     “name”: “string” // Tên mức thuế                 }             ],             “purchaseTax”: {                 “id”: “long”,                 “productId”: “long”, // ID hàng hóa                 “taxId”: “int”, // ID thuế                 “value”: “decimal?”, // Mức thuế                 “name”: “string” // Tên mức thuế             }  }     ]  } |

#### **2.4.2. Lấy chi tiết hàng hóa**

**–****Mục đích sử dụng**: Trả lại chi tiết của một sản phẩm cụ thể theo ID, theo Code

**– Phương thức và URL:**

- Theo Id : **GET** https://public.kiotapi.com/products/{id}
- Theo Code : **GET** https://public.kiotapi.com/products/code/{code}
- Có lấy thuộc tính đã xóa mềm của hàng hóa: **GET**https://public.kiotapi.com/products/{id}?includeSoftDeletedAttribute=true

**[​](https://public.kiotapi.com/products/code%7bcode%7d)–** **Request:** Sử dụng hàm **GET** với tham số:

***“id”***: long // ID của hàng hóa
***“code”***: string // Mã của hàng hóa

*“includeSoftDeletedAttribute”*: bool //Có lấy thông tin danh sách thuộc tính bị xóa của hàng hóa (mặc định là true nếu không truyền tham số này => Nghĩa là lấy tất cả thuộc tính bao gồm thuộc tính đã bị xóa. Ngược lại nếu = false thì loại bỏ các thuộc tính đã bị xóa).

**– Response:**

|  |
| --- |
| {  “id”: long, // ID hàng hóa  “code”: string, // Code hàng hóa  “barCode”: string, // Mã vạch hàng hóa  “retailerId”: int, // ID cửa hàng  “allowsSale”: Boolean?, // Sản phẩm được bán trực tiếp hay không  “name”: string, // Tên sản phẩm  “categoryId”: int, // ID của nhóm hàng hóa  “tradeMarkId”: int, // ID của thương hiệu  “type”: byte?, // Loại hàng hóa  “categoryName”: string, // Tên của nhóm hàng hóa  “fullName”: string, // Tên sản phẩm bao gồm unit và thuộc tính?   “description”: string, // Mô tả sản phẩm  “hasVariants”: Boolean?, // Sản phẩm có thuộc tính hay không  “attributes”: // Danh sách thuộc tính  [{  “productId”: long, // ID thuộc tính  “attributeName”: string, // Tên thuộc tính  “attributeValue”: string // Giá trị thuộc tính  }],  “unit”: string, // Đơn vị tính của 1 sản phẩm,  “masterProductId”: long?,  “masterUnitId”: long, // ID của hàng hóa đơn vị cơ bản (null)  “conversionValue”: double?, // Đơn vị quy đổi  “units”: // Danh sách đơn vị tính  [{  “id”: long, // ID sản phẩm  “code”: string, // Mã sản phẩm ,  “name”: string, //Tên sản phẩm  “fullName”: string, // Tên sản phẩm bao gồm thuộc tính và đơn vị tính       “unit”: string, // Đơn vị tính  “conversionValue”: double, // Đơn vị quy đổi  “basePrice”: decimal, // Giá bán của sản phẩm  }],  “images”: string [], // Danh sách hình ảnh của hàng hóa          “inventories”: // Danh sách tồn kho trên các chi nhánh  [{  “productId”: long, // Id của sản phẩm  “productCode”: string, // Mã của sản phẩm  “productName”: string, // Tên của sản phẩm  “branchId”: long, // Id của chi nhánh  “branchName”: long, // Tên của chi nhánh  “onHand”: double?, // Tồn kho theo chi nhánh  “cost”: decimal?, // Giá sản phẩm  “reserved”: double // Đặt hàng theo chi nhánh  }],  “priceBooks”: // Danh sách bảng giá, mặc định có bảng giá chung  [{  “priceBookId”: long, // ID bảng giá  “priceBookName”: string, // Tên bảng giá  “productId”: long// ID sản phẩm  “isActive”: Boolean, // Có được sử dụng?  “startDate”: datetime?, // Có hiệu lực từ ngày  “endDate”: datetime?, // Có hiệu lực đến ngày  “price”: decimal, // Giá bán theo bảng giá  }],   “productFormulas”: // Danh sách hàng thành phần (nếu có)  [{  “materialId”: long, // ID hàng thành phần  “materialCode”: string, // Mã hàng thành phần  “materialFullName”: string// Tên hàng thành phần bao gồm thuộc tính và đơn vị tính  “materialName”: string, // Tên hàng thành phần  “quantity”: int, // Số lượng  “basePrice”: decimal, // Giá bán hàng thành phần  “productId”: long?, // ID hàng thành phần  “product”: // Chi tiết hàng thành phần                         {  “createdDate”: datetime?, // Ngày tạo hàng hóa  “id”: long, // ID hàng thành phần  “retailerId”: long, // ID cửa hàng  “code”: string , // Mã hàng thành phần  “name”: string?, // Tên hàng thành phần  “fullName”: datetime?, // Tên hàng thành phần bao gồm thuộc tính và đơn vị tính  “categoryId”: int, // ID của nhóm hàng hóa  “allowsSale”: Boolean, // Sản phẩm được bán trực tiếp hay không  “hasVariants”: Boolean?, // Sản phẩm có thuộc tính hay không  “basePrice”: decimal, // Giá bán của sản phẩm  “unit”: string, // Đơn vị tính  “conversionValue”: double?, // Đơn vị quy đổi  “modifiedDate”: datetime?, // Ngày gần nhất có cập nhật hàng hóa  “isActive”: Boolean, // Trạng thái kinh doanh hàng hóa (true: Đang kinh doanh | false: ngừng kinh doanh)  “isRewardPoint”: bool?, // Có tích điểm hay không  “orderTemplate”: string //Mẫu ghi chú (hóa đơn đặt hàng)  }  }],  “basePrice”: decimal, // giá sản phẩm  “weight”: double, // trọng lượng sản phẩm  “modifiedDate”: datetime, // thời gian cập nhật  “createdDate”: datetime, // thời gian tạo  “isLotSerialControl”: bool?,//Có phải imei hay không  “isBatchExpireControl”: bool?,//Có phải Hàng lô/ date hay không  “productSerials”:  // Danh sách Imei  [{  “productId”: long, //Id sản phẩm  “serialNumber”: string, //số serial Imei  “status”: int, // 1: còn hàng, 0: hết hàng  “branchId”: int, // id chi nhánh  “quantity”: double?, //Số lượng: 1  “createdDate”: datetime, //ngày tạo  “modifiedDate”: datetime?, //ngày sửa  }],  “productBatchExpires”: // Danh sách lô  [{  “productId”: long, //Id sản phẩm  “onHand”: double, //Tồn kho của lô  “batchName”:  string, //Tên lô  “expireDate”: datetime, //ngày hết hạn lô  “fullNameVirgule”: string, //Tên đầy đủ của lô  “branchId”: int, // ID chi nhánh  }]  “productShelves”: // Danh sách vị trí sản phẩm trên các chi nhánh  [{  “branchId”: long, // Id của chi nhánh  “branchName”: string, // Tên của chi nhánh  “ProductShelves”: string // Vị trí sản phẩm (Vị trí 1 | Vị trí 2)   ``` }] ```   “taxType”: string, // Loại thuế của sản phẩm (“khau\_tru” hoặc “truc\_tiep”)  “taxRate”: string, // Mức thuế khấu trừ tương ứng (Cho phép các giá trị: 0, 5, 8, 10, “KCT”, “KKKNT”) (áp dụng nếu taxType = “khau\_tru”)  “taxRateDirect”: decimal? // Tỷ lệ tính thuế trực tiếp (%) (Cho phép các giá trị: 1, 2, 3, 5, null) (áp dụng nếu taxType = “truc\_tiep”)  “productTaxs”: [  {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  ],  “purchaseTax”: {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  } |

#### **2.4.3. Thêm mới hàng hóa**

**– Mục đích sử dụng**: Tạo mới hàng hóa

**– Phương thức và URL: POST** <https://public.kiotapi.com/products>

**– Request:** JSON mã hóa yêu cầu gồm 1 object hàng hóa:

|  |
| --- |
| {                     “name”: string, // Tên hàng hóa                   “code”: string, // Mã hàng hóa  “barCode”: string, // Mã vạch hàng hóa, tối đa 16 ký tự  “fullName”: string, // Tên sản phẩm bao gồm thuộc tính và đơn vị tính  “categoryId”: int, // Id nhóm hàng hóa  “allowsSale”: Boolean, // Sản phẩm được bán trực tiếp hay không  “description”: string, // Mô tả sản phẩm  “hasVariants”: boolean, // Sản phẩm có thuộc tính hay không  “isProductSerial”: true, // Có phải sản phẩm serial hay không  “attributes”: [{  “attributeName”: string, // Tên thuộc tính (Nếu tên thuộc tính chưa tồn tại trong hệ thống thì tự động tạo mới thuộc tính)  “attributeValue”: string // Giá trị thuộc tính  }], // Danh sách thuộc tính   “unit”: string, // Đơn vị tính của 1 sản phẩm   “masterProductId”: long?, //ID hàng hoá cùng loại   “masterUnitId”: long?, // ID của hàng hóa đơn vị cơ bản, = NULL nếu là đơn vị cơ bản   “conversionValue”: double,   “inventories”: [{  “branchId”: long, // ID của chi nhánh  “branchName”: long, // Tên của chi nhánh  “onHand”: double?, // Tồn kho theo chi nhánh  “cost”: decimal? // Giá sản phẩm  }], // Danh sách tồn kho trên các chi nhánh  “basePrice”: decimal?, // Giá sản phẩm  “weight”: double?, // Trọng lượng sản phẩm,  “images”: string [], // Danh sách hình ảnh hàng hóa (dạng link)  “productTaxs”: [  {  “taxId”: “int” // ID thuế bán hàng  }  ],  “purchaseTax”: {  “taxId”: “int” // ID thuế nhập hàng  }  } |

**– Response:**

|  |
| --- |
| {  “id”: int, // ID hàng hóa                 “code”: string, // Mã hàng hóa  “barCode”: string, // Mã vạch hàng hóa  “name”: string, // Tên hàng hóa  “fullName”: string, // Tên hàng hóa bao gồm thuộc tính và đơn vị tính  “description”: string, // Tên hàng hóa  “images”: string [], // Danh sách hình ảnh hàng hóa (dạng link)  “categoryId”: int,  “categoryName”: string,  “unit”: string,  “masterProductId”: long?,  “masterUnitId”: long,  “conversionValue”: double?,  “hasVariants”: Boolean, // Sản phẩm có thuộc tính hay không   “attributes”: [{  “productId”: long, // ID thuộc tính  “attributeName”: string, // Tên thuộc tính  “attributeValue”: string // Giá trị thuộc tính  }] // Danh sách thuộc tính  “basePrice”: decimal, // Giá bán  “inventories”: [{  “productId”: long, // ID của sản phẩm  “productCode”: string, // Mã của sản phẩm  “productName”: string, // Tên của sản phẩm  “branchId”: long, // ID của chi nhánh  “branchName”: long, // Tên của chi nhánh  “onHand”: double?, // Tồn kho theo chi nhánh  “cost”: decimal?, // Giá sản phẩm  “reserved”: double // Đặt hàng theo chi nhánh  }]  “basePrice”: decimal, // Giá bán theo bảng giá  “retailerId”: int, // ID cửa hàng  “modifiedDate”: datetime, // Thời gian cập nhật  “productTaxs”: [  {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  ],  “purchaseTax”: {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  } |
|  |

#### **2.4.4. Cập nhật hàng hóa**

**– Mục đích sử dụng**: Cập nhật hàng hóa theo ID

**–** **Phương thức và URL:** **PUT** https://public.kiotapi.com /products/id

**–** **Request:** Sử dụng hàm **PUT** với ID hàng hóa qua 1 object JSON.

***“branchId”***: int, //Id chi nhánh hiện tại
***“id”***: long // ID hàng hóa

**– Body**

|  |
| --- |
| {  “name”: string, // Tên hàng hóa                   “code”: string, // Mã hàng hóa  “barCode”: string, // Mã vạch hàng hóa, tối đa 16 ký tự  “categoryId”: int, // ID nhóm hàng hóa  “allowsSale”: Boolean, // Sản phẩm được bán trực tiếp hay không  “description”: string, // Mô tả sản phẩm  “hasVariants”: boolean, // Sản phẩm có thuộc tính hay không  “attributes”: [{  “attributeName”: string, // Tên thuộc tính (Nếu tên thuộc tính chưa tồn tại trong hệ thống thì tự động tạo mới thuộc tính)  “attributeValue”: string // Giá trị thuộc tính  }], // Danh sách thuộc tính  “unit”: string, // Đơn vị tính của 1 sản phẩm  “masterUnitId”: long, // ID của hàng hóa đơn vị cơ bản, = NULL nếu là đơn vị cơ bản  “conversionValue”: int, // Đơn vị quy đổi, = 1 nếu là đơn vị cơ bản  “inventories”:  [{   “branchId”: long, // ID của chi nhánh  “branchName”: long, // Tên của chi nhánh  “onHand”: double?, // Tồn kho theo chi nhánh   “cost”: decimal? // Giá sản phẩm  }], // Danh sách tồn kho trên các chi nhánh  “basePrice”: decimal, // Giá sản phẩm  “weight”: double, // Trọng lượng sản phẩm,  “isActive”: bool?, // Trạng thái hóa động (true: đang hoạt động | false: ngừng hoạt động)  “isRewardPoint”: bool?, // Có tích điểm hay không  “productTaxs”: [  {  “taxId”: “int” // ID thuế bán hàng  }  ],  “purchaseTax”: {  “taxId”: “int” // ID thuế nhập hàng  }  } |

**– Response:**

|  |
| --- |
| {  “id”: int, // ID hàng hóa                 “code”: string, // Mã hàng hóa  “barCode”: string, //Mã vạch hàng hóa  “name”: string, // Tên hàng hóa  “fullName”: string, // Tên hàng hóa bao gồm thuộc tính và đơn vị tính   “description”: string, // Tên hàng hóa   “images”: string [], // Danh sách hình ảnh hàng hóa (dạng link)   “categoryId”: int,   “categoryName”: string,  “unit”: string,   “masterUnitId”: long,  “conversionValue”: double,  “hasVariants”: boolean, // Sản phẩm có thuộc tính hay không  “attributes”: [{  “attributeName”: string, // Tên thuộc tính  “attributeValue”: string // Giá trị thuộc tính   }] // Danh sách thuộc tính  “basePrice”: decimal, // Giá bán  “inventory”: [{  “productId”: long, // ID của sản phẩm  “productCode”: string, // Mã của sản phẩm  “productName”: string, // Tên của sản phẩm  “branchId”: long, // Id của chi nhánh  “branchName”: long, // Tên của chi nhánh   “onHand”: double?, // Tồn kho theo chi nhánh  “cost”: decimal?, // Giá vốn sản phẩm  “reserved”: double // Đặt hàng theo chi nhánh  }] // Danh sách tồn kho trên các chi nhánh  “basePrice”: decimal, // Giá bán theo bảng giá  “retailerId”: int, // ID cửa hàng  “modifiedDate”: datetime, // Thời gian cập nhật  “productTaxs”: [  {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  ],  “purchaseTax”: {  “id”: “long”,  “productId”: “long”, // ID hàng hóa  “taxId”: “int”, // ID thuế  “value”: “decimal?”, // Mức thuế  “name”: “string” // Tên mức thuế  }  } |

#### **2.4.5. Xóa hàng hóa**

**– Mục đích sử dụng**: Xóa hàng hóa theo ID

**–** **Phương thức và URL:** **DELETE** [https://public.kiotapi.com/products/{id}](https://public.kiotapi.com/products/%7bid%7d)

**– Request:** Gồm Id của hàng hóa trong URL:

***“id”***: long // ID của hàng hóa

**–** **Response:** Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

#### **2.4.6. Lấy thông tin thuộc tính sản phẩm**

**–** **Mục đích sử dụng**: lấy toàn bộ thông tin thuộc tính của tất cả các sản phẩm

**– Phương thức và URL**: **GET** <https://public.kiotapi.com/attributes/allwithdistinctvalue>

**– Response:****​**

|  |
| --- |
| [{  “name”: string, //tên thuộc tính  “id”: long, //id của thuộc tính  “attributeValues”:[  {  “value”: string, //giá trị của thuộc tính  “attributeId” long, // id của thuộc tính  },  {  “value”: string, //giá trị của thuộc tính  “attributeId” long, // id của thuộc tính  },  …  ]  }] |

#### **2.4.7. Thêm mới danh sách hàng hóa**

**– Mục đích sử dụng**: Tạo mới danh sách hàng hóa

**–** **Phương thức và URL:** **POST** https://public.kiotapi.com/listaddproducts

**–** **Request:** JSON mã hóa yêu cầu gồm 1 danh sách object hàng hóa riêng biệt với nhưng tham số sau:

|  |
| --- |
| {   ```     "listProducts": [ ```  ```         { ```  ```             "name": string, // Tên hàng hóa   ```  ```             "code": string, // Mã hàng hóa ```  ```             "fullName": string, // Tên sản phẩm bao gồm unit và thuộc tính? ```  ```             "categoryId": int, // ID nhóm hàng hóa ```  ```             "allowsSale": Boolean, // Sản phẩm được bán trực tiếp hay không ```  ```             "description": string, // Mô tả sản phẩm, ```  ```             "hasVariants": boolean, // Sản phẩm có thuộc tính hay không ```  ```             "attributes": [ ```  ```                 { ```  ```                     "attributeName": string, // Tên thuộc tính (Nếu tên thuộc tính chưa tồn tại trong hệ thống thì tự động tạo mới thuộc tính) ```  ```                     "attributeValue": string // Giá trị thuộc tính ```  ```                 } ```  ```             ], // Danh sách thuộc tính ```  ```             "unit": string, // Đơn vị tính của 1 sản phẩm ```  ```             "masterProductId": long?, //ID hàng hoá cùng loại ```  ```             "masterUnitId": long, // ID của hàng hóa đơn vị cơ bản, = NULL nếu là đơn vị cơbản ```  ```             "conversionValue": double, ```  ```             "branchId": int?, //ID chi nhánh hiện tại ```  ```             "inventories": [ ```  ```                 { ```  ```                     "branchId": long, // ID của chi nhánh ```  ```                     "branchName": long, // Tên của chi nhánh ```  ```                     "onHand": double?, // Tồn kho theo chi nhánh ```  ```                     "cost": decimal? // Giá sản phẩm ```  ```                 } ```  ```             ], // Danh sách tồn kho trên các chi nhánh ```  ```             "basePrice": decimal, // Giá sản phẩm ```  ```             "weight": double, // Trọng lượng sản phẩm ```  ```             "images": string [], // Danh sách hình ảnh của hàng hóa dạng link, ```  ```             "productTaxs": [ ```  ```                 { ```  ```                     "taxId": int // ID thuế bán hàng ```  ```                 } ```  ```             ], ```  ```             "purchaseTax": { ```  ```                 "taxId": int // ID thuế nhập hàng ```  ```             } ```  ```         } ```  ```     ] ```  ``` } ``` |

**– Response:**

|  |
| --- |
| {   ```                "message": "Thêm mới danh sách sản phẩm thành công" ```  ``` }     ``` |

**2.4.8. Cập nhật danh sách hàng hóa**

**– Mục đích sử dụng**: Cập nhật danh sách hàng hóa

**– Phương thức và URL: PUT** https://public.kiotapi.com/listupdatedproducts

**–** **Request:** JSON mã hóa yêu cầu gồm 1 danh sách object hàng hóa riêng biệt với nhưng tham số sau: 

|  |
| --- |
| {   ```     "listProducts": [ ```  ```         { ```  ```             "id": long, // ID của hàng hóa    ```  ```             "name": string, // Tên hàng hóa   ```  ```             "code": string, // Mã hàng hóa ```  ```             "fullName": string, // Tên hàng hóa bao gồm thuộc tính và đơn vị tính ```  ```             "categoryId": int, // ID nhóm hàng hóa ```  ```             "allowsSale": Boolean, // Sản phẩm được bán trực tiếp hay không ```  ```             "description": string, // Mô tả sản phẩm ```  ```             "hasVariants": boolean, // Sản phẩm có thuộc tính hay không ```  ```             "attributes": [ ```  ```                 { ```  ```                     "attributeName": string, // Tên thuộc tính (Nếu tên thuộc tính chưa tồn tại trong hệ thống thì tự động tạo mới thuộc tính) ```  ```                     "attributeValue": string // Giá trị thuộc tính ```  ```                 } ```  ```             ], // Danh sách thuộc tính ```  ```             "unit": string, // Đơn vị tính của 1 sản phẩm ```  ```             "masterProductId": long?, //ID hàng hoá cùng loại ```  ```             "masterUnitId": long, // ID của hàng hóa đơn vị cơ bản, = NULL nếu là đơn vị cơ bản ```  ```             "conversionValue": double, ```  ```             "branchId": int?, // ID chi nhánh hiện tại ```  ```             "inventories": [ ```  ```                 { ```  ```                     "branchId": long, // ID của chi nhánh ```  ```                     "branchName": long, // Tên của chi nhánh ```  ```                     "onHand": double?, // Tồn kho theo chi nhánh ```  ```                     "cost": decimal? // Giá sản phẩm ```  ```                 } ```  ```             ], // Danh sách tồn kho trên các chi nhánh ```  ```             "basePrice": decimal, // Giá sản phẩm ```  ```             "weight": double, // Trọng lượng sản phẩm, ```  ```             "images": string [], // Danh sách hình ảnh của hàng hóa Image: link ảnh của hàng hóa ```  ```             "productTaxs": [ ```  ```                 { ```  ```                     "taxId": int // ID thuế bán hàng ```  ```                 } ```  ```             ], ```  ```             "purchaseTax": { ```  ```                 "taxId": int // ID thuế nhập hàng ```  ```             } ```  ```         } ```  ```     ] ```  ``` } ``` |

**– Response:**

|  |
| --- |
| {   ```         "message": "Cập nhật danh sách sản phẩm thành công" } ``` |

#### **2.4.9. Lấy danh sách tồn kho hàng hóa**

**Mục đích sử dụng**: Trả về toàn bộ hàng hóa theo cửa hàng đã được xác nhận (authenticated retailer)

**Phương thức và URL:** **GET**https://public.kiotapi.com/productOnHands

**Request:** Sử dụng hàm GET với tham số: 

|  |
| --- |
| {      “orderBy”: string, optional //Sắp xếp dữ liệu theo trường orderBy (ví dụ: orderBy=Code)      “lastModifiedFrom”: datetime? // thời gian cập nhật      “branchIds”: [int] // danh sách chi nhánh,      “pageSize”: int, // số items trong 1 trang, mặc định 20 items, tối đa 100 items      “currentItem”: int, // lấy dữ liệu từ bản ghi currentItem   } |

Nếu có “*OrderDirection*“, chọn sắp xếp kết quả về theo:

- ASC (Mặc định)
- DESC

**Response:**

|  |
| --- |
| “total”: int, // Tổng số hàng hóa  “pageSize”: int,  “data”: [{      “id”: long, // ID hàng hóa      “code”: string, // Code hàng hóa      “createdDate”: datetime? // ngày tạo      “modifiedDate”: datetime? //ngày cập nhật      “inventories”: [          {           “branchId”: long, // Id chi nhánh           “onhand”: double, // tồn kho           “reserved”: double, // đặt hàng kho          }      ], // danh sách tồn kho của hàng hóa theo chi nhánh   }], |

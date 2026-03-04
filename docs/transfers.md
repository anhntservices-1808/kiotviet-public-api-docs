### **2.16. Chuyển hàng**

#### **2.16.1. Lấy danh sách chuyển hàng**

**– Mục đích sử dụng**: Trả về danh sách phiếu chuyển hàng.

**– Phương thức và URL: GET** <https://public.kiotapi.com/transfers>

– **Request:** Sử dụng hàm GET với tham số

|  |
| --- |
| {  “toBranchIds”: int[], optional // IDs chi nhánh nhận  “fromBranchIds”: int[], optional // IDs chi nhánh chuyển  “status”: int[], optional // Tình trạng phiếu chuyển  “pageSize”: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items                  “currentItem”: int?, // Lấy dữ liệu từ bản ghi currentItem,                  “fromReceivedDate”: DateTime?, // Từ thời gian nhận chuyển hàng,                  “toReceivedDate”: DateTime?, // Đến thời gian nhận chuyển hàng,                  “fromTransferDate”: DateTime?, // Từ thời gian chuyển hàng,                  “toTransferDate”: DateTime?, // Đến thời gian chuyển hàng  } |

– **Respones:**

|  |
| --- |
| {  “total”: int,  “pageSize”: int,  “data”: [{  “id”: long //Id phiếu  “code”: string //Mã phiếu  “fromBranchId”: int, //Id chi nhánh chuyển  “toBranchId”: int, // Id chi nhánh nhận  “status”: int, //trạng thái phiếu chuyển  “retailerId”: long, // Id gian hàng  “description”: string, // ghi chú  “transferDetails” :[{  “productId”: long, // Id hàng hóa  “ProductCode”: string, // mã hàng hóa  “sendQuantity”: double, // Số lượng hàng hóa chuyển  “recieveQuantity”: double, // Số lượng hàng hóa nhận  “price”: decimal, //Giá trị  “sendPrice”: decimal,// giá chuyển  “receivePrice”: decimal, // giá nhận  }]// Thông tin chuyển hàng chi tiết  }]  } |

#### **2.16.2. Lấy chi tiết chuyển hàng**

**– Mục đích sử dụng**: Trả lại chi tiết của một phiếu chuyển hàng cụ thể theo ID

**– Phương thức và URL:**

Theo Id : **GET**[https://public.kiotapi.com/transfers/{id}](https://public.kiotapi.com/products/%7bid%7d)

**– Request:** Sử dụng hàm GET với tham số: “id”: long // ID của phiếu chuyển hàng

**– Response**

|  |
| --- |
| {  “id”: long, //ID phiếu chuyển hàng  “code”: string, //Mã phiếu chuyển hàng  “status”: int, // Trạng thái phiếu chuyển hàng  “transferredDate”: datetime, // Ngày chuyển  “receivedDate”: datetime, // Ngày nhận  “createdById”: long, // ID người tạo  “createdByName”: string, //Tên người tạo  “fromBranchId”: long, // ID chi nhánh nguồn  “fromBranchName”: string, // Tên chi nhánh nguồn  “toBranchId”: long, // ID chi nhánh đích  “toBranchName”: string, //Tên chi nhánh đích  “noteBySource”: string, // Ghi chú nguồn  “noteByDestination”: string, // ghi chú đích  “details”: [  {  “id”: long, //ID chi tiết phiếu chuyển hàng  “productId”: long, // ID sản phẩm  “productCode”: string, // Mã sản phẩm  “productName”: string, // Tên sản phẩm  “transferredQuantity”: int, // Số lượng sản phẩm  “price”: decimal, // Đơn giá sản phẩm  “totalTransfer”: decimal, // Tổng tiền chuyển  “totalReceive”: decimal // Tổng tiền nhận  }  ]  } |

#### **2.16.3. Thêm mới chuyển hàng**

**– Mục đích sử dụng**: Trả về danh sách phiếu chuyển hàng.

**– Phương thức và URL: POST**<https://public.kiotapi.com/transfers>

– **Request body**

|  |
| --- |
| {  “fromBranchId”: long, //id chi nhánh chuyển  “toBranchId”: long, //id chi nhánh nhận  “isDraft”: int, //id chi nhánh nhận  “code”: string, //id chi nhánh nhận  “description”: string, //id chi nhánh nhận  “status”: int, //id chi nhánh nhận  “transferDetails”: [  {  “productCode”: string, //mã hàng hóa  “productId”: long, //id hàng hóa  “sendQuantity”: double, //số lượng chuyển  “recivedQuantity”: double, //số lượng nhận  “price”: decimal //giá chuyển  }  ] //danh sách chi tiết phiếu chuyển  }  {  “message”: string, // thông báo thành công  “data”: {  “code”: string, // Mã phiếu  chuyển  “description”: string, // Nội dung  ghi chú  “dispatchedDate”: datetime, // Ngày  chuyển  “fromBranchId”: long, // id chi  nhánh chuyển  “id”: long, // id phiếu  chuyển  “isActive”: bool, // trạng thái  “retailerId”: long, // id  retailer  “status”: int, // trạng thái  phiếu chuyển  “toBranchId”: long, // id chi nhánh chuyển  “transferDetails”: [  {  “productCode”: string, //mã hàng hóa  “productId”: long, //id hàng hóa  “sendQuantity”: double, //số lượng chuyển  “recivedQuantity”: double, //số lượng nhận  “sendPrice”: decimal, //giá chuyển  “receivePrice”: decimal, //giá nhận  “price”: decimal  }  ]  }  } |

#### **2.16.4. Cập nhật chuyển hàng**

**– Mục đích sử dụng:** Cập nhật phiếu chuyển hàng theo ID

**– Phương thức và URL: PUT**[**https://public.kiotapi.com**](https://public.kiotapi.com/ "https://public.kiotapi.com/")**/**[**transfers**](https://public.kiotapi.com/transfers "https://public.kiotapi.com/transfers")**/id**

**– Request:**Sử dụng hàm PUT với ID phiếu chuyển hàng qua 1 object JSON
“id”: long // ID phiếu chuyển hàng.

**Body**

|  |
| --- |
| {      “fromBranchId”: long, // ID chi nhánh nguồn      “toBranchId”: long, // ID chi nhánh đích         “isDraft”: boolean,  // Tạo dạng phiếu tạm                 “code”: string, // Mã phiếu chuyển           “description”: string, // Mô tả           “status”: int, // Trạng thái phiếu chuyển      “transferDetails”: [          {              “transferId”: long, // ID phiếu chuyển              “productCode”: string,   // Mã sản phẩm              “productId”: long,     // ID sản phẩm                “sendQuantity”: double, // Số lượng gửi                 “recivedQuantity”: double, // Số lượng nhận              “price”: decimal // Đơn giá          }      ]                                  } |

**Response:**

|  |
| --- |
| {      “message”: string, // Thông báo trạng thái trả về, thành công/thất bại      “data”: {          “code”: string, // Mã phiếu chuyển  “description”: string, // Mô tả          “dispatchedDate”: datetime, // Ngày tạo          “fromBranchId”: long, // ID chi nhánh nguồn          “id”: long, // ID phiếu chuyển          “isActive”: boolean, // đang hoạt động ?          “retailerId”: long, // ID gian hàng          “status”: int, // Trạng thái          “toBranchId”: long, // ID chi nhánh đích          “transferDetails”: [              {                  “productId”: long, // ID sản phẩm                  “productCode”: string, // Mã sản phẩm                  “sendQuantity”: double, // Số lượng gửi                  “receiveQuantity”: double, // Số lượng nhận                  “sendPrice”: decimal, // Giá gửi                  “receivePrice”: decimal, // Giá nhận                  “price”: decimal, // Đơn giá                  “transferId”: long// ID phiếu chuyển              }          ]      }  } |

#### **2.16.5. Xóa phiếu chuyển hàng**

– **Mục đích sử dụng**: Xóa phiếu chuyển hàng theo ID
– **Phương thức và URL**: DELETE https://public.kiotapi.com/transfers/{id}
– **Request**: Gồm Id của phiếu chuyển hàng: 
     “id”: long // ID của phiếu chuyển hàng
– **Response**: Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

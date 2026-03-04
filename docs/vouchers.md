### **2.24. Voucher**

#### **2.24.1. Lấy danh sách đợt phát hành**

**– Mục đích sử dụng**: Trả về danh sách đợt phát hành voucher và chi tiết đợt phát hành.

**– Phương thức và URL: GET** [https://public.kiotapi.com/vouchercampaign](https://public.kiotapi.com/transfers)

– **Request:** Sử dụng hàm GET với tham số

“includeVoucherBranchs”: Boolean, optional //có lấy thông tin danh sách chi nhánh áp dụng voucher

  “includeVoucherUsers”: Boolean, optional //có lấy thông tin danh sách người tạo áp dụng voucher

  “isActive”: Boolean, optional //trạng thái đợt phát hành

  “id”: long,optional //id đợt phát hành

  “isGlobal”: boolean,optional //có áp dụng cho toàn hệ thống

  “forAllCusGroup”: boolen,optional //có áp dụng cho toàn bộ khách hàng

  “forAllUser”: boolean,optional //có áp dụng cho toàn bộ người tạo

– **Respones:**

|  |
| --- |
| {    “total”: int, //tổng    “data”: [{        “id”: long, //id đợt phát hành        “code”: string, //mã đợt phát hành        “name”: string, //tên đợt phát hành        “isActive”: boolean, //trạng thái đợt phát hành        “startDate”: datetime, //thời gian áp dụng bắt đầu        “endDate”: datetime, //thời gian áp dụng kết thúc        “expireTime”: long, //số ngày kể từ ngày phát hành sẽ hết hạn sử dụng voucher        “prereqCategoryIds”: int[], //danh sách id nhóm hàng        “prereqProductIds”: long[], //danh sách id hàng hóa        “prereqPrice”: decimal, //tổng tiền hàng        “quantity”: int, //tổng số voucher        “price”: decimal, //mệnh giá        “useVoucherCombineInvoice”: boolean, //áp dụng gộp nhiều voucher trên 1 hóa đơn        “isGlobal”: boolean, //có áp dụng cho toàn hệ thống        “forAllCusGroup”: boolen, //có áp dụng cho toàn bộ khách hàng        “forAllUser”: boolean, //có áp dụng cho toàn bộ người tạo        “voucherBranchs”: [{              “branchId”: int, //id chi nhánh              “branchName”: string, //tên chi nhánh        }],        “voucherUsers”: [{              “userId”: int, //id người tạo              “userName”: string, //tên người tạo        }]    }]  } |

#### **2.24.2. Lấy danh sách voucher trong đợt phát hành**

**– Mục đích sử dụng**: Trả về danh sách voucher trong đợt phát hành.

**– Phương thức và URL:**

Theo Id : **GET**[https://public.kiotapi.com/voucher](https://public.kiotapi.com/products/%7bid%7d)

**– Request:** Sử dụng hàm GET với tham số:

“campaignId”: long, //id đợt phát hành voucher

 “status”: int, optional //trạng thái = [0: chưa sử dụng | 1: đã phát hành | 2: đã sử dụng | 3: đã hủy]

**– Response**

|  |
| --- |
| {    “total”: int, //tổng      “data”: [{          “id”: long, //id voucher          “code”: string, //mã voucher          “voucherCampaignId”: long, //id đợt phát hành voucher          “releaseDate”: datetime, //ngày phát hành          “expireDate”: datetime, //ngày hết hạn          “usedDate”: datetime, //ngày sử dụng          “status”: int, //trạng thái = [0: chưa sử dụng | 1: đã phát hành | 2: đã sử dụng | 3: đã hủy]          “sellType”: int, //hình thức = [0: tặng | 1: bán]          “price”: decimal, //giá trị voucher          “partnerType”: string, //nhóm người mua nhận voucher = [U: nhân viên | C: khách hàng | S: nhân viên | O: khác | D: Đối tác giao hàng]          “partnerId”: long, //id người mua nhận voucher          “partnerName”: string, //tên người mua nhận voucher  }]  } |

#### **2.24.3. Tạo mới voucher**

**– Mục đích sử dụng**: Tạo mới voucher theo đợt phát hành.

**– Phương thức và URL: POST**[https://public.kiotapi.com/voucher](https://public.kiotapi.com/transfers)

– **Request**: Sử dụng hàm POST với tham số:

|  |
| --- |
| {      “voucherCampaignId”: long, //id đợt phát hành voucher đang ở trạng thái kích hoạt      “data”: [{          “code”: string, //mã voucher      }]  } |

– **Response**:

|  |
| --- |
| {      “message”: “Thêm mới voucher thành công”  } |

#### **2.24.4. Phát hành voucher**

**– Mục đích sử dụng:** Phát hành voucher theo đợt phát hành (theo hình thức tặng)

**– Phương thức và URL: POST**[**https://public.kiotapi.com/voucher/release/give**](https://public.kiotapi.com/ "https://public.kiotapi.com/")

**– Request**:Sử dụng hàm POST với tham số:

|  |
| --- |
| {                      “CampaignId”: long, //id đợt phát hành voucher đang ở trạng thái kích hoạt                       “Vouchers”: [                       {                                         “Code”: string, //mã voucher                        }      ], // chỉ áp dụng với voucher đang ở trạng thái là 0: chưa sử dụng      “ReleaseDate”: datetime, //ngày phát hành  } |

**– Response:**

|  |
| --- |
| {      “message”: “Cập nhật voucher thành công”  } |

#### **2.24.5. Hủy voucher**

– **Mục đích sử dụng**: Hủy voucher theo đợt phát hành
– **Phương thức và URL**: DELETE https://public.kiotapi.com/voucher/cancel
– **Request**: Sử dụng hàm POST với tham số:

|  |
| --- |
| {                      “CampaignId”: long, //id đợt phát hành voucher đang ở trạng thái kích hoạt                       “Vouchers”: [                       {                                         “Code”: string, //mã voucher                        }], // chỉ áp dụng với voucher đang ở trạng thái là 0: chưa sử dụng  } |

– **Response**: Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {      “message”: “Cập nhật voucher thành công”  } |

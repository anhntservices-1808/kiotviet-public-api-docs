### **2.11. Webhook**

Webhook là mô hình một public API chủ động gọi vào một server của bên thứ ba khi có thay đổi xảy ra. Nó tương đương với mô hình data push (trái ngược với polling), trong đó server chủ động gọi cho client thay vì client phải thường xuyên kiểm tra server.

**Lưu ý:**

– Thời gian phản hồi của một yêu cầu tối đa là 5 giây, vượt qua ngưỡng này thì yêu cầu gửi từ KiotViet sang bên đăng ký được tính là thất bại.

– Bên đăng ký hãy lựa chọn mã trạng thái và cách xử lý với yêu cầu không hợp lệ một cách hợp lý, vì trong trường hợp yêu cầu gửi đến là từ phía KiotViet, và mã trạng thái phản hồi của bên đăng ký thuộc một trong số các mã 4xx (400, 401, 403, 404, 405) thì dịch vụ webhook KiotViet sẽ ngưng việc gửi yêu cầu tới điểm cuối đó.

API Webhook được mô tả chi tiết như bên dưới:

#### **2.11.1. Đăng ký Webhook**

**–** **Mục đích sử dụng:** Đăng ký webhook

**– Phương thức và URL: POST** <https://public.kiotapi.com/webhooks>

**– Request:**

|  |
| --- |
| {                      “Webhook”: {                     “Type”: string, //Kiểu sự kiện                                          “Url”: string, //Địa chỉ đăng ký (điểm cuối)                          “IsActive”: boolean, //Trạng thái hoạt động                          “Description”: string,  //Mô tả                           “Secret”: string  //Mã bí mật (không bắt buộc sử dụng)      }  } |

**– Response:**

|  |
| --- |
| {                                      “id”: long, //webhook id                       “type”: string, //Kiểu sự kiện                      “url”: string, //Địa chỉ đăng ký (điểm cuối)                         “isActive”: boolean, //Trạng thái hoạt động      “retailerId”: int, //Id cửa hàng       “description”: string, //Mô tả  } |

**Thông tin về mã bí mật**:

KiotViet triển khai việc tạo chữ ký sử dụng thuật toán HMAC SHA-256 từ mã bí mật **(secret)** do bên đăng ký cung cấp khi tạo webhook kết hợp với dữ liệu **(request body)** từ yêu cầu gửi tới bên đăng ký.

|  |
| --- |
| var hash = body.CreateHmacSignature(Secret); //Using HMAC SHA-256 algorithm  httpRequest.Headers.Add(“X-Hub-Signature”, hash); |

Lưu ý:

– Cơ chế tạo chữ ký này chỉ giúp đảm bảo “tính xác thực” (authenticity) rằng dữ liệu thực sự được gửi từ nguồn mà bên đăng ký mong muốn (ở đây chính là dịch vụ webhook của KiotViet).

– Cơ chế này không mã hoá dữ liệu (payload) hoặc cung cấp thêm bất kỳ tính bảo mật nào khác (confidentiality), dữ liệu vẫn sẽ ở dạng văn bản thuần túy (plain text), do đó điểm cuối của bên đăng ký phải luôn được bảo mật bằng HTTPS.

**Cách sử dụng mã bí mật**:

1. Tạo và lưu trữ mã bí mật ngẫu nhiên (8 ký tự trở lên), sau đó mã hoá các ký tự này bằng Base64

2. Khi đăng ký webhook, trong yêu cầu đăng ký truyền thêm **Secret** với giá trị là mã bí mật đã được mã hoá ở bước 1:

|  |
| --- |
| {      “Webhook”: {          “Type”: String, //Kiểu sự kiện          “Url”: String, //Địa chỉ đăng ký (điểm cuối)          “IsActive”: Boolean, //Trạng thái hoạt động          “Description”: String, //Mô tả          “Secret”: String //Mã bí mật đã được mã hoá Base64      }  } |

3. Khi có sự kiện phát sinh, KiotViet sẽ tạo ra chữ ký từ mã bí mật do bên đăng ký cung cấp **(secret)** và dữ liệu của yêu cầu gửi sang bên đăng ký **(request body)**, sau đó truyền chữ ký này thông qua header **X-Hub-Signature**, bên đăng ký sẽ cần lấy giá trị chữ ký từ header để so khớp với chữ ký do bên đăng ký tạo ra (bên đăng ký cũng sẽ tạo ra chữ ký dựa trên mã bí mật đã cung cấp cho KiotViet và dữ liệu do KiotViet gửi đến).

4. Nếu chữ ký không khớp thì bên đăng ký hãy bỏ qua yêu cầu đó và không xử lý nữa

5. Trả về mã trạng thái 401 nếu chữ ký không khớp.

Để an toàn hơn, bên đăng ký nên lưu trữ mã bí mật này một cách an toàn và nên thường xuyên thay đổi mã bí mật và đồng bộ mã này với dịch vụ webhook của KiotViet.

Lưu ý: Bên đăng ký hãy lựa chọn mã trạng thái và cách xử lý với yêu cầu không hợp lệ một cách hợp lý, vì trong trường hợp yêu cầu gửi đến là từ phía KiotViet và việc so khớp chữ ký không như mong muốn, dẫn đến bên đăng ký trả về một trong số các mã trạng thái 4xx (400, 401, 403, 404, 405) thì dịch vụ webhook KiotViet sẽ ngưng việc gửi yêu cầu tới điểm cuối đó.

#### **2.11.2. Hủy đăng ký Webhook**

**– Mục đích sử dụng:** Hủy đăng ký Webhook

**– Phương thức và URL: DELETE** [https://public.kiotapi.com/webhooks/{id}](https://public.kiotapi.com/webhooks/%7bid%7d)

**–** **Request:** Request sẽ bao gồm Id của webhook trong URL:

***“id”***: int // ID của Webhook

**– Response:** Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Hủy đăng ký webhook thành công”  } |

#### **2.11.3. Khách hàng**

– Cập nhật khách hàng: 
**customer.update**

|  |
| --- |
| {  “Id”: string,  “Attempt”: int,  “Notifications”: [{  “Action”: string,  “Data”: [{  “Id”: long,  “Code”: string,  “Name”: string,  “Gender”: bool?,  “BirthDate”: Datetime?,  “ContactNumber”: string,  “Address”: string,  “LocationName”: string,  “Email”: string,  “ModifiedDate”: DateTime,  “Type”: byte?,  “Organization”: string,  “TaxCode”: string,  “Comments”: string  }]  }]  } |

– Xóa khách hàng 
**customer.delete**

|  |
| --- |
| {“RemoveId”: int []} |

#### **2.11.4. Hàng hóa**

– Cập nhật hàng hóa:
**product.update**

|  |
| --- |
| {  “Id”: string,  “Attempt”: int,  “Notifications”: [{  “Action”: string,  “Data”: [{  “Id”: long,  “Code”: string,  “Name”: string,  “FullName”: string,  “CategoryId”: int,  “CategoryName”: string,  “masterProductId” : long?,  “AllowsSale”: bool,  “HasVariants”: bool,  “BasePrice”: Decimal,  “Weight”: double?,  “Unit”: string,  “MasterUnitId”: long?,  “ConversionValue”: double?,  “ModifiedDate”: DateTime?,  “Attributes”:[{  “ProductId”: long,  “AttributeName”: string,  “AttributeValue” : string  }],  “Units”:[{  “Id”: long,  “Code”: string,  “Name”: string,  “FullName”: string,  “Unit”: string  “ConversionValue”: double,  “BasePrice”: Decimal  }],  “Inventories”: [{  “ProductId”: long,  “ProductCode”: string,  “ProductName”: string,  “BranchId”: int,  “BranchName”: string,  “Cost”: Decimal,  “OnHand”: double,  “Reserved”: double  }],  “PriceBooks”:[{  “ProductId”: long,  “PriceBookId”: long,  “PriceBookName”: string,  “Price” : Decimal,  “IsActive”: bool,  “StartDate”: DateTime?,  “EndDate”: DateTime?  }],  “Images”: [{“Image”: string}]  }]  }]  } |

– Xóa hàng hóa:
**product.delete**

|  |
| --- |
| {“RemoveId”: int []} |

#### **2.11.5. Tồn kho**

– Cập nhật tồn kho
**stock.update**

|  |
| --- |
| {  “Id”: string,  “Attempt”: int,  “Notifications”: [{  “Action”: string,  “Data”: [{  “ProductId”: long,  “ProductCode”: string,  “ProductName”: string,  “BranchId”: int,  “BranchName”: string,  “Cost”: Decimal,  “OnHand”: double,  “Reserved”: double  }]  }]  } |

#### **2.11.6. Đặt hàng**

– Cập nhật đặt hàng
**order.update**

|  |
| --- |
| {  “Id”: string,  “Attempt”: int,  “Notifications”: [{  “Action”: string,  “Data”: [{  “Id”: long,  “Code”: string,  “PurchaseDate”: DateTime,  “BranchId”: int,  “SoldById”: long?,  “SoldByName”: string,  “CustomerId”: long?,  “CustomerCode”: string,  “CustomerName”: string,  “Total”: Decimal,  “TotalPayment”: Decimal,  “Discount”: Decimal?,  “DiscountRatio”: double?  “Status” : int,  “StatusValue”: string,  “Description”: string,  “UsingCod”: bool  “ModifiedDate”: Datetime?  “OrderDetails”:[{  “ProductId”: long,  “ProductCode”: string,  “ProductName”: string,  “Quantity”: double,  “Price”: Decimal,  “Discount”: Decimal?,  “DiscountRatio”: double?  }]  }]  }]  } |

#### **2.11.7. Hóa đơn**

– Cập nhật hóa đơn
**invoice.update**

|  |
| --- |
| {  “Id”: string,  “Attempt”: int,  “Notifications”:[{  “Action”: string,  “Data”: [{  “Id”: long,  “Code”: string,  “PurchaseDate”: DateTime,  “BranchId”: int,  “BranchName”: string,  “SoldById”: long,  “SoldByName”: string,  “CustomerId”: long?,  “CustomerCode”: string,  “CustomerName”: string,  “Total”: Decimal,  “TotalPayment”: Decimal,  “Discount”: Decimal?,  “DiscountRatio”: double?,  “Status”: byte, (1: hoàn thành, 2: đã hủy, 3: đang xử lý: 5: không giao được)  “StatusValue”: string,  “Description”: string,  “UsingCod”: bool,  “ModifiedDate”: DateTime?,  “InvoiceDelivery”: {  “DeliveryCode”: string,  “Status”: byte, (1: chưa giao hàng, 2: đang giao hàng, 3: đã giao hàng, 4: đang chuyển hoàn, 5 đã chuyển hoàn, 6: đã hủy  “StatusValue”: string,  “Type”: byte?,  “Price”: Decimal?,  “Receiver”: string,  “ContactNumber”: string,  “Address”: string,  “LocationId”: int?,  “LocationName”: string,  “Weight”: double?,  “Length”: double?,  “Width”: double?,  “Height”: double?,  “PartnerDeliveryId”: long?,  “PartnerDelivery”:{  “Code”: string,  “Name”: string,  “ContactNumber”:string,  “Address”: string,  “Email”: string  }  },  “InvoiceDetails”: [{  “ProductId”: long,  “ProductCode”: string,  “ProductName”: string,  “Quantity”: double,  “Price”: Decimal,  “Discount”: Decimal?,  “DiscountRatio”: double?  }],  “Payments”: [{  “Id”: long,  “Code”: string,  “Amount”: Decimal,  “AccountId”: int?,  “BankAccount”: string,  “Description”: string,  “Method”: string,  “Status”: byte?,  “StatusValue”: string,  “TransDate”: DateTime  }]  }]  }]  } |

#### **2.11.8. Bảng giá**

– **pricebook.update**: Nhận request khi có thay đổi thông tin của bảng giá.

|  |
| --- |
| {      “Id”: string,      “Attempt”: int,      “Notifications”: [{          “Action”: string,          “Data”: [{              “Id”: long                      // Id bảng giá              “Name”: string                  // tên bảng giá              “IsActive”: bool,           // trạng thái hoạt động hay không              “IsGlobal”: bool,           // có phải là bảng giá chung không              “StartDate”: date,          // ngày bắt đầu áp dụng              “EndDate”: DateTime,            // ngày hết hạn              “ForAllCusGroup”: bool,     // áp dụng cho tất cả nhóm khách hàng              “ForAllUser”: bool,         // áp dụng cho tất cả user              “PriceBookBranches” :[{                  “Id”: long,                 // Id quan hệ bảng giá – chi nhánh                  “PriceBookId”: long,        // Id bảng giá                  “BranchId”: long,           // Id chi nhánh áp dụng,                  “BranchName”: string,       // Tên chi nhánh áp dụng              }],              “PriceBookCustomerGroups” :[{                  “CustomerGroupName”: string,                  “Id”: long,                 // Id quan hệ bảng giá – nhóm khách hàng                  “PriceBookId”: long,        // Id bảng giá                  “CustomerGroupId”: long,    // Id nhóm khách hàng              }],              “PriceBookUsers” :[{                  “UserName”: string,         // Tên người dùng                  “Id”: long,                 // Id quan hệ                  “PriceBookId”: long,        // Id bảng giá                  “UserId”: long,             // Id người dùng              }],          }],      }]  } |

– **pricebook.delete:**Nhận request khi có bảng giá bị xóa.

|  |
| --- |
| {      “Id”: string,      “Attempt”: int,      “Notifications”: [{          “Action”: string          “Data”: [              long    // Id bảng giá          ]      }]  } |

– **pricebookdetail.update:**Nhận quest khi thông tin hàng hóa trong bảng giá thay đổi (ví dụ: thêm hàng hóa vào bảng giá).

|  |
| --- |
| {      “Id”: string,      “Attempt”: int,      “Notifications”: [{          “Action”: string          “Data”: [{              “PriceBookId”: long,    // Id bảng giá              “ProductId”: long,  // Id hàng hóa              “Price”: decimal          }]      }]  } |

– **pricebookdetail.delete:** Nhận request khi hàng hóa trong bảng giá bị xóa khỏi bảng giá.

|  |
| --- |
| {      “Id”: string,      “Attempt”: int,      “Notifications”: [{          “Action”: string,          “Data”: [{              “PricebookId”: long,    // Id bảng giá              “ProductIds”: [                  long                // ID hàng hóa bị xóa khỏi bảng giá              ]          }]      }]  } |

#### **2.11.9. Danh mục hàng hóa**

– **category.update**

|  |
| --- |
| {                      “Id”: string,      “Attempt”: int,      “Notifications”: [{                      “Action”: string,          “Data”: [{                                                               “Id”: int,          “Name”: string,          “ParentId”: int?,          “IsDeleted”: bool,          “CreatedDate”: Datetime,          “ModifiedDate”: Datetime?,          “RetailerId”: int,          “Rank”: int,          “HasChild”: bool              }]            }]         }]  } |

– **category.delete**

|  |
| --- |
| {      “RemoveId”: int []  } |

#### **2.11.10. Chi nhánh**

– **branch.update**

|  |
| --- |
| {                      “Id”: string,      “Attempt”: int,      “Notifications”: [{                      “Action”: string,          “Data”: [{                                                               “Id”: long,                                                               “Name” : string,                                                                “ContactNumber”:string,                                                                “SubContactNumber”: string,                                                                 “Address”: string,                                                                 “Location”: string,                                                                 “WardName”: string,                                                                 “IsActive”: bool,                                                                 “IsLock”: bool,                                                                 “CreatedDate”: Datetime,                                                                 “ModifiedDate”: Datetim? ,                                                                 “RetailerId”: int                }]            }]         }]  } |

– **branch.delete**

|  |
| --- |
| {      “RemoveId”: int []  } |

#### **2.11.11. Danh sách webhook**

– **Mục đích sử dụng**: Trả về thông tin danh sách webhook

– **Phương thức và URL**: GET <https://public.kiotapi.com/webhooks>

– **Request**: Sử dụng hàm GET

– **Response:**

|  |
| --- |
| {      “total”: int,      “pageSize”: int, //Số items trong 1 trang, mặc định 20 items, tối đa 100 items      “data”: [{          “id”: long, //Webhook id          “type”: string, //Loại webhook          “url”: string, //Địa chỉ đăng ký            “isActive”: boolean, //Trạng thái hoạt động          “retailerId”: int, //Id cửa hàng          “description”: string, //Mô tả          “modifiedDate”: datetime, //Thời gian      }]  } |

#### **2.11.12. Chi tiết webhook**

– **Mục đích sử dụng**: Trả lại thông tin chi tiết của webhook theo Id

**– Phương thức và URL**: GET <https://public.kiotapi.com/webhooks>/{id}

**– Request**: Sử dụng hàm GET

**– Response**:

|  |
| --- |
| {           “id”: long, //Webhook id      “type”: string, //Loại webhook      “url”: string, //Địa chỉ đăng ký        “isActive”: boolean, //Trạng thái hoạt động      “retailerId”: int, //Id cửa hàng      “description”: string, //Mô tả  } |

### **2.3. Nhóm hàng**

Mô tả chi tiết cho các liên quan đến thông tin nhóm hàng hóa như sau:

#### **2.3.1. Lấy danh sách nhóm hàng**

**– Mục đích sử dụng**: Trả về toàn bộ danh mục hàng hóa (nhóm hàng hóa). Danh sách này được sắp xếp theo thứ tự bảng chữ cái (a-z). Hệ thống chỉ cho phép nhóm hàng hóa có tối đa 3 cấp, và không cho phép xóa nhóm hàng cha nếu đang có chứa nhóm hàng con và không cho phép xóa nhóm hàng con nếu đang được sử dụng.

**– Phương thức và URL: GET** <https://public.kiotapi.com/categories>

**– Request:** Sử dụng hàm **GET** với tham số:

*“lastModifiedFrom”*: datetime? // thời gian cập nhật
*“pageSize”*: int?, // số items trong 1 trang, mặc định 20 items, tối đa 100 items
*“currentItem”*: int, // lấy dữ liệu từ bản ghi hiện tại, nếu không nhập thì mặc định là 0
*“orderBy”*: string, //Sắp xếp dữ liệu theo trường orderBy (Ví dụ: orderBy=name)
*“orderDirection”*: string, //Sắp xếp kết quả trả về theo: Tăng dần Asc (Mặc định), giảm dần Desc
*“hierachicalData”*: Boolean, // nếu HierachicalData=true thì mình sẽ lấy nhóm hang theo cấp mà không quan tâm lastModifiedFrom. Ngược lại, HierachicalData=false thì sẽ lấy 1 list nhóm hang theo lastModifiedFrom nhưng không có phân cấp

**– Response:**

- **Nếu *hierachicalData* là true**

|  |
| --- |
| “total”: int,  “pageSize”: int,  “data”:  [  {  “categoryId”: int, // ID nhóm hàng hóa  “parentId”: int?, // Nếu danh mục có danh mục cha thì có id cụ thể, nếu không có danh mục cha, ParentId=null  “categoryName”: string, // Tên nhóm hàng hóa  “retailerId”: int, // Id cửa hàng  “hasChild”: boolean?, // nhóm hàng có con hay không “modifiedDate”: datetime? // thời gian cập nhật “createdDate”: datetime  “children”: []  }],  “removedIds”: int [], // danh sách ID nhóm hàng bị xóa dựa trên Modified Date  “timestamp”: datetime  } |

- **Nếu *hierachicalData* là fasle**

|  |
| --- |
| “total”: int,  “pageSize:” int,  “data”: [  {  “categoryId”: int, // ID nhóm hàng hóa  “parentId”: int?, // Nếu danh mục có danh mục cha thì có id cụ thể, nếu không có danh mục cha, ParentId=null  “categoryName”: string, // Tên nhóm hàng hóa  “retailerId”: int, // Id cửa hàng  “hasChild”: boolean?, // nhóm hàng có con hay không  “modifiedDate”: datetime? // thời gian cập nhật  “createdDate”: datetime  }],  “removedIds”: int [], // danh sách ID nhóm hàng bị xóa dựa trên Modified Date  “timestamp”: datetime  } |

#### **2.3.2. Lấy chi tiết nhóm hàng**

**– Mục đich sử dụng:** Trả lại thông tin chi tiết của nhóm hàng hóa theo ID

**– Phương thức và URL: GET** [https://public.kiotapi.com/categories/{id}](https://public.kiotapi.com/categories/%7bid%7d)

**– Request:** Sử dụng hàm **GET** với tham số:
                 ***“id”***: long // ID của nhóm hàng

**– Response:**

|  |
| --- |
| “data”: {                      “categoryId”: int, // ID nhóm hàng hóa                      “parentId”: int?, // Nếu danh mục có danh mục cha                      “categoryName”: string, // Tên nhóm hàng hóa                      “retailerId”: int, // ID cửa hàng                      “hasChild”: int?, // ID cửa hàng                       “modifiedDate: datetime?, // Thời gian cập nhật                       “createdDate”: datetime,                       “children”: []     } |

**2.3.3.Thêm mới nhóm hàng**

**–** **Mục đích sử dụng**: Thêm mới một nhóm hàng

**– Phương thức và URL: POST** <https://public.kiotapi.com/categories>

**–** **Request:** JSON mã hóa yêu cầu gồm 1 object nhóm hàng riêng biệt với nhưng tham số sau:
                     ***“categoryName”***: string // tên nhóm hàng hóa
                     ***“parentId”***: int // nếu nhóm hàng có nhóm hàng cha (hệ thống cho phép tối đa 3 cấp nhóm)
**–** **Body**

|  |
| --- |
| {  “categoryName”: string   } |

**– Response:**

|  |
| --- |
| {    “message”: “Cập nhật dữ liệu thành công”,    “data”: {                      “categoryId”: int, // ID nhóm hàng hóa                      “parentId”: int?, // Nếu danh mục có danh mục cha                      “categoryName”: string, // Tên nhóm hàng hóa (Tối đa 125 ký tự)                      “retailerId”: int, // ID cửa hàng                      “hasChild”: boolean?, // Có danh mục con                      “modifiedDate”: datetime?,                      “createdDate”: datetime,                      “children”: []                     }  } |

#### **2.3.4. Cập nhật nhóm hàng**

**–** **Mục đích sử dụng:** Cập nhật nhóm hàng hóa theo ID

**–** **Phương thức và URL:** **PUT** <https://public.kiotapi.com/categories/id>

**–** **Request:** Sử dụng hàm PUT với ID nhóm hàng qua 1 object JSON.

      ***id”***: long // ID nhóm hàng hóa       

**– Body**

|  |
| --- |
| {  “parentId”: int, // Nếu danh mục có danh mục cha  “categoryName”: string // Tên nhóm hàng hóa (tối đa 125 ký tự)  } |

**– Response:**

|  |
| --- |
| {    “message”: “Cập nhật dữ liệu thành công”,    “data”: {                      “categoryId”: int, // Id nhóm hàng hóa                      “parentId”: int, // Nếu danh mục có danh mục cha                      “categoryName”: string, // Tên nhóm hàng hóa (tối đa 125 ký tự)                      “retailerId”: int, // Id cửa hàng                      “hasChild”: false, // Có danh mục con                      “modifiedDate”: datetime,                      “createdDate”: datetime,                      “children”: []    }  } |

#### **2.3.5. Xóa nhóm hàng**

**– Mục đích sử dụng:** Xóa nhóm hàng theo ID

**–** **Phương thức và URL:** **DELETE** [https://public.kiotapi.com/categories/{id}](https://public.kiotapi.com/categories/%7bid%7d)

**– Request:** Request sẽ bao gồm Id của nhóm hàng trong URL:
                  ***“id”***: long // ID của nhóm hàng

**– Response:** Trả lại thông tin xóa thành công (Code 200)

|  |
| --- |
| {  “message”: “Xóa dữ liệu thành công”  } |

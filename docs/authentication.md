### **2.1. Authenticate**

Kiotviet API xác thực dựa trên cơ chế xác thực OAuth 2.0, để kết nối được hệ thống cần có 2 thông tin: ClientId và Mã bảo mật. Thông tin này được truy cập vào “Thiết lập cửa hàng” bằng tài khoản admin => Chọn Thiết lập kết nối API

![](https://cdn-kvweb.kiotviet.vn/kiotviet-website/wp-content/uploads/2021/07/PublicAPIRT_280721.png)

*Trong trường hợp không thể lấy được thông tin trên vui lòng liên hệ với bộ phận CSKH để được hỗ trợ.*

– Sau khi có được thông tin ClientId và Mã bảo mật (client\_secret). Có thể sử dụng các thư viện theo từng ngôn ngữ để lấy thông tin Access Token, ví dụ:

- Với C#: <https://www.nuget.org/packages/OAuth2Client/>
- Với PHP: <https://github.com/thephpleague/oauth2-client>

– Thông tin endpoint authenticate như sau:

- Authorization Endpoint: <http://id.kiotviet.vn/connect/authorize>
- ​Token Endpoint: <http://id.kiotviet.vn/connect/token>

– ​Hoặc có thể call API bên dưới **(2.2)**

### **2.2. Lấy thông tin Access Token**

**– Mục đích sử dụng**: API lấy thông tin Access Token để truy cập

**– Phương thức và URL**: POST <https://id.kiotviet.vn/connect/token>

**–** **Request:**

scopes: PublicApi.Access //Phạm vi truy cập (Public API)

grant\_type: client\_credentials //Thông tin truy cập dạng token

client\_id: 83a5bcbe-3c39-458c-bdd9-128112cef3f7 //Client Id

client\_secret: 3B52F3A9DDE194966DAE2CE0A478B2DEC15254D6 //Client secret

**​- Header**

“Content-Type”:”application/x-www-form-urlencoded”

scope

**​- Body**

|  |
| --- |
| scopes=PublicApi.Access&grant\_type=client\_credentials&client\_id=e4fe37ab-5d10-4919-bf59-d9a568456d0b&client\_secret=01A3703244752CFF6350A801F900742179C7CCDA |

**– Response:**

|  |
| --- |
| {                      “access\_token”: “”,                      “expires\_in”: 86400,                      “token\_type”: “Bearer”  } |

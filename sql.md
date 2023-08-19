SQL injection exists in the ibos office OA. Procedure

official website:http://www.ibos.com.cn/

version:4.5.5

POC

Route: r=weibo/comment/addcomment

The injection parameter touid exists

Successfully burst the database name by reporting an error injection

![WPS图片(1)](https://github.com/13aiZe1/cve/assets/103416802/86d9ae04-f124-4e4a-a718-954fdd958ce5)

The addComment() method under the model layer is invoked through the actionAddComment() method.

![WPS图片(2)](https://github.com/13aiZe1/cve/assets/103416802/3440d514-5e80-455b-93db-05b352707a46)

addComment() then calls the addComment() method under the parent class
![WPS图片(3)](https://github.com/13aiZe1/cve/assets/103416802/c29803eb-d2ba-49ee-8753-a440a069e689)

The addComment() method receives the uploaded parameters as an array via post

![WPS图片(4)](https://github.com/13aiZe1/cve/assets/103416802/94abd5ee-fc89-4bbe-a2fa-df7dc7e97ac4)

Following the above branch, data[] is brought directly into the addComment() method

![WPS图片(5)](https://github.com/13aiZe1/cve/assets/103416802/0849e547-62e5-4fa4-9f2f-ab2526f05440)

There is the escapeData() security check, but the touid parameter passed in here is not intval(), for unknown reasons

![WPS图片(6)](https://github.com/13aiZe1/cve/assets/103416802/1c338e83-928d-482a-a449-17f4a45961aa)

Finally, the data is brought to the fetchRealnameByUid() method in the model layer to execute the SQL statement

![WPS图片(7)](https://github.com/13aiZe1/cve/assets/103416802/d89a3d01-c1d9-4ebb-bbae-ec82560034ac)
![WPS图片(8)](https://github.com/13aiZe1/cve/assets/103416802/0ed3da65-d389-441f-b1da-92461673ae41)

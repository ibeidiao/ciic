# 免登录对接说明

## 请求地址和参数说明
对接使用form提交，[提交地址](https://www.ibeidiao.com/ciic/login.htm)<br />
POST请求<br />
请求参数需要四个参数，如下

参数|类型|必填|备注
--|:--:|--:|--:
mobile|String|是|手机号码
type|String|是|登录类型，传10，代表使用手机登录
timestamp|String|是|时间戳，如1547113868139
sign|String|是|签名

##  签名方式
sign = SHA1加密(appSecret + mobileV1timestampV2typeV3)<br />
V1：手机号码<br />
V2：当前时间戳<br />
V3：值为10<br />
**请注意参数顺序**

##  注意事项
- 请求参数有效期为30分钟，以timestamp来判断

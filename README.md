# 免登录对接说明
对接使用form提交，需要四个参数，如下

参数|类型|必填|备注
--|:--:|--:|--:
mobile|String|是|手机号码
type|String|是|登录类型，传10
timestamp|String|是|时间戳，如1547113868139
sign|String|是|签名

# 签名方式
Sha1Encrypt(appSecret + mobileV1timestampV2typeV3)<br />
V1：手机号码<br />
V2：当前时间戳<br />
V3：值为10

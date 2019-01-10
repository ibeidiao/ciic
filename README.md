# 免登录对接说明

## 请求地址和参数说明
对接使用form提交，[提交地址](https://www.ibeidiao.com/ciic/login.htm)<br />
**POST**请求<br />
请求参数需要四个参数，如下

参数|类型|必填|备注
--|:--:|--:|--:
mobile|String|是|手机号码
type|String|是|登录类型，传10，代表使用手机登录
timestamp|String|是|时间戳，如1547113868139
sign|String|是|签名

## 签名方式
sign = SHA1加密(appSecret + mobileV1timestampV2typeV3)<br />
V1：手机号码<br />
V2：当前时间戳<br />
V3：值为10<br />
**请注意参数顺序**

## 例子
```XML
<a href="javascript:;" class="go-bd">去背调</a>
```
```JavaScript
$('body').on('click', '.go-bd', function(e) {
  var $this = $(this);
  
  $.ajax({
    async : true, 
    url : 本地获取登录参数url,
    type : 'post',
    dataType : 'json'
  }).then(
    function(json) {
      // 此处获取mobile, type, timestamp, sign值
      ...
      
      var obj = {
        mobile: mobile,
        type: type,
        timestamp: timestamp,
        sign: sign
      };
      
      // 动态创建form
      var $newForm = $('<form></form>');
      $newForm.attr('method', 'post');
      $newForm.attr('action', 'https://www.ibeidiao.com/ciic/login.htm');
      $newForm.attr('target', '_blank');
			
      for (var k in obj) {
        var newElement = $('<input type="hidden" id="' + k + '" name="' + k + '" />');
        newElement.val(obj[k]);
        $newForm.append(newElement);
      }
      
      $('body').append($newForm);
      $newForm.submit();
      $newForm.remove();
    },
    function(e) {
      // 错误处理
    }
  );
  
  return false;
});
```

## 注意事项
- 请求参数有效期为30分钟，以timestamp来判断

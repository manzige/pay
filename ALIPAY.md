
# 唤起支付宝转账到支付宝

可通过支付宝转账URI可以唤起支付宝转账到支付宝账户，并锁定账户、金额、备注。实现最终效果UIR为：

`alipays://platformapi/startapp?appId=20000067&url=alipays%3A%2F%2Fplatformapi%2Fstartapp%3FappId%3D20000123%26actionType%3Dscan%26biz_data%3D%7B%22s%22%3A%22money%22%2C%22u%22%3A%222088402759328420%22%2C%22a%22%3A%226.66%22%2C%22m%22%3A%22PID%E8%BD%AC%E8%B4%A6%22%7D`

# 实现方法

最终URI拆解，其中
`alipays://platformapi/startapp?appId=20000067` 为支付宝收款码页面；url 参数值为 `alipays://platformapi/startapp?appId=20000123&actionType=scan&biz_data={"s":"money","u":"2088402759328420","a":"6.66","m":"PID转账"}` urlencode 后的值，其中 url 参数中的biz_data 值涉及几个参数：u 为用户的PID、a 为付款金额、 m 为付款信息；


# 支付宝PID

支付宝PID为支付宝账户的ID，可通过支付宝账户扫一扫功能，扫描 `https://render.alipay.com/p/f/fd-ixpo7iia/index.html` 转化的二维码获取

现在你可以拿起你的支付宝，拼接一个属于自己的任意金额的收款二维码了～


# 唤起支付宝转账到银行卡
可通过支付宝转账到银行卡URI唤起支付宝转账到银行卡并填充目标银行卡信息，实现最终效果UIR为：`alipays://platformapi/startapp?appId=09999988&actionType=toCard&sourceId=bill&cardNo=6214865110032519&bankAccount=%E6%B1%9F%E7%82%9C%E5%8B%87&money=1&amount=1&bankMark=CMB&bankName=%E6%8B%9B%E5%95%86%E9%93%B6%E8%A1%8C&`。
支付宝转账到银行卡预填充信息

# 实现方法
URI再 encode 前为 ：`alipays://platformapi/startapp?appId=09999988&actionType=toCard&sourceId=bill&cardNo=621486***2519&bankAccount=XXX&money=1&amount=1&bankMark=CMB&bankName=招商银行`。

拆解URI，其中 `alipays://platformapi/startapp?appId=09999988` 为唤起支付宝转账到银行卡的页面URI、actionType=toCard 转账类型 toCard-到银行卡、 cardNo=6217000030001234567、银行卡号、bankAccount=XXX 银行账户名、money=0.01 转账金额、amount=0.01 转账额度、bankMark=CCB 银行代号、bankName=招商银行 银行名称。

如果你使用了第一个URI直接扫码，跳转到支付宝后，会看见一个空白页面，可能你会说这个方法行不通，既然能写出这个方法，那肯定是能通的，只是你的步骤出错了。

唤起支付宝转账到银行卡并预填充银行卡账户的步骤如下：

- 开始
- 开启飞行模式
- 点击链接
- 跳转到支付宝
- 关闭飞行模式
- 自动刷新页面
- 结束
跟着流程走一遍，你会有惊喜的。

支付宝还提供了通过银行卡账号来获取银行信息的接口，这样就不用自己维护银行代号及名称了，接口地址为：`https://ccdcapi.alipay.com/validateAndCacheCardInfo.json?cardNo=6226661203661552&cardBinCheck=true,传入卡号carNo` 即返回银行代号。

# 看到别人有使用这个链接
`alipays://platformapi/startapp?saId=10000007&qrcode=https://qr.alipay.com/fkx11699ksrjokuurzkjjf5?_s=web-other`
qrcode 后面的地址为收款码识别出来的地址

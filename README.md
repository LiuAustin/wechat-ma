# 微信第三方开放平台代小程序实现业务

#### 介绍
假如说，有多个业务，功能模式相同的公众号/小程序，如果只是小程序开发，那是不是需要复制多套代码，改appid信息，在微信公众号后台，配置域名服务器以及密钥等繁琐的信息，每改一个提交发布一次，进行重复的步骤。随着要维护的公众号/小程序数量逐步增加，需要投入的资源以及成本也随之增加。
有没有想过，只需要开发一套公众号/小程序代码，以之为模板，再来一套后台管理系统，把在微信公众号后台做的那些事都搬到我们自己的系统中。来一个业务相同的小程序，只需要管理员授权后，只要在我们的系统中点点几个按钮，就可以把小程序发布上线，一次开发供 N 个公众号使用，提供标准化的接口服务来满足业务的基础需求。通过扫描二维码授权给平台，帮助 N 多个公众号代实现业务，不再需要理解繁琐参数设置，并且密码不提供给开发者，保证安全，真正做到解放运营同学和开发的双手，有更多的时间去谈女朋友，那该多好。没错，微信第三方平台开发就是来帮你节省更多时间去把妹的神器。

#### 概述
微信公众平台-第三方平台（简称第三方平台）开放给所有通过开发者资质认证后的开发者使用。在得到公众号或小程序运营者（简称运营者）授权后，第三方平台开发者可以通过调用微信开放平台的接口能力，为公众号或小程序的运营者提供账号申请、小程序创建、技术开发、行业方案、活动营销、插件能力等全方位服务。同一个账号的运营者可以选择多家适合自己的第三方为其提供产品能力或委托运营。
从具体的业务场景上说，第三方平台包括以下场景：
提供行业解决方案，如针对电商行业的解决方案，或针对旅游行业的解决方案等；
行业：（横向）提供更加专业的运营能力，精细化运营用户公众号或小程序；
功能：（纵向）对公众平台功能的优化，如专门优化图文消息视觉样式和排版的工具，或专门定制的 CRM 用户管理功能，或功能强大的小程序插件等。
接入第三方开发的前提是要有微信开放平台应用，详细创建步骤请参考

https://developers.weixin.qq.com/doc/oplatform/Third-party_Platforms/how_to_apply.html


#### 技术选型
前后端分离

系统环境

● JDK >= 1.8

● MySQL >= 5.7

● Maven >= 3.0

后台框架

● Spring Boot 2.2.x

● Spring Framework 5.2.x

● Spring Security 5.2.x

● Apache MyBatis 3.5.x

● Hibernate Validation 6.0.x

● Alibaba Druid 1.2.x

前端框架

● Vue 2.6.x

● Axios 0.21.0

● Element 2.14.x


#### 效果展示
![Image text](https://img-blog.csdnimg.cn/20200912082612399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912080534730.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

1、获取验证票据

验证票据（component_verify_ticket），在第三方平台创建审核通过后，微信服务器会向其 ”授权事件接收URL” 每隔 10 分钟以 POST 的方式推送 component_verify_ticket

接收 POST 请求后，只需直接返回字符串 success。为了加强安全性，postdata 中的 xml 将使用服务申请时的加解密 key 来进行加密，在收到推送后需进行解密。

2、获取令牌

令牌（component_access_token）是第三方平台接口的调用凭据。令牌的获取是有限制的，每个令牌的有效期为 2 小时，请自行做好令牌的管理，在令牌快过期时（比如1小时50分），重新调用接口获取。

3、快速创建小程序

快速创建小程序接口优化了小程序注册认证的流程，能帮助第三方平台迅速拓展线下商户，拓展商户的服务范围，占领小程序线下商业先机。采用法人人脸识别方式替代小额打款等认证流程，极大的减轻了小程序主体、类目资质信息收集的人力成本。第三方平台只需收集法人姓名、法人微信、企业名称、企业代码信息这四个信息，便可以向企业法人下发一条模板消息来采集法人人脸信息，完成全部注册、认证流程。以及法人收到创建成功后的小程序APPID时，同时下发模板消息给法人，提示法人进行邮箱和密码的设置，便于后续法人登陆小程序控制台进行管理。

通过该接口创建小程序默认为“已认证”。为降低接入小程序的成本门槛，通过该接口创建的小程序无需交 300 元认证费。

![Image text](https://img-blog.csdnimg.cn/20200912080724207.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912080730879.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

4、获取预授权码

预授权码（pre_auth_code）是第三方平台方实现授权托管的必备信息，每个预授权码有效期为 10 分钟。需要先获取令牌才能调用。

5、引导商户授权获取授权信息

第三方服务商构建授权链接放置自己的网站，用户点击后，弹出授权页面。

![Image text](https://img-blog.csdnimg.cn/20200912080830953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912080835707.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912080841817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

6、设置小程序基本信息

设置小程序名称，当名称没有命中关键词，则直接设置成功；当名称命中关键词，需提交证明材料，并需要审核。修改小程序的头像。修改功能介绍。修改小程序隐私设置，即修改是否可被搜索。

![Image text](https://img-blog.csdnimg.cn/2020091208125551.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912081258741.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

7、支付授权

即填写商户号和商户号密钥，以及上传p12证书

![Image text](https://img-blog.csdnimg.cn/20200912081347317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

8、设置服务器域名

授权给第三方的小程序，其服务器域名只可以为第三方平台的服务器，当小程序通过第三方平台发布代码上线后，小程序原先自己配置的服务器域名将被删除，只保留第三方平台的域名，所以第三方平台在代替小程序发布代码之前，需要调用接口为小程序添加第三方平台自身的域名。

注意：

需要先将域名登记到第三方平台的小程序服务器域名中，才可以调用接口进行配置。

最多可以添加1000个合法服务器域名；其中，Request域名、Socket域名、Uploadfile域名、Download域名、Udp域名的设置数量均最大支持200个。

每月可提交修改申请50次。

![Image text](https://img-blog.csdnimg.cn/20200912081408881.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912081417305.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

9、设置业务域名

授权给第三方的小程序，其业务域名只可以为第三方平台的服务器，当小程序通过第三方发布代码上线后，小程序原先自己配置的业务域名将被删除，只保留第三方平台的域名，所以第三方平台在代替小程序发布代码之前，需要调用接口为小程序添加业务域名。

注意：

需要先将业务域名登记到第三方平台的小程序业务域名中，才可以调用接口进行配置。

为授权的小程序配置域名时支持配置子域名，例如第三方登记的业务域名如为 qq.com，则可以直接将 qq.com 及其子域名（如 xxx.qq.com）也配置到授权的小程序中。

![Image text](https://img-blog.csdnimg.cn/2020091208145594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

![Image text](https://img-blog.csdnimg.cn/20200912081459620.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

10、上传小程序代码

第三方平台需要先将草稿添加到代码模板库，或者从代码模板库中选取某个代码模板，得到对应的模板 id（template_id）；然后调用本接口可以为已授权的小程序上传代码。

![Image text](https://img-blog.csdnimg.cn/20200912081526789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

11、成员管理

第三方平台在帮助旗下授权的小程序提交代码审核之前，可先让小程序运营者体验，体验之前需要将运营者的个人微信号添加到该小程序的体验者名单中。

注意： 如果运营者同时也是该小程序的管理员，则无需绑定，管理员默认有体验权限。

![Image text](https://img-blog.csdnimg.cn/20200912081605788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

12、获取体验版二维码

![Image text](https://img-blog.csdnimg.cn/20200912081652433.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

13、提交审核

![Image text](https://img-blog.csdnimg.cn/20200912081723535.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

14、审核撤回

注意： 单个帐号每天审核撤回次数最多不超过 1 次，一个月不超过 10 次。

![Image text](https://img-blog.csdnimg.cn/20200912081802104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

15、发布已通过审核的小程序

![Image text](https://img-blog.csdnimg.cn/202009120818332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

16、小程序版本回退
注意：

如果没有上一个线上版本，将无法回退

只能向上回退一个版本，即当前版本回退后，不能再调用版本回退接口。

![Image text](https://img-blog.csdnimg.cn/20200912081913330.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)

17、获取小程序码

![Image text](https://img-blog.csdnimg.cn/20200912081938961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpdUF1c3Rpbg==,size_16,color_FFFFFF,t_70#pic_center)


#### 联系我们

![Image text](https://ysd-1300312604.cos.ap-shanghai.myqcloud.com/goods/goods_editor/20210529/d5591ebea3b14b7fb493c6b970571630.png)

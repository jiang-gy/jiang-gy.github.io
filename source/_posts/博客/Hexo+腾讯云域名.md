

### 1 购买域名

如果想要免费的域名，可以到下面网址购买：[http://www.dot.tk/en/index.html?lang=en](https://cloud.tencent.com/developer/tools/blog-entry?target=http%3A%2F%2Fwww.dot.tk%2Fen%2Findex.html%3Flang%3Den&source=article&objectId=1964349) (没有尝试过)

如果有条件，最好到阿里云或者腾讯云等地方[购买域名](https://cloud.tencent.com/act/pro/domain-sales?from_column=20065&from=20065)，1元优惠域名还是很多的。

此处注意实名认证+购买域名后，需要经过一定的时间，域名才会生效。

本网站在腾讯云购买的域名，因此本文主要以腾讯云为案例介绍

### 2 具体步骤



其余步骤网上资料挺多，这里就不写了。

腾讯云与阿里云等平台的管理台差不多。此次介绍腾讯云如何进入管理台。

进入腾讯云的管理控制台-域名与网站-云解析 DNS，进入域名的解析设置。

后面主要步骤主要参考链接2进行

注意CNAME中直接填写user+github.io即可，不需要https和多余的//

主要存在的问题可能是报错：

Domain does not resolve to the GitHub Pages server. For more information, see

主要是DNS没有配置好，可以重点看一下参考链接3。配置好的截图应该是这样的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201110175924108.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0NTI4Nw==,size_16,color_FFFFFF,t_70#pic_center)

配置多个IP是为了防止自己网站ip变化。腾讯云最多配置两个，但是也不影响使用

![image-20240308151249838](C:\Users\ANTL\AppData\Roaming\Typora\typora-user-images\image-20240308151249838.png)



### 参考链接

1. [腾讯云DNS解析](https://cloud.tencent.com/document/product/302/3446#cc909468-2c70-4a0a-b4d0-132a3846762b)
2. [Github Pages 绑定域名遇到的坑](https://blog.csdn.net/i_do_not_know_you/article/details/105594269)
3. [github页面绑定域名/Domain‘s DNS record could not be retrieved](https://blog.csdn.net/weixin_43645287/article/details/109603945?ops_request_misc=&request_id=&biz_id=102&utm_term=Domain%27s%20DNS%20record%20could%20not%20&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-.first_rank_v2_pc_rank_v29&spm=1018.2226.3001.4187)

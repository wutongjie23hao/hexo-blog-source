title: 购买域名-设置DNS
date: 2015-05-22 13:28:12
tags:
- hexo
categories:
- hexo
---
[原文链接](http://zipperary.com/2013/05/27/domain-name-and-dns/)
博客搭建好之后就一直想买个域名，这几天在考虑域名和后缀的选择问题。后缀好说，首选``.com``，次选``.me``或``.net``。至于域名，由于本名拼音（zhaowei）和博名（zipperary）都已经被注册，只好另外构思。最终选择了zipperary.com这个域名。想法来源于library这个词，...rary取意存放之地，所以zipperary的意思就是zippera的博客存放之地了。
域名的购买，首选Goddady。原因如下：
在国外，不受国内各种干扰。
国外域名商中唯一支持支付宝付款的。
价格不高，还经常有优惠。
信誉好，口碑好，靠谱。

但由于是全英文，还有Goddady强大的推销力，到处在引导你购买它的优惠服务，这样，注册和购买还是费些时间的。我的域名标价是年费11美元，税后根据实时汇率，也就六十多中国大洋，不算贵。
域名购买完成后就要在Goddady网站里设置dns服务商了。Goddady会默认提供两个国外的，对于国内网站和国内访问来说，最好使用国内的dns服务商，这里选择口碑最好使用最多的免费dns服务商dnspod.cn。这里解释下goddady和dnspod的关系。
Goddady是域名服务商，我们需要在这里选择由哪个dns服务商为我们的网站提供域名解析服务。用下面的方式，指定为dnspod：
![dns-config1](http://ww4.sinaimg.cn/large/5e8cb366jw1e538mz2fwaj20m60c8dhg.jpg)
设置好之后，去dnspod.cn注册账号，添加网站(zipperary.com)，设置域名到ip的映射关系，如下：
![dns-config2](http://ww3.sinaimg.cn/large/5e8cb366jw1e538pcdcxtj20tt0at75b.jpg)
![dns-config3](http://ww2.sinaimg.cn/large/5e8cb366jw1e538q78xoqj20st0aowfq.jpg)
*(注：除了A记录，也可以添加为CNAME记录，记录值就是zippera.github.io这种形式。两种方式任选其一即可。)*
接下来需要去自己的网站进行域名设置。不同的网站不同的设置方式，对于hexo，进入source文件夹，创建名为``CNAME``的文件，编辑：
```bash
zipperary.com
```
这样就设置好了，访问<http://zipperary.com> 就能看到自己的网站了。
如果想使用``www.zipperary.com``形式，``CNAME``文件中相应地变为``www.zipperary.com``即可。
需要注意的是，goddady和dnspod的设置都会有时间不等的延迟，并不一定会马上生效。
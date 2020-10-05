**DNS原理**

chrome -> baidu.com

1. 访问本地dns server请求域名的ip地址，有则返回，只有开始基于ip的访问
2. 没有，访问根dns server，全球一共有13个，亚洲的在日本，有则返回，没有时返回知道该域名对应ip的dns server的地址
3. 访问知道该域名对应ip的dns.server的地址，获取ip，然后开始基于ip的访问

DNS分类

域名 -> ip (ipv4 A记录，ipv6 AAA记录)

域名 -> 域名（CName）

域名 -> url

域名 -> 文本
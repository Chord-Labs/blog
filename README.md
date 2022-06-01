# blog
some js projects

yarn 过程中遇到的问题

场景
项目中打包遇到了点问题，所以想删除原先装好的依赖包，重新yarn，结果神奇的报错了，无语。。。
遇到的问题

（1）error An unexpected error occurred: "https://raw.githubusercontent.com/seonim-ryu/Squire/fd40b4e3020845825701e9689f190bab3f4775d4/package.json: connect ECONNREFUSED 0.0.0.0:443".

原因：找不到 https://raw.githubusercontent.com

解决方案：通过**https://www.ipaddress.com/** 查询 **raw.githubusercontent.com** 的IP，并在hosts中配置

```
185.199.108.133  raw.githubusercontent.com
```
（2）fatal: unable to access 'https://github.com/nhn/raphael.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
原因：代理出现问题
解决方案：执行命令
```
git config --global --add remote.origin.proxy ""
```
```
git config --global --unset remote.origin.proxy
git config --global remote.origin.proxy ""
git config --global http.https://github.com.proxy "socks5://127.0.0.1:1081"
git config --global https.https://github.com.proxy "socks5://127.0.0.1:1081"
```

nginx配置报错： connect() to 127.0.0.1:8080 failed (13: Permission denied) while connecting to upstream,


运行以下的命令
```
setsebool -P httpd_can_network_connect 1
```

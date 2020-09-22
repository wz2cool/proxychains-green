# proxychains-green

proxychains 是一个非常强大的命令行代理工具，不过因为需要编译到系统感觉安装比较麻烦，特别有些场景需要自己软件里面呆着 proxychains 工具，这个时候就可以考虑使用本项目已经打包好的绿色版本。

proxychains 绿色版，无需 gcc 编译，这里最好使用 centos5.tar.gz 版本的，这样高版本的系统也是可以用的， 更多细节可以参考 proxychains 原项目：https://github.com/rofl0r/proxychains-ng

# 使用方式

```bash
$ tar -xvf centos5.tar.gz
$ cd centos5
$ ./proxychains4
```

我们直接就可以看到相关的参数

```bash
$ ./proxychains4
Usage:	./proxychains4 -q -f config_file program_name [arguments]
	-q makes proxychains quiet - this overrides the config setting
	-f allows one to manually specify a configfile to use
	for example : proxychains telnet somehost.com
More help in README file
```

设置代理， 修改 proxychains.conf 文件

```bash
$ vi proxychains.conf
```

改成自己的代理，然后保存退出

```bash
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
# socks4        127.0.0.1 9050
http            192.168.16.201 808
```

测试访问, 这里我们尝试拿一下百度首页, -f 参数是指定配置文件

```bash
$ ./proxychains4 -f ./proxychains.conf wget www.baidu.com

[proxychains] config file found: ./proxychains.conf
[proxychains] preloading ./libproxychains4.so
[proxychains] DLL init: proxychains-ng 4.14
--2020-09-22 19:07:19--  http://www.baidu.com/
Resolving www.baidu.com... 224.0.0.1
Connecting to www.baidu.com|224.0.0.1|:80... [proxychains] Strict chain  ...  192.168.16.201:808  ...  www.baidu.com:80  ...  OK
connected.
HTTP request sent, awaiting response... 200 OK
Length: 2381 (2.3K) [text/html]
Saving to: ?.ndex.html?

100%[===============================================================================================================================>] 2,381       --.-K/s   in 0s      

2020-09-22 19:07:20 (373 MB/s) - ?.ndex.html?.saved [2381/2381]
```

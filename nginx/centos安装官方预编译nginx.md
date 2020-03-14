### 安装方式
- 下载源码编译安装: 参考[Installing NGINX Open Source](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/)
- 安装官方提前编译好的nginx: 参考[Installing Prebuilt CentOS and RHEL Packages](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#prebuilt_redhat)


本文采用安装官方提前编译好的nginx。


### 关闭selinux
selinux目前很多企业都不用，默认都是关闭的，否则可能引起很多莫名奇妙的问题，参考[Linux 下为何要关闭 SELinux](https://www.zhihu.com/question/20559538)。
首先使用命令`$ getenforce`查看selinux状态,终端输出
```
Disabled
```
可见这个功能是关闭的。如果没关可以参考 [centos7关闭防火墙和selinux](https://www.jianshu.com/p/d6414b5295b8)关闭。

### selinux对nginx影响
如果没有关闭selinux,CentOS7使用反向代理需要打开网络访问权限:
```
$ sudo setsebool httpd_can_network_connect 1 
```
打开网络权限之后，反向代理可以使用了。

另外是端口问题，参考[CentOS 7 下 yum 安装和配置 Nginx](https://qizhanming.com/blog/2018/08/06/how-to-install-nginx-on-centos-7)




### 添加yum源
查看本机os版本：
```
[root@hadoop-master ~]# cat /etc/redhat-release
CentOS Linux release 7.4.1708 (Core) 
```

nginx不在默认的yum源中，可以使用epel或者官网的yum 源，本例使用官网的yum源：
```
sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

```
可用rpm列表：http://nginx.org/packages/centos/7/noarch/RPMS/

执行输出：
```
[root@hadoop-master ~]# sudo rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
Retrieving http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
warning: /var/tmp/rpm-tmp.6H5vz9: Header V4 RSA/SHA1 Signature, key ID 7bd9bf62: NOKEY
Preparing...                          ################################# [100%]
Updating / installing...
   1:nginx-release-centos-7-0.el7.ngx ################################# [100%]

```

### 安装
执行下面的命令安装：
```
$ sudo yum install nginx
```

### 配置文件位置
位置如下：
```
Config dir – /etc/nginx/
Master/Global config file – /etc/nginx/nginx.conf
Port 80 http config file – /etc/nginx/conf.d/default
TCP ports opened by Nginx – 80 (HTTP), 443 (HTTPS)
Document root directory – /usr/share/nginx/html
```
参考[How to install and use Nginx on CentOS 7 / RHEL 7](https://www.cyberciti.biz/faq/how-to-install-and-use-nginx-on-centos-7-rhel-7/)





### 启动nginx
启动nginx:
```
$ sudo systemctl start nginx
```

执行`curl -I 127.0.0.1`确认是否启动成功：
```
[root@hadoop-master ~]# curl -I 127.0.0.1
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Fri, 30 Aug 2019 05:06:07 GMT
Content-Type: text/html
Content-Length: 612
Last-Modified: Tue, 13 Aug 2019 15:04:31 GMT
Connection: keep-alive
ETag: "5d52d17f-264"
Accept-Ranges: bytes

```


### 停止nginx
停止服务:
```
$ sudo systemctl stop nginx
```


### 停机重启
停止服务:
```
$ sudo systemctl restart nginx
```



### 不停机重启
如果nginx配置更新，可以实现不停机在线更新：
```
$ sudo systemctl reload nginx
```

### 设置开机自动启动

```
$ sudo systemctl enable nginx
```
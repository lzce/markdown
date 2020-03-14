### 安装依赖
安装gcc g++的依赖:
```
$ sudo apt-get install build-essential
$ sudo apt-get install libtool
```
安装[pcre](http://www.pcre.org/)库:
```
$ sudo apt-get update
$ sudo apt-get install libpcre3 libpcre3-dev
```
安装[zlib](http://www.zlib.net/)库:
```
$ sudo apt-get install zlib1g-dev
```
安装openssl:
```
$ sudo apt-get install openssl
```

### 编译并安装nginx
首先下载nginx源码:
```
$ wget http://nginx.org/download/nginx-1.15.0.tar.gz
```
nginx全部可用的源码版本可以去http://nginx.org/download/查看。
然后解压：
```
$ tar -zxvf  nginx-1.15.0.tar.gz
```
进入解压后的文件夹：
```
$ cd nginx-1.15.0
```
配置nginx:
```
$ ./configure --prefix=/data/nginx 
```
更多可以配置的选项参考[Configuring the Build Options](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#configuring-the-build-options)


以上命令指定将nginx安装在`/data/nginx `.执行该命令输出为：
```
checking for OS
 + Linux 4.15.0-38-generic x86_64
checking for C compiler ... found
 + using GNU C compiler
 + gcc version: 7.3.0 (Ubuntu 7.3.0-27ubuntu1~18.04) 
checking for gcc -pipe switch ... found
checking for -Wl,-E switch ... found
checking for gcc builtin atomic operations ... found
checking for C99 variadic macros ... found
checking for gcc variadic macros ... found
checking for gcc builtin 64 bit byteswap ... found
checking for unistd.h ... found
checking for inttypes.h ... found
checking for limits.h ... found
checking for sys/filio.h ... not found
checking for sys/param.h ... found
checking for sys/mount.h ... found
checking for sys/statvfs.h ... found
checking for crypt.h ... found
checking for Linux specific features
checking for epoll ... found
checking for EPOLLRDHUP ... found
checking for EPOLLEXCLUSIVE ... found
checking for O_PATH ... found
checking for sendfile() ... found
checking for sendfile64() ... found
checking for sys/prctl.h ... found
checking for prctl(PR_SET_DUMPABLE) ... found
checking for prctl(PR_SET_KEEPCAPS) ... found
checking for capabilities ... found
checking for crypt_r() ... found
checking for sys/vfs.h ... found
checking for nobody group ... not found
checking for nogroup group ... found
checking for poll() ... found
checking for /dev/poll ... not found
checking for kqueue ... not found
checking for crypt() ... not found
checking for crypt() in libcrypt ... found
checking for F_READAHEAD ... not found
checking for posix_fadvise() ... found
checking for O_DIRECT ... found
checking for F_NOCACHE ... not found
checking for directio() ... not found
checking for statfs() ... found
checking for statvfs() ... found
checking for dlopen() ... not found
checking for dlopen() in libdl ... found
checking for sched_yield() ... found
checking for sched_setaffinity() ... found
checking for SO_SETFIB ... not found
checking for SO_REUSEPORT ... found
checking for SO_ACCEPTFILTER ... not found
checking for SO_BINDANY ... not found
checking for IP_TRANSPARENT ... found
checking for IP_BINDANY ... not found
checking for IP_BIND_ADDRESS_NO_PORT ... found
checking for IP_RECVDSTADDR ... not found
checking for IP_SENDSRCADDR ... not found
checking for IP_PKTINFO ... found
checking for IPV6_RECVPKTINFO ... found
checking for TCP_DEFER_ACCEPT ... found
checking for TCP_KEEPIDLE ... found
checking for TCP_FASTOPEN ... found
checking for TCP_INFO ... found
checking for accept4() ... found
checking for eventfd() ... found
checking for int size ... 4 bytes
checking for long size ... 8 bytes
checking for long long size ... 8 bytes
checking for void * size ... 8 bytes
checking for uint32_t ... found
checking for uint64_t ... found
checking for sig_atomic_t ... found
checking for sig_atomic_t size ... 4 bytes
checking for socklen_t ... found
checking for in_addr_t ... found
checking for in_port_t ... found
checking for rlim_t ... found
checking for uintptr_t ... uintptr_t found
checking for system byte ordering ... little endian
checking for size_t size ... 8 bytes
checking for off_t size ... 8 bytes
checking for time_t size ... 8 bytes
checking for AF_INET6 ... found
checking for setproctitle() ... not found
checking for pread() ... found
checking for pwrite() ... found
checking for pwritev() ... found
checking for sys_nerr ... found
checking for localtime_r() ... found
checking for clock_gettime(CLOCK_MONOTONIC) ... found
checking for posix_memalign() ... found
checking for memalign() ... found
checking for mmap(MAP_ANON|MAP_SHARED) ... found
checking for mmap("/dev/zero", MAP_SHARED) ... found
checking for System V shared memory ... found
checking for POSIX semaphores ... not found
checking for POSIX semaphores in libpthread ... found
checking for struct msghdr.msg_control ... found
checking for ioctl(FIONBIO) ... found
checking for struct tm.tm_gmtoff ... found
checking for struct dirent.d_namlen ... not found
checking for struct dirent.d_type ... found
checking for sysconf(_SC_NPROCESSORS_ONLN) ... found
checking for sysconf(_SC_LEVEL1_DCACHE_LINESIZE) ... found
checking for openat(), fstatat() ... found
checking for getaddrinfo() ... found
checking for PCRE library ... found
checking for PCRE JIT support ... found
checking for zlib library ... found
creating objs/Makefile

Configuration summary
  + using system PCRE library
  + OpenSSL library is not used
  + using system zlib library

  nginx path prefix: "/data/nginx"
  nginx binary file: "/data/nginx/sbin/nginx"
  nginx modules path: "/data/nginx/modules"
  nginx configuration prefix: "/data/nginx/conf"
  nginx configuration file: "/data/nginx/conf/nginx.conf"
  nginx pid file: "/data/nginx/logs/nginx.pid"
  nginx error log file: "/data/nginx/logs/error.log"
  nginx http access log file: "/data/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"

```
编译nginx:
```
$ make
```
等待编译完成后安装nginx:
```
$ sudo make install
```

### 启动和停止nginx
可以执行下面的命令启动nginx:
```
$ sudo /data/nginx/sbin/nginx -c /data/nginx/conf/nginx.conf
```
注意，`-c`参数用于指定配置文件。也可以不指定该参数，nginx会以软件内置的默认参数启动。启动成功以后，浏览器中访问服务器的ip,会显示`Welcome to nginx`。
关闭nginx的命令为:
```
$ sudo /data/nginx/sbin/nginx -s stop
```
这种关闭命令比较粗暴，可以使用下面的命令等nginx中的命令执行完成后优雅停机：
```
$ sudo /data/nginx/sbin/nginx -s  quit
```
### 动态更新配置文件
可以在nginx不停机的情况下动态更新配置文件，命令为
```
$ sudo  /data/nginx/sbin/nginx -s reload
```



### 参考
- [Ubuntu16.04.1 安装Nginx](https://www.cnblogs.com/piscesLoveCc/p/5794926.html)
- [阿里云Ubuntu 16.04系统下安装Nginx](https://www.jianshu.com/p/cee284a90c0e)
- [Installing NGINX Open Source](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/)
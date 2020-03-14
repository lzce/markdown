### 安装
首先去https://nginx.org/en/download.html下载nginx的windows版，比如[nginx/Windows-1.15.5](https://nginx.org/download/nginx-1.15.5.zip)。下载以后解压到想安装的文件夹中，比如`D:\softwares`.


### 启动
打开一个cmd窗口，进入nginx文件夹`D:\softwares\nginx-1.15.5`。然后可以使用命令`start nginx`或者`nginx.exe`启动nginx.

### 重启

```shell
$ nginx -s reload
```

### 关闭
经过测试，nginx不能使用windows powershell或者git bash等命令行工具关闭，只能使用最传统的cmd.
可以使用命令`nginx.exe -s stop`或者`nginx.exe -s quit`关闭nginx.
nginx.conf:
```
     server {
        listen       80;#默认端口是80，如果端口没被占用可以不用修改
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
        root        D:\workspace\worldex\freight_project\dist;#vue项目的打包后的dist

        location / {
            try_files $uri $uri/ @router;#需要指向下面的@router否则会出现vue的路由在nginx中刷新出现404
            index  index.html index.htm;
        }
        #对应上面的@router，主要原因是路由的路径资源并不是一个真实的路径，所以无法找到具体的文件
        #因此需要rewrite到index.html中，然后交给路由在处理请求资源
        location @router {
            rewrite ^.*$ /index.html last;
        }
        #.......其他部分省略
  }

```



### 参考
- [nginx部署vue项目](https://my.oschina.net/u/1760791/blog/1575808)
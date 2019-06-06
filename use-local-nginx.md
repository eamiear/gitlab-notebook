# 使用本地NGINX

#### 禁用自带NGINX，并将UNIX套接字改为TCP端口

##### 禁用内置Nginx

在`/etc/gitlab/gitlab.rb`中设置：

```rb
nginx['enable'] = false
```
##### 设置 web-server 外部用户

在`/etc/gitlab/gitlab.rb`中设置：

```rb
 web_server['external_users'] = ['root']
```

gitlab 默认不设置外部web服务用户，需要自行配置。

上面的`root`为nginx用户名，在`/nginx/conf/nginx.conf`文件查看：

```bash
[root@kz conf]# cat nginx.conf
user root;
...

```

#### 配置Web服务信任代理

web-server跟GitLab服务不在同一机器上时，代理列表应该填入Web服务的IP地址：

```rb
 gitlab_rails['trusted_proxies'] = [ '192.168.1.0/24', '192.168.2.1', '2001:0db8::/32' ]
```

#### 使用Apache服务时，设置gitlab-workhorse（可选）

Apache无法连接UNIX套接字，需替换成连接TCP端口。

在`/etc/gitlab/gitlab.rb`中设置：

```rb
# 默认8181端口
gitlab_workhorse['listen_network'] = "tcp"
gitlab_workhorse['listen_addr'] = "127.0.0.1:9000"
```

#### 重载配置及重启

```bash
gitlab-ctl reconfigure

gitlab-ctl restart
```

#### 配置本机nginx代理

找到nginx配置文件，如`/usr/local/nginx/conf/nginx.conf`，添加代理配置：

```nginx
upstream gitlab_server{
    server localhost:9000;
    keepalive 50;
}
server {
    listen       80;
    server_name  iot.on-bright.com;

    charset utf-8;
    location / {
        root   html;
        index  index.html index.htm;
        proxy_pass http://gitlab_server;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
}
```

**注意**： gitlab的访问需要一级目录？ 如果路由配置为`/gitlab`，访问时会找不到文件。

重启nginx:

```bash
./nginx -s reload
```

### 常规命令

#### 查看网络状态

```
netstat -tunlp
```

#### 查看gitlab执行日志

```
gitlab-ctl tail
```

### 附件

#### nginx配置

[nginx.conf](config/nginx.conf)

#### gitlab配置

[gitlab.rb](config/gitlab.rb)

### 参考

[`Using a non-bundled web-server`](https://docs.gitlab.com/omnibus/settings/nginx.html#using-a-non-bundled-web-server)
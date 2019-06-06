# Gitlab pages

## 配置

### 添加子域名(泛域名解析)

在服务器上添加域名解析，如阿里云等
```
*.page.xxx.com 192.168.22.23
```

配置好后，用户可通过`username.page.xxx.com`访问pages

### 修改gitlab配置文件
   
```
vi /etc/gitlab/gitlab.rb

pages_external_url "http://page.xxx.com"
gitlab_pages['enable'] = true
```

执行gitlab重配置、重启命令:

```
gitlab-ctl reconfigure

gitlab-ctl restart
```

配置成功，则admin页面上的 GitLab Pages项处于启用状态

![gitlab-page](snapshot/gitlab-pages.png)

### 编写 .gitlab-ci.yml 文件

项目需要使用Pages功能时，在根目录下添加并填写 .gitlab-ci.yml 文件。


## 参考

[`GitLab Pages`](https://docs.gitlab.com/ee/administration/pages/index.html)
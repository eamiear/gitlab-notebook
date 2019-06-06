# 汉化

### 查看当前GitLab版本

```bash
[root@kz /]# cat /opt/gitlab/embedded/service/gitlab-rails/VERSION
11.11.0

```

### 下载汉化包

用wget下载：

```shell
wget https://gitlab.com/xhang/gitlab/-/archive/11-11-stable-zh/gitlab-11-11-stable-zh.tar
```

或手工下载再上传:

[`https://gitlab.com/xhang/gitlab`](https://gitlab.com/xhang/gitlab)

解压汉化包：

```bash
# 当前目录路经为/opt/gitlab/embedded/service/
[root@kz service]# tar -xvf gitlab-11-11-stable-zh.tar
```

### 备份gitlab文件

```bash
[root@kz service]# tar -cvf gitlab-rails-bak.rar gitlab-rails/*
```

### 汉化包替换覆盖

```bash
[root@kz service]# cp -rf gitlab-11-10-stable-zh/* /opt/gitlab/embedded/service/gitlab-rails/
cp: cannot overwrite non-directory '/opt/gitlab/embedded/service/gitlab-rails/log' with directory 'gitlab-11-10-stable-zh/log'
cp: cannot overwrite non-directory '/opt/gitlab/embedded/service/gitlab-rails/tmp' with directory 'gitlab-11-10-stable-zh/tmp'
```

### 重载配置

```bash
[root@kz service]# gitlab-ctl reconfigure
```

### 重启

```bash
[root@kz service]# gitlab-ctl restart
```

### 常见问题

#### cp 出现覆盖提示

查看命令别名列表：

```bash
[root@kz conf]# alias -p
alias cp='cp -i'
alias l.='ls -d .* --color=auto'
```
`cp -i` 表示文件覆盖时提示。

取消别名：

```bash
[root@kz conf]# unalias cp
```

# 安装

系统环境： CentOS 6

gitlab版本: ce | 11.11.0

### 安装

#### 安装配置依赖

下面命令同时打开防火墙系统的HTTP和SSH权限。

```bash
sudo yum install -y curl policycoreutils-python openssh-server cronie
sudo lokkit -s http -s ssh

```

安装Postfix启动邮件通知服务。

```
sudo yum install postfix
sudo service postfix start
sudo chkconfig postfix on

```

#### 添加GitLab包仓库并安装

添加仓库：

```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash

```

安装：

```bash
sudo EXTERNAL_URL="https://gitlab.example.com" yum -y install gitlab-ce

```

`EXTERNAL_URL` 指定外部访问地址，安装时会自动配置，并将该地址作为GitLab访问入口。

如果使用`https://`地址，GitLab自动生成相关证书文件。如果使用自己的证书，用`http://`即可。

#### 访问登陆

浏览器地址栏输入`EXTERNAL_URL`的地址进行访问，首次访问需要重置管理员密码，管理员账号为 root。密码重置完后重新登陆。

### 参考

[`Omnibus package installation`](https://about.gitlab.com/install/#centos-6)
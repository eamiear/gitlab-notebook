# Gitlab pages

### 安装 Runner

1. 添加 GitLab 官方仓库：

```shell
# For RHEL/CentOS/Fedora

curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash
```

2. 安装最新版本的GitLab Runner，或跳到下一步骤安装指定版本

```shell
 # For RHEL/CentOS/Fedora
 sudo yum install gitlab-runner
```

3. 安装特定版本的GitLab Runner

```shell
 # for RPM based systems
 yum list gitlab-runner --showduplicates | sort -r
 sudo yum install gitlab-runner-10.0.0-1
```

### 注册Runner

Runner 有五种类型：

* shared - 执行所有未分配项目的作业
* group -  执行所在组所有未分配项目的作业
* specific - 执行已分配项目的作业
* locked - Runner不能分配给其他项目
* paused - Runner不能接收任何新作业

#### 注册共享Runner

管理员账号才能注册共享Runner，且仅能注册一个。

1. 在 `admin/runners`页上获取共享Runner token

![shared-token](snapshot/shared-token.png)

2. [注册流程](#注册流程)


3. 注册完成后，`admin/runners`页面看到runner记录

![shared-runner](snapshot/shared-runner.png)

4. 添加子域名

#### 注册流程

1. 执行下面命令：

```bash
[root@kz gitlab]# gitlab-runner register

```

2. 输入GitLab实例URL（`admin/runner`页中的链接）：

```bash
[root@kz gitlab]# gitlab-runner register
Runtime platform                                    arch=amd64 os=linux pid=14694 revision=ac2a293c version=11.11.2
Running in system-mode.                            
                                                   
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
http://47.110.228.131/

```

3. 输入token（`admin/runners`页上获取）:

```bash
Please enter the gitlab-ci token for this runner:
D3s24_Nsx4HoABtA19yfSBkd

```

4. 输入Runner描述，后续可在页面上修改
   
```bash
Please enter the gitlab-ci description for this runner:
[iZbp19xg5vv2b5wnt0avavZ]: shared-runner

```

5. 输入Runner标签，后续可在GitLab平台修改

```bash
Please enter the gitlab-ci tags for this runner (comma separated):
shared
Registering runner... succeeded                     runner=D_Nsx4Ho

```

6. 选择执行器

不确定选择哪个就选择 shell

```bash
Please enter the executor: docker, virtualbox, docker+machine, docker-ssh+machine, docker-ssh, parallels, shell, ssh, kubernetes:
shell
```

全部脚本：

```bash

[root@kz gitlab]# gitlab-runner register
Runtime platform                                    arch=amd64 os=linux pid=15281 revision=ac2a293c version=11.11.2
Running in system-mode.                            
                                                   
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
http://47.110.228.131/
Please enter the gitlab-ci token for this runner:
D3s24_Nsx4HoABtA19yfSBkd
Please enter the gitlab-ci description for this runner:
[iZbp19xg5vv2b5wnt0avavZ]: ob-shared-runner
Please enter the gitlab-ci tags for this runner (comma separated):
shared
Registering runner... succeeded                     runner=D_Nsx4Ho
Please enter the executor: docker, virtualbox, docker+machine, docker-ssh+machine, docker-ssh, parallels, shell, ssh, kubernetes:
shell
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!

```


### 参考

[`Installing the Runner`](https://docs.gitlab.com/runner/install/linux-repository.html)

[`Registering Runners`](https://docs.gitlab.com/runner/register/index.html)

[`Registering a shared Runner`](https://docs.gitlab.com/ee/ci/runners/#registering-a-shared-runner)

[`GitLab Pages`](https://docs.gitlab.com/ee/administration/pages/index.html)
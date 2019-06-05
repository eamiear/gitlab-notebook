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

Runner 分为全局共享Runner及仓库Runner。

#### 注册共享Runner




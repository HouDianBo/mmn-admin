# 安装 [Kubernetes](https://kubernetes.io/zh-cn/docs/concepts/)

搭建系统前，首先需要安装环境。 建议使用至少 16G 内存的电脑启动环境

这篇文档讲了如何在 Linux 系统安装 [k3s](https://docs.k3s.io/zh/)。
Windows 系统可以使用 Docker Desktop 启动 Kubernetes 服务。

## 安装 k3s

安装前需要确保机器的磁盘有足够的剩余空间，为了避免把磁盘占满，k8s 在磁盘占用达到一定百分比之后就不会再启动 pod 了。

```shell
curl -sfL https://rancher-mirror.rancher.cn/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn sh -
```

## 修改配置文件权限

```shell
sudo chown "$(id -un):$(id -gn)" /etc/rancher/k3s/k3s.yaml
```

## 检查安装结果

使用 `k3s kubectl get pods -A` 查看 pod，发现所有的 pod 都是 pending 状态，错误信息如下：

```
Warning  FailedScheduling  12m    default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
```

看到 disk-pressure 关键词，清理磁盘后 pod 就变成 Running 状态了。

## kubectl 配置文件 （仅限使用 k3s 的情况）

k3s 的 kubectl 配置文件位置是 /etc/rancher/k3s/k3s.yaml

通常使用 kubectl 或 helm 命令时，读取的是 /home/.kube/config 文件，如果不希望每次都指定配置文件位置，建议把 kubectl 配置文件导出到 home 目录下。

```shell
mkdir -p ~/.kube
k3s kubectl config view --raw > ~/.kube/config
```

- [上一篇 创建项目](./010-Initialize%20Project.md)
- [下一篇 部署 Keycloak](./030-Deploy%20Keycloak.md)

# 部署 [Keycloak](https://keycloak.org/) 到 Kubernetes

## 使用 Bitnami 的 Helm Chart 部署 Keycloak

- **ns** 是 [Namespace（命名空间）](https://kubernetes.io/zh-cn/docs/concepts/overview/working-with-objects/namespaces/) 的缩写

```shell
# 添加 Helm Chart Repository
helm repo add bitnami https://charts.bitnami.com/bitnami

# 更新 Repository 索引，否则可能找不到 Chart
helm repo update

# 创建 Kubernetes Namespace（命名空间）
kubectl create ns mmn

# 将 Keycloak 安装到 mmn 这个 Namespace
helm -n mmn install keycloak bitnami/keycloak --values ./assets/keycloak-values.yaml 
```

## 配置 hosts 文件

配置 keycloak.local 域名， 例如 Linux 可以在 `/etc/hosts` 文件中添加一行

```text
127.0.0.1       keycloak.local
```

## 等待安装完成

- **sts** 是 [StatefulSet](https://kubernetes.io/zh-cn/docs/concepts/workloads/controllers/statefulset/) 的缩写

```shell
kubectl -n mmn rollout status sts keycloak
```

## 访问 [Keycloak](http://keycloak.local/admin/)

使用用户/密码 admin/admin 登录 Keycloak 控制台

## 配置 Realm

1. 点击左上角 **master** 下拉框
2. 点击 **Create Realm** 按钮
3. 在 **Realm name** 的输入框中输入要创建的 Realm 名称，如 mmn
4. 点击 **Create** 按钮

## 新建用户

创建几个用户用来测试。

- [上一篇 安装 Kubernetes](020-Install%20Kubernetes.md)
- [下一篇 套皮的认证中心](./040-Auth.md)

# 管理系统 - 从搭建环境开始

很多年前就想搭建一个自己的后台管理系统，受限于精力和技术水平，一直拖延到现在。快到中年危机的年纪，必须得做点儿什么了。

本项目的开发步骤在 [doc](./doc) 目录。

## 项目目标

### 第一阶段：代码粗糙、UI 能用、使用开源组件节省工作量

- 项目后端基于 [Quarkus](https://quarkus.io/) 而不是 SpringBoot 实现（Quarkus 的代码比较轻量易学）
- 使用原生 [Kubernetes](https://kubernetes.io/) 实现服务注册与发现
- 使用 [Kubernetes ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/) 管理项目配置（配置生效需要重启服务）
- 认证授权模块使用开源产品 [Keycloak](https://www.keycloak.org/)
- 前端使用 [Next.js](https://nextjs.org/) + [Material UI](https://mui.com/)

### 第二阶段：优化

- 侧边栏展开与折叠
- 切换主题
- 使用 [qiankun](https://qiankun.umijs.org/zh/guide) 实现微前端
- 基于 [Linkerd](https://linkerd.io/) 实现 service mesh
- 使用 [Jaeger](https://www.jaegertracing.io/) 实现链路追踪

### 第三阶段：控制平台

通过管理页面，一键部署、重启、升级 mmn-admin。

## 项目功能

### 核心项目

- 用户管理 - 调用 Keycloak 的 API
- 角色管理 - 调用 Keycloak 的 API
- 用户组管理 - 调用 Keycloak 的 API
- 菜单管理 - 每个模块的菜单自己注册，服务下线后菜单隐藏
- 配置管理 - 每个模块的配置自己注册
- 字典管理

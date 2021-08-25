文档：https://jimmysong.io/kubernetes-handbook/cloud-native/quick-start.html

helm： Kubernetes 应用的包管理工具，用来管理 chart——预先配置好的安装包资源

1.安装（mac）：brew install helm

2.常用命令：

- tree [chartName]    查看目录结构

- helm create：在本地创建新的 chart；

- helm dependency：管理 chart 依赖；

- helm intall：安装 chart；

- helm lint：检查 chart 配置是否有误；

- helm list：列出所有 release；

- helm package：打包本地 chart；

- helm repo：列出、增加、更新、删除 chart 仓库；

- helm rollback：回滚 release 到历史版本；

- helm pull：拉取远程 chart 到本地；

- helm search：使用关键词搜索 chart；

- helm uninstall：卸载 release；

- helm upgrade：升级 release；

3.安装chart：helm install [NAME] [CHART] [flags]





kubectl：command line interface to help you start running commands against Kubernetes clusters,kubectl 是一个命令行工具，用于与 Kubernetes 集群和其中的 pod 通信。使用它你可以查看集群的状态，列出集群中的所有 pod，进入 pod 中执行命令等。你还可以使用 YAML 文件定义资源对象，然后使用 kubectl 将其应用到集群中。



ReplicationController 或 ReplicaSet：用于管理pod生命周期的组件

命令：kubectl apply 创建更新资源

（http://kubernetes.kansea.com/docs/user-guide/kubectl/kubectl/）

什么是 Replica 和 ReplicaSet？

        为了保证应用程序的弹性，需要在不同节点上创建多个 pod 的副本。这些被称为 Replica。假设你所需的状态策略是 “让名为 webserver-1 的 pod 始终维持在 3 个副本”，这意味着 ReplicationController 或 ReplicaSet 将监控活动副本的数量，如果其中有任何一个 replica 因任何原因不可用（例如节点的故障），那么 Deployment Controller 将自动创建一个新的系统（定义如下）。

        所需状态是在 deployment 中定义的。 Master 节点的中有一个子系统叫做 Deployment Controller，负责实际执行并使当前状态不断趋向于所需状态。

        因此，举例来说，如果你目前有 2 个 pod 的副本，而你所希望的状态应该有 3 个，那么 Replication Controller 或 ReplicaSet 会自动检测到这个要求，并指示 Deployment Controller 根据预定义的设置部署一个新的 pod。





Kubelet 可以选择是否执行在容器上运行的两种探针执行和做出反应：

- livenessProbe：指示容器是否正在运行。如果存活探测失败，则 kubelet 会杀死容器，并且容器将受到其 重启策略 的影响。如果容器不提供存活探针，则默认状态为 Success。

- readinessProbe：指示容器是否准备好服务请求。如果就绪探测失败，端点控制器将从与 Pod 匹配的所有 Service 的端点中删除该 Pod 的 IP 地址。初始延迟之前的就绪状态默认为 Failure。如果容器不提供就绪探针，则默认状态为 Success。

该什么时候使用存活（liveness）和就绪（readiness）探针?

如果容器中的进程能够在遇到问题或不健康的情况下自行崩溃，则不一定需要存活探针; kubelet 将根据 Pod 的restartPolicy 自动执行正确的操作。

如果您希望容器在探测失败时被杀死并重新启动，那么请指定一个存活探针，并指定restartPolicy 为 Always 或 OnFailure。

如果要仅在探测成功时才开始向 Pod 发送流量，请指定就绪探针。在这种情况下，就绪探针可能与存活探针相同，但是 spec 中的就绪探针的存在意味着 Pod 将在没有接收到任何流量的情况下启动，并且只有在探针探测成功后才开始接收流量。



Pod：

- k8s管理的是pod而不是直接管理容器（通常使用controller管理），pod中可以包含一个或多个容器

- 同一个 Pod 中的容器会自动的分配到同一个 node 上。同一个 Pod 中的容器共享资源、网络环境和依赖，它们总是被同时调度。

1.网络：每个pod有唯一的IP，pod内所有容器共享IP地址及端口

2.存储：一个pod可以有多个Volume，Pod 中的所有容器都可以访问共享的 volume。Volume 也可以用来持久化 Pod 中的存储资源，以防容器重启后文件丢失。

- controller管理pod（YAML文件中的kind类型标示了使用哪种controller）

1.Controller 可以创建和管理多个 Pod，提供副本管理、滚动升级和集群级别的自愈能力。例如，如果一个 Node 故障，Controller 就能自动将该节点上的 Pod 调度到其他健康的 Node 上。

包含一个或者多个 Pod 的 Controller 示例：

Deployment

StatefulSet

DaemonSet

通常，Controller 会用你提供的 Pod Template 来创建相应的 Pod。

2.Pod Templates

Pod 模版是包含了其他 object 的 Pod 定义，例如 Replication Controllers，Jobs 和 DaemonSets。Controller 根据 Pod 模板来创建实际的 Pod。

- pod安全策略：kind: PodSecurityPolicy

若直接部署pod，则应用PodSecurityPolicy 控制基于角色和组的已授权容器的访问 。

若基于deployment、replicaset创建，允许所有的 PodSecurityPolicy 对象，并且不能够有效地实现细分权限

- 生命周期

1. 挂起（Pending）：Pod 已被 Kubernetes 系统接受，但有一个或者多个容器镜像尚未创建。等待时间包括调度 Pod 的时间和通过网络下载镜像的时间，这可能需要花点时间。

1. 运行中（Running）：该 Pod 已经绑定到了一个节点上，Pod 中所有的容器都已被创建。至少有一个容器正在运行，或者正处于启动或重启状态。

1. 成功（Succeeded）：Pod 中的所有容器都被成功终止，并且不会再重启。

1. 失败（Failed）：Pod 中的所有容器都已终止了，并且至少有一个容器是因为失败终止。也就是说，容器以非0状态退出或者被系统终止。

1. 未知（Unknown）：因为某些原因无法取得 Pod 的状态，通常是因为与 Pod 所在主机通信失败。

![](https://i.loli.net/2021/08/25/dmw3Rpo9UvcDB7H.png)

Kubelet 可以选择是否执行在容器上运行的两种探针执行和做出反应：

a.livenessProbe：指示容器是否正在运行。如果存活探测失败，则 kubelet 会杀死容器，并且容器将受到其 重启策略 的影响。如果容器不提供存活探针，则默认状态为 Success。

b.readinessProbe：指示容器是否准备好服务请求。如果就绪探测失败，端点控制器将从与 Pod 匹配的所有 Service 的端点中删除该 Pod 的 IP 地址。初始延迟之前的就绪状态默认为 Failure。如果容器不提供就绪探针，则默认状态为 Success。

该什么时候使用存活（liveness）和就绪（readiness）探针?

如果容器中的进程能够在遇到问题或不健康的情况下自行崩溃，则不一定需要存活探针; kubelet 将根据 Pod 的restartPolicy 自动执行正确的操作。

如果您希望容器在探测失败时被杀死并重新启动，那么请指定一个存活探针，并指定restartPolicy 为 Always 或 OnFailure。

如果要仅在探测成功时才开始向 Pod 发送流量，请指定就绪探针。在这种情况下，就绪探针可能与存活探针相同，但是 spec 中的就绪探针的存在意味着 Pod 将在没有接收到任何流量的情况下启动，并且只有在探针探测成功后才开始接收流量。




---
title: 设置容器的默认资源限制
---

_v2.2.0 或更新版本可用_

设置资源配额的时候，如果您在项目或命名空间中设置了任何 CPU 相关，或内存相关的配额（如资源限制或资源预留），在创建 Pod 时，Pod 中所有容器都需要配置各自的 CPU 或内存的限制或者预留，详情请参考[Kubernetes 官方文档](https://kubernetes.io/docs/concepts/policy/resource-quotas/#requests-vs-limits)。

为了避免在每一个容器里都设置一遍资源限制，您可以在命名空间中设置容器的默认资源限制。

## 修改容器的默认资源限制

_v2.2.0 或更新版本可用_

当您遇到下列任意一种情况时，您可以修改容器的默认资源限制。

- 您已经对项目设置了 CPU 或内存的资源配额，现在需要给容器设置一个对应的默认值。

- 您需要修改容器的默认资源限制。

- 访问 Rancher **全局**页面，找到对应的集群。

- 从主菜单中选择**项目/命名空间**。

- 在项目列表中找到您需要修改的项目，选择 **... > 编辑**

- 展开**容器默认限制**，修改默认值。

## 沿用资源限制

在完成在项目层级设置默认容器资源限制之后，项目中的所有新建的命名空间都会沿用这个资源限制参数。对修改资源限制之前已经在项目内的命名空间而言，它们不会自动沿用修改之后的容器资源限制，您需要手动管理这些命名空间，把它们的资源限制修改为新的参数，这样操作，才可以使新创建的容器使用您想要的配置。

> **说明：** 在 Rancher v2.2.0 版本之前，您不可以发布没有资源限制的应用商店应用。在 Rancher v2.2.0 及更新版本内，您可以在项目中设置容器的默认资源限制，然后运行应用商店应用。

在命名空间层级设置容器的默认资源限制以后，这个默认参数会下发到容器中。在创建工作负载的过程中，这些资源限制/资源预留数值是可以被覆盖的。

## 容器资源限制类型

可以修改的容器资源限制类型如下表所示：

| 资源类型 | 描述                                                                                                                                                    |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CPU 限制 | 可以分配给容器的 CPU 最大值，单位：[millicores](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu)。 |
| CPU 预留 | 保障容器正常运行所需的 CPU 最小值，单位：millicores。                                                                                                   |
| 内存限制 | 可以分配给容器的内存最大值，单位：bytes。                                                                                                               |
| 内存预留 | 保障容器正常运行所需的内存最小值，单位：bytes。                                                                                                         |
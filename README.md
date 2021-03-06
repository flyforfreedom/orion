# Orion AI Platform

Orion vGPU软件由[VirtAI Tech 趋动科技](https://virtai.tech)开发，是一个为云或者数据中心内的AI应用、CUDA应用提供GPU资源池化、GPU虚拟化能力的系统软件。通过高效的通讯机制连接应用与GPU资源池，使得AI应用、CUDA应用可以不受GPU物理位置的限制，部署在云或者数据中心内任何一个物理机、Container或者VM内。

* 兼容已有的AI应用和CUDA应用，无需修改已有应用程序。
* 细粒度的GPU虚拟化支持。
* 应用可使用远程物理节点上GPU，应用部署无需受GPU服务器位置、资源数量的约束。
* vGPU资源动态分配动态释放。无需重启Container/VM/物理机。
* 通过对GPU资源池的管理和优化，提高整个云和数据中心GPU的利用率和吞吐率。
* 通过统一管理GPU，降低GPU的管理复杂度和成本。

# [Quick Start](doc/quick-start)
快速安装部署并体验GPU虚拟化的使用

# [User Guide](doc/Orion-User-Guide.md)
Orion vGPU软件用户手册

# [Docker Image](client-dockerfiles)
预装好深度学习框架（TensorFlow, PyTorch），以及Orion Client Runtime的容器镜像。

# <a id="tech-blog"></a>More
我们通过若干技术博客，向用户展示更多的Orion vGPU软件使用场景。

* [应用程序动态链接CUDA Runtime 库的简易编译方法](cuda-wrapper)
* [使用k8s容器化部署Orion vGPU组件](orion-kubernetes-deploy)
* [Kubernetes-Orion-Plugin 在k8s集群中调度vGPU资源](./doc/Orion-k8s-device-plugin.md)
* [TensorFlow 使用Orion vGPU软件加速模型训练与推理](./blogposts/tensorflow_models.md)
* [PyTorch 使用Orion vGPU软件加速模型训练与推理](./blogposts/pytorch_models.md)

# What's New
* **2019/11/20** 简化本地容器共享内存配置，支持更多库和框架 （[旧版本更新指南](./how-to-update.md)）

    配置简化：本地容器不需要挂载 /dev/shm/orionsock 共享内存 （**要求 host IPC 权限**）

    * 对于 `docker run` 启动的容器，要求指定 `--ipc host` 参数
    * 对于由 Kubernetes 启动的容器，需要在 yaml 配置文件中指定 `hostIPC: true`

    支持 TF 2.0, PyTorch 1.3, NVCaffe 深度学习框架

    支持 [NCCL](https://developer.nvidia.com/nccl) 2.4.x 作为多卡训练的后端

* **2019/11/1**  [应用程序动态链接CUDA Runtime 库的简易编译方法](cuda-wrapper)

* **2019/10/29** 增加 [PaddlePaddle 1.5 镜像](client-dockerfiles/client-cu10.0-paddle1.5-py3)

    ```bash
    docker pull virtaitech/orion-client:cu10.0-paddle1.5-py3
    ```

* **2019/10/25** CUDA 10.1 及多种框架支持，基于Kubernetes的全容器化部署方案，

    支持 CUDA 10.1，支持 TF 1.14，PyTorch 1.2, Kaldi 5.3, PaddlePaddle 1.5.2

    提供 [Orion vGPU基于Kubernetes的全容器化部署](orion-kubernetes-deploy) 方案
    
    支持 [NVIDIA GPU Container (NGC)](https://ngc.nvidia.com/catalog/containers?orderBy=modifiedDESC&query=&quickFilter=containers&filters=)

    * [在 NGC 镜像中安装 Orion Client Runtime](ngc-dockerfiles)

* **2019/09/03** 支持多CUDA版本：CUDA 9.0, 9.1, 9.2, 10.0； 提供 k8s-orion-plugin

    Orion Server 可以动态支持多种CUDA版本共存，只需要确保 `/usr/local` 目录下有对应的CUDA SDK，例如 `/usr/local/cuda-10.0`，`/usr/local/cuda-9.0`。
        
    Orion Client端，取决于用户程序的需求，需要安装对应于不同 CUDA 版本的 Orion Client Runtime。

# Contact Us

如果您在使用本产品的过程中遇到问题，欢迎在GitHub上提交issue，或者通过邮件联系我们：

feedback@virtaitech.com
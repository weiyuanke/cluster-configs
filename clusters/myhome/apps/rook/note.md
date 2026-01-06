过程中的几个问题：
- kubeadm + calico + kube-proxy的模式下，节点上无法访问通过clusterIP暴露出来的mon服务，导致认证/授权失败；
- 重新创建ceph集群后，由于元数据残留有上一个集群的fsid，导致对应的osd无法启动；需要通过命令进行清理：ceph-volume lvm zap /dev/xxxx --destroy 注意：通过wipefs、dd等都无法有效清理；
- 磁盘在加入ceph集群后，目前能正确识别容量并自动调整权重；
- 需要调整failureDomain，可以从host调整到osd，并且调整副本数量为2，提高资源利用率；

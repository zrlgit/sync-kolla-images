# sync-kolla-images

定期同步 openstack kolla 镜像到阿里云 registry.aliyuncs.com/kolla-helm。

openstack kolla 官方存储镜像的仓库是 quay.io/openstack.kolla，这个仓库位于国外，在国内访问会非
常慢。这个项目借助 github action 结合 [image-syncer](https://github.com/AliyunContainerService/image-syncer) 
每天同步 kolla 镜像到阿里云，目前我们只同步了 xena, yoga, master 三个版本的镜像，如果你需要其他版本
的镜像请在 [github issue](https://github.com/kungze/sync-kolla-images/issues) 中留言。

## 使用

### kolla-ansible

[kolla-ansible](https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html) 是 openstack 官方
提供的的项目，通过一些列的 ansible 脚本实现 openstack 的容器化部署。kolla-ansible 的安装请参考官方文档，
这里就不单独讲解了。

安装完成后修改 kolla-ansible 配置文件 globals.yml


```yaml
kolla_base_distro: "ubuntu"
kolla_install_type: "source"
openstack_release: "yoga"
docker_registry: "registry.aliyuncs.com"
docker_namespace: "kolla-helm"
```

### kolla-helm

[kolla-helm](https://github.com/kungze/kolla-helm) 是 [kungze](https://github.com/kungze) 团队想实现的一套
基于 k8s 的一套 openstack 容器化部署方案，目前这个项目还初始开发中，我们会持续完善相关文档。

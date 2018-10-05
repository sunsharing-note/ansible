**ansible-playbook**

假设有以下任务，在远程主机上配置Yum源，安装nginx并启动nginx服务，可采用以下方式完成。

* ansible test1 -m yum_repository -a 'name=aliEpel description="alibaba EPEL" baseurl=https://mirrors.aliyun.com/epel/$releasever\Server/$basearch/'
* ansible test1 -m yum -a 'name=nginx state=installed enablerepo=aliEpel disable_gpg_check=yes'
* ansible test1 -m service -a "name=nginx state=started"
* ansible test1 -m service -a "name=nginx state=stopped"

我们可以使用playbook来完成多个任务，比如ping和创建文件

```
---
- hosts: test1
  remote_user: root
  tasks:
  - name: test ping
    ping:
  - name: create directory
    file:
      path: /data/test
      state: directory
```

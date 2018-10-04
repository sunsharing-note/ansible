##### ansible安装

* yum install epel-release -y    安装epel源
* yum install git python python-pip -y  安装依赖
* #pip install pip --upgrade
* #pip install ansible
* 我们使用pip阿里云加速来安装
* pip install pip --upgrade -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com 
* pip install --no-cache-dir ansible -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
* ssh-keygen -t rsa -b 2048
* ssh-copy-id  root@192.168.40.200
* ssh-copy-id  root@192.168.40.201
* ssh-copy-id  root@192.168.40.202

**注**：这种方式安装需要自己在/etc目录下创建ansible文件夹，再在其目录下创建编辑hosts文件。
```
[root@ansible-k8s1 etc]# ansible all -m ping
192.168.40.202 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.40.201 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.40.200 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

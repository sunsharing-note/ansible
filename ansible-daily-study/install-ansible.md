##### ansible安装

* yum install epel-release -y
* yum install git python python-pip -y
* pip install pip --upgrade -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
* pip install --no-cache-dir ansible -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
* ssh-keygen -t rsa -b 2048
* ssh-copy-id  root@192.168.40.200
* ssh-copy-id  root@192.168.40.201
* ssh-copy-id  root@192.168.40.202

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

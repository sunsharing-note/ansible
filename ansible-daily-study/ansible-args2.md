**说明**: 我们在执行playbook的时候，ansible默认去执行了一个任务，也就是手机playbook中所定义的主机的信息，其默认调用了ansible的setup模块，而我们使用ansible test1 -m setup时收集到的信息众多，加入只需要内存的信息，可以使用如下的方式，可以使用通配符。另外，收集到的信息很有用，比如可以根据系统是centos6还是centos7作决定执行相关的脚本，还可以使用debug模块进行调试、测试。

```
[root@ansible-k8s1 data]# ansible test1 -m setup -a 'filter=ansible_memory_mb'
test1 | SUCCESS => {
    "ansible_facts": {
        "ansible_memory_mb": {
            "nocache": {
                "free": 1851,
                "used": 133
            },
            "real": {
                "free": 1760,
                "total": 1984,
                "used": 224
            },
            "swap": {
                "cached": 0,
                "free": 4095,
                "total": 4095,
                "used": 0
            }
        }
    },
    "changed": false
}

[root@ansible-k8s1 data]# ansible test1 -m setup -a 'filter=*memory*'
test1 | SUCCESS => {
    "ansible_facts": {
        "ansible_memory_mb": {
            "nocache": {
                "free": 1851,
                "used": 133
            },
            "real": {
                "free": 1760,
                "total": 1984,
                "used": 224
            },
            "swap": {
                "cached": 0,
                "free": 4095,
                "total": 4095,
                "used": 0
            }
        }
    },
    "changed": false
}

```

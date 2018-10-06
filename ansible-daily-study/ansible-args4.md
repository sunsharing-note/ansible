**说明**: ansible中还有其他的一些内置变量，如groups group_names inventory_dir incentory_hostname

```
[root@ansible-k8s1 data]# ansible test1 -m debug -a "msg={{inventory_dir}}"
test1 | SUCCESS => {
    "msg": "/etc/ansible"
}
[root@ansible-k8s1 data]# ansible test1 -m debug -a "msg={{play_hosts}}"
test1 | SUCCESS => {
    "msg": [
        "test1",
        "test2",
        "test3"
    ]
}
[root@ansible-k8s1 data]# ansible test1 -m debug -a "msg={{groups.testA}}"
test1 | SUCCESS => {
    "msg": [
        "test1",
        "test2"
    ]
}
[root@ansible-k8s1 data]# ansible test1 -m debug -a "msg={{group_names}}"
test1 | SUCCESS => {
    "msg": [
        "test",
        "testA"
    ]
}
[root@ansible-k8s1 data]# ansible test1 -m debug -a "msg={{groups.test}}"
test1 | SUCCESS => {
    "msg": [
        "test3",
        "test1",
        "test2"
    ]
}

```

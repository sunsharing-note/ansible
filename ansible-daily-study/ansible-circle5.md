**需求**: 需要创建几个文件夹，test2 test4 test6 test8 test10 另：with_random_choice从列表中随机返回一个

```
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "{{ item }}}"
    with_sequence: start=1 end=5 stride=1 **注** 此处可改为 with_sequence: count=5 还可以添加format="number is %0.2f"进行格式化输出
[root@ansible-k8s1 data]# ansible-playbook --syntax-check circle-test.yaml

playbook: circle-test.yaml
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => (item=1) => {
    "msg": "1}"
}
ok: [test1] => (item=2) => {
    "msg": "2}"
}
ok: [test1] => (item=3) => {
    "msg": "3}"
}
ok: [test1] => (item=4) => {
    "msg": "4}"
}
ok: [test1] => (item=5) => {
    "msg": "5}"
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0


```

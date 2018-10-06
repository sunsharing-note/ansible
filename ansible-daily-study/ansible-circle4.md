```
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "{{ item }}"
    with_indexed_items:
    - test1
    - test2
    - test3
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => (item=[0, u'test1']) => {
    "msg": [
        0,
        "test1"
    ]
}
ok: [test1] => (item=[1, u'test2']) => {
    "msg": [
        1,
        "test2"
    ]
}
ok: [test1] => (item=[2, u'test3']) => {
    "msg": [
        2,
        "test3"
    ]
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0
```
```
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "index is : {{ item.0 }}, value is : {{ item.1 }}"
    with_indexed_items:
    - test1
    - test2
    - test3
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => (item=[0, u'test1']) => {
    "msg": "index is : 0, value is : test1"
}
ok: [test1] => (item=[1, u'test2']) => {
    "msg": "index is : 1, value is : test2"
}
ok: [test1] => (item=[2, u'test3']) => {
    "msg": "index is : 2, value is : test3"
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0
```

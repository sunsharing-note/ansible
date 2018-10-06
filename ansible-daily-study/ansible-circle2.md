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
    with_items:
    - [ 1, 2, 3 ]
    - [ a, b ]
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *********************************************************************************************************************************

TASK [debug] *********************************************************************************************************************************
ok: [test1] => (item=1) => {
    "msg": 1
}
ok: [test1] => (item=2) => {
    "msg": 2
}
ok: [test1] => (item=3) => {
    "msg": 3
}
ok: [test1] => (item=a) => {
    "msg": "a"
}
ok: [test1] => (item=b) => {
    "msg": "b"
}

PLAY RECAP ***********************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0


[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "{{ item }}"
    with_list:
    - [ 1, 2, 3 ]
    - [ a, b ]
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *********************************************************************************************************************************

TASK [debug] *********************************************************************************************************************************
ok: [test1] => (item=[1, 2, 3]) => {
    "msg": [
        1,
        2,
        3
    ]
}
ok: [test1] => (item=[u'a', u'b']) => {
    "msg": [
        "a",
        "b"
    ]
}

PLAY RECAP ***********************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0

[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "{{ item }}"
    with_flattened:
    - [ 1, 2, 3 ]
    - [ a, b ]
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *********************************************************************************************************************************

TASK [debug] *********************************************************************************************************************************
ok: [test1] => (item=1) => {
    "msg": 1
}
ok: [test1] => (item=2) => {
    "msg": 2
}
ok: [test1] => (item=3) => {
    "msg": 3
}
ok: [test1] => (item=a) => {
    "msg": "a"
}
ok: [test1] => (item=b) => {
    "msg": "b"
}

PLAY RECAP ***********************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0

[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: debug
    debug:
      msg: "{{ item }}"
    with_together:
    - [ 1, 2, 3 ]
    - [ a, b ]
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => (item=[1, u'a']) => {
    "msg": [
        1,
        "a"
    ]
}
ok: [test1] => (item=[2, u'b']) => {
    "msg": [
        2,
        "b"
    ]
}
ok: [test1] => (item=[3, None]) => {
    "msg": [
        3,
        null
    ]
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0

```

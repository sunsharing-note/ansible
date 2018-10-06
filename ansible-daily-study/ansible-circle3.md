**需求**: 我需要创建a,b,c三个目录，这三个目录下都有相同的两个子目录test1,test2,通常我们使用mkdir -p {a,b,c}/{test1,test2},用ansible的shell模块也是可以的。
这里用循环来做。
```
[root@ansible-k8s1 data]# ansible-playbook --syntax-check circle-test.yaml

playbook: circle-test.yaml
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: create directory
    file:
      path: "/data/{{ item.0 }}/{{ item.1 }}"
      state: directory
    with_cartesian:
    - [ a, b, c ]
    - [ test1, test2 ]
[root@ansible-k8s1 data]# ansible-playbook  circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [create directory] ******************************************************************************************************************************
changed: [test1] => (item=[u'a', u'test1'])
changed: [test1] => (item=[u'a', u'test2'])
changed: [test1] => (item=[u'b', u'test1'])
changed: [test1] => (item=[u'b', u'test2'])
changed: [test1] => (item=[u'c', u'test1'])
changed: [test1] => (item=[u'c', u'test2'])

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=1    unreachable=0    failed=0


```

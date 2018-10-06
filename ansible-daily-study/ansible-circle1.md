**说明**: 使用循环可以用让我们事半功倍，平时创建四个文件夹，需要写四个file，而使用循环则方便很多，一次搞定。如下

```
[root@ansible-k8s1 data]# ansible-playbook  --syntax-check circle-test.yaml

playbook: circle-test.yaml
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  vars:
    dirs:
    - "/data/test1"
    - "/data/test2"
    - "/data/test3"
    - "/data/test4"
  remote_user: root
  gather_facts: no
  tasks:
  - name: create directory
    file:
      path: "{{ item }}"
    with_items: "{{ dirs }}"
[root@ansible-k8s1 data]# ansible-playbook  circle-test.yaml

PLAY [test1] *******************************************************************************************************************************************************

TASK [create directory] ********************************************************************************************************************************************
changed: [test1] => (item=/data/test1)
changed: [test1] => (item=/data/test2)
changed: [test1] => (item=/data/test3)
changed: [test1] => (item=/data/test4)

PLAY RECAP *********************************************************************************************************************************************************
test1                      : ok=1    changed=1    unreachable=0    failed=0


```

```
[root@ansible-k8s1 data]# ansible-playbook --syntax-check circle-test.yaml

playbook: circle-test.yaml
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: task1
    shell: "{{ item }}"
    with_items:
    - "ls /data"
    - "ls /home"
    register: returnvalue
  - name: debug
    debug:
      msg: "{{ item.stdout }}"
    with_items: "{{ returnvalue.results }}"
[root@ansible-k8s1 data]# ansible-playbook  circle-test.yaml

PLAY [test1] *********************************************************************************************************************************

TASK [task1] *********************************************************************************************************************************
changed: [test1] => (item=ls /data)
changed: [test1] => (item=ls /home)

TASK [debug] *********************************************************************************************************************************
ok: [test1] => (item={'_ansible_parsed': True, 'stderr_lines': [], '_ansible_item_result': True, u'end': u'2018-10-06 21:18:08.007912', '_ansible_no_log': False, u'stdout': u'test1\ntest2\ntest3\ntest4', u'cmd': u'ls /data', u'rc': 0, 'item': u'ls /data', u'delta': u'0:00:00.004222', '_ansible_item_label': u'ls /data', u'stderr': u'', u'changed': True, u'invocation': {u'module_args': {u'warn': True, u'executable': None, u'_uses_shell': True, u'_raw_params': u'ls /data', u'removes': None, u'argv': None, u'creates': None, u'chdir': None, u'stdin': None}}, 'stdout_lines': [u'test1', u'test2', u'test3', u'test4'], u'start': u'2018-10-06 21:18:08.003690', '_ansible_ignore_errors': None, 'failed': False}) => {
    "msg": "test1\ntest2\ntest3\ntest4"
}
ok: [test1] => (item={'_ansible_parsed': True, 'stderr_lines': [], '_ansible_item_result': True, u'end': u'2018-10-06 21:18:08.346233', '_ansible_no_log': False, u'stdout': u'test', u'cmd': u'ls /home', u'rc': 0, 'item': u'ls /home', u'delta': u'0:00:00.035620', '_ansible_item_label': u'ls /home', u'stderr': u'', u'changed': True, u'invocation': {u'module_args': {u'warn': True, u'executable': None, u'_uses_shell': True, u'_raw_params': u'ls /home', u'removes': None, u'argv': None, u'creates': None, u'chdir': None, u'stdin': None}}, 'stdout_lines': [u'test'], u'start': u'2018-10-06 21:18:08.310613', '_ansible_ignore_errors': None, 'failed': False}) => {
    "msg": "test"
}

PLAY RECAP ***********************************************************************************************************************************
test1                      : ok=2    changed=1    unreachable=0    failed=0
```


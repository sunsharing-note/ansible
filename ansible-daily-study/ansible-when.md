**ansible条件判断**: when 运算符有 > < == >= <= != not or and 默认情况下，ansible在遇到错误之后，后续的任务就不再执行了，但有时候我们需要跳过，则可以利用
ignore_errors: true
```
[root@ansible-k8s1 data]# cat when-test.yaml
---
- hosts: test1
  remote_user: root
  tasks:
  - name: debug
    debug:
      msg: "system is centos"
    when: ansible_distribution == "CentOS"
[root@ansible-k8s1 data]# ansible-playbook when-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [test1]

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => {
    "msg": "system is centos"
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=2    changed=0    unreachable=0    failed=0
```
```
[root@ansible-k8s1 data]# cat when-test.yaml
---
- hosts: test1
  remote_user: root
  tasks:
  - name: task1
    shell: "ls /111"
    register: return
    ignore_errors: true
  - name: task2
    debug:
      msg: " yes "
    when: return.rc == 0
  - name: task3
    debug:
      msg: " no "
    when: return.rc != 0
[root@ansible-k8s1 data]# ansible-playbook  when-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [test1]

TASK [task1] *****************************************************************************************************************************************
fatal: [test1]: FAILED! => {"changed": true, "cmd": "ls /111", "delta": "0:00:00.003972", "end": "2018-10-07 16:47:30.522612", "msg": "non-zero return code", "rc": 2, "start": "2018-10-07 16:47:30.518640", "stderr": "ls: cannot access /111: No such file or directory", "stderr_lines": ["ls: cannot access /111: No such file or directory"], "stdout": "", "stdout_lines": []}
...ignoring

TASK [task2] *****************************************************************************************************************************************
skipping: [test1]

TASK [task3] *****************************************************************************************************************************************
ok: [test1] => {
    "msg": " no "
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=3    changed=1    unreachable=0    failed=0


```

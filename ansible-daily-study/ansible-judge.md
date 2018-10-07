ansible判断： exists defined undefined none success successded failure failed  changed change skip skipped file directory link mount exists
lower upper event odd divisibelby(num) version subset superset string  number与when配合使用，fail模块，failed_when changed_when

另外，通常使用when关键字只能去执行一个任务，但是如果需要执行多个任务，这时需要block，将多个任务组成一个块。

```
[root@ansible-k8s1 data]# cat tests-test.yaml
---
- hosts: test1
  remote_user: root
  tasks:
  - name: debug1
    debug:
      msg: " 111 "
  - name: block
    block:
    - name: debug2
      debug:
        msg: " 222 "
    - name: debug3
      debug:
        msg: " 333 "
    when: 2 > 1
[root@ansible-k8s1 data]# ansible-playbook tests-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [test1]

TASK [debug1] ****************************************************************************************************************************************
ok: [test1] => {
    "msg": " 111 "
}

TASK [debug2] ****************************************************************************************************************************************
ok: [test1] => {
    "msg": " 222 "
}

TASK [debug3] ****************************************************************************************************************************************
ok: [test1] => {
    "msg": " 333 "
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=4    changed=0    unreachable=0    failed=0
```
```
[root@ansible-k8s1 data]# cat tests-test.yaml
---
- hosts: test1
  remote_user: root
  tasks:
  - name: block
    block:
    - name: shell
      shell: "ls /111"
    rescue: #救援的意思，当任务失败后执行，除了rescue，还可以有always，无论block失败与否，都执行它下面的任务
    - name: debug
      debug:
        msg: " error "
[root@ansible-k8s1 data]# ansible-playbook tests-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [test1]

TASK [shell] *****************************************************************************************************************************************
fatal: [test1]: FAILED! => {"changed": true, "cmd": "ls /111", "delta": "0:00:00.003883", "end": "2018-10-07 17:22:01.672520", "msg": "non-zero return code", "rc": 2, "start": "2018-10-07 17:22:01.668637", "stderr": "ls: cannot access /111: No such file or directory", "stderr_lines": ["ls: cannot access /111: No such file or directory"], "stdout": "", "stdout_lines": []}

TASK [debug] *****************************************************************************************************************************************
ok: [test1] => {
    "msg": " error "
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=2    changed=0    unreachable=0    failed=1

```

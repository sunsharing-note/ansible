**说明**: 在ansible中引用变量可更灵活，变量在作为开头使用的时候，需要使用双引号引起来；而不作为开头使用的时候则不需要。当然也有例外，如果在引用时，使用
等号来引用，则不需要考虑引号的问题。

```
[root@ansible-k8s1 data]# cat args-test.yaml
---
- hosts: test1
  remote_user: root
  vars:
    test_home: test
    nginx:
      conf80: /data/nginx/80.conf
      conf8080: /data/nginx/8080.conf
  tasks:
  - name: task1
    file:
      path: /data/{{ test_home }}
      state: directory
      owner: test
      group: test
      mode: 0757
  - name: task2
    file:
      path: "{{ nginx.conf80 }}"
      state: touch
  - name: task3
    file:
      path: "{{ nginx.conf8080 }}"
      state: touch
[root@ansible-k8s1 data]# ansible-playbook  args-test.yaml

PLAY [test1] **********************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************
ok: [test1]

TASK [task1] **********************************************************************************************************
changed: [test1]
TASK [task2] *********************************************************************************************************************************
changed: [test1]

TASK [task3] *********************************************************************************************************************************
changed: [test1]

PLAY RECAP ***********************************************************************************************************************************
test1                      : ok=4    changed=2    unreachable=0    failed=0

```

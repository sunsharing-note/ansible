**说明**: 我们在剧本中编写了很多任务，但是有时候这些任务不是都要执行，只需要执行部分任务，这个时候就可以利用tags,在任务中打标签，在执行剧本的时候，指定tags,ansible还具有5个特殊标签

* always
* tagged
* never
* untagged
* all

打标签的方式多样化，每个任务可以打多个标签，这就让我们可以通过指定一类标签来执行一类的任务，比如数据备份任务，而且如果多个任务拥有同一个标签，还可以把
相同的那一个标签写在playbook中，即与tasks同级。

使用如下命令列出剧本中的标签

```
[root@ansible-k8s1 data]# ansible-playbook --list-tags tag-test.yaml

playbook: tag-test.yaml

  play #1 (test1): test1        TAGS: []
      TASK TAGS: [task1, task2, task3]
```

```
[root@ansible-k8s1 data]# cat tag-test.yaml
---
- hosts: test1
  remote_user: root
  tasks:
  - name: task1
    file:
      path: /data/test1
      state: touch
    tags: task1
  - name: task2
    file:
      path: /data/test2
      state: touch
    tags: task2
  - name: task3
    file:
      path: /data/test3
      state: touch
    tags: task3

[root@ansible-k8s1 data]# ansible-playbook  --tags=task2 tag-test.yaml

PLAY [test1] *************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************
ok: [test1]

TASK [task2] *************************************************************************************************************
changed: [test1]

PLAY RECAP ***************************************************************************************************************
test1                      : ok=2    changed=1    unreachable=0    failed=0

[root@ansible-k8s1 data]# ansible-playbook  --skip-tags=task2 tag-test.yaml

PLAY [test1] *************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************
ok: [test1]

TASK [task1] *************************************************************************************************************
changed: [test1]

TASK [task3] *************************************************************************************************************
changed: [test1]

PLAY RECAP ***************************************************************************************************************
test1                      : ok=3    changed=2    unreachable=0    failed=0


```

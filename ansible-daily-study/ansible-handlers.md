**说明**: 有时候通过ansible执行一些任务时，希望先前的条件达成后，才执行后面的任务；否则就不执行后面的任务。比如，nginx的配置修改了才重启nginx，否则就不重启nginx

handlers是另外一种任务列表，与tasks是平级的，只是满足一定条件之后才会执行。

```
这个示例有问题
---
- hosts: test1
  remote_user: root
  tasks:
  - name: modify nginx config
    shell: cd /etc/nginx/; sed -i 's/8081/8082/g' nginx.conf
    notify:
      restart nginx
  handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

**说明**: 一般情况下，所有tasks执行完了才会去执行handlers；如果需要使用- meta: flush_handlers，这样的话，在meta之前的任务执行完成之后就会去执行handlers

```
---
- hosts: test70
  remote_user: root
  tasks:
  - name: task1
    file: path=/testdir/testfile
          state=touch
    notify: handler1
  - name: task2
    file: path=/testdir/testfile2
          state=touch
    notify: handler2
 
  - meta: flush_handlers
 
  - name: task3
    file: path=/testdir/testfile3
          state=touch
    notify: handler3
 
  handlers:
  - name: handler1
    file: path=/testdir/ht1
          state=touch
  - name: handler2
    file: path=/testdir/ht2
          state=touch
  - name: handler3
    file: path=/testdir/ht3
          state=touch
 ```
 
listen

```
---
- hosts: test70
  remote_user: root
  tasks:
  - name: task1
    file: path=/testdir/testfile
          state=touch
    notify: handler group1
 
  handlers:
  - name: handler1
    listen: handler group1
    file: path=/testdir/ht1
          state=touch
  - name: handler2
    listen: handler group1
    file: path=/testdir/ht2
          state=touch
```




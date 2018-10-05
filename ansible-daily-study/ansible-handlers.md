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

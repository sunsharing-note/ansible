* ansible-doc -l 查看ansible支持的模块
* ansible-doc -s fetch 查看模块的用法

```
[root@ansible-k8s1 ~]# ansible test1 -m fetch -a "src=/data/test.txt dest=/data"
test1 | SUCCESS => {
    "changed": true,
    "checksum": "c4f9375f9834b4e7f0a528cc65c055702bf5f24a",
    "dest": "/data/test1/data/test.txt",
    "md5sum": "f447b20a7fcbf53a5d5be013ea0b15af",
    "remote_checksum": "c4f9375f9834b4e7f0a528cc65c055702bf5f24a",
    "remote_md5sum": null
}
echo "12345" >>test.txt
[root@ansible-k8s1 data]# ansible test1 -m fetch -a "src=/data/test.txt dest=/data"
test1 | SUCCESS => {
    "changed": true,
    "checksum": "c4f9375f9834b4e7f0a528cc65c055702bf5f24a",
    "dest": "/data/test1/data/test.txt",
    "md5sum": "f447b20a7fcbf53a5d5be013ea0b15af",
    "remote_checksum": "c4f9375f9834b4e7f0a528cc65c055702bf5f24a",
    "remote_md5sum": null
}

```
* 说明：ansible以结果为导向

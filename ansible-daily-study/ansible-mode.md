##### ansible常用模块

* copy 复制文件
* file 对文件或目录的操作
* blockinfile 在指定文本中插入一段“文本”
* lineinfile 确保某一行文本存在于指定文本中
* find 查找指定文件
* replace 替换文件
* command 在远程主机上执行命令 不支持> . |类似的操作符 不会经过远程主机shell处理
* shell 与command相比 在远程主机/bin/sh处理
* script 在远程主机上执行ansible主机上的脚本
* cron 计划任务
* service 管理远程主机上的服务
* user 管理远程主机上的用户
* group 管理远程主机上的组
* yum_repository 管理远程主机的Yum仓库
* yum yum源管理包



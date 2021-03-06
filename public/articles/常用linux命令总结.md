# 常用linux shell命令总结
为了不每次需要敲命令实现一个简单任务的时候都去google（虽然回来翻这篇文章也需要时间），我决定记录一下自己常用的一些linux shell命令，同时也考虑一些常用工具的用法总结。对于一些的特殊的功能，将独立成其他的文章（比如内网穿透一文）。本文将对linux的不断熟悉过程中进行不定期更新:-D！
## 进程操作
```sh
# 删除一组特定的进程(其中cut截取的列数可能需要根据系统不同动态调整)
ps aux | grep keyword | cut -c 9-15 | xargs kill -9
```
## 文件
```sh
# 查看剩余空间（-h, --human-readable;  -l, --local）
df -hl
# 递归替换所有jpeg后缀图片为jpg后缀（其中-print0和xargs -0是为了防止文件名带有空格）
find . -type f -name '*.jpeg' -print0 | xargs -0 rename 's/\.jpeg/\.jpg/'
```
## 网络
```shell
# 查看所有监听端口
# t: tcp, l: listen, p: process info, n: disable name resolution
netstat -tlpn
# 查看端口占用情况
lsof -i :port
```
## docker
```sh
# 删除所有exited的container
docker rm $(docker ps -a -f status=exited -q)
# Purging All Unused or Dangling Images, Containers, Volumes, and Networks
docker system prune
```
## ssh
```sh
ssh-keygen -t rsa
ssh-copy-id [-i pub_file] username@destination
# 通过ssh远程挂载
sshfs $user@$host:$remote_dir_path $local_dir_path 
# 利用ssh进行端口映射（详见《内网穿透的几种姿势》）
ssh -CqTnNf -L srcIP:srcPort:desIP:desPort user@middle_server
```
## git
```sh
# 从最近的commit恢复特定文件（checkout被拆分成了restore和switch）
git restore file
```


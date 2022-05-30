### docker build 来自dockerfile
```sh
docker build - < <Dockerfile文件名称> -t <dockerImage别名>
```
### docker 本地运行
```sh
docker run -t -i <dockerImage别名> /bin/bash
```
### docker 拷贝
```sh
docker cp <本地文件路径> <dockerImageRun的ip端口地址root@后面的一串字符>:/路径 
比如：docker cp /Users/leedanatech/GitCode/aizuoye-ios a0106d6edcaa:/files/aizuoye
```
### docker与gitlab
```sh
## 登录
docker login <git的端口地址路径>
比如： docker login host:port/path 
## build
docker build -t  <git的端口地址路径>:<tag> .
这里面会自动找到dockerfile在当前目录下进行build
## push到远程
docker push <git的端口地址路径>:<tag>
```

### 参考
[docker 入门]http://shouce.jb51.net/docker_practice/

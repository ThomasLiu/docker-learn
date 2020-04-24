# docker-learn

docker learn code

常用命令, [Docker 命令大全](https://www.runoob.com/docker/docker-command-manual.html)

```sh
docker pull NAME # 获取一个在在 docker hub 上的镜像
docker images # 查看镜像
docker image prune # 删除 <none> 的镜像
docker inspect NAME|ID # 获取容器/镜像的元数据

docker build -t image_test . # 使用当前目录的 docker 文件构建 TAG 为 image_test 的镜像

docker run --name test -p 8080:80 -d image_test # 基于 image_test 镜像 生成一个容器名字为 test，把里面的80端口映射到 8080，加了 -d 参数默认不会进入容器

docker run -it -d mysql:5.7 /bin/bash # 生成容器 基于 mysql:5.7 镜像，在控制台上操作

docker ps -a # 查看所有的容器
docker ps # 查看在运行的容器

docker start NAME|ID # 通过 docker ps -a 查到的容器，根据里面的 NAME|ID 启动 对应的容器
docker restart NAME|ID # 重启在运行的容器

docker attach --sig-proxy=false NAME|ID # 链接到正在运行的容器，监控其日志， --sig-proxy=false 参数让 退出容器终端时，不会导致容器的停止，attach 默认退出退出容器终端时容器也会停止
docker logs -f NAME|ID # 查看该容器的终端输出历史，-f: 让 docker logs 像使用 tail -f 一样来输出容器内部的标准输出

docker container prune # 清理掉所有处于终止状态的容器

```

## Docker 实践尝试

参考资料

- [Docker + Jenkins 部署完整 node 项目](https://segmentfault.com/a/1190000021462867?utm_source=tag-newest)

## 团队化 Docker 开发

参考资料

- [用 Docker 快速配置前端开发环境](http://dockone.io/article/1714)

## Docker 构建优化

### 分析构建过程

查看 commit msg 可以了解整个镜像体积优化过程

参考资料

- [Nodejs Docker 镜像体积优化实践](https://blog.csdn.net/weixin_33735077/article/details/91372328)

### 分析构建过程

计算 dockerfile 每一条 instruction 的耗时

```sh
# 1. 开启这个实验性 flag
export DOCKER_BUILDKIT=1

# 2. 添加参数 --progress plain 获得更加直观的输出结果
docker build -t YOUR_IMAGE_NAME:YOUR_TAG -f YOUR_DOCKERFILE --progress plain .
```

找出是哪些部分最占空间

```sh
# 忽略一些 du 的错误
docker run -it YOUR_IMAGE_NAME:YOUR_TAG du -sh /* 2>&1 | grep -v "cannot access"

# 查看某个具体文件夹
docker run -it YOUR_IMAGE_NAME:YOUR_TAG du -sh /usr/* | grep -v "cannot access"
```

参考资料

- [Node.js docker 优化实践](https://zhuanlan.zhihu.com/p/83793004)

### 生产环境高效构建

- [使用 Docker 高效部署前端应用](http://dockone.io/article/9879)
- [Dockerfile 最佳实践](http://dockone.io/article/9658)

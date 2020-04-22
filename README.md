# docker-learn

docker learn code

常用命令, [Docker 命令大全](https://www.runoob.com/docker/docker-command-manual.html)

```sh
docker images # 查看镜像
docker image prune # 删除 <none> 的镜像
docker inspect NAME|ID # 获取容器/镜像的元数据

docker build -t image_test . # 使用当前目录的 docker 文件构建 TAG 为 image_test 的镜像
```

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
docker run -it 2719554387f3 du -sh /* 2>&1 | grep -v "cannot access"
```

参考资料

- [Node.js docker 优化实践](https://zhuanlan.zhihu.com/p/83793004)

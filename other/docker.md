# Docker 简单使用方式

## 参考文章

- [Get Started](https://docs.docker.com/docker-for-mac/#explore-the-application)
- [Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)

## 安装与验证 (MAC)

1. 下载安装
2. 运行程序 docker
3. 运行 `docker --version`, `docker-compose --version`, `docker-machine --version`
   这三个命令验证安装.
3. 运行 `docker run -d -p 80:80 --name webserver nginx` 启动一个 nginx 的镜像. 第一次
   应该需要下载. 启动完成后, 使用浏览器访问 http://localhost:80 查看访问是否成功.

## 关键概念

- **container**: 一个运行环境.

- **image**: Docker 会把程序及其依赖关系打包成一个 image, 是用于创建 container 的模板.

## 常用命令

### Container 相关
- `docker container ls` / `docker ps`: 列出运行中的 container.

  -a 可以列出不是处于运行中 container

- `docker container stop xxx` 停止运行中的 container.

## 常见问题
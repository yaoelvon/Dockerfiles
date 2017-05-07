# hexo
增、删、改、移动hexo博客文件后，本地自动编译部署+自动更新到github

## 可用镜像(hub.docker.com)
```
基础镜像：fengyao/hexo:base
可用镜像：fengyao/hexo:release-v0.05.0601
```

## 文件说明
```
Dockerfile.base    用于构建基础镜像
Dockerfile         用于构建安装hexo相关库，生成可用镜像
docker-compose.yml 编排脚本，用于一次运行nginx容器和hexo自动部署容器
monitor.sh         监控脚本，用于检测文件异动，自动进行hexo编译和部署，并提交到github
```

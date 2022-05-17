# Reader入门之快速搭建

> [Reader](https://github.com/hectorqin/reader)是我从2021年8月开始开发的**开源阅读**服务器版，至今发布了79个小版本，目前主要功能基本开发完毕，大家可以放心使用。

## 主要功能

- 自定义书源，支持导入**开源阅读**的大部分书源，支持本地和远程导入书源。
- 支持书源搜索及发现，找书更方便。
- 支持**开源阅读**的订阅源，可以看你想看的内容。
- 支持导入本地TXT、EPUB阅读。
- 支持**本地书仓**功能，一键导入本地所有书籍。
- 阅读界面支持高度自定义，切换字体、颜色、背景、行距、段距、加粗等，支持
  上下、左右翻页模式。
- 适配电脑端、手机端，真正实现**多端阅读**。
- 支持与**开源阅读**通过Webdav同步阅读进度。
- 支持替换净化，支持**听书**功能，支持定时拉取书籍更新。

> 注意，**听书**功能需要浏览器支持。

## 使用云服务器/NAS等硬件搭建

> 需要云服务器/nas等支持运行docker的硬件

### Docker-Compose 部署

官方 [Github](https://github.com/hectorqin/reader) 仓库里面提供了 docker-compose 的配置文件 `docker-compose.yaml`，只需要根据个人需求修改少许配置，即可以快速部署，还自带自动更新功能。

安装步骤：

```bash
# 安装docker，已安装请跳过
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

#安装docker-compose，已安装请跳过
#Debian/Ubuntu
apt install docker-compose -y

#CentOS
# 安装dcoker-compose
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# 查看 docker-compose 版本
docker-compose --version

# 创建目录
mkdir -p /home/reader/logs /home/reader/storage
cd /home/reader

# 下载默认书源，可选
mkdir -p /home/reader/storage/data/default/
wget -c https://namofree.gitee.io/yuedu3/legado3_booksource_by_Namo.json -O /home/reader/storage/data/default/bookSource.json

# 下载项目里的 docker-compose.yaml
wget https://raw.githubusercontent.com/hectorqin/reader/master/docker-compose.yaml

# 根据 docker-compose.yaml 里面的注释编辑所需配置
# 启动 docker-compose
docker-compose up -d

# 停止 docker-compose
docker-compose stop
```

### Docker直接运行

直接使用**Docker**运行

```bash
# 安装docker，已安装请跳过
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# 创建目录
mkdir -p /home/reader/logs /home/reader/storage
cd /home/reader

# 下载默认书源，可选
mkdir -p /home/reader/storage/data/default/
wget -c https://namofree.gitee.io/yuedu3/legado3_booksource_by_Namo.json -O /home/reader/storage/data/default/bookSource.json

# 运行
# arm64架构、内存小的机器可以用 hectorqin/reader:openj9-latest 镜像，直接用 hectorqin/reader:openj9-latest  替换下面命令中的 hectorqin/reader 即可
# 单用户版
#docker run -d --restart=always --name=reader -e "SPRING_PROFILES_ACTIVE=prod" -e "READER_APP_CACHECHAPTERCONTENT=true" -v $(pwd)/logs:/logs -v $(pwd)/storage:/storage -p 8080:8080 hectorqin/reader

# 多用户版
#docker run -d --restart=always --name=reader -e "SPRING_PROFILES_ACTIVE=prod" -e "READER_APP_SECURE=true" -e "READER_APP_CACHECHAPTERCONTENT=true" -e "READER_APP_SECUREKEY=管理密码" -e "READER_APP_INVITECODE=注册邀请码" -v $(pwd)/logs:/logs -v $(pwd)/storage:/storage -p 8080:8080 hectorqin/reader
```

### Java环境直接运行

需要先配置 **jdk8** 的JAVA环境

> 不推荐，更新比较慢

```
# 安装 JAVA8，安装步骤此处省略
# 配置 JAVA_HOME 、PATH 等环境变量

# 创建目录
mkdir -p /home/reader/logs /home/reader/storage
cd /home/reader

# 下载默认书源，可选
mkdir -p /home/reader/storage/data/default/
wget -c https://namofree.gitee.io/yuedu3/legado3_booksource_by_Namo.json -O /home/reader/storage/data/default/bookSource.json

# 下载 jar 软件包，去 Github 找到最新下载链接
wget https://github.com/hectorqin/reader/releases/download/v2.0.3/reader-2.0.0.jar -O reader.jar

# 运行
# 单用户
java -jar reader.jar --reader.server.port=8080 --spring.profiles.active=prod --reader.app.cacheChapterContent=true --reader.app.userLimit=50 --reader.app.userBookLimit=200
# 多用户
java -jar reader.jar --reader.server.port=8080 --spring.profiles.active=prod --reader.app.cacheChapterContent=true --reader.app.userLimit=50 --reader.app.userBookLimit=200 --reader.app.secure=true --reader.app.secureKey=管理密码 --reader.app.inviteCode=注册邀请码
```

### 群晖 Docker 运行

参考网友`悬崖上的剁椒鱼头`的教程： [你学废了吗 篇十二：Docker部署最强开源阅读app-多用户版（覆盖全设备使用）](https://post.smzdm.com/p/ar6xm99z/)

## 使用免费云部署平台搭建

> 国外的 Koyeb、Railway 等免费服务受网络影响较大，比较慢

参考公众号`阿虚同学`的教程： [这款最强网文神器竟然出网页版了！！5分钟教你完全免费搭建一个](https://mp.weixin.qq.com/s?__biz=MzA5NjEwNjE0OQ==&mid=2247507645&idx=1&sn=85dedac002e13ebd94fd1398dc8810c9&chksm=90b7bd77a7c034615c122bc295266c2c4ab2ff1aaf9c3f9a385b382e0f5a82a967cb26cdfa19&scene=178&cur_album_id=1523717901302710273#rd)

## 桌面端

> 需要安装 JAVA8 环境，并配置好环境变量

从官方 [Github](https://github.com/hectorqin/reader/releases) 仓库下载最新的版本，安装使用即可。

## 使用

通过上面的几种方法成功运行后，用浏览器打开 `http://IP:端口/` 即可访问 **Web** 书架，随时随地的看你想看了 😊

#### 更多使用教程，陆续更新中

- WebDAV 怎么同步？
- 本地书仓怎么使用？
- 书源怎么导入和失效检测？
- 阅读界面怎么自定义？

#### 推荐阅读

- [你学废了吗 篇十二：Docker部署最强开源阅读app-多用户版（覆盖全设备使用）](https://post.smzdm.com/p/ar6xm99z/)
-  [这款最强网文神器竟然出网页版了！！5分钟教你完全免费搭建一个](https://mp.weixin.qq.com/s?__biz=MzA5NjEwNjE0OQ==&mid=2247507645&idx=1&sn=85dedac002e13ebd94fd1398dc8810c9&chksm=90b7bd77a7c034615c122bc295266c2c4ab2ff1aaf9c3f9a385b382e0f5a82a967cb26cdfa19&scene=178&cur_album_id=1523717901302710273#rd)

---

欢迎关注我的公众号“**假装大佬**”，原创技术文章第一时间推送。

<center>
    <img src="https://cdn.jsdelivr.net/gh/filess/img18@main/2022/05/14/1652503172603-2ab0ce52-181c-4878-8739-676bd9177791.jpg" style="width: 125px;">
</center>
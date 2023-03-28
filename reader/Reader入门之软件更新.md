# Reader入门之软件更新

**Reader** 已经更新到 `v2.7.2` 了，还没有更新的粉丝可以按照下面的教程更新一波。

## 使用云服务器/NAS等硬件搭建

### Docker-Compose 部署

官方提供的 `docker-compose.yaml`  文件自带了 `watchtower` 的自动更新，如果不是用的官方配置，可以参考官方的配置文件进行修改，再重新运行即可。官方配置文件链接 [https://raw.githubusercontent.com/hectorqin/reader/master/docker-compose.yaml](https://raw.githubusercontent.com/hectorqin/reader/master/docker-compose.yaml)

### Docker 直接运行

**Docker** 直接运行的软件需要先更新镜像。

```bash
# arm64架构、内存小的机器可以用 hectorqin/reader:openj9-latest 镜像，直接用 hectorqin/reader:openj9-latest  替换下面命令中的 hectorqin/reader 即可
docker pull hectorqin/reader

# 停止原来的容器，reader 是容器名
docker stop reader

# 删除原来的容器
docker rm reader

# 重新运行新的镜像
# 单用户版
# docker run -d --restart=always --name=reader -e "SPRING_PROFILES_ACTIVE=prod" -e "READER_APP_CACHECHAPTERCONTENT=true" -v $(pwd)/logs:/logs -v $(pwd)/storage:/storage -p 8080:8080 hectorqin/reader

# 多用户版
docker run -d --restart=always --name=reader -e "SPRING_PROFILES_ACTIVE=prod" -e "READER_APP_SECURE=true" -e "READER_APP_CACHECHAPTERCONTENT=true" -e "READER_APP_SECUREKEY=管理密码" -e "READER_APP_INVITECODE=注册邀请码" -v $(pwd)/logs:/logs -v $(pwd)/storage:/storage -p 8080:8080 hectorqin/reader
```

### Java环境直接运行

只需要下载最新的 jar 文件，重命名为 `reader.jar`，替换旧文件，然后重新运行 jar 即可。

```bash
# 停止旧服务
ps -ef | grep 'reader' | grep 'java' | grep -v grep |awk '{print $2}'| xargs kill -9 2>&1

# 运行
# 单用户
#java -jar reader.jar --reader.server.port=8080 --spring.profiles.active=prod --reader.app.cacheChapterContent=true --reader.app.userLimit=50 --reader.app.userBookLimit=200

# 多用户
java -jar reader.jar --reader.server.port=8080 --spring.profiles.active=prod --reader.app.cacheChapterContent=true --reader.app.userLimit=50 --reader.app.userBookLimit=200 --reader.app.secure=true --reader.app.secureKey=管理密码 --reader.app.inviteCode=注册邀请码
```

### 群晖 Docker 运行

参考网友`北京-狗子`的教程： [如何优雅的使用一条命令更新群晖docker容器-Watchtower教程](https://post.smzdm.com/p/awzggnqp/)

## 使用免费云部署平台搭建

`Railway` ，`Koyeb`，`replit.com` 等免费云部署平台一般是使用你 fork 的 `Reader` 仓库的源码进行部署的，所以要更新 `Reader`，只需要去 `Github` 上面更新你 fork 的 `Reader` 仓库即可。

直达链接 `https://github.com/你的用户名/你的仓库名/compare/master...hectorqin:reader:master`，打开这个链接后，确认一下前面的仓库是你 fork 的自己的仓库，后面是官方仓库

![提交PR](https://fastly.jsdelivr.net/gh/filess/img7@main/2022/10/30/1667096851801-7a797a26-985d-4832-be78-81ade70fec0f.png)

再点击右边的 `Create pull request`，进入下面的界面，随便写个标题，再次点击下面的 `Create pull request`，这样就成功提交了合并请求。

![创建PR](https://fastly.jsdelivr.net/gh/filess/img0@main/2022/10/30/1667099600054-de20cbc0-2cb1-410f-8c93-8a4049c8a1a3.png)

再点击下面的 `Merge pull request` 进行合并，这样就更新了你的 fock 仓库，云部署平台应该就会自动部署更新了。

![合并PR](https://fastly.jsdelivr.net/gh/filess/img6@main/2022/10/30/1667099633373-13b4608a-ac6b-489f-a381-21694571bed8.png)


## 桌面端



直接下载新版本，覆盖安装即可。


#### 更多使用教程，陆续更新中

- [怎么快速搭建 Reader？](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483670&idx=1&sn=5a1399ad4a98177a365aa8f8aee8e6a7)
- [WebDAV 怎么同步？](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483683&idx=1&sn=0f9bb1b0c84d94c9d7bd11995c031012)
- [Reader 常见问题](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483689&idx=1&sn=dc193cccb4461f678f44d7d6a5461bea)
- [本地书仓怎么使用？](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483698&idx=1&sn=70a7e2aa151109d7d994d447e0e94d6e)
- 书源怎么导入和失效检测？
- 阅读界面怎么自定义？

---

欢迎关注我的公众号“**假装大佬**”，原创技术文章第一时间推送。

<center>
    <img src="https://cdn.jsdelivr.net/gh/filess/img18@main/2022/05/14/1652503172603-2ab0ce52-181c-4878-8739-676bd9177791.jpg" style="width: 125px;">
</center>
# Reader入门之常见问题

## 搭建相关

1.railway 部署后，怎么更新？

- 从官方仓库拉取更新，合并到自己仓库的 master 分支，然后去 railway 重新部署

> 请注意，有书友反馈 railway 不能设置挂载磁盘，因此更新后所有数据都会丢失，请谨慎使用。建议更新之前，先去保存一下 WebDAV 备份，然后下载备份文件到本地，然后再更新，更新之后再上传备份文件恢复。PS: 备份恢复的功能暂时未完善，下一版会实现Web页面下载上传 WebDAV 备份文件。

2.N1 等 arm64 设备使用 `hectorqin/reader:lastest` 镜像报错

- arm64 镜像请使用官方提供的 `openj9-latest` 镜像。

> 官方提供的镜像有两种，一种是不带 openj9 标签的，镜像基于Alpine，占用空间较小，但是占用内存较多，而且不支持 arm64；另一种是带 openj9 标签的，镜像基于 Ubuntu，占用空间较大，但是占用内存较小，支持 arm64。

## 书源相关

1.为什么第一次安装好之后什么东西都没有？

- Reader和开源阅读一样只是一个转码工具，不提供内容，第一次安装好后，需要自己手动导入书源，可以从公众号 [假装大佬]、TG群等地方获取由书友制作分享的书源。

2.第一次导入书源后，搜书提示未配置书源？

- Web页面可能有bug，导入书源后请重新选择搜索分组进行搜索。

3.导入书源报错，怎么排查问题？

- 如果是本地书源文件，请检查书源文件格式，必须是JSON数组格式
- 如果是远程书源文件，请下载下来后重试，如果还出错，请检查书源文件格式，必须是JSON数组格式

4.不同设备打开书架，书源、RSS源、书籍分组、替换规则等不是最新的怎么办？

- Web页面会缓存一些书源、RSS源、书籍分组、替换规则等变化较小的数据，以加快页面访问速度。因此，不同设备访问可能会出现数据不同步的情况，这时只需要注销登录后再重新登录就行了。

> 如果只需要更新本地缓存的书源，可以点击 书源管理 - 缓存书源

## 书架相关

1.书籍封面显示空白，既不是默认封面，也不是加载出错

- 新版本应该已经修复了此问题。封面图片做了懒加载，尝试滚动一下书籍列表看看。

2.怎么修改书籍分组？

- 点击书籍封面，在弹出的书籍信息窗口设置分组。

3.怎么自定义书籍封面？

- 点击书籍封面，在弹出的书籍信息窗口，点击封面图片，上传自定义封面。

4.怎么删除书架书籍？

- 点击 编辑 按钮，再点击书籍旁边的 x。

5.如何禁止或允许某本书更新？

- 点击书籍封面，在弹出的书籍信息窗口设置是否追更。

## 阅读相关

1.正常模式 和 Kindle 模式有什么区别？

- 正常模式会打开书架页面的侧边栏、书海、RSS等功能。
- Kindle 模式会关闭翻页动画，修改背景图片，关闭书架页面的侧边栏、书海、RSS等功能，从而节省内存。

> Kindle 模式只是一个尝试，实际上 Kindle 也不兼容 Reader 的 web页面

2.怎么缓存章节？

- 阅读界面，点击阅读进度百分比，会显示缓存选项。

3.怎么修改 TTS ?

- 暂时只支持浏览器内置的 TTS 语音，可以横向滚动来选择内置的 TTS，不支持自定义。

4.iOS 怎么修改字体？

- iOS 浏览器没有内置楷体、宋体等这些字体，所以修改字体是无效的，以后可能会支持加载远程字体文件。

5.阅读界面怎么加入书架？

- 点击屏幕中间，唤出菜单栏，点击左边的 i 图标，弹出书籍信息界面，在界面点击加入书架。

## 本地书籍相关

1.导入 TXT 文件提示 “LoadTocError” 或 “List is empty” 是怎么回事？

- 导入预览界面，切换章节解析规则，刷新目录。

2.导入预览界面对部分把正文（如所有含引号的句子）识别成章节，如何解决？

- 导入预览界面，切换章节解析规则，刷新目录。

3.导入 Epub 文件提示 “Chapterlist is empty” 是怎么回事？

- 导入的 Epub 文件不规范，以后有时间会加强 Epub 解析逻辑。

4.导入的 TXT 文件章节内容显示乱码是怎么回事？

- 部分编码在阅读上会识别错误，建议先用文本编辑器转换为常用的UTF-8格式。

## WebDAV 相关

1.WebDAV 用浏览器打开返回 401

- WebDAV 服务是不支持浏览器直接访问的，需要直接去阅读App配置。

#### 更多使用教程，陆续更新中

- [怎么快速搭建 Reader？](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483670&idx=1&sn=5a1399ad4a98177a365aa8f8aee8e6a7)
- [WebDAV 怎么同步？](https://mp.weixin.qq.com/s?__biz=MjM5MzMyMDgyMA==&mid=2249483683&idx=1&sn=0f9bb1b0c84d94c9d7bd11995c031012)
- 本地书仓怎么使用？
- 书源怎么导入和失效检测？
- 阅读界面怎么自定义？

---

欢迎关注我的公众号“**假装大佬**”，原创技术文章第一时间推送。

<center>
    <img src="https://cdn.jsdelivr.net/gh/filess/img18@main/2022/05/14/1652503172603-2ab0ce52-181c-4878-8739-676bd9177791.jpg" style="width: 125px;">
</center>
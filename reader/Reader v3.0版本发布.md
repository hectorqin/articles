# Reader v3 版本发布

`v3`版本主打功能是 `kindle` 端，经过几个小版本的迭代，`kindle` 端终于可以正常使用了，当然免不了还有很多bug，大家可以积极去 `github` 上提 issue 反馈。

## 新增功能

`v3` 版本相对于 `v2` 版本增加了以下功能：

- 新增epub iframe模式自定义字体支持
- 新增simple-web端，支持kindle使用（限时免费到 2023-04-15，后续新版本可能会继续延长限免时间）
- 新增授权管理，多用户版用户上限降低至 15（已超出的无法再注册，但可以继续使用）
- 新增用户管理、书籍管理、书签管理等分页排序过滤功能
- 新增书源请求头设置
- 新增书籍批量缓存操作
- 新增contextPath设置项，可设置子目录访问reader
- 新增书架搜索作者及分类
- 新增书架布局设置，新增分列布局
- 修改书籍分组的字段类型，支持更多分组
- 新增用户更多设置项，如书籍上限、书源上限、是否可以编辑书源等
- 新增pdf格式的支持

## 最新接口配置

```yml
reader:
  app:
    workDir: ""            # 工作目录
    showUI: false          # 是否显示UI
    debug: false           # 是否调试模式
    packaged: false        # 是否打包为客户端
    secure: false          # 是否需要登录鉴权，开启后将支持多用户模式
    inviteCode: ""         # 注册邀请码，为空时则开放注册，否则注册时需要输入邀请码
    secureKey: ""          # 管理密码，开启鉴权时，前端管理用户空间的管理密码
    proxy: false           # 是否使用代理
    proxyType: "HTTP"      # 代理类型
    proxyHost: ""          # 代理 Host
    proxyPort: ""          # 代理 port
    proxyUsername: ""      # 代理鉴权 用户名
    proxyPassword: ""      # 代理鉴权 密码
    cacheChapterContent: false # 是否缓存章节内容
    userLimit: 50          # 用户上限，最大 50
    userBookLimit: 200     # 用户书籍上限，默认最大 200
    debugLog: false        # 是否打开调试日志
    autoClearInactiveUser: 0 # 是否自动清理不活跃用户，为0不清理，大于0为清理超过 autoClearInactiveUser 天未登录的用户
    mongoUri: ""           # mongodb uri 用于备份数据
    mongoDbName: "reader"  # mongodb 数据库名称
    shelfUpdateInteval: 10 # 书架自动更新间隔时间，单位分钟，必须是10的倍数
    remoteWebviewApi: ""   # 远程webview的接口地址
    defaultUserEnableWebdav: true       # 新用户默认是否启用webdav
    defaultUserEnableLocalStore: true   # 新用户默认是否启用localStore
    defaultUserEnableBookSource: true   # 新用户默认是否启用书源编辑
    defaultUserEnableRssSource: true    # 新用户默认是否启用RSS源编辑
    defaultUserBookSourceLimit: 100     # 新用户默认书源数量上限
    defaultUserBookLimit: 200           # 新用户默认书籍数量上限

  server:
    port: 8080             # 监听端口
    contextPath: ""        # 子目录路径
    webUrl: http://localhost:${reader.server.port}    # web链接

```

## 关于授权

`v3` 版本进一步限制了多用户版本的用户数量上限，主要是出于保护这个项目的考虑。另外授权功能是为接下来新增的付费功能（如kindle端、增加用户数上限等）做准备的，但是目前还不太完善，所以暂时还没法支持获取授权。

欢迎关注我的公众号“**假装大佬**”，原创技术文章第一时间推送。

<center>
    <img src="https://cdn.jsdelivr.net/gh/filess/img18@main/2022/05/14/1652503172603-2ab0ce52-181c-4878-8739-676bd9177791.jpg" style="width: 125px;">
</center>
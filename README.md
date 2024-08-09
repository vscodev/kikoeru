# Kikoeru

[![dockeri.co](https://dockerico.blankenship.io/image/vscodev/kikoeru)](https://hub.docker.com/r/vscodev/kikoeru)

*一个自托管的 DLsite 音声作品整理和媒体播放软件, 使用 Go 和 Vue.js。*

## 推广

如果你希望将 Kikoeru 部署在VPS上，推荐使用轻量应用服务器，性价比更高。

- [阿里云轻量应用服务器](https://www.aliyun.com/product/swas?source=5176.11533457&userCode=6lssewap)
- [腾讯云轻量应用服务器](https://curl.qcloud.com/UiP0o3BV)

## 功能

- 自动从 DLsite 爬取作品元数据，支持所有作品类型（RJ/BJ/VJ），包括已下架的作品。
- 支持多种存储，你可以从本机存储、阿里云盘、百度网盘以及 OneDrive 中刮削作品资源。
- 强大的个性化搜索功能，支持多关键字、多标签检索，支持对搜索结果二级筛选过滤。
- 支持多种格式的字幕显示，`.lrc` 、`.srt` 、`.vtt` 以及 `.ass` ，支持字幕偏移。

## 预览

![home](assets/home.png)

![works](assets/works.png)

![work](assets/work.png)

![histories](assets/histories.png)

## 安装

创建一个工作目录，例如 `kikoeru` 。

```sh
mkdir kikoeru
cd kikoeru
```

拉取 Kikoeru 镜像，创建容器并运行。

```sh
docker run -d --name kikoeru -p 2333:2333 -v $PWD/data:/opt/kikoeru/data -e TZ=Asia/Shanghai -e PUID=$(id -u) -e PGID=$(id -g) -e UMASK=022 --restart unless-stopped vscodev/kikoeru:latest
```

首次运行 Kikoeru 会自动创建管理员帐号，你可通过 `docker logs` 命令查看。

```sh
docker logs kikoeru
```

忘记密码可通过 `kikoeru admin` 命令重置。

```sh
docker exec -it kikoeru ./kikoeru admin
```

## 添加存储

Kikoeru 支持添加多种存储，配置填写可参考 [Alist](https://alist.nn.ci/zh/guide/) 。

## 导入作品

每个作品对应一个目录，且文件夹名称必须包含一个有效的作品ID，示例：

```
RJ334212
[みやぢ屋][RJ334212]ガチ恋不可避の耳リフレ2~ぼくっこ店員ゆずるの出張サービス~
```

点击「扫描」按钮 Kikoeru 会在后台扫描相应存储的的作品资源，自动从 DLsite 爬取作品元数据并导入到媒体库。

**不要包含重复的作品，否则会被覆盖，而且顺序是不确定的。**

## 反向代理

你需要在 NGINX 网站配置文件的 `server` 字段中添加

```
location / {
    proxy_pass         http://127.0.0.1:2333;
    proxy_http_version 1.1;
    proxy_cache_bypass $http_upgrade;

    # Proxy SSL
    proxy_ssl_server_name on;

    # Proxy headers
    proxy_set_header Host              $host;
    proxy_set_header Upgrade           $http_upgrade;
    proxy_set_header Connection        $connection_upgrade;
    proxy_set_header X-Real-IP         $remote_addr;
    proxy_set_header Forwarded         $proxy_add_forwarded;
    proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-Host  $host;
    proxy_set_header X-Forwarded-Port  $server_port;
    proxy_set_header Range             $http_range;
    proxy_set_header If-Range          $http_if_range;

    # Proxy timeouts
    proxy_connect_timeout              60s;
    proxy_send_timeout                 60s;
    proxy_read_timeout                 60s;
}
```

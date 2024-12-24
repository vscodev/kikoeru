# Kikoeru

一个自托管的DLsite音声作品整理和媒体播放软件，为你提供极致的音声视听体验。

![screenshot](screenshot.png)

## 功能

- 自动从DLsite爬取作品元数据，支持所有作品类型（RJ/BJ/VJ），包括已下架的作品。
- 支持多种存储，你可以通过本地、网盘、WebDAV甚至AList导入作品资源。
- 强大的个性化搜索功能，支持多关键字、多标签检索，支持对搜索结果二级筛选过滤。
- 支持多种格式的字幕显示，`.lrc` 、`.srt` 、`.vtt` 以及 `.ass` ，支持字幕偏移。

## 安装

创建一个工作目录，例如 `kikoeru` 。

```sh
mkdir kikoeru
cd kikoeru
```

拉取Kikoeru镜像，创建容器并运行。

```sh
docker run -d --name kikoeru -p 2333:2333 -v $PWD/data:/opt/kikoeru/data -e TZ=Asia/Shanghai -e PUID=$(id -u) -e PGID=$(id -g) -e UMASK=022 --restart unless-stopped ghcr.io/vscodev/kikoeru:latest
```

首次运行Kikoeru会自动创建管理员帐号，你可通过 `docker logs` 命令查看。

```sh
docker logs kikoeru
```

忘记密码可通过 `kikoeru admin` 命令重置。

```sh
docker exec -it kikoeru ./kikoeru admin
```

## 导入作品

Kikoeru支持从以下存储驱动导入作品资源，配置填写可参考 [AList](https://alist.nn.ci/zh/guide/) 。

- [x] 本机存储
- [x] [阿里云盘](https://www.alipan.com)
- [x] [百度网盘](https://pan.baidu.com)
- [x] [OneDrive](https://onedrive.live.com)
- [x] WebDAV
- [x] [AList](https://github.com/AlistGo/alist)

> [!TIP]
> WebDAV驱动仅建议在上游原生支持WebDAV协议的情况下使用，AList用户请直接使用AList驱动。

每个作品对应一个目录，且文件夹名称必须包含一个有效的作品ID，示例：

```
RJ334212
[みやぢ屋][RJ334212]ガチ恋不可避の耳リフレ2~ぼくっこ店員ゆずるの出張サービス~
```

> [!CAUTION]
> 不要包含重复的作品，否则会被覆盖，而且顺序是不确定的。

## 反向代理

你需要在NGINX网站配置文件的 `server` 字段中添加

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

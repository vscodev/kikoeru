<div align="center">
  <h1>Kikoeru</h2>
  <p><em>Self-hosted DLsite works database</em></p>
<div>
  <a href="https://github.com/vscodev/kikoeru/actions">
    <img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/vscodev/kikoeru/windows-release.yml">
  </a>
  <a href="https://github.com/vscodev/kikoeru/releases">
    <img alt="GitHub release" src="https://img.shields.io/github/v/release/vscodev/kikoeru">
  </a>
  <a href="https://hub.docker.com/r/vscodev/kikoeru">
    <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/vscodev/kikoeru?color=%2348BB78&logo=docker&label=pulls">
  </a>
</div>
</div>

## Preview

![home](assets/home.png)

![works](assets/works.png)

![work](assets/work.png)

## Usages

```
Self-hosted DLsite works database

Usage:
  kikoeru [command]

Available Commands:
  clean       Clean works metadata
  completion  Generate the autocompletion script for the specified shell
  help        Help about any command
  refresh     Refresh works metadata
  start       Start the server
  sync        Sync works metadata

Flags:
      --debug          debug mode
  -h, --help           help for kikoeru
  -x, --proxy string   use the specified proxy

Use "kikoeru [command] --help" for more information about a command.
```

https://github.com/vscodev/kikoeru/assets/71597201/d1f2134a-3651-4f44-b868-9c79466639e0

Change the current directory to `kikoeru` and create a new folder named `media` .

```bash
cd /path/to/kikoeru
mkdir media
```

Put your works in the `media` folder, one work, one directory, and the directory name must contain a valid work id. For examples:

```
media/RJ395908
media/Miyadi/[みやぢ屋][RJ334212]ガチ恋不可避の耳リフレ2
media/音撫屋/RJ203751
```

### Sync works metadata

```bash
./kikoeru sync
```

Kikoeru will automatically scan the media library and crawl works metadata from DLsite.

**Note:** If you have trouble connecting to DLsite, please use proxies through kikoeru's `-x` or `--proxy` flag. For examples:

```
./kikoeru sync -x socks5://127.0.0.1:7890
```

### Start the server

```bash
./kikoeru start
```

Visit `http://localhost:2333` through your browser, enjoy~

## Thanks

The project is inspired by [kikoeru-express](https://github.com/kikoeru-project/kikoeru-express) , developed with Go, TypeScript and Vue 3.

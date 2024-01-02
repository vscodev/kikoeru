<div align="center">
  <h1>Kikoeru</h2>
  <p><em>Self-hosted DLsite works database</em></p>
<div>
  <a href="https://github.com/vscodev/kikoeru/blob/main/LICENSE">
    <img alt="License" src="https://img.shields.io/github/license/vscodev/kikoeru">
  </a>
  <a href="https://github.com/vscodev/kikoeru/actions">
    <img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/vscodev/kikoeru/docker-image.yml">
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

![genres](assets/genres.png)

![work](assets/work.png)

![subtitle](assets/subtitle.png)

![artists](assets/artists.png)

![dark](assets/dark.png)

## Usages

**[白话版搭建指南](https://afdian.net/p/4c16ae9c8b1d11ee8ed35254001e7c00)**

```
Self-hosted DLsite works database

Usage:
  kikoeru [command]

Available Commands:
  cleanup     Cleanup works metadata
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

Change the current directory to `kikoeru` :

```bash
cd /path/to/kikoeru
```

### Initialize

Execute the following command:

```bash
./kikoeru start
```

When you see `http server started on [::]:2333` in the terminal, everything works well, just press <kbd>Ctrl</kbd> + <kbd>C</kbd> to stop it.

### Sync works metadata

Put your works in the `media` folder, one work, one directory, and the directory name must fully matches the work id.

**Good:** `RJ334212`

**Bad:** `Rj334212` `rj334212` `334212`

Then execute the following command:

```bash
./kikoeru sync
```

### Start the server

```bash
./kikoeru start
```

Yes, it's the same as the initialize command.


# 贡献指南

[简体中文](CONTRIBUTING.md) | [English](CONTRIBUTING.en-US.md)

所有插件的配置文件都应当存放在 `channels` 目录中。每个插件的名称都以小写存放在对应的目录中。比如，ViaVersion 插件的配置需要存放在 `channels/viaversion` 目录。

配置目录必须具有 `index.json`，这是 UPU 首先会请求的文件。如果此文件不存在，那么 UPU 会放弃请求。这一机制也可以用于草稿，如果配置还没准备好，可以暂时不添加这个文件。

`index.json` 的结构如下：
```json
{
    "name": "<PluginId>",
    "platform":{
        "universal": "universal.json",
        "bukkit": "bukkit.json",
        "velocity": "velocity.json"
    }
}
```

`name` 字段代表插件的正式名称，如“ViaVersion”，`platform` 中每个成员名对应一个平台，特别的，`universal` 对应通用的配置，不区分平台。值指定为当前目录下的文件名，如 ViaVersion 插件的 `universal.json` 配置代表 `channels/viaversion/universal.json` 文件。

UPU 会首先查找当前平台的配置，如果没有找到，则回退 `universal` 配置，如果也没有找到，则放弃请求。

`universal.json` 的结构在[文档](https://docs.upu.dreamvoid.me/core/config/channel.json)中有详细解释，不过，位于仓库的配置文件中不应当存在有效的 `selectedChannel` 字段（可以设置为 null 方便用户快速设置）。此外，仓库中的配置还存在一个 `last_update` 字段，这个字段是一个 `long` 类型的数字，用于检查本地文件是否过期，需要更新配置。这个字段虽然可以设置为任意长整数，但最佳做法是设置为当前日期，便于更新。

## 更新渠道要求

若要将你的配置贡献给 UPU 官方仓库，需要遵循以下几点要求：

* 仅当没有其他渠道可用时，才允许使用 `SpigotMC` 渠道。
  * 由于 SpigotMC 极其特殊，UPU 使用 [Spiget](https://spiget.org/) 获取 SpigotMC 资源信息，为了防止滥用，我们要求在其他渠道可用的情况下尽可能减少 Spiget 的负担。
* 除非你是插件开发者/取得了插件开发者的授权，否则不允许添加类型为 `url` 的更新渠道。
  * 这是为了避免给其他插件开发者造成不必要的困扰。
* 渠道配置文件中 `selectedChannel` 不得存在非 `null` 的默认值。
* 除非有合适的理由，否则更新渠道配置必须包含 `universal.json`，包括那些仅在部分平台推出的插件。

确保符合要求后，通过 GitHub 的 Pull Request 功能创建一个拉取请求，在我们确认你的配置无误后就会合并到仓库，供所有 UPU 的使用者下载。
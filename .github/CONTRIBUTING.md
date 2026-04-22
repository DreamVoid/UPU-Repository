# 贡献指南

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
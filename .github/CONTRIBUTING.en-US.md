# Contribution Guidelines

[简体中文](CONTRIBUTING.md) | [English](CONTRIBUTING.en-US.md)

All plugin configuration files should be stored in the `channels` directory. Each plugin name should be stored in its corresponding directory, in lowercase. For example, the ViaVersion plugin configuration should be stored in the `channels/viaversion` directory.

The configuration directory must contain an `index.json` file, which is the first file UPU will request. If this file does not exist, UPU will abandon the request. This mechanism can also be used for drafts; if the configuration is not yet ready, this file can be omitted temporarily.

The structure of `index.json` is as follows:
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

The `name` field represents the plugin's official name, such as "ViaVersion". Each member name in `platform` corresponds to a platform. Specifically, `universal` corresponds to a universal configuration, not platform-specific. The value is specified as a filename in the current directory; for example, the `universal.json` configuration for the ViaVersion plugin represents the `channels/viaversion/universal.json` file.

UPU will first look for the configuration of the current platform. If it is not found, it will fall back to the `universal` configuration. If it is still not found, it will abandon the request.

The structure of `universal.json` is explained in detail in the [documentation](https://docs.upu.dreamvoid.me/en/core/config/channel.json). However, the configuration file in the repository should not contain a valid `selectedChannel` field (it can be set to null for quick user setup). Additionally, the repository configuration also contains a `last_update` field, which is a `long` type number used to check if the local file has expired and needs updating. While this field can be set to any long integer, the best practice is to set it to the current date for easy updating.
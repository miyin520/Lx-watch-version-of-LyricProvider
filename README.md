# 手表洛雪音乐歌词支持

基于 [LyricProvider](https://github.com/tomakino/LyricProvider) 修改的 Xposed 歌词提供器模块，
用于向[词幕](https://github.com/tomakino/CSLyric)提供 **LX 手表版** 的歌词。

## 与上游的区别

| 项目 | 上游 | 本项目 |
| --- | --- | --- |
| 应用名 | 洛雪音乐歌词支持 | 手表洛雪音乐歌词支持 |
| 包名 | `io.github.proify.lyricon.lxprovider` | `io.github.proify.lxmusic.watch` |
| 适配应用 | 官方 LX Music（`cn.toside.music.mobile`） | LX 手表版（`cn.miyin.music.watch`） |

官方 LX Music 的适配仍然保留，本模块同时支持两者。

## 安装

1. 安装本模块的 APK
2. 在 LSPosed 中启用模块，作用域勾选 **LX 手表版**（`cn.miyin.music.watch`）
3. 重启 LX 手表版

## 对应关系

| 项目 | 包名 | 歌词模块类 |
| --- | --- | --- |
| 官方 LX Music | `cn.toside.music.mobile` | `cn.toside.music.mobile.lyric.LyricModule` |
| LX 手表版 | `cn.miyin.music.watch` | `cn.miyin.music.watch.lyric.LyricModule` |

LX 手表版项目地址：https://github.com/miyin520/lx-music

## 修改内容

仅修改 `lx-music` 模块中的以下文件：

- `HookEntry.kt`：增加 `loadApp("cn.miyin.music.watch", LXMusic("cn.miyin.music.watch.lyric.LyricModule"))`
- `Constants.kt`：模块包名改为 `io.github.proify.lxmusic.watch`
- `build.gradle.kts`：`applicationId` 与版本号调整
- `strings.xml`：应用名与模块说明调整

其余模块与上游保持一致。

## 版本号规范

版本号格式为 `主版本.次版本.修订号`。

| 位置 | 含义 | 递增条件 |
| --- | --- | --- |
| 主版本 | 不兼容变更 | 无法覆盖安装，或升级后需要清除应用数据 |
| 次版本 | 新增功能 | 增加新功能时递增，修订号归零 |
| 修订号 | 缺陷修复 | 每修复一次问题递增 |

`versionCode` 同步递增。发布标签格式为 `v<版本号>-watch`。

## 签名

模块使用固定签名密钥，证书 SHA-256 指纹：

```
64:0E:31:A4:CD:4D:20:FA:BD:1C:48:25:56:2C:83:69:26:C7:C6:43:5C:3A:1A:4B:6D:8A:58:63:70:FC:C2:39
```

密钥文件不随仓库分发，构建时通过环境变量提供：

```bash
export RELEASE_STORE_FILE=/path/to/lyricprovider.jks
export RELEASE_STORE_PASSWORD=***
export RELEASE_KEY_ALIAS=lyricprovider
export RELEASE_KEY_PASSWORD=***
```

更换密钥会导致已安装的模块无法覆盖升级，必须卸载重装。

## 构建

环境要求：JDK 17、Android SDK（compileSdk 37）、Gradle 9.3.1。

```bash
./gradlew :lx-music:assembleRelease
```

产物位于 `lx-music/build/outputs/apk/release/`。

签名密钥不随仓库分发，构建方式见上一节「签名」。

## 许可

本项目遵循上游的 [Apache License 2.0](LICENSE)。

原始项目版权归 Proify、Tomakino 所有；本修改部分版权归修改者所有。
修改内容依据 Apache License 2.0 第 4 条 (d) 项在上文说明。

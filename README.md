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

## 构建

环境要求：JDK 17、Android SDK（compileSdk 37）、Gradle 9.3.1。

```bash
./gradlew :lx-music:assembleRelease
```

产物位于 `lx-music/build/outputs/apk/release/`。

签名文件 `lx-music/release.jks` 未包含在仓库中，构建前需自行生成，并通过环境变量
`RELEASE_STORE_PASSWORD`、`RELEASE_KEY_ALIAS`、`RELEASE_KEY_PASSWORD` 提供。

## 许可

本项目遵循上游的 [Apache License 2.0](LICENSE)。

原始项目版权归 Proify、Tomakino 所有；本修改部分版权归修改者所有。
修改内容依据 Apache License 2.0 第 4 条 (d) 项在上文说明。

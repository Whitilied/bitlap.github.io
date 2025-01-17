---
toc: content
nav:
  path: /lab/smt
---

<img align="right" width="20%" height="30%" src="/images/smt.png" alt="https://bitlap.org"/>

# scala-macro-tools

| Project Stage | CI              | Codecov                                   |
| ------------- | --------------- | ----------------------------------------- |
| ![Stage]      | ![CI][badge-ci] | [![codecov][badge-codecov]][link-codecov] |

| Scaladex                                                                    | Jetbrains Plugin                              | Nexus Snapshots                                                  |
| --------------------------------------------------------------------------- | --------------------------------------------- | ---------------------------------------------------------------- |
| [![scala-macro-tools Scala version support][badge-scaladex]][link-scaladex] | [![Version][badge-jetbrains]][link-jetbrains] | [![Sonatype Nexus (Snapshots)][badge-snapshots]][link-snapshots] |

## 该库的目的

学习 Scala 宏编程（macro）和抽象语法树（ast）。

> 本项目目前处于实验阶段，有建议、意见或者问题欢迎提 issue。如果本项目对你有帮助，欢迎点个 star。

**[中文说明](./README_CN.md) | [English](./README.md)**

# 环境

- Java 8、11 编译通过
- Scala 2.11.12、2.12.14、2.13.6 编译通过

# 模块功能

## `tools`

- `@toString`
- `@json`
- `@builder`
- `@log`
- `@apply`
- `@constructor`
- `@equalsAndHashCode`
- `@jacksonEnum`
- `@elapsed`
- `@javaCompatible`
- `ProcessorCreator`

> Intellij 插件 `Scala-Macro-Tools`。

## `cacheable-core`

基于 zio 的类似 Spring`@Cacheable`和`@CacheEvict`注解的缓存 API 定义。该模块不包含具体的存储媒介。

- `@cacheable` / `Cache.apply`
- `@cacheEvict` / `Cache.evict`

## `cacheable-caffeine`

基于 zio 和 caffeine 的内存缓存实现，需要`cacheable-core`。

## `cacheable-redis`

基于 zio 和 zio-redis 的分布式缓存实现，需要`cacheable-core`。

# 文档

[https://bitlap.org/lab/smt](https://bitlap.org/lab/smt)

# 如何使用

添加库依赖，在 sbt 中

> 在 gradle，maven 中，通常`smt-tools`被替换为`smt-tools_2.12`这种。其中，`2.12`表示 Scala 版本号。
> **使用 tools 模块**
> **使用 tools 模块**

```scala
"org.bitlap" %% "smt-tools" % "<VERSION>" //从0.4.0开始名字改成 smt-tools
```

**使用 cacheable 模块 API**

```scala
// 内部包含的依赖: zio, zio-streams, zio-logging
"org.bitlap" %% "smt-cacheable-core" % "<VERSION>"
```

**使用 redis 实现的 cacheable 模块**

> TODO，目前不可用，无分布式锁

```scala
// 分布式缓存, 内部包含的依赖: zio-redis, config, zio-schema, zio-schema-json, 可选的 (zio-schema-derivation用于样例类序列化)
// 依赖于`smt-cacheable-core`（不支持 Scala2.11.x）
"org.bitlap" %% "smt-cacheable-redis" % "<VERSION>"
```

**使用 caffeine 实现的 cacheable 模块**

```scala
// 本地缓存, 内部包含的依赖: config, caffeine
// 依赖于`smt-cacheable-core`
"org.bitlap" %% "smt-cacheable-caffeine" % "<VERSION>"
```

该库已发布到 maven 中央仓库，请使用最新版本。仅将本库导入构建系统（例如 gradle、sbt）是不够的。你需要多走一步。

| Scala 2.11               | Scala 2.12               | Scala 2.13                            |
| ------------------------ | ------------------------ | ------------------------------------- |
| 导入 macro paradise 插件 | 导入 macro paradise 插件 | 开启 编译器标记 `-Ymacro-annotations` |

```scala
addCompilerPlugin("org.scalamacros" % "paradise_<your-scala-version>" % "<plugin-version>")
```

`<your-scala-version>`必须是 Scala 版本号的完整编号，如`2.12.13`，而不是`2.12`。

如果这不起作用，可以谷歌寻找替代品。

在`scala 2.13.x`版本中，macro paradise 的功能直接包含在 scala 编译器中。然而，仍然必须启用编译器标志`-Ymacro annotations`。

[stage]: https://img.shields.io/badge/Project%20Stage-Experimental-yellow.svg
[badge-ci]: https://github.com/bitlap/scala-macro-tools/actions/workflows/ScalaCI.yml/badge.svg
[badge-scaladex]: https://index.scala-lang.org/bitlap/scala-macro-tools/smt-tools/latest-by-scala-version.svg?platform=jvm
[badge-jetbrains]: https://img.shields.io/jetbrains/plugin/v/17202-scala-macro-tools
[badge-codecov]: https://codecov.io/gh/bitlap/scala-macro-tools/branch/master/graph/badge.svg?token=IA596YRTOT
[badge-snapshots]: https://img.shields.io/nexus/s/org.bitlap/smt-tools_2.13?server=https%3A%2F%2Fs01.oss.sonatype.org
[link-jetbrains]: https://plugins.jetbrains.com/plugin/17202-scala-macro-tools
[link-codecov]: https://codecov.io/gh/bitlap/scala-macro-tools
[link-scaladex]: https://index.scala-lang.org/bitlap/scala-macro-tools/smt-tools
[link-snapshots]: https://s01.oss.sonatype.org/content/repositories/snapshots/org/bitlap/

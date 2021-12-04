---
toc: content
nav:
  path: /zh-CN/lab/smt
---

<img align="right" width="30%" height="30%" src="/images/smt.png" alt="https://dreamylost.cn"/>

# [scala-macro-tools](https://github.com/jxnu-liguobin/scala-macro-tools)

[![Build](https://github.com/jxnu-liguobin/scala-macro-tools/actions/workflows/ScalaCI.yml/badge.svg)](https://github.com/jxnu-liguobin/scala-macro-tools/actions/workflows/ScalaCI.yml)
[![codecov](https://codecov.io/gh/jxnu-liguobin/scala-macro-tools/branch/master/graph/badge.svg?token=IA596YRTOT)](https://codecov.io/gh/jxnu-liguobin/scala-macro-tools)
[![Maven Central](https://img.shields.io/maven-central/v/io.github.jxnu-liguobin/scala-macro-tools_2.13.svg?label=Maven%20Central)](https://search.maven.org/search?q=g:%22io.github.jxnu-liguobin%22%20AND%20a:%22scala-macro-tools_2.13%22)
[![Version](https://img.shields.io/jetbrains/plugin/v/17202-scala-macro-tools)](https://plugins.jetbrains.com/plugin/17202-scala-macro-tools)

## 该库的目的

学习 Scala 宏编程（macro）和抽象语法树（ast）。

> 本项目目前处于实验阶段，有建议、意见或者问题欢迎提 issue。如果本项目对你有帮助，欢迎点个 star。

## 环境

- 使用 Java 8, 11 编译通过
- 使用 Scala 2.11.x ~ 2.13.x 编译通过

## 功能

- `@toString`
- `@json`
- `@builder`
- `@synchronized`
- `@log`
- `@apply`
- `@constructor`
- `@equalsAndHashCode`
- `@jacksonEnum`
- `@elapsed`

> Intellij 插件 `Scala-Macro-Tools`。

## 如何使用

添加库依赖，在 sbt 中

> 在 gradle，maven 中，通常`scala-macro-tools`被替换为`scala-macro-tools_2.12`这种。其中，`2.12`表示 Scala 版本号。

```scala
"io.github.jxnu-liguobin" %% "scala-macro-tools" % "<VERSION>"
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
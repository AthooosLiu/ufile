# 简介

## 概述

US3SYNC 是一款将不同源的数据同步到 US3 的迁移工具。通过将 US3SYNC 部署在本地或者云主机中，可以便捷地从本地或者其他云环境中将数据迁移到 US3 存储空间。

## 工作原理

![](http://ufile-release.cn-bj.ufileos.com/us3sync/doc/structure.jpg)

图中master节点与worker节点功能：

- master节点：
> 单点部署，负责迁移任务的管理。其主要逻辑是从源端拉取文件列表，然后将需要迁移的文件派发给worker进程迁移。

- worker节点：
> 支持节点扩展，负责迁移文件。其主要逻辑是从源端下载文件，然后将文件上传到目的端。

master节点与worker节点可以部署在同一台机器，也可以部署在多台机器上，用户可以根据需要自行扩展worker节点，下面分别介绍：

- 部署在同一台机器：
> master节点和worker节点通过启动时配置的**内部通信监听地址**进行通信。用户需要确保配置给worker节点的路径是单独的路径，不可与master路径以及其他worker路径重复。

- 部署在不同机器：
> master节点和worker节点通过启动时配置的**内部通信监听地址**进行通信，确保该地址在worker机器上可以访问。用户需要确保配置给worker节点的路径是单独的路径，不可与master路径以及其他worker路径重复。

## 主要功能

1. 支持从 s3，oss，qiniu，youpai，US3 云存储迁移数据到 US3 中。
2. 支持从 NAS 存储或者本地目录将数据迁移到 US3 中。
3. 支持指定 URL 资源列表将数据迁移到 US3 中。
4. 支持 web 管理，通过 web 管理迁移任务，迁移节点。
5. 支持源端管理
6. 支持配置任务定期执行
7. 支持失败文件列表导出

**注：暂不支持源端为归档类型的文件迁移到 US3。**

## 文件结构

```
US3SYNC
├── bin
│ |── master            # master 可执行程序
│ └── worker            # worker 可执行程序
├── conf
│ └── config.toml       # 配置文件
├── cert                # https证书
├── log                 # master日志文件存放路径
├── pika                # 依赖pika
└── console.sh          # 启动脚本
```

## 与原迁移工具对比

原迁移工具使用请参照：[原迁移工具](/ufile/tools/tools/ufile_import)

| US3SYNC              | ufile-import                       |
| ------------------------ | ---------------------------------- |
| 提供界面管理操作         | 只支持命令行操作                   |
| 配置文件整合为单个       | 多个配置文件                       |
| 数据不落盘，提高迁移效率 | 数据落盘，需要根据需要提供磁盘资源 |
| 使用 pika 缓存           | 使用 redis 缓存                    |
| 按分片粒度并发，带宽稳定 | 按文件粒度并发，对大文件迁移不友好 |
| 支持按照大小进行数据校验 | 不支持校验                         |

## 版本和运行环境

### 软件版本

当前版本：1.2.0

### 运行环境

- Master节点：Linux（x86 64位）
- Worker节点：Linux（x86 64位）
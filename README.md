# NEVSTOP TagDB Library

[English](./README(en).md) | [中文](./README.md)

NEVSTOP TagDB 是专为 LabVIEW 环境设计的高级数据管理库，提供配置与 Tag 数据的高效读写、存储和共享能力。库内置优化的数据结构与缓存机制，为 LabVIEW 应用程序实现可靠的数据持久化与实时访问。

## 目录结构

```
├── .github/          # GitHub 工作流配置
├── Benchmark/        # 性能测试相关文件
├── Documentation/    # 文档和图标资源
├── src/              # 源代码目录
│   ├── Example/      # 示例程序
│   ├── Probes/       # 自定义调试探针
│   └── TagDB/        # 核心库文件
│       ├── API/      # 公共接口函数
│       ├── Add-ons/  # 附加功能
│       └── Typedef/  # 类型定义
├── LabVIEW-TagDB.lvproj  # 主项目文件
└── LabVIEW-TagDB.vipb    # VIPackage 构建文件
```

## 核心特性

### 1. 灵活的数据存储
- 支持配置数据和 Tag 数据的持久化存储
- 通过 VIM (VI Macro) 自动支持 LabVIEW 所有数据类型的读写与转换
- 针对 Reference 类型数据进行了特别优化，确保高效存储和检索

### 2. 多线程安全
- 提供完善的多线程环境下的数据共享机制
- 内置线程安全保护，避免并发访问冲突
- 支持跨VI、跨任务的数据访问和同步

### 3. 高性能设计
- 实现高效的缓存机制，提供快速数据访问
- 优化的数据结构，减少内存占用和提高检索效率
- 支持按名称获取 DBRef，类似 LabVIEW Named Queue，简化跨 VI 的数据访问模式

### 4. 配置管理
- 完整的配置文件导入导出功能
- 支持保存和恢复系统状态信息
- 提供配置锁定功能，防止意外修改

### 5. 调试支持
- 提供三种自定义 Probe，方便运行时调试和监控
- 包括 TagDB Probe、TagDB Table Probe 和 TagDB Monitor Probe

## API 参考

### 基础操作函数

| 函数名称 | 功能描述 |
|---------|---------|
| TagDB-Obtain.vi | 获取 TagDB Refnum，创建或打开现有数据库 |
| TagDB-Release.vi | 释放 TagDB Refnum，关闭数据库 |
| TagDB-IsValid.vi | 检查 TagDB Refnum 是否有效 |

### 数据读写函数

| 函数名称 | 功能描述 |
|---------|---------|
| TagDB-Write.vim | 写入/更新单个 Tag 的值 |
| TagDB-Write Data Recursive.vim | 递归写入/更新数据结构到 Tags |
| TagDB-Write Data Elements.vim | 写入 Cluster 数据时，按元素名称逐一写入对应 Tag |
| TagDB-Read.vim | 读取单个 Tag 的值 |
| TagDB-Read Data By Element Names.vim | 读取 Cluster 数据时，按元素名称逐一读取对应 Tag |
| TagDB-Read By RegExp.vim | 使用正则表达式批量读取 Tag |
| TagDB-Delete.vi | 删除 Tag |
| TagDB-Delete Single.vi | 通过名称删除单个 Tag |
| TagDB-Delete Multiple.vi | 批量删除多个 Tag |

### 配置管理函数

| 函数名称 | 功能描述 |
|---------|---------|
| TagDB-Load.vi | 从文件加载 TagDB 配置 |
| TagDB-Save.vi | 将 TagDB 配置保存到文件 |
| TagDB-Set Lock.vi | 锁定/解锁 TagDB，限制或开放新 Tag 的添加 |

### 实用工具函数

| 函数名称 | 功能描述 |
|---------|---------|
| TagDB-Status.vi | 获取 TagDB 当前状态信息 |
| TagDB-List.vi | 列出数据库中所有 Tag 名称 |
| TagDB_Find Names.vi | 查找符合条件的 Tag 名称 |
| TagDB-Timestamp.vi | 获取 TagDB 操作的时间戳 |
| TagDB-UpdateUI.vi | 更新与 Tag 关联的 UI 控件 |
| TagDB-Change Detector.vi | 检测 Tag 值的变化 |
| TagDB-Truncate.vi | 清空 TagDB 数据库中的所有 Tag 数据 |

## 最佳实践

### 数据管理
- **多线程数据共享**：以 TagDB 作为多线程应用的数据共享中心，取代全局变量
- **配置信息存储**：将系统配置保存在 TagDB 中，便于导入/导出和版本管理
- **临时数据缓存**：利用 TagDB 缓存功能实现数据点的异步更新与快速访问
- **控件引用管理**：存储前面板控件 Reference，方便动态操作 UI

### 性能优化
- 对频繁访问的数据，善用 TagDB 的缓存机制
- 大量数据操作时，优先使用批量操作函数以提高效率
- 在关键操作期间使用锁定功能，防止数据被意外修改

### 调试技巧
- 使用内置三种 Probe 工具监控运行时 TagDB 的状态与数据变化
- 使用 TagDB-Status.vi 定期检查数据库状态，及时发现异常
- 使用 TagDB-Change Detector.vi 监控特定 Tag 的值变化，便于调试复杂交互逻辑

## 示例程序

库包含多个示例程序，展示不同场景下的使用方法：

- **TagDB Example.vi**：基础功能演示
- **TagDB Application Example**：带有完整模型配置系统的实际应用演示
- **TagDB For Control Reference.vi**：用于 UI 控件的 Reference 类型数据处理示例
- **TagDB Multi-Thread Example**：多线程环境下的使用示例
- **TagDB Read Data Example.vi**：综合读取示例，涵盖单次读取、按元素名称读取（Cluster 数据）及正则表达式读取
- **TagDB Write Data Example.vi**：综合写入示例，涵盖单次写入、按元素名称写入（Cluster 数据）及递归数据结构写入
- **TagDB Using regexp Example.vi**：正则表达式查询示例
- **TagDB Refresh UI Value.vi**：UI 值刷新示例，展示如何实时更新 UI 控件值

## 安装说明

使用 VIPM (VI Package Manager) 安装 VIP 包

## 系统要求

- LabVIEW 2017 或更高版本
- 建议使用 VIPM 2017 或更高版本进行安装

## 许可证

本项目使用 Apache-2.0 license，详见 [LICENSE](LICENSE) 文件。

## 贡献指南

欢迎提交问题报告和改进建议。如需贡献代码，请遵循以下流程：
1. Fork 本仓库
2. 创建功能分支
3. 提交更改
4. 推送到分支
5. 提交 Pull Request



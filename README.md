# NEVSTOP TagDB Library

用于在 LabVIEW 系统中提供配置及 Tag 数据的读写功能。

## 特性

- 实现配置及 Tag 数据的保存功能
- 提供多线程环境下的数据共享功能
- 通过 Xnode/VIM 自动支持 LabVIEW 任何数据类型的转换
- 提供 cache 机制，实现快速数据访问
- 提供按名称获取 DBRef 的方法，类似 LabVIEW Named Queue
- 针对 Reference 类型进行了优化
- 支持配置文件，可导入导出配置及状态信息
- 提供自定义 Probe，便于调试

## VI 函数面板

- 获取 TagDB Refnum
- 更新 Tag
- 获取 Tag
- 删除 Tag
- 载入配置文件
- 保存配置文件
- 获取 TagDB 状态
- 锁定 TagDB（禁止增加新的Tag）
- 释放 TagDB

## 最佳实践

- 多线程保存临时数据
- 保存系统配置信息，对配置进行导入导出
- 利用 Cache 功能实现 Tag 数据点的异步更新与快速访问
- 存储 LabVIEW 前面板控件 Refnum


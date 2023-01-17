# LabVIEW TagDB Library


用于在 LabVIEW 系统中提供配置、Tag 数据的读写功能。

## FEATURE

 - REQ_FEATURE_TAGDB 实现配置、Tag数据的数据保存功能。
 - REQ_FEATURE_MULTITHREAD 提供多线程中的数据共享功能
 - REQ_FEATURE_XNODE 通过 Xnode 支持 LabVIEW 任何数据类型自动转换
 - REQ_FEATURE_CACHE 提供 cache 机制，提供快速的数据访问
 - REQ_FEATURE_NAMEDDB 提供名称获取 DBRef 方法，类似 LabVIEW Named Queue。
 - REQ_FEATURE_REF 针对 Reference 类型优化
 - REQ_FEATURE_CFG 支持配置文件，可导入导出配置、状态信息
 - REQ_FEATURE_PROBE 提供自定义Probe，便于调试
 
## VI PALETTE

REQ_FEATURE_VIPALETTE

 - 获取 TagDB Refnum
 - 载入配置文件
 - 保存配置文件
 - 锁定 TagDB（禁止增加新的Tag）
 - 更新 Tag
 - 获取 Tag 
 - 删除 Tag
 - 获取 TagDB 状态
 - 释放 TagDB

## BEST PRACTICE

REQ_FEATURE_BESTPRACETICE

 - 多线程保存临时数据
 - 保存系统配置信息，对配置进行导入导出。
 - 提供 Tag 数据点的异步更新，利用 Cache 功能快速的访问数据。
 - 存储LabVIEW 前面板控件 Refnum。 


# LabVIEW TagDB Library Requiements

细分实现 LabVIEW TagDB Library 需求文档描述。用于 NIRG 分析使用。

	
## TagDB

TagDB 核心Tag功能，使用 LabVIEW Class 实现 TagDB。
[Covers: REQ_FEATURE_TAGDB]
[Covers: REQ_FEATURE_MULTITHREAD]

### TagDB 内部数据定义：
    - DVR : REQ_TAGDB_DVR TagDB 数据池，保存核心数据的 Variant 使用 Data Value Reference 保存，Class Wire 连接的不同线程，可以访问数据。
       - Variant：使用 LabVIEW Variant attribute Hashmap<String,Variant> 的功能，保存所有的 Tag 数据。
       - db Flag : db 修改标志。
       - db Item Flag ： db Tag 列表修改标志。
       - TagDB name : 名称
    - Attributes：易失配置，同一个TagDB，配置也可以不同，使用属性节点进行配置。
	   - REQ_TAGDB_ATTR_TrimSpace ：(T) 忽略Name的前后空白

### TagDB Name定义：
    - Tag 变量 : REQ_TAGDB_NAME 非临时变量则为 Tag，一般为配置信息。
    - 临时变量 : REQ_TAGDB_TEMPNAME 使用'::[\w]+::'表示的变量为临时变量，存储/载入时，忽略这部分变量。

### 内部设计一个 FGV 保存所有命名 TagDB，用于命名队列的获取。
[Covers: REQ_FEATURE_NAMEDDB]

    -  REQ_TAGDB_NAMEDDB

### Variant 存储到文件中，实现配置文件的保存、载入。
[Covers: REQ_FEATURE_CFG]

    - REQ_TAGDB_CFG_LOAD
    - REQ_TAGDB_CFG_LOAD_IGNORE_TEMP
    - REQ_TAGDB_CFG_SAVE

### Tag 读写逻辑

   - REQ_TAGDB_VALUE_MISSED_TAG_AS_ERROR : (T) 读取 Tag 时，发现 Tag 不存在，默认产生 50001 错误
   - REQ_TAGDB_VALUE_MISSED_TEMPTAG_AS_noERROR ：(F) 读取 临时Tag 时，发现 Tag 不存在，默认不产生 50001 错误

### 针对 Reference 类型优化
[Covers: REQ_FEATURE_REF]

    - REQ_TAGDB_REF

### 提供 Template, 在数据没有发生修改的情况下，使用Cache，不直接读取 TagDB。
[Covers: REQ_FEATURE_CACHE]

    - TagDB_Value.vi
       - REQ_TAGDB_TEMPLATE_VALUE_NAME
       - REQ_TAGDB_TEMPLATE_VALUE_REF
       - REQ_TAGDB_TEMPLATE_VALUE_REGEXP
       - REQ_TAGDB_TEMPLATE_VALUE_REGEXP_REF
    - TagDB_SetValue.vi
       - REQ_TAGDB_TEMPLATE_SETVALUE

## XNode

使用XNode，实现所有的数据类型的支持。
[Covers: REQ_FEATURE_XNODE]

	- @REQ_XNODE_MENU_REGEXP : 菜单选择是否启用正则表达式
	- @REQ_XNODE_MENU_COMMONDATETYPE : 菜单支持常用的数据类型
	- @REQ_XNODE_ICON : 使用不同的 Icon 表示 Value/SetValue 的状态。

	
## VIAPI

提供 VI Palette 能够访问的VI API 接口。
[Covers: REQ_FEATURE_VIPALETTE]

     - REQ_API_Obtain 获取 TagDB
     - REQ_API_ISVALID 验证 TagDB 是否有效
     - REQ_API_Load 载入配置文件
     - REQ_API_Save 保存配置文件
     - REQ_API_SetValue 更新 Tag
     - REQ_API_Value 获取 Tag 
        - REQ_API_Value_NAME 通过名称获取 Tag 数据
        - REQ_API_Value_REGEXP 通过正则获取 Tag 数据
     - REQ_API_DelValue 删除 Tag
     - REG-API_TAGNAMES 通过正则获取 Tag 数据名称
     - REQ_API_Status 获取 TagDB 状态
     - REQ_API_Free 释放 TagDB
     - REQ_API_PROPNODE 属性节点访问内部属性
        - REQ_API_TAGLIST : 内部tag列表
        - REQ_API_DBCHANGED : TagDB 是否发生修改
        - REQ_API_DBITEMCHANGED ： Tag列表是否发生变化
        - REQ_API_PROP_TRIMSPACE ： 忽略Name的前后空白
	

## PROBE

提供自定义的Probe，用于TagDB 调试。
[Covers: REQ_FEATURE_PROBE]

	Probe 可以显示内容：
	 1. TagDB 名称
	 2. TagDB Item Flag 状态
	 3. TagDB Change Flag 状态
	 4. TagDB Tag List
	 5. 选中的 Tag 数据(Variant)


## Examples

LabVIEW 范例，用于演示 TagDB 的使用场景。
[Covers: REQ_FEATURE_BESTPRACETICE]

    - REQ_EXAMPLE_TAGDBDEMO : 演示 TagDB 数据读写功能、配置文件功能。    
    - REQ_EXAMPLE_MULTITHREAD : 演示 TagDB 多线程中配置、数据异步更新功能。
    - REQ_EXAMPLE_REF : 演示 TagDB 对 LabVIEW Control Reference 的优化。
	- REQ_EXAMPLE_APPLICATION : 演示在系统中的使用。
	- REQ_EXAMPLE_PARSEFILE : 演示离线分析 vcfg 数据。
















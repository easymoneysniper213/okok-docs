## 资产模型Asset
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|资产的 ID
|parent|INT|FOREIGN KEY REFERENCES Asset(id)|上一级资产 ID，如果没有则记作 NULL
|name|VARCHAR||资产的名称
|assetClass|INT||资产类型的 ID
|user|INT|FOREIGN KEY REFERENCE User(id) |资产挂账人的用户 ID 
|price|DECIMAL(8,2)||资产的现价格
|description|VARCHAR||资产的说明
|position|VARCHAR||资产的位置信息
|expire|INT||资产是否被清退 
|count|INT||数量型资产的数量
|assetTree|VARCHAR|FOREIGN KEY REFERENCES AssetTree(name)|资产属于资产层级树的哪一个节点
|department|INT|FOREIGN KEY REFERENCES Department(id)|资产属于哪一个部门
|create_time|DATETIME||资产的创建时间
|deadline|INT||资产的限期
|initial_price|DECIMAL(8,2)||资产的原价格
|status|INT||资产状态，1表示空闲，2表示员工使用中，3表示维保中
|history|VARCHAR||资产相关历史（维保、领用、退库、转移）
|warning_date|INT||资产的告警日期
|warning_amount|INT||资产的告警数量
|picture_link|VARCHAR||资产的图片链接
|richtxt|VARCHAR||资产的富文本描述


## 资产树节点模型AssetTree
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|资产树节点的 ID
|parent|INT|FOREIGN KEY REFERENCES Asset(id)|上一级资产 ID，根节点的记作 NULL
|name|VARCHAR||资产的名称
|department|INT|FOREIGN KEY REFERENCES Department(id)|资产属于哪一个部门


## 请求模型PendingRequests
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|请求的 ID
|initiator|INT|FOREIGN KEY  REFERENCES User(id)|申请发起者的用户名字
|participant|INT|FOREIGN KEY  REFERENCES User(id)|申请接受者(一般为资产管理员)
|target|INT|FOREIGN KEY  REFERENCES User(id)|申请中涉及另一用户名字(若没有则记作NULL)
|count|INT||申请资产数量
|asset|INT|FOREIGN KEY  REFERENCES Asset(id)|涉及领用的资产
|type|INT||申请的类型，如领用 （1）/ 退库（2） /  维保（3） / 转移（4）等
|result|INT||审批的结果(0表示未审批，1表示成功，2表示失败)
|request_time|DATETIME||请求的发起时间，以时间戳保存
|review_time|DATETIME||审批时间，以时间戳保存（未审批默认为无限远）
|maintain_asset|INT|FOREIGN KEY  REFERENCES Asset(id)|涉及维保的资产
|feishu_message_id|VARCHAR||该请求在飞书客户端中的消息id
|valid|INT||请求是否有效

## 资产统计模型AssetStatistics
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|该资产统计的id
|asset|INT|FOREIGN KEY  REFERENCES Asset(id)|该统计涉及的资产
|cur_department|INT|FOREIGN KEY REFERENCES Department(id)|该统计的资产所在的部门
|cur_user|INT|FOREIGN KEY  REFERENCES User(id)|统计的资产所属于的用户
|cur_price|DECIMAL(8,2)||统计的资产目前的价值
|cur_time|DATETIME||统计创建的时间
|cur_status|INT||统计的资产目前的状态，1表示空闲，2表示员工使用中，3表示维保中
|cur_count|INT||统计的资产目前的数量

## 异步任务模型AsyncTasks
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|该异步任务的id
|entity|INT|FOREIGN KEY  REFERENCES ENTITY(id)|该异步任务所属于的业务实体
|manager|INT|FOREIGN KEY  REFERENCES USER(id)|该异步任务所属于的管理员
|create_time|DATETIME||异步任务创建的时间
|number_need|INT||异步任务需要导入的资产数
|number_succeed|INT||异步任务成功导入的资产数
|finish|INT||异步任务的状态，0表示进行中，1是成功，2是失败
|failed_message|VARCHAR||导致该异步任务失败的具体信息
|port_type|INT||异步任务类型，0表示导入，1表示导出
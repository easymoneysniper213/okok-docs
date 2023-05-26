## 业务实体模型Entity
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|主键
|name|VARCHAR(32)|UNIQUE|业务实体名称
|log_journal|VARCHAR||业务实体的登录登出日志
|operation_journal|VARCHAR||业务实体的关键操作日志


## 部门模型Department
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|主键
|name|VARCHAR(32)|UNIQUE|部门名称
|parent|INT|FOREIGN KEY REFERENCES Department(id) |上一级组织 ID，根节点记作 NULL 
|entity|INT|FOREIGN KEY REFERENCES Entity(id)|组织所在的实体
|userNumber|INT||该部门下用户的数目
|subDeparmentNumber|INT||该部门下子部门的数目

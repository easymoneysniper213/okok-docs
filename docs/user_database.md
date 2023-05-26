## 用户模型User
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|用户的ID
|name|VARCHAR(128)|UNIQUE|用户的名称
|password|VARCHAR(32)||用户密码的MD5值
|entity|INT|FOREIGN KEY REFERENCES Entity(id)|用户所在的业务实体
|department|INT|FOREIGN KEY REFERENCES Department(id)|用户所在的组织
|character|INT||用户的角色权限
|lock|BOOL||用户是否被锁定
|session|VARCHAR(32)||已经登录用户的session_id
|email|VARCHAR(32)|UNIQUE|用户的邮箱
|feishu_name|VARCHAR||用户绑定的飞书用户名
|feishu_open_id|VARCHAR||用户绑定的飞书用户的open_id
|feishu_phone|VARCHAR||用户绑定的飞书用户手机号


## 第三方应用模型URL
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|主键
|url|VARCHAR(32)|UNIQUE|URL
|name|VARCHAR(32)||URL名称
|authority_level|INT||权限等级，1为一般用户可见，2为资产管理员可见，3为系统管理员可见
|entity|INT|FOREIGN KEY REFERENCES Entity(id)|URL所挂载的业务实体

## 日志模型Journal
|字段|类型|属性|说明|
|-|-|-|-
|id|INT|PRIMARY KEY|主键
|time|DATETIME||操作发起的时间
|user|INT|FOREIGN KEY REFERENCES User(id) |操作的用户
|operation_type|INT||操作的名称:登录登出为1,关键信息修改(put)为2,创建相关(post)为3,删除相关(delete)为4
|object_type|INT||操作的对象名称:用户相关为1,部门相关为2,资产相关为3,request相关为4,URL相关为5
|object_name|VARCHAR(128)||操作对象的名字
|message|VARCHAR(128)||操作者补充的操作信息
|entity|INT|FOREIGN KEY REFERENCES Entity(id)| 日志所挂载的业务实体
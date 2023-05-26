## 飞书快捷登录接口

**接口描述**：此接口用于绑定飞书账号的用户快速登录系统

`[POST] /api/qrLogin`



## 绑定飞书账号接口

**接口描述**：此接口用于用户绑定飞书账号

`[PUT] /api/feishu_name/{session}`


## 同步飞书用户接口

**接口描述**：此接口用于绑定飞书账号的系统管理员同步飞书用户

`[POST] /api/feishu_users/{session}`


## 同步更新飞书新增用户接口

**接口描述**：此接口用于在系统中同步更新飞书新增用户

`[POST] /api/feishu_get_event`


## 飞书审批接口

**接口描述**：此接口用于飞书审批后在系统中同步更新审批结果

`[POST] /api/feishu_approval`
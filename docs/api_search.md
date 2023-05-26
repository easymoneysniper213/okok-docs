## 搜索所有用户接口

**接口描述**：此接口用于超级管理员进行全部用户的筛选和搜索

`[POST] /api/get_user_all/{session}`



## 搜索部门下所有用户接口

**接口描述**：此接口用于资产管理员进行自身部门下全部用户的筛选和搜索

`[POST] /api/get_user_department/{session}`



## 搜索业务实体下所有用户接口

**接口描述**：此接口用于系统管理员进行自身业务实体下全部用户的筛选和搜索

`[POST] /api/get_user_entity/{session}`



## 搜索业务实体下登录登出日志接口

**接口描述**：此接口用于系统管理员进行自身业务实体下登录登出日志的筛选和搜索

`[POST] /api/get_logjournal/{session}/{entity_name}`



## 搜索业务实体下关键操作日志接口

**接口描述**：此接口用于系统管理员进行自身业务实体下关键操作日志的筛选和搜索

`[POST] /api/get_operationjournal/{session}/{entity_name}`



## 搜索未领用资产接口

**接口描述**：此接口用于一级用户对某个资产管理员持有的未领用资产进行筛选和搜索

`[POST] /api/search_unallocated_assets/{session}/{manager_name}`



## 搜索个人资产接口

**接口描述**：此接口用于一级用户对个人拥有的全部资产进行筛选和搜索

`[POST] /api/search_personal_assets/{session}`

## 搜索资产接口

**接口描述**：此接口用于资产管理员对某资产分类树节点下全部资产进行筛选和搜索

`[POST] /api/search_assets/{session}`
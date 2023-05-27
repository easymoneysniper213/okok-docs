## 搜索所有用户接口

**接口描述**：此接口用于超级管理员进行全部用户的筛选和搜索

`[POST] /api/get_user_all/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
|id | int  | 待搜索的id |
| name   | str  | 待搜索的姓名               |
| entity   | str  | 待搜索的业务实体名称               |
| department  | str  | 待搜索的部门名称               |
| character  | int  | 待搜索的角色               |
| lock  | bool  | 待搜索的用户状态               |
| page  | bool  | 要求的页面位置               |

请求参数中，id、lock、character为精确匹配，name、entity、department为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有用户信息(至少为1至多为6) |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "id": 1,
        "name": "n",
        "entity": "a",
        "department":"b",
        "character":1,
        "lock":false,
        "page":1
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false, 
    "email" :"" 
  }
  ]
}
```
</details>
</details>

## 搜索部门下所有用户接口

**接口描述**：此接口用于资产管理员进行自身部门下全部用户的筛选和搜索

`[POST] /api/get_user_department/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
|id | int  | 待搜索的id |
| name   | str  | 待搜索的姓名               |
| character  | int  | 待搜索的角色               |
| lock  | bool  | 待搜索的用户状态               |
| page  | bool  | 要求的页面位置               |

请求参数中，id、lock、character为精确匹配，name为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有用户信息(至少为1至多为6) |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "id": 1,
        "name": "n",
        "character":1,
        "lock":false,
        "page":1
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false, 
    "email" :"" 
  }
  ]
}
```
</details>
</details>

## 搜索业务实体下所有用户接口

**接口描述**：此接口用于系统管理员进行自身业务实体下全部用户的筛选和搜索

`[POST] /api/get_user_entity/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
|id | int  | 待搜索的id |
| name   | str  | 待搜索的姓名               |
| department  | str  | 待搜索的部门名称               |
| character  | int  | 待搜索的角色               |
| lock  | bool  | 待搜索的用户状态               |
| page  | bool  | 要求的页面位置               |

请求参数中，id、lock、character为精确匹配，name、department为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有用户信息(至少为1至多为6) |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "id": 1,
        "name": "n",
        "department":"b",
        "character":1,
        "lock":false,
        "page":1
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":false, 
    "email" :"" 
  }
  ]
}
```
</details>
</details>

## 搜索业务实体下登录登出日志接口

**接口描述**：此接口用于系统管理员进行自身业务实体下登录登出日志的筛选和搜索

`[POST] /api/get_logjournal/{session}/{entity_name}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
|date | str  | 待搜索的日志日期 |
| info   | str  | 待搜索的日志信息               |
| name | str  | 待搜索的用户名称               |
| page  | bool  | 要求的页面位置               |

请求参数中，date为精确匹配，name、info为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有日志信息(至少为1至多为6) |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                         |
| ------ | -------------------------- | -------------------------------------------- |
| 1      | 你无此权限 | 访问日志的系统管理员不属于传入的entity_name对应的业务实体 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "date":"2020-01-11" ,
        "info": "ab",
        "name":"a",
        "page":1
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":2,
  "data":[
  {
    "time":2023-05-08 09:52:15,
    "user":"liusn",
    "message":"liusn登录了启源资产管理系统",
  },
  {
    "time":2023-05-08 09:51:13,
    "user":"liusn",
    "message":"liusn登出了启源资产管理系统",
  }
  ]
}
```
</details>
</details>

## 搜索业务实体下关键操作日志接口

**接口描述**：此接口用于系统管理员进行自身业务实体下关键操作日志的筛选和搜索

`[POST] /api/get_operationjournal/{session}/{entity_name}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
|date | str  | 待搜索的日志日期 |
| info   | str  | 待搜索的日志信息               |
| name | str  | 待搜索的用户名称               |
| page  | bool  | 要求的页面位置               |

请求参数中，date为精确匹配，name、info为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有日志信息(至少为1至多为6) |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                         |
| ------ | -------------------------- | -------------------------------------------- |
| 1      | 你无此权限 | 访问日志的系统管理员不属于传入的entity_name对应的业务实体 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "date":"2020-01-11" ,
        "info": "ab",
        "name":"a",
        "page":1
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data":[
  {
    "time":2023-05-08 09:58:08,
    "user":"manager",
    "opeation_type":3,
    "object_type":2,
    "object_name":"CST",
    "message":"管理员manager创建了部门CST"
  },
  {
    "time":2023-05-08 09:58:06,
    "user":"manager",
    "operation_type":4,
    "object_type":2,
    "object_name":"grade_1",
    "message":"管理员manager删除了部门grade_1"
  }
  ]
}
```
</details>
</details>

## 搜索未领用资产接口

**接口描述**：此接口用于一级用户对某个资产管理员持有的未领用资产进行筛选和搜索

`[POST] /api/search_unallocated_assets/{session}/{manager_name}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 待搜索的资产的id |
| name   | str  | 待搜索的资产的名称               |
| price_inf   | double  | 待搜索的资产的价值下限               |
| price_sup   | double  | 待搜索的资产的价值上限               |
| description  | str  | 该资产的描述               |
| asset_tree_node  | str  | 要搜索的资产挂载的资产分类树节点              |
| page  | bool  | 要求的页面位置               |

请求参数中，id为精确匹配，asset_tree_node、description、name为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）
price为范围匹配（即在[price_inf,price_sup]区间内均满足）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有日志信息(至少为1至多为6) |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                         |
| ------ | -------------------------- | -------------------------------------------- |
| 2      | 所选资产管理员非法 | 所选资产管理员非法(如不存在或者不在一个部门下等) |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "asset_tree_node": "默认分类",
        "id": 520,
        "name": "Love",
        "price_inf": 52.00,
        "price_sup": 520.0,
        "description": "No need to explain",
        "page": 1,
}

```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data":[
    {
  "id":1,
  "parentName":"a", 
  "name":"aaa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  },
  {
  "id":2,
  "parentName":"a", 
  "name":"aa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  }
  ]
}
```
</details>
</details>

## 搜索个人资产接口

**接口描述**：此接口用于一级用户对个人拥有的全部资产进行筛选和搜索

`[POST] /api/search_personal_assets/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 待搜索的资产的id |
| name   | str  | 待搜索的资产的名称               |
| price_inf   | double  | 待搜索的资产的价值下限               |
| price_sup   | double  | 待搜索的资产的价值上限               |
| description  | str  | 该资产的描述               |
| asset_tree_node  | str  | 要搜索的资产挂载的资产分类树节点              |
| page  | bool  | 要求的页面位置               |

请求参数中，id为精确匹配，asset_tree_node、description、name为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）
price为范围匹配（即在[price_inf,price_sup]区间内均满足）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有日志信息(至少为1至多为6) |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "asset_tree_node": "默认分类",
        "id": 520,
        "name": "Love",
        "price_inf": 52.00,
        "price_sup": 520.0,
        "description": "No need to explain",
        "page": 1,
}

```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data":[
    {
  "id":1,
  "parentName":"a", 
  "name":"aaa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  },
  {
  "id":2,
  "parentName":"a", 
  "name":"aa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  }
  ]
}
```
</details>
</details>

## 搜索资产接口

**接口描述**：此接口用于资产管理员对某资产分类树节点下全部资产进行筛选和搜索

`[POST] /api/search_assets/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 待搜索的资产的id |
| name   | str  | 待搜索的资产的名称               |
| price_inf   | double  | 待搜索的资产的价值下限               |
| price_sup   | double  | 待搜索的资产的价值上限               |
| description  | str  | 该资产的描述               |
| asset_tree_node  | str  | 要搜索的资产挂载的资产分类树节点              |
| page  | bool  | 要求的页面位置               |

请求参数中，id为精确匹配，asset_tree_node、description、name为模糊匹配（即如果输入为"a",则"ab"、"babb"均可与之匹配）
price为范围匹配（即在[price_inf,price_sup]区间内均满足）

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有日志信息(至少为1至多为6) |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
        "asset_tree_node": "默认分类",
        "id": 520,
        "name": "Love",
        "price_inf": 52.00,
        "price_sup": 520.0,
        "description": "No need to explain",
        "page": 1,
}

```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "pages":1,
  "data":[
    {
  "id":1,
  "parentName":"a", 
  "name":"aaa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  },
  {
  "id":2,
  "parentName":"a", 
  "name":"aa",
  "assetClass":1,
  "userName":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "departmentName":"y",
  "create_time":"2020-12-11",
  "deadline":5,
  "initial_price":2.0,
  "status":1,
  }
  ]
}
```
</details>
</details>
## 用户创建接口

**接口描述：**该接口用于超级管理员或系统管理员创建用户

`[POST] /api/user/{session}`

**请求参数**

| 参数       | 类型 | 说明                                         |
| ---------- | ---- | -------------------------------------------- |
| name       | str  | 用户的用户名                                 |
| password   | str  | 用户的密码                                   |
| entity     | str  | 用户的业务实体的名字                         |
| department | str  | 用户的部门的名字(若创建系统管理员则默认为"") |
| character  | int  | 用户的权限                                   |
| lock       | bool | 用户的锁定信息                               |
| email      | str  | 用户的邮箱信息                               |

无成功响应参数，接口调用成功则用户会被直接创建添加到数据库中，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 相关说明                                                                         |
| ------ | -------------------------------- | -------------------------------------------------------------------------------- |
| 1      | 你无此权限                       | 创建用户者不为超级管理员或系统管理员，或系统管理员想创建不属于自己业务实体的用户 |
| 2      | 提供的业务实体不存在             | 未找到请求体名字对应的业务实体                                                   |
| 2      | 提供的部门不存在                 | 创建非系统管理员但未找到请求体名字对应的部门                                     |
| 2      | 提供的部门并不该业务实体         | 提供的部门外键连接到的业务实体与提供的业务实体不匹配                             |
| 2      | 该用户名或邮箱对应的用户已经存在 | 创建的用户的名字或邮箱出现重复                                                   |
| 20     | 一个业务实体最多有5个系统管理员  | 创建的用户类型为系统管理员，但该业务实体的系统管理员过多，不符合规范             |
| 20     | 一个部门最多有5个资产管理员      | 创建的用户类型为资产管理员，但该部门的资产管理员过多，不符合规范                 |
| 20     | 一个部门最多有550个用户          | 创建的用户类型为用户，但该部门的普通用户过多，不符合规范                         |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "name": "example_user",
  "password": "password123",
  "entity" : "aba",
  "department":"tsinghua",
  "character":1,
  "lock":False,
  "email" :""
}
```

</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "info":"Succeed",
}
```

</details>
</details>

## 修改用户相关信息接口

**接口描述：**该接口用于较高级管理员修改低级管理员用户或自己的信息(如锁定或更改密码等)

`[PUT] /api/user/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| password | str  | 若需更改密码，为更改后的密码信息，若不需要则为原密码 |
| lock     | str  | 锁定信息，若要锁定该用户则传入"True"                 |
| id       | int  | 需要修改信息的用户的id                               |

无成功响应参数，接口调用成功则用户信息则被修改，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                               | 说明                                           |
| ------ | -------------------------------------- | ---------------------------------------------- |
| 2      | 目标用户不存在                         | 根据提供的id找不到对应用户                     |
| 5      | 你无权修改同级或级别高于你的用户的信息 | 操作者更改的角色权限更高，无法更改             |
| 1      | 你无此权限                             | 系统管理员修改不属于其业务实体的角色信息       |
| 250    | 不要尝试锁定自己！！！！！             | 锁定只能由权限更高的角色完成，自己不能锁定自己 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "password": "password123",
  "lock":False,
}
```

</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "info":"Success",
}
```

</details>
</details>

## 获取用户角色接口

**接口描述：**该接口用于获取当前登录用户的角色，便于前端根据不同的角色渲染不同的页面

`[GET] /api/character/{session}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数      | 类型 | 说明                   |
| --------- | ---- | ---------------------- |
| character | int  | 目前登录用户的角色权限 |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                                          |
| ------ | -------------------------- | ------------------------------------------------------------- |
| 2      | 用户的会话标识符信息不正确 | 用户提供的sessionId不符合规范，如长度不为32位，包含特殊字符等 |
| 1      | 用户还未登录               | 根据用户提供的sessionId找不到具体用户                         |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
        无
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "data":{
    "character":1
  }
}
```

</details>
</details>

## 获取全部用户列表接口

**接口描述：**该接口用户超级管理员拉取所有用户的信息

`[GET] /api/user_list_all/{session}/{page}`

此接口方法为GET，故无请求参数，url路径中的page代表获取的页数

补充：由于用户数量以万计，返回所有用户再由前端进行填充展示会严重影响效率，因此本组在此处的优化为采取分页操作，超级管理员第一次进入该页面时默认传入 `page`为1，之后后端会根据用户数量返回所有页数（一页展示的用户数量为6）与第一页用户信息，随后超级管理员便可以点击不同的页数来查看所有用户信息了。后面凡是url路径带有 `page`的接口均是实行了分页操作，与该接口类似（同时由于分页可能产生的失败响应状态后文也不再重复展示）。

**成功响应参数**

| 参数  | 类型 | 说明                                 |
| ----- | ---- | ------------------------------------ |
| pages | int  | 总页数                               |
| data  | list | 该页面的所有用户信息(至少为1至多为6) |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                         |
| ------ | -------------------------- | -------------------------------------------- |
| 4      | 请求的页面数超过了总页面数 | 传入的page数过大超过了总page数，无法成功返回 |
| 4      | 请求的页面数必须为正整数   | 传入的page数小于等于0，不合法                |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
        无
</details>
<details>
  <summary>响应</summary>

```json
{
  "code": 0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False, 
    "email" :"" 
  }
  ]
}
```

</details>
</details>

## 用户更改自己的密码接口

**接口描述：**该接口用于用户更改自己的密码，需要先验证旧密码才能更改新密码

`[PUT] /api/user_password/{session}`

**请求参数**

| 参数        | 类型 | 说明                 |
| ----------- | ---- | -------------------- |
| oldpassword | str  | 用户验证身份的旧密码 |
| newpassword | str  | 用户想更改的新密码   |

无成功响应参数，接口调用成功则用户密码被修改，返回Succeed

**失败响应状态**

| 状态码 | 错误信息               | 说明                                |
| ------ | ---------------------- | ----------------------------------- |
| 2      | 您输入的初始密码不正确 | oldpassword不匹配，验证失败无法修改 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "oldpassword":"abb",
  "newpassword":"abb"
}
```

</details>
<details>
  <summary>响应</summary>

```json
{
   "code":0,
   "info":"Succeed",
}
```

</details>
</details>

## 用户更改自己的邮箱接口

**接口描述：**该接口用于用户更改自己的邮箱，需要先验证旧密码通过验证才能更改邮箱

`[PUT] /api/user_email/{session}`

**请求参数**

| 参数        | 类型 | 说明                 |
| ----------- | ---- | -------------------- |
| oldpassword | str  | 用户验证身份的旧密码 |
| email       | str  | 用户想更改的新邮箱   |

无成功响应参数，接口调用成功则用户邮箱被修改，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2      | 您输入的初始密码不正确           | oldpassword不匹配，验证失败无法修改 |
| 5      | 指定邮箱的用户已经存在，无法修改 | 更改后的邮箱冲突了用户的邮箱唯一性  |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "oldpassword":"abb",
  "email":"xpy@163.com"
}
```

</details>
<details>
  <summary>响应</summary>

```json
{
   "code":0,
   "info":"Succeed",
}
```

</details>
</details>

## 获取同部门资产管理员接口

**接口描述**：此接口用于资产管理员获取同部门的资产管理员

`[GET] /api/asset_manager/{session}/{department_name}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                   |
| ---- | ---- | -------------------------------------- |
| data | list | 为包含该部门的所有资产管理员信息的列表 |

**失败响应状态**

| 状态码 | 错误信息       | 说明                                    |
| ------ | -------------- | --------------------------------------- |
| 2      | 未找到目标部门 | 根据url路径传入的部门名称找不到对应部门 |


<details>
 <summary>示例</summary>

响应

```json
{"code":0,
 "data":[
 {
   "id":1,
   "name":"liusn",
 },
 {
   "id":2,
   "name":"xpy",
 },
]
}
```


</details>

## 获取同业务实体资产管理员接口

**接口描述**：此接口用于资产管理员获取同业务实体下所有的资产管理员

`[GET] /api/asset_manager_entity/{session}/{entity_name}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                       |
| ---- | ---- | ------------------------------------------ |
| data | list | 为包含该业务实体的所有资产管理员信息的列表 |

**失败响应状态**

| 状态码 | 错误信息           | 说明                                            |
| ------ | ------------------ | ----------------------------------------------- |
| 2      | 未找到目标业务实体 | 根据url路径传入的业务实体名称找不到对应业务实体 |


<details>
 <summary>示例</summary>

响应

```json
{"code":0,
 "data":[
 {
   "id":1,
   "name":"liusn",
 },
 {
   "id":2,
   "name":"xpy",
 },
]
}
```

</details>

## 管理员获取同业务实体全部用户接口

**接口描述**：此接口用于管理员获取同业务实体下所有的用户

`[GET] /api/user_entity/{session}/{entity_name}/{page}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                 |
| ---- | ---- | ------------------------------------ |
| data | list | 为包含该业务实体的所有用户信息的列表 |

**失败响应状态**

| 状态码 | 错误信息             | 说明                                            |
| ------ | -------------------- | ----------------------------------------------- |
| 2      | 对应的业务实体不存在 | 根据url路径传入的业务实体名称找不到对应业务实体 |


<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False, 
    "email" :"" 
  }
  ]
}
```

</details>

## 一级用户获取同业务实体全部用户接口

**接口描述**：此接口用于一级用户获取同业务实体下所有的用户

`[GET] /api/user_entity4user/{session}/{page}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                 |
| ---- | ---- | ------------------------------------ |
| data | list | 为包含该业务实体的所有用户信息的列表 |

此接口除鉴权操作外无其他失败响应状态


<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :"" 
  }
  ]
}
```


</details>

## 用户获取个人信息接口

**接口描述**：此接口用于用户获取自己的个人信息

`[GET] /api/cur_entity/{session}/{page}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数           | 类型 | 说明                                 |
| -------------- | ---- | ------------------------------------ |
| entityName     | str  | 用户属于的业务实体的名字(若无则为"") |
| departmentName | str  | 用户属于的部门的名字(若无则为"")     |
| name           | str  | 用户的名字                           |
| feishu_name    | str  | 用户的飞书用户名                     |
| feishu_phone   | str  | 用户的飞书电话号码                   |
| email          | str  | 用户的锁定状态                       |
| lock           | int  | 用户的锁定状态                       |

此接口除鉴权操作外无其他失败响应状态

<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "data": 
  {
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email":"",
    "lock":0,
    "feishu_name":"xpy",
    "feishu_phone":114514
  }
}
```

</details>

## 管理员获取同部门下全部用户接口

**接口描述**：此接口用于管理员获取同部门下所有的用户

`[GET] /api/user_department/{session}/{department_name}/{page}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                             |
| ---- | ---- | -------------------------------- |
| data | list | 为包含该部门的所有用户信息的列表 |

**失败响应状态**

| 状态码 | 错误信息         | 说明                                  |
| ------ | ---------------- | ------------------------------------- |
| 2      | 对应的部门未找到 | 根据url路径中的部门名字找不到对应部门 |


<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "pages":1,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False,
    "email" :"" 
  },
  {
    "id": 2,
    "name": "user2",
    "password": "password123",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "character":1,
    "lock":False, 
    "email" :"" 
  }
  ]
}
```


</details>

## 一级用户获取同部门下全部用户接口

**接口描述**：此接口用于一级用户获取同部门下所有的用户

`[GET] /api/user_department_2/{session}/{department_name}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                             |
| ---- | ---- | -------------------------------- |
| data | list | 为包含该部门的所有用户信息的列表 |

**失败响应状态**

| 状态码 | 错误信息         | 说明                                  |
| ------ | ---------------- | ------------------------------------- |
| 2      | 对应的部门未找到 | 根据url路径中的部门名字找不到对应部门 |


<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :""
  },
  {
    "id": 2,
    "name": "user2",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :""
  }
  ]
}
```

</details>

## 资产管理员获取某部门下全部资产管理员接口

**接口描述**：此接口用于资产管理员获取某部门下全部资产管理员

`[GET] /api/managers_department/{session}/{department_name}`

此接口方法为GET，无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                   |
| ---- | ---- | -------------------------------------- |
| data | list | 为包含该部门的所有资产管理员信息的列表 |

**失败响应状态**

| 状态码 | 错误信息         | 说明                                  |
| ------ | ---------------- | ------------------------------------- |
| 2      | 对应的部门未找到 | 根据url路径中的部门名字找不到对应部门 |

<details>
 <summary>示例</summary>

响应

```json
{
  "code": 0,
  "data": [
  {
    "id":1,
    "name": "example_user",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :"",
    "lock":0,
  },
  {
    "id": 2,
    "name": "user2",
    "entityName" : "aba",
    "departmentName":"tsinghua",
    "email" :"",
    "lock":0,
  }
  ]
}
```

</details>

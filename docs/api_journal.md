## 系统管理员获取业务实体用户登录登出日志接口

**接口描述**：此接口用于系统管理员获取自身业务实体登录登出日志

`[GET] /api/logjournal/{session}/{entity_name}/{page}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数  | 类型 | 说明                             |
| ----- | ---- | -------------------------------- |
| pages | int  | 总页数                           |
| data  | list | 该页面的日志信息(至少为1至多为8) |

**失败响应状态**

| 状态码 | 错误信息   | 说明                                                      |
| ------ | ---------- | --------------------------------------------------------- |
| 1      | 你无此权限 | 访问日志的系统管理员不属于传入的entity_name对应的业务实体 |


<details>
 <summary>示例</summary>

响应

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

## 系统管理员获取业务实体用户关键操作日志接口

**接口描述**：此接口用于系统管理员获取自身业务实体用户关键操作日志

`[GET] /api/operationjournal/{session}/{entity_name}/{page}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数  | 类型 | 说明                             |
| ----- | ---- | -------------------------------- |
| pages | int  | 总页数                           |
| data  | list | 该页面的日志信息(至少为1至多为8) |

**失败响应状态**

| 状态码 | 错误信息   | 说明                                                      |
| ------ | ---------- | --------------------------------------------------------- |
| 1      | 你无此权限 | 访问日志的系统管理员不属于传入的entity_name对应的业务实体 |

<details>
 <summary>示例</summary>

响应

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

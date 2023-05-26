## 业务实体创建接口

**接口描述：**该接口用于超级管理员创建业务实体

`[POST]/api/entity/{session}`

**请求参数**

| 参数 | 类型 | 说明                 |
| ---- | ---- | -------------------- |
| name | str  | 创建的业务实体的名字 |

无成功响应参数，接口调用成功则用户邮箱被修改，返回Succeed

**失败响应状态**

| 状态码 | 错误信息               | 说明                                   |
| ------ | ---------------------- | -------------------------------------- |
| 2      | 已经有了重名的业务实体 | 对应名字的业务实体已经存在，此操作无效 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "name":"a"
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "info":"Succeed"
}
```
</details>
</details>


## 获取所有业务实体列表接口

**接口描述**：该接口用于超级管理员获取所有业务实体的信息

`[GET]/api/entity/{session}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明               |
| ---- | ---- | ------------------ |
| data | list | 所有业务实体的信息 |

此接口除鉴权外无其他失败响应

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
  "data":[
  {
    "id":1,
    "name":"tsinghua1",
  },
  {
    "id":2,
    "name":"tsinghua2",
  }
  ]
}

```
</details>
</details>


## 修改业务实体信息接口

**接口描述**：该接口用于超级管理员修改相关业务实体的信息(即名字)

`[PUT]/api/entity/{session}`

**请求参数**

| 参数 | 类型 | 说明                   |
| ---- | ---- | ---------------------- |
| id   | int  | 要修改的业务实体的id   |
| name | str  | 修改的业务实体的新名字 |

无成功响应参数，接口调用成功则业务实体名字被修改，返回Succeed

**失败响应状态**

| 状态码 | 错误信息             | 说明                                                           |
| ------ | -------------------- | -------------------------------------------------------------- |
| 2      | 该ID的业务实体不存在 | 给出的id错误，找不到对应业务实体                               |
| 3      | 修改信息不合理       | 检测到名字并未发生修改，或新名字对应的业务实体已经存在无法修改 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "name":"b"
}
```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "info":"Succeed"
}
```
</details>
</details>


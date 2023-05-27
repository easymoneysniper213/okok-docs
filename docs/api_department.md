## 获取业务实体下全部部门接口

**接口描述**：此接口用于管理员获取自己业务实体下下全部部门

`[GET] /api/all_departments/{session}/{entity_name}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                       |
| ---- | ---- | -------------------------- |
| data | list | 该业务实体下所有的部门列表 |

**失败响应状态**

| 状态码 | 错误信息           | 说明                                      |
| ------ | ------------------ | ----------------------------------------- |
| 1      | 指定业务实体不存在 | 根据传入的entity_name找不到对应的业务实体 |

<details>
 <summary>示例</summary>

响应

```
{
  "code":0,
  "data":[
   {
     "id":1,
     "name":"CST1",
   },
   {
     "id":3,
     "name":"CST2",
   }
]
}
```

</details>

## 获取某部门全部合法父部门接口

**接口描述**：此接口用于系统管理员获取业务实体下某部门的的全部合法父部门，即可以作为某部门的父部门的所有部门(去除了某部门现有父部门和子部门的其他部门)

`[GET] /api/valid_parent_departments/{session}/{department_name}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                             |
| ---- | ---- | -------------------------------- |
| data | list | 该业务实体下所有的合法父部门列表 |

**失败响应状态**

| 状态码 | 错误信息       | 说明                             |
| ------ | -------------- | -------------------------------- |
| 3      | 当前部门不存在 | 根据传入的部门名字找不到对应部门 |

<details>
 <summary>示例</summary>

响应

```
{
  "code":0,
  "data":[
   {
     "id":1,
     "name":"CST1",
   },
   {
     "id":3,
     "name":"CST2",
   }
]
}
```

</details>


## 创建部门接口

**接口描述**：此接口用于系统管理员创建部门

`[POST] /api/department/{session}`

**请求参数**

| 参数   | 类型 | 说明                           |
| ------ | ---- | ------------------------------ |
| entity | str  | 部门对应的业务实体的名字       |
| parent | str  | 部门的父部门，若无父部门则传"" |
| name   | str  | 部门的名字                     |

无成功响应参数，接口调用成功则该部门直接被创建，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                                             | 说明                                                  |
| ------ | ---------------------------------------------------- | ----------------------------------------------------- |
| 2      | 输入业务实体名字不合法                               | 传入业务实体名字为空串或只带空格的字符串              |
| 2      | 输入部门名字不合法                                   | 传入部门名字为空串或只带空格的字符串                  |
| 2      | 给出的业务实体未找到                                 | 根据传入的业务实体名字未找到对应的业务实体            |
| 2      | 一个业务实体下最多有两百个部门                       | 该业务实体下部门爆满超过200，若想创建请先删除无关部门 |
| 2      | 已存在同名的部门                                     | 违背了同一业务实体下不能有同名部门的原则              |
| 2      | 给定的父部门不存在                                   | 根据传入的父部门名字未找到对应的父部门                |
| 2      | 不可以将当前部门的父部门设定为另一个业务实体下的部门 | 父部门属于的业务实体并不属于该业务实体                |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "entity":"a"
  "parent":""
  "name":"清华大学计算机系"
}
```

</details>
<details>
  <summary>响应</summary>

```json
{
 "code":0,
 "info":Succeed,
}
```


</details>

</details>

## 获取根部门接口

**接口描述**：本接口用于获取业务实体下的顶层部门列表，规定只有超级管理员可以获取所有业务实体中的顶层部门列表，其他用户仅可获取自己所处业务实体的顶层部门列表。

`[GET] /api/department/{session}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                       |
| ---- | ---- | -------------------------- |
| data | list | 业务实体下所有顶层部门列表 |

此接口除鉴权外无其他失败响应状态


<details>
 <summary>示例</summary>

响应

```json
{
  "code":0
  "data":[
  {
    "id":1,
    "name":"tsinghua1",
    "entityName":"tsinghua",
    "userNumber":1,
    "subDepartmentNumber":2,
  },
  {
    "id":2,
    "name":"tsinghua2",
    "entityName":"tsinghua",
    "userNumber":1,
    "subDepartmentNumber":2,
  },
  ]
}
```


</details>

## 修改部门信息接口

**接口描述**：此接口用于系统管理员修改业务实体下所有部门信息

`[PUT] /api/department/{session}`

**请求参数**

| 参数   | 类型 | 说明                                                                                 |
| ------ | ---- | ------------------------------------------------------------------------------------ |
| id     | int  | 修改部门的id                                                                         |
| parent | str  | 若要修改部门的父部门，则传入父部门名字，若不需要则传入之前的父部门名字(若无则为空串) |
| name   | str  | 若要修改部门的名字，则传入新的部门名字，若不需要则传入之前的名字                     |

无成功响应参数，接口调用成功则该部门信息被修改成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                           | 说明                                                                     |
| ------ | ---------------------------------- | ------------------------------------------------------------------------ |
| 2      | 输入部门名不合法                   | 传入部门名字为空串或只带空格的字符串                                     |
| 2      | 该ID的部门不存在                   | 根据传入的id找不到相关部门                                               |
| 2      | 已存在同名的部门                   | 新名字对应的部门已经在该业务实体下存在                                   |
| 2      | 给出的父部门不存在                 | 根据传入的父部门名字未找到对应的父部门                                   |
| 2      | 不可以将部门移至另一个业务实体下   | 父部门属于的业务实体与部门的业务实体不同，设定父部门只能在当前业务实体下 |
| 2      | 不可以将该部门的子部门设定为父部门 | 新的父部门不可属于部门的子部门，否则出现父子循环关系                     |



<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1
  "parent":""
  "name":"清华大学计算机系"
}
```



</details>
<details>
  <summary>响应</summary>

```json
{
  "code": 0,
  "info":Succeed,
}
```


</details>

</details>

## 获取子部门信息接口

**接口描述**：该接口用于获取一个部门的下一层子部门，若用户不为超级管理员，则必须保证访问的部门与其所属业务实体一致，超级管理员则无此限制。

`[GET] /api/sub_department/{session}/{department_name}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                       |
| ---- | ---- | -------------------------- |
| data | list | 业务实体下所有顶层部门列表 |

**失败响应状态**

| 状态码 | 错误信息           | 说明                                           |
| ------ | ------------------ | ---------------------------------------------- |
| 1      | 给定的父部门不存在 | 根据url路径中的department_name找不到对应父部门 |


<details>
 <summary>示例</summary>

响应

```json
{
  "code":0
  "data":[
  {
    "id":1,
    "name":"tsinghua1",
    "userNumber":3,
    "subDepartmentNumber":1,
  },
  {
    "id":2,
    "name":"tsinghua2",
    "userNumber":3,
    "subDepartmentNumber":1,
  },
  ]
}
```


</details>

## 删除部门信息接口

**接口描述**：此接口用于系统管理员删除某个部门，规定只能删除叶节点，且该部门下不可以有用户。

`[DELETE] /api/department/{session}/{department_name}`

此接口方法为DELETE，故无请求参数

无成功响应参数，接口调用成功则部门直接被删除，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                 | 说明                                               |
| ------ | ------------------------ | -------------------------------------------------- |
| 2      | 该名称的部门不存在       | 根据url路径传入的department_name找不到要删除的部门 |
| 2      | 不可以删除非叶节点的部门 | 若该部门有子部门，则规定不可删除                   |
| 2      | 不可以删除有用户的部门   | 若该部门有用户，则规定不可删除                     |
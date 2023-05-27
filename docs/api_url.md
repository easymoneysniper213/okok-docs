## 获取url的接口

**接口描述**：此接口用于用户获取自己能看到的url

`[GET] /api/url/{session}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                    |
| ---- | ---- | ----------------------- |
| data | list | 包含url所有数据项的列表 |

**失败响应状态**

| 状态码 | 错误信息                  | 说明                                            |
| ------ | ------------------------- | ----------------------------------------------- |
| 7      | 超级管理员不能得到URL列表 | URL列表只限普通用户、资产管理员与系统管理员查看 |

<details>
 <summary>示例</summary>

响应

```json
{
 "code":0,
 "data":[
{ 
   "id":1,
   "url":https://baidu.com,
   "name":"百度",
   "authority_level":1,
   "entity":"tsinghua",
},
]
}
```


</details>

## 修改url的接口

**接口描述**：此接口用于系统管理员修改不同等级用户能看到的url

`[PUT] /api/url/{session}`

请求参数为一个长度固定为5的list，list中每一项包含url列表的所有数据项，若想更改的项数少于5则请求体内为空值

无成功响应参数，接口调用成功则相关第三方url被直接修改，用户可查看并返回Succeed

**失败响应状态**

| 状态码 | 错误信息             | 说明                                               |
| ------ | -------------------- | -------------------------------------------------- |
| 7      | url列表长度错误      | url列表长度不为5                                   |
| 5      | 检测到冲突url        | url出现重复                                        |
| 2      | 给出的业务实体不存在 | 根据请求体内传入的业务实体名字找不到对应的业务实体 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{[
  {
    "entity":"P",
    "url":"pornhub.com",
    "name":"PornHub"
    "character":1
  },
  {
    "entity":"P",
    "url":"pornhub.com",
    "name":"PornHub"
    "character":1
  },
  {
    "entity":"",
    "url":"",
    "name":""
    "character":1
  },
  {
    "entity":"P",
    "url":"pornhub.com",
    "name":"PornHub"
    "character":1
  },
  {
    "entity":"P",
    "url":"pornhub.com",
    "name":"PornHub"
    "character":1
  },
]}
```


</details>
<details>
  <summary>响应</summary>

```json
{
 "code":0,
 "info":Succeed
}
```


`</details>`

</details>

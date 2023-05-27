## 创建导出任务接口

**接口描述**：此接口用于创建导出资产任务

`[POST] /api/export_task/{session}`

**请求参数**

请求参数为一个list，该list包含需要导出的资产id。

无成功响应参数，接口调用成功则创建导出任务，配合 `[GET] /api/export_task/{session}/{id}`API即可查看导出的资产信息。

无失败响应状态，导出任务一定成功，对导出失败的资产加以记录，但该API接口一定成功退出。

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>


```json
{
  [
    1,
    2,
    3,
  ]
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

## 获取指定导出任务接口

**接口描述**：此接口用于查询指定id的导出异步任务信息

`[GET] /api/export_task/{session}/{id}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                       |
| ---- | ---- | ------------------------------------------ |
| data | list | 一个列表，列表信息为所有成功导出的资产信息 |

**失败响应状态**

| 状态码 | 错误信息                                | 说明                                   |
| ------ | --------------------------------------- | -------------------------------------- |
| 4      | 该API只可用于查看导出异步任务的成功记录 | 根据id索引到的异步任务信息不为导出任务 |

<details>
 <summary>示例</summary>

响应

```json
{
 "code":0,
 "data":[
    "id": 1,
    "parentName": "",
    "name": "chairs,
    "assetClass": 0,
    "userName": liusn
    "price": 10.00,
    "description": "",
    "position": "",
    "expire": 0,
    "count": 10,
    "assetTree": "默认分类",
    "departmentName": "CST",
    "create_time": 2023-05-27,
    "deadline": 10,
    "initial_price": 10.00,
    "warning_amount": -1,
    "warning_date": -1,
    "expire_date": 10,
     "status": 1,
  }
  ]
}
```


</details>

## 获取业务实体下的异步任务接口

**接口描述**：此接口用于资产管理员获取指定业务实体下的异步任务列表

`[GET] /api/async_task/{session}`

此接口方法为GET，故无请求参数

**成功返回参数**

| 参数 | 类型 | 说明                                 |
| ---- | ---- | ------------------------------------ |
| data | list | 一个列表，列表信息为异步任务相关信息 |

此接口除鉴权操作外无其他失败响应状态

<details>
 <summary>示例</summary>

响应

```json
{
 "code":0,
 "data":[
   {
     "id": 1,
     "manager": "liusn",
     "create_time": "2023-05-26 19:28:33",
     "number_need": 100,
     "number_succeed": 98,
     "finish": 2,
     "port_type": 1,
   },
   {
     "id": 2,
     "manager": "liusn1",
     "create_time": "2023-05-26 19:28:26",
     "number_need": 10,
     "number_succeed": 10,
     "finish": 1,
     "port_type": 1,
   },
]
}
```

</details>

## 创建异步任务导入资产接口

**接口描述**：此接口用于资产管理员通过异步任务创建资产

`[POST] /api/asset/{session}`

请求参数为一个list，该list包含需要创建的资产的信息

无成功响应参数，接口调用成功则任务直接创建，返回Succeed，可在任务列表中查看

无失败响应状态，导入任务一定成功，对导入失败的资产加以记录，导入成功的资产直接创建，但该API接口一定成功退出。


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
[
{
 "name":"chairs",
 "parent":"",
 "assetClass":0,
 "user":liusn,
 "price":10.0,
 "description":"",
 "position":"",
 "expire":0,
 "count":10,
 "assetTree":"默认分类",
 "department":"CST",
 "deadline":10,
},
]
}
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

</details>

</details>

## 获取导入失败任务接口

**接口描述**：此接口用于资产管理员获取指定id的导入异步任务的失败信息

`[GET] /failed_task/{session}/{id}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                                   |
| ---- | ---- | ------------------------------------------------------ |
| data | list | 包含所有导入失败资产的全部传入信息，附带失败信息的列表 |

**失败响应状态**

| 状态码 | 错误信息                        | 说明                                     |
| ------ | ------------------------------- | ---------------------------------------- |
| 6      | 对应id的异步任务不存在          | 根据传入的id找不到对应导入异步任务       |
| 8      | 不能通过此API获取导出的异步任务 | 根据传入的id定位到的异步任务不为导入任务 |


<details>
 <summary>示例</summary>

响应

```
{
[
{
 "name":"chairs",
 "parent":"",
 "assetClass":0,
 "user":liusn,
 "price":10.0,
 "description":"",
 "position":"",
 "expire":0,
 "count":0,
 "assetTree":"默认分类",
 "department":"CST",
 "deadline":10,
 "message":"资产数量不可小于1",
},
]
}
```


</details>

## 重新评测失败的导入异步任务接口

**接口描述**：此接口用于重新评测某失败的导入异步任务

`[PUT] /failed_task/{session}/{id}`

请求参数为一个list，为之前 `[GET] /failed_task/{session}/{id}`API返回的失败信息修改后的列表，代表重新评测的资产信息(必须与导入失败的资产数量相同)

无成功响应参数，接口调用成功则任务被重新评测，返回Succeed，可在任务列表中查看

**失败响应状态**

| 状态码 | 错误信息                                           | 说明                                     |
| ------ | -------------------------------------------------- | ---------------------------------------- |
| 6      | 对应id的异步任务不存在                             | 根据传入的id找不到对应导入异步任务       |
| 8      | 不能通过此API重新评测某导出任务                    | 根据传入的id定位到的异步任务不为导入任务 |
| 8      | 新传入的POST资产信息一定要与之前的失败信息长度相同 | 所有失败信息并未被全部重新评测           |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
[
{
 "name":"chairs",
 "parent":"",
 "assetClass":0,
 "user":liusn,
 "price":10.0,
 "description":"",
 "position":"",
 "expire":0,
 "count":10,
 "assetTree":"默认分类",
 "department":"CST",
 "deadline":10,
},
]
}
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


</details>

</details>

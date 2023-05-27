## 获取部门下全部资产状态信息接口

**接口描述**：此接口用于资产管理员获取该部门下全部资产状态信息

`[GET] /count_status_asset/{session}`

此接口方法为GET，故无请求参数

**成功响应参数**

| 参数 | 类型 | 说明                                                                                    |
| ---- | ---- | --------------------------------------------------------------------------------------- |
| data | list | 部门下全部资产状态信息列表，列表共8项，前4项代表条目型资产状态，后4项代表数量型资产状态 |

此接口除鉴权操作外无其他失败响应状态

<details>
 <summary>示例</summary>

响应

```json
{
  "code":0
  "data":
  [
    {
      "type": "expire",
      "count": 1, 
    },
    {
      "type": "idle",
      "count": 2, 
    },
    {
      "type": "use",
      "count": 3, 
    },
    {
      "type": "maintain",
      "count": 4, 
    },
    {
      "type": "expire",
      "count": 1, 
    },
    {
      "type": "idle",
      "count": 2, 
    },
    {
      "type": "use",
      "count": 3, 
    },
    {
      "type": "maintain",
      "count": 4, 
    },
   ]
}
```

</details>

## 获取资产价值曲线接口

**接口描述**：本接口用于获取某一资产的信息变化情况

`[GET] /info_curve/{session}/{asset_id}/{visible_type}`

此接口方法为GET，故无请求参数，url路径中 ``visible_type``为1、2、3时分别表示获取近7天、近30天、全部时间的信息

**成功响应参数**

| 参数 | 类型 | 说明                             |
| ---- | ---- | -------------------------------- |
| data | list | 一个包含资产指定时间段信息的列表 |

``cur_price``为该时刻价格，``cur_status``为该时刻状态，``cur_count``为该时刻数量，``cur_time``为时刻

**失败响应状态**

| 状态码 | 错误信息           | 说明                              |
| ------ | ------------------ | --------------------------------- |
| 5      | 检测到错误可见类型 | ``visible_type``不为1、2、3中之一 |
| 4      | 未找到目标资产     | 根据url路径中的id找不到对应资产   |

<details>
 <summary>示例</summary>

响应

```json
{
  "code":0
  "data":[
  {
    "cur_price": 11.00,
    "cur_status": 1,
    "cur_count": 5,
    "cur_time": xx,
  },
  {
    "cur_price": 11.00,
    "cur_status": 1,
    "cur_count": 5,
    "cur_time": xx,
  },
  ......
  ]
}
```

</details>

## 获取部门下全部资产数目和价值变化曲线接口

**接口描述**：此接口用于资产管理员获取部门下全部资产数目和价值变化曲线

`[GET] /count_price_curve/{session}/{visible_type}`

此接口方法为GET，故无请求参数，url路径中 ``visible_type``为1、2、3时分别表示获取近7天、近30天、全部时间的信息

**成功响应参数**

| 参数        | 类型 | 说明                 |
| ----------- | ---- | -------------------- |
| data_item   | list | 条目型资产的变化列表 |
| data_amount | list | 数量型资产的变化列表 |
| data_total  | list | 全部资产的变化列表   |

**失败响应状态**

| 状态码 | 错误信息           | 说明                              |
| ------ | ------------------ | --------------------------------- |
| 5      | 检测到错误可见类型 | ``visible_type``不为1、2、3中之一 |


<details>
 <summary>示例</summary>

响应

```json
{
  "code":0
  "data_item":[
  {
    "cur_count": 123123,
    "cur_price": 200019.51
    "cur_time":xx,
  },
  {
    "cur_count": 123123,
    "cur_price": 200019.51,
    "cur_time":xx,
  },
  ......
  ]
  "data_amount":[
  {
    "cur_count": 123123123,
    "cur_price": 529.00
    "cur_time":xx,
  },
  {
    "cur_count": 123123123,
    "cur_price": 529.00
    "cur_time":xx,
  },
  ......
  ]
  "data_total":[
  {
    "cur_count": 123246246,
    "cur_price": 200548.51,
    "cur_time":xx,
  },
  {
    "cur_count": 123246246,
    "cur_price": 200548.51
    "cur_time":xx,
  },
  ......
  ]
}
```



</details>

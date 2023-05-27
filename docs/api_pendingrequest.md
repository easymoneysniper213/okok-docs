## 创建请求接口

**接口描述**：此接口用于用户向资产管理员发送请求

`[POST] /api/pending_request/{session}`

**请求参数**

| 参数        | 类型 | 说明                                                                     |
| ----------- | ---- | ------------------------------------------------------------------------ |
| initiator   | str  | 请求的发起人名字(用户)                                                   |
| participant | str  | 请求的接收者名字(资产管理员)                                             |
| target      | str  | 请求涉及到的目标人名字(资产转移时表示资产转移方，其他情况不需要置为空串) |
| asset_id    | int  | 审批涉及到的资产的id                                                     |
| type        | int  | 审批涉及到的操作类型                                                     |
| count       | int  | 审批涉及到的数量型资产的数量(若为条目型资产则强制为1)                    |

无成功响应参数，接口调用成功则审批单直接发送给资产管理员，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                                           | 说明                                                         |
| ------ | -------------------------------------------------- | ------------------------------------------------------------ |
| 2      | 提交请求的用户不存在                               | 根据传入的initiator找不到对应用户                            |
| 2      | 提交请求的用户的角色不合法                         | 提交请求一方不为普通用户                                     |
| 3      | 通过请求的用户不存在                               | 根据传入的participant找不到对应用户                          |
| 8      | 通过请求的用户的角色不合法                         | 接收请求一方不为资产管理员，或二者不在同一个业务实体下       |
| 9      | 未找到目标用户                                     | 根据传入的target找不到对应用户                               |
| 8      | 通过资产的用户的角色不合法                         | 请求涉及到的目标人不为普通用户，或二者不在同一业务实体下     |
| 5      | 申请类型不合法                                     | 申请类型type不为1、2、3、4之一                               |
| 4      | 所涉及的资产不存在                                 | 根据传入的资产id找不到对应资产                               |
| 3      | f"资产{tar_asset.name}不是数量型资产，请重新检查"  | 资产类型为条目型资产但是数量却不为1                          |
| 4      | f"资产{tar_asset.name}数量不足"                    | 数量型资产的现有数量小于count                                |
| 250    | 如果您不想获得此资产，请什么都不做，而不是浪费时间 | count传入不合法，count不为正整数，无意义                     |
| 6      | 不要那么操之过急，操之过急也没用                   | 检测到多个冲突审批单存在，说明用户点击过快，不会提交多次审批 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "initiator":"sbsbsb",
  "participant":"114514",
  "target":"lyq",
  "asset_id":"1",
  "type":1,
  "count":1,
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

## 返回请求结果接口

**接口描述**：此接口用于资产管理员向用户发送请求结果

`[PUT] /api/return_pending_request/{session}`

**请求参数**

| 参数   | 类型 | 说明               |
| ------ | ---- | ------------------ |
| id     | int  | 返回的审批请求的id |
| result | int  | 审批结果           |

无成功响应参数，接口调用成功则审批单直接返回给用户，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                       | 说明                                                         |
| ------ | ------------------------------ | ------------------------------------------------------------ |
| 1      | 资产管理员下的该请求不存在     | 根据传入的id找不到该请求，或该id对应的请求不在此资产管理员下 |
| 7      | 该审批单已失效，无法通过此申请 | 由于资产数量等在审批通过前发生变更，导致此次审批无法通过     |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "result":1,
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

## 获取待处理请求列表接口

**接口描述**：此接口用于资产管理员获取待处理请求列表

`[GET] /api/pending_request_list/{session}/{asset_manager_name}`

此接口方法为GET，故无请求参数

**成功响应参数**

一个由审批单组成的列表data，其中每一项包含以下项信息

| 参数            | 类型 | 说明                                           |
| --------------- | ---- | ---------------------------------------------- |
| id              | int  | 审批请求的id                                   |
| initiatorName   | str  | 请求发起用户的名字                             |
| participantName | str  | 请求接收方资产管理员的名字                     |
| targetName      | str  | 请求涉及到的目标用户的名字                     |
| assetName       | str  | 请求涉及到的资产名字                           |
| assetID         | int  | 请求涉及到的资产id                             |
| type            | int  | 请求涉及到的操作类型                           |
| result          | int  | 请求结果                                       |
| request_time    | str  | 请求发起的时间                                 |
| review_time     | str  | 请求被返回的时间(若还未返回则默认为无限远时间) |
| count           | int  | 请求涉及到的资产数量                           |
| valid           | int  | 请求的有效性                                   |

**失败响应状态**

| 状态码 | 错误信息                   | 说明                                  |
| ------ | -------------------------- | ------------------------------------- |
| 2      | 对应名字的资产管理员不存在 | 根据url传入的名字找不到对应资产管理员 |

<details>
 <summary>示例</summary>

响应

```json
{
 "code":0,
 "data":[
         {
          "id":1,
          "initiatorName":"liusn",
          "participantName":"xpy",
          "targetName":"",
          "assetName":"chairs",
          "assetID":23,
          "type":1,
          "result":0,
          "request_time":"2023-05-27 15:30:45",
          "review_time":"2023-05-27 15:32:45",
          "count":12,
          "valid":1,
         },
         {
          "id":2,
          "initiatorName":"liusn",
          "participantName":"xpy",
          "targetName":"",
          "assetName":"tables",
          "assetID":25,
          "type":2,
          "result":1,
          "request_time":"2023-05-26 15:30:45",
          "review_time":"2023-05-26 15:32:45",
          "count":15,
          "valid":1,
          },
        ]
}
```


</details>

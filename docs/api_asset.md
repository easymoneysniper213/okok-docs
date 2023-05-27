## 创建资产接口

**接口描述**：此接口用于资产管理员创建资产

`[POST] /api/post_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| parent | int  | 该资产父资产的id |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| user   | str  | 该资产的挂账人              |
| price   | double  | 该资产的价值               |
| description  | str  | 该资产的描述               |
| expire  | str  | 该资产是否被清退               |
| count  | int  | 数量型资产的数量               |
| assetTree  | str  | 该资产挂载的资产分类树节点              |
| department  | str  | 该资产挂载的部门名              |
| deadline  | int  | 该资产距离到期的时间             |
| richtext  | str  | 该资产的富文本描述             |

**成功响应参数**

无成功响应参数，接口调用成功则创建资产成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 5     | 仅数量型资产的数量可大于 1           | 仅数量型资产的数量可大于 1 |
| 250     | 资产数量不可小于 1 | 资产数量不可小于 1 |
| 1     | 对应部门不存在 | 输入的部门名称对应部门不存在 |
| 1     | 未找到指定层级分类 | 未找到指定资产分类树节点 |
| 2     | 资产类别与层级分类不匹配 | 即数量型资产挂载到条目型资产分类树节点下，反之亦然 |
| 1     | 父资产不符合规范 | 父资产必须为条目型，且不能为本身的子资产 |
| 1     | 未找到该资产挂账人 | 未找到该资产挂账人 |
| 2     | 指定资产挂账人不处于当前部门 | 指定资产挂账人不处于当前部门 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
  "parent":1, 
  "name":"a",
  "assetClass":1,
  "user":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "department":"y",
  "deadline":5,
  "richtext":"",
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

## 修改资产信息接口

**接口描述**：此接口用于资产管理员修改资产信息

`[PUT] /api/asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| parent | int  | 该资产父资产的id |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| user   | str  | 该资产的挂账人              |
| price   | double  | 该资产的价值               |
| description  | str  | 该资产的描述               |
| expire  | str  | 该资产是否被清退               |
| count  | int  | 数量型资产的数量               |
| assetTree  | str  | 该资产挂载的资产分类树节点              |
| department  | str  | 该资产挂载的部门名              |
| deadline  | int  | 该资产距离到期的时间             |
| richtext  | str  | 该资产的富文本描述             |

**成功响应参数**

无成功响应参数，接口调用成功则修改资产信息成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 20     | 资产和其父资产不可相同           | 资产和其父资产不可相同 |
| 5     | 仅数量型资产的数量可大于 1           | 仅数量型资产的数量可大于 1 |
| 700     | 资产数目不可以小于等于0 | 资产数目不可以小于等于0  |
| 2     | 你不能修改资产的清退状态 | 你不能修改资产的清退状态 |
| 2     | 你不能修改资产的类型 | 你不能修改资产的类型 |
| 2     | 无法修改维保中的资产信息 | 无法修改维保中的资产信息 |
| 2     | 你不能修改资产所属的部门 | 你不能修改资产所属的部门 |
| 2     | 无法在维护资产信息中修改资产所有者 | 只能通过申请转移、退库、领用等进行所有者的转移 |
| 1     | 对应部门不存在 | 输入的部门名称对应部门不存在 |
| 1     | 未找到指定层级分类 | 未找到指定资产分类树节点 |
| 2     | 资产类别与层级分类不匹配 | 即数量型资产挂载到条目型资产分类树节点下，反之亦然 |
| 1     | 父资产不符合规范 | 父资产必须为条目型，且不能为本身的子资产 |
| 8     | 已经有同名资产存在 | 修改名称时已经有同名资产存在 |
| 1     | 未找到该资产挂账人 | 未找到该资产挂账人 |
| 2     | 指定资产挂账人不处于当前部门 | 指定资产挂账人不处于当前部门 |
| 20     | 没有作修改 | 没有对资产作任何修改 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
  "id":1,
  "parent":1, 
  "name":"a",
  "assetClass":1,
  "user":"xxx",
  "price":1.0,
  "description":"",
  "position":"",
  "expire":0,
  "count":1,
  "assetTree":"all_asset",
  "department":"y",
  "deadline":5,
  "richtext":"",
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

## 用户获取持有资产信息接口

**接口描述**：此接口用于一级用户获取自己的资产信息

`[GET] /api/asset_user_list/{session}/{page}`

**请求参数**

无

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| parentName | str  | 该资产父资产的名称 |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| userName   | str  | 该资产的挂账人名称              |
| price   | double  | 该资产的现价值               |
| description  | str  | 该资产的描述               |
| expire  | str  | 该资产是否被清退               |
| count  | int  | 数量型资产的数量               |
| assetTree  | str  | 该资产挂载的资产分类树节点              |
| departmentName  | str  | 该资产挂载的部门名              |
| create_time  | datetime  | 该资产的创建日期              |
| deadline  | int  | 该资产距离到期的时间             |
| initial_price  | double  | 该资产的初始价值            |

**失败响应状态**

除鉴权错误外，无其他失败响应状态

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
  }
  ]
}
```
</details>
</details>




## 用户获取未领用的资产接口

**接口描述**：此接口用于一级用户获取指定资产管理员名下未被领用的资产信息

`[GET] /api/unallocated_asset/{session}/{asset_manager_name}/{page}`

**请求参数**

无

url路径中的asset_manager_name表示搜索的资产管理员的姓名

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| parentName | str  | 该资产父资产的名称 |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| userName   | str  | 该资产的挂账人名称              |
| price   | double  | 该资产的现价值               |
| description  | str  | 该资产的描述               |
| expire  | str  | 该资产是否被清退               |
| count  | int  | 数量型资产的数量               |
| assetTree  | str  | 该资产挂载的资产分类树节点              |
| departmentName  | str  | 该资产挂载的部门名              |
| create_time  | datetime  | 该资产的创建日期              |
| deadline  | int  | 该资产距离到期的时间             |
| initial_price  | double  | 该资产的初始价值            |

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 未找到目标资产管理员         | 未找到目标资产管理员 |
| 6     | 不要向非自己部门的资产管理员请求领用资产         | 一级用户不可以向非自己部门的资产管理员请求领用资产 |
| 7     | 目标不是资产管理员         | 请求目标不是资产管理员 |



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
  }
  ]
}
```
</details>
</details>

## 调拨资产接口

**接口描述**：此接口用于资产管理员向指定资产管理员调拨资产

`[PUT] /api/allot_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 要调拨的资产的数量               |
| name  | str  | 该资产要调拨到的资产管理员名称              |

**成功响应参数**

无成功响应参数，接口调用成功则调拨资产成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 指定ID的资产不存在 | 操作的资产不存在 |
| 2     | 指定名称的资产管理员不存在 | 操作指定的资产管理员不存在 |
| 2     | 你只能调拨资产给资产管理员 | 你只能调拨资产给资产管理员 |
| 2     | 指定名字的资产树结点不存在 | 资产转移时指定名字的资产树结点不存在 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |
| 529    | 请不要浪费时间? | 未进行任何调拨操作 |



<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "cnt":1,
  "name":"a",
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

## 转移资产接口

**接口描述**：此接口用于一级用户向另一个一级用户转移资产

`[PUT] /api/transfer_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 要转移的资产的数量               |
| sender  | str  | 该资产转移前的所有者姓名             |
| target  | str  | 该资产需要转移到的用户姓名             |
| request_id  | int | 该资产转移请求对应的id             |

**成功响应参数**

无成功响应参数，接口调用成功则资产转移成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 250     | 如果不要转移资产，请勿浪费时间 | 输入资产数量小于等于0 |
| 2     | 指定名称的发送者不存在 | 操作指定的发送者不存在 |
| 2     | 只有用户可以进行资产转移 | 只有一级用户可以进行资产转移 |
| 2     | 指定名称的目标用户不存在 | 指定名称的目标用户不存在 |
| 2     | 目标用户角色必须为一级用户 | 目标用户角色必须为一级用户 |
| 501    | 该操作非法 | 对应的资产转移请求不合法 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |
| 529    | 没有作资产的转移 | 没有作资产的转移 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
    "id":1,
    "sender":"aba",
    "target":"bab",
    "count":2,
    "request_id":3,
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


## 维保资产接口

**接口描述**：此接口用于资产管理员维保资产

`[PUT] /api/maintain_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 维保完成后返还数量，仅可等于交付维保的数量              |
| new_deadline  | int  | 新的期限，与当前日期之和不可小于原到期时间           |
| new_price  | double  | 新的价格，不可超过initial_price             |
| name  | str | 维保完成后交还的用户名称             |

**成功响应参数**

无成功响应参数，接口调用成功则资产维保成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 250     | 如果不要维保资产，请勿浪费时间 | 输入资产数量小于等于0 |
| 2     | 只有用户可以进行资产维保 | 只有一级用户可以进行资产维保 |
| 2     | 该资产维保的申请用户不存在 | 指定名称的目标用户不存在 |
| 2     | 目标用户角色必须为一级用户 | 目标用户角色必须为一级用户 |
| 2     | 指定信息的资产不存在 | 指定信息的资产不存在 |
| 5     | 新价格不可以比初始价格高 | 维保后新价格不可以比初始价格高 |
| 6     | 新的截止日期不可以早于原先的截止日期 | 维保后新的截止日期不可以早于原先的截止日期 |
| 4     | 维保资产数目错误 | 维保资产数目错误 |
| 501    | 该操作非法 | 对应的资产转移请求不合法 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "name":"aba",
  "new_deadline":2, 
  "new_price":1.00 ,
  "count":2,
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

## 清退资产接口

**接口描述**：此接口用于资产管理员清退资产

`[PUT] /api/expire_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 清退的该资产的数量              |

**成功响应参数**

无成功响应参数，接口调用成功则资产清退成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 250     |请不要浪费时间 | 输入资产数量小于等于0 |
| 1     | 该ID的资产不存在 | 该ID的资产不存在 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "count":2,
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

## 领用资产接口

**接口描述**：此接口用于资产管理员为某个一级用户分配其申请领用的资产

`[PUT] /api/receive_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 用户领用的资产数量              |
| name  | str | 领用资产的用户名称             |
| request_id  | int | 该资产领用请求对应的id             |

**成功响应参数**

无成功响应参数，接口调用成功则资产领用成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 250     | 如果不要领用资产，请勿浪费时间 | 输入资产数量小于等于0 |
| 2     | 只有用户可以进行资产领用 | 只有一级用户可以进行资产领用 |
| 2     | 该资产领用的申请用户不存在 | 指定名称的目标用户不存在 |
| 2     | 目标用户角色必须为一级用户 | 目标用户角色必须为一级用户 |
| 2     | 指定信息的资产不存在 | 指定信息的资产不存在 |
| 501    | 该操作非法 | 对应的资产领用请求不合法 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "name":"aba",
  "count":2,
  "request_id":1,
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

## 退库资产接口

**接口描述**：此接口用于资产管理员回收某个一级用户申请退库的资产

`[PUT] /api/return_asset/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| count  | int  | 用户退库的资产数量             |
| name  | str | 要求退库的用户名称             |
| request_id  | int | 该资产退库请求对应的id             |

**成功响应参数**

无成功响应参数，接口调用成功则资产领用成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 250     | 如果不要退库资产，请勿浪费时间 | 输入资产数量小于等于0 |
| 2     | 只有用户可以进行资产退库 | 只有一级用户可以进行资产退库 |
| 2     | 该资产退库的申请用户不存在 | 指定名称的目标用户不存在 |
| 2     | 目标用户角色必须为一级用户 | 目标用户角色必须为一级用户 |
| 2     | 指定信息的资产不存在 | 指定信息的资产不存在 |
| 501    | 该操作非法 | 对应的资产退库请求不合法 |
| 3     | 资产{asset.name}不是数量型资产，请再次检查 | 请求的条目型资产数目大于1 |
| 4     | 资产{asset.name}数量不足 | 请求的资产数目不足 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "id":1,
  "name":"aba",
  "count":2,
  "request_id":1,
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

## 获取某用户名下资产接口

**接口描述**：此接口用于资产管理员获取某用户名下的所有资产信息

`[GET] /asset/{session}/{user_name}/{page}`

**请求参数**

无
url路径中的user_name表示需要获取资产的用户的姓名

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| parentName | str  | 该资产父资产的名称 |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| userName   | str  | 该资产的挂账人名称              |
| price   | double  | 该资产的现价值               |
| description  | str  | 该资产的描述               |
| expire  | str  | 该资产是否被清退               |
| count  | int  | 数量型资产的数量               |
| assetTree  | str  | 该资产挂载的资产分类树节点              |
| departmentName  | str  | 该资产挂载的部门名              |
| create_time  | datetime  | 该资产的创建日期              |
| deadline  | int  | 该资产距离到期的时间             |
| initial_price  | double  | 该资产的初始价值            |

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 未找到目标用户        | 未找到目标用户 |
| 7     | 目标不是用户        | 请求目标不是用户 |



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
  }
  ]
}
```
</details>
</details>

## 获取维保资产列表接口

**接口描述**：此接口用于资产管理员获取该部门下所有正在维保的资产

`[GET] /get_maintain_list/{session}`

**请求参数**

无
url路径中的user_name表示需要获取资产的用户的姓名

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| assetID | int  | 该资产的id |
| requestID | int  | 该维保请求的id |
| assetName   | str  | 该资产的名称               |
| assetPrice  | double  | 该资产的现价值               |
| assetInitialPrice  | double  | 该资产的初始价值            |
| assetAmount  | int  | 该资产的数量               |
| assetDeadline   | str  | 该资产到期的日期              |
| assetOwner  | str  | 该资产的挂账人名称              |
| min_ddl_days  | str  | 该资产的距离到期的时间               |


**失败响应状态**

除了鉴权错误响应外无其他失败响应

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
    "assetID": 1,
    "requestID": 1,
    "assetName": "a",
    "assetPrice": 1.0,
    "assetInitialPrice": 2.0,
    "assetAmount": 100,
    "assetDeadline": "2022-11-11",
    "assetOwner": "an",
    "min_ddl_days": "29",
    }
  ]
}
```
</details>
</details>

## 获取资产历史列表接口

**接口描述**：此接口用于资产管理员获取某指定资产的指定类型的资产操作历史列表

`[GET] /asset_query/{session}/{id}/{history_type}`

**请求参数**

无

url路径中的id表示需要获取资产的id,history_type表示需要获取资产历史的类型(转移、领用、退库、维保等)

type为1表示查询转移历史（包括转移到以及被转移的历史），type为2表示查询维保历史（包括交付维保以及维保结束交付的历史），type为3表示查询领用历史（包括被领用以及领用的历史），type为4表示查询退库历史，type为5表示查询全部历史

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| time | datetime  | 该资产历史信息的时间 |
| type | str  | 该资产历史的类型 |
| message  | str  | 该资产历史的具体信息               |


**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 6     | type类型不正确          | type必须为1、2、3、4、5其中之一 |
| 5    | 对应id的资产找不到          | 对应id的资产找不到 |



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
  "data":[{
    "time":2023-05-06 13:58:33,
    "type":"转移",
    "message":"The assets are transferred from assets with user sb",
  },
  {
    "time":2023-05-06 12:43:44,
    "type":"维保",
    "message":"The assets are delivered to asset manager sb for maintenance",
  },
  {
    "time":2023-05-06 12:40:18,
    "type":"领用",
    "message":"Assets are claimed by user sb "
  },
  ]
}
```
</details>
</details>

## 获取资产图片链接接口

**接口描述**：此接口用于资产管理员获取某指定资产的图片链接和富文本内容

`[GET] /picture/{session}/{asset_id}`

**请求参数**

无

url路径中的asset_id表示需要获取资产的id

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| links | str  | 该资产的图片链接 |
| richtext | str  | 该资产的富文本描述 |



**失败响应状态**

除了鉴权错误响应外无其他失败响应

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
        "links":"http://www.baidu.com",
        "richtext":"aba" 
    }
  ]
}
```
</details>
</details>

## 修改资产图片链接接口

**接口描述**：此接口用于资产管理员修改某指定资产的图片链接和富文本内容

`[PUT] /picture/{session}/{asset_id}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| links | str  | 该资产的图片链接 |
| richtext | str  | 该资产的富文本描述 |

url路径中的asset_id表示需要修改资产的id

**成功响应参数**

无成功响应参数，接口调用成功则资产领用成功，返回Succeed

**失败响应状态**

除了鉴权错误响应外无其他失败响应

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
    "links":"http://www.baidu.com",
    "richtext":"aba" 
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

## 修改告警策略接口

**接口描述**：此接口用于资产管理员修改某指定资产告警策略

`[PUT] /warning/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| date | int  | 该资产的告警日期 |
| amount | int  | 该资产的告警数量 |
| id | int  | 该资产的id |

**成功响应参数**

无成功响应参数，接口调用成功则资产领用成功，返回Succeed

**失败响应状态**


| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 1     | 该资产不存在          | 对应id的资产不存在 |
| 3    | 条目型资产不可以设置数目          | 条目型资产不可以设置数目 |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "date":1,
  "amount":8,
  "id":1,
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


## 获取告警策略接口

**接口描述**：此接口用于资产管理员获取业务实体下全部资产告警策略

`[GET] /warning_get/{session}/{page}`

**请求参数**

无

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| price   | double  | 该资产的现价值               |
| description  | str  | 该资产的描述               |
| count  | int  | 数量型资产的数量               |
| warning_date  | int  | 该资产的告警日期(若未设置则默认为-1)         |
| warning_amount  | int  | 该资产的告警数量(若未设置则默认为-1)          |

**失败响应状态**

除鉴权错误外，无其他失败响应状态


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
  "name":"aaa",
  "assetClass":1,
  "price":1.0,
  "description":"",
  "count":1,
  "warning_date":1,
  "warning_amount":-1,
  },
  {
  "id":2,
  "name":"baa",
  "assetClass":1,
  "price":1.0,
  "description":"",
  "count":1,
  "warning_date":-1,
  "warning_amount":11,
  }
  ]
}
```
</details>
</details>

## 获取已告警资产接口

**接口描述**：此接口用于资产管理员获取业务实体下全部已告警资产

`[GET] /warning_list/{session}`

**请求参数**

无

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 该资产的id |
| name   | str  | 该资产的名称               |
| assetClass   | int  | 该资产的类型(数量型或条目型)               |
| price   | double  | 该资产的现价值               |
| description  | str  | 该资产的描述               |
| amount  | int  | 资产数量相较于告警阈值缺少的数量              |
| user  | str  | 该资产的挂账人名称              |
| assetTree  | str  | 该资产的资产树节点名称             |
| date  | int  | 该资产距告警日期的天数             |
| parent  |str  | 该资产的父资产的名称            |

**失败响应状态**

除了鉴权错误外，没有其他的失败响应状态。

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
  "name":"aaa",
  "assetClass":1,
  "price":1.0,
  "description":"",
  "amount":1,
  "user":"ab",
  "assetTree":"默认分类",
  "parent":"",
  "date":1
  },
  ]
}
```
</details>
</details>

## 获取资产潜在父资产接口

**接口描述**：此接口用于资产管理员获取某指定资产所有可能的父资产

`[GET] /all_item_assets/{session}/{asset_id}`

**请求参数**

无

url中的asset_id为需要获取父资产的资产的id，如果为0则表示该用户名下的所有合法资产。

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| id | int  | 父资产的id |
| name   | str  | 父资产的名称               |


**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 指定资产无效或不存在          | 指定资产无效或不存在 |

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
  "name":"aaa",
  },
      {
  "id":2,
  "name":"aab",
  },
  ]
}
```
</details>
</details>
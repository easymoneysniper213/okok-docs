## 创建资产树节点接口

**接口描述**：此接口用于资产管理员创建资产树节点

`[POST] /api/asset_tree/{session}`

**请求参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| parent | int  | 该资产层级树节点父节点的id |
| name   | str  | 该资产层级树节点的名称               |
| department  | str  | 该资产层级树节点挂载的部门名              |


**成功响应参数**

无成功响应参数，接口调用成功则创建资产树节点成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 指定名称的父节点不存在          | 指定名称的父节点不存在 |
| 2     | 无法在此处创建一个资产分类 | 无法在此处创建一个资产分类 |
| 2     | 该名称的部门不存在 | 输入的部门名称对应部门不存在 |
| 2     | 同名资产分类已存在 | 同名资产分类已存在 |


<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>
  
```json
{
  "name":"aba",
  "parent":"a",
  "department":"b"
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

## 获取某个资产树节点的子节点接口

**接口描述**：此接口用于资产管理员获取某个特定资产树节点的全部子节点

`[GET] /api/sub_asset_tree/{session}/{asset_tree_node_name}`

**请求参数**

无

url中的asset_tree_node_name表示特定的资产树节点，下面操作即为获取其子节点

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| name   | str  | 资产层级树子节点的名称               |

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 指定名称的父节点不存在          | 指定名称的父节点不存在 |


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
  "code":0
  "data":[
    {
      "name":"电子产品",
    },
    {
      "name":"钢制品",
    },
    ...
    ]
}
```
</details>
</details>

## 删除某个资产树节点接口

**接口描述**：此接口用于资产管理员删除某个特定资产树节点

`[DELETE] /api/sub_asset_tree/{session}/{asset_tree_node_name}`


**请求参数**

无

url中的asset_tree_node_name表示特定的资产树节点，下面操作即为删除该节点

**成功响应参数**

无成功响应参数，接口调用成功则删除资产树节点成功，返回Succeed

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 44     | 该资产树节点不可以删除          | "默认分类"、“数量型资产”、“条目型资产”这三个资产分类树节点不可删除 |
| 2     | 指定名称的资产分类不存在          | 指定名称的资产分类不存在 |
| 2    | 你不可以删除一个非叶子的资产分类          | 规定不可以删除一个非叶子的资产分类 |
| 2     | 你不可以删除一个已经含有资产的资产分类          | 规定不可以删除一个已经含有资产的资产分类 |

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
  "info":"Success",
}
```
</details>
</details>

## 获取某个部门资产树根节点接口

**接口描述**：此接口用于资产管理员获取该部门资产树根节点（即“默认分类”）

`[GET] /api/asset_tree_root/{session/{department_name}`

**请求参数**

无

url中的department_name表示部门名称，下面操作即为获取其资产分类树的根节点

**成功响应参数**

| 参数     | 类型 | 说明                                                 |
| -------- | ---- | ---------------------------------------------------- |
| name   | str  | 该部门资产层级树根节点的名称               |

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 该名称的部门不存在          | 指定名称的部门不存在 |
| 2     | 资产分类不存在          | 该部门作为根节点的资产分类不存在 |

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
  "data":
  {
    "name":"默认分类",
  },
}
```
</details>
</details>

## 获取某个资产树节点下所有资产的接口

**接口描述**：此接口用于资产管理员获取某个特定资产树节点下所有资产

`[GET] /api/asset_tree_node/{session}/{asset_tree_node_name}/{page}/{expire}`

**请求参数**

无

url中的asset_tree_node_name表示资产分类树节点名称，下面操作即为获取该资产分类树节点下的所有资产；

url中的expire表示资产是否被清退，用于指定资产清退状态；

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
| status  | int  | 该资产目前的状态            |

**失败响应状态**

| 状态码 | 错误信息                         | 说明                                |
| ------ | -------------------------------- | ----------------------------------- |
| 2     | 指定名称的资产分类不存在          | 该部门下指定名称的资产分类不存在 |

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
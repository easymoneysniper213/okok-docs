## 创建资产树节点接口

**接口描述**：此接口用于资产管理员创建资产树节点

`[POST] /api/asset_tree/{session}`


## 获取某个资产树节点的子节点接口

**接口描述**：此接口用于资产管理员获取某个特定资产树节点的全部子节点

`[GET] /api/sub_asset_tree/{session}/{asset_tree_node_name}`

## 删除某个资产树节点接口

**接口描述**：此接口用于资产管理员删除某个特定资产树节点

`[DELETE] /api/sub_asset_tree/{session}/{asset_tree_node_name}`


## 获取某个部门资产树根节点接口

**接口描述**：此接口用于资产管理员获取该部门资产树根节点（即“默认分类”）

`[GET] /api/asset_tree_root/{session/{department_name}`


## 获取某个资产树节点下所有资产的接口

**接口描述**：此接口用于资产管理员获取某个特定资产树节点下所有资产

`[GET] /api/asset_tree_node/{session}/{asset_tree_node_name}/{page}/{expire}`
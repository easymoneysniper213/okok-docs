## 创建资产接口

**接口描述**：此接口用于资产管理员创建资产

`[POST] /api/post_asset/{session}`


## 修改资产信息接口

**接口描述**：此接口用于资产管理员修改资产信息

`[PUT] /api/asset/{session}`


## 用户获取持有资产信息接口

**接口描述**：此接口用于一级用户获取自己的资产信息

`[GET] /api/asset_user_list/{session}/{page}`


## 用户获取持有资产信息接口

**接口描述**：此接口用于一级用户获取自己的资产信息

`[GET] /api/asset_user_list/{session}/{page}`


## 用户获取未领用的资产接口

**接口描述**：此接口用于一级用户获取指定资产管理员名下未被领用的资产信息

`[GET] /api/unallocated_asset/{session}/{asset_manager_name}/{page}`

## 调拨资产接口

**接口描述**：此接口用于资产管理员向指定资产管理员调拨资产

`[PUT] /api/allot_asset/{session}`

## 转移资产接口

**接口描述**：此接口用于一级用户向另一个一级用户转移资产

`[PUT] /api/transfer_asset/{session}`

## 转移资产接口

**接口描述**：此接口用于资产管理员将某个一级用户的资产转移给另一个一级用户

`[PUT] /api/transfer_asset/{session}`

## 维保资产接口

**接口描述**：此接口用于资产管理员维保资产

`[PUT] /api/maintain_asset/{session}`

## 清退资产接口

**接口描述**：此接口用于资产管理员清退资产

`[PUT] /api/expire_asset/{session}`

## 领用资产接口

**接口描述**：此接口用于资产管理员为某个一级用户分配其申请领用的资产

`[PUT] /api/receive_asset/{session}`


## 退库资产接口

**接口描述**：此接口用于资产管理员回收某个一级用户申请退库的资产

`[PUT] /api/return_asset/{session}`


## 获取某用户名下资产接口

**接口描述**：此接口用于资产管理员获取某用户名下的所有资产信息

`[GET] /asset/{session}/{user_name}/{page}`



## 获取维保资产列表接口

**接口描述**：此接口用于资产管理员获取该部门下所有正在维保的资产

`[GET] /get_maintain_list/{session}`


## 获取资产历史列表接口

**接口描述**：此接口用于资产管理员获取某指定资产的指定类型的资产操作历史列表

`[GET] /asset_query/{session}/{id}/{history_type}`


## 获取资产图片链接接口

**接口描述**：此接口用于资产管理员获取某指定资产的图片链接和富文本内容

`[GET] /picture/{session}/{asset_id}`


## 修改资产图片链接接口

**接口描述**：此接口用于资产管理员修改某指定资产的图片链接和富文本内容

`[PUT] /picture/{session}/{asset_id}`


## 修改告警策略接口

**接口描述**：此接口用于资产管理员修改某指定资产告警策略

`[PUT] /warning/{session}`



## 获取告警策略接口

**接口描述**：此接口用于资产管理员获取业务实体下全部资产告警策略

`[GET] /warning_get/{session}/{page}`



## 获取已告警资产接口

**接口描述**：此接口用于资产管理员获取业务实体下全部已告警资产

`[GET] /warning_list/{session}`


## 获取条目型资产接口

**接口描述**：此接口用于资产管理员获取某指定条目型资产

`[GET] /all_item_assets/{session}/{asset_id}`

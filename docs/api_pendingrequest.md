## 创建请求接口

**接口描述**：此接口用于用户向资产管理员发送请求

`[POST] /api/pending_request/{session}`


## 返回请求结果接口

**接口描述**：此接口用于资产管理员向用户发送请求结果

`[PUT] /api/return_pending_request/{session}`


## 获取待处理请求列表接口

**接口描述**：此接口用于资产管理员获取待处理请求列表

`[GET] /api/pending_request_list/{session}/{asset_manager_name}`
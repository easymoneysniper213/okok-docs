## 获取业务实体下全部部门接口

**接口描述**：此接口用于管理员获取自己业务实体下下全部部门

`[GET] /api/all_departments/{session}/{entity_name}`


## 获取某部门全部合法父部门接口

**接口描述**：此接口用于系统管理员获取某部门全部合法父部门

`[GET] /api/valid_parent_departments/{session}/{department_name}`


## 创建部门接口

**接口描述**：此接口用于系统管理员创建部门

`[POST] /api/department/{session}`


## 获取根部门接口

**接口描述**：此接口用于系统管理员获取业务实体下所有根部门

`[GET] /api/department/{session}`


## 修改部门信息接口

**接口描述**：此接口用于系统管理员修改业务实体下所有部门信息

`[PUT] /api/department/{session}`


## 获取子部门信息接口

**接口描述**：此接口用于系统管理员获取某个部门全部子部门信息

`[GET] /api/sub_department/{session}/{department_name}`


## 删除部门信息接口

**接口描述**：此接口用于系统管理员删除某个部门

`[DELETE] /api/department/{session}/{department_name}`
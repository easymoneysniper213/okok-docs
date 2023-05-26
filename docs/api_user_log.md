## 用户登录接口

**接口描述**：此接口用于进行用户的登录，本系统没有注册功能，用户来源于超级管理员与系统管理员的创建。

`[POST] /api/login`

**请求参数**

| 参数     | 类型 | 说明                     |
| -------- | ---- | ------------------------ |
| identity | str  | 登录所用的用户名字或邮箱 |
| password | str  | 用户密码的散列值(MD5)    |

**成功响应参数**

| 参数      | 类型 | 说明             |
| --------- | ---- | ---------------- |
| session   | str  | 用户的会话标识符 |
| character | int  | 用户的角色类型   |

**失败响应状态**

| 状态码 | 错误信息         | 相关说明                                         |
| ------ | ---------------- | ------------------------------------------------ |
| 2      | 用户名或密码错误 | 用户输入的名字或邮箱不存在，或用户输入的密码错误 |

补充：出于保护用户的安全信息，并不会对用户的登录失败信息做具体的名字、邮箱或密码提示；同时认为可以重复登录，但由于登录会为该用户赋唯一的sessionId，先前登录的用户所有操作将失效，也保证了安全。

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
    {
      "identity":"zhang_san",
      "password":"99b1ff8f11781541f7f89f9bd41c4a17"
    }

```
</details>
<details>
  <summary>响应</summary>

```json
    {
    "code":0,
    "data":
      {
      "session":"Rd8Gs0jw0jdbUeJzf7EIBwkwr7aYit74",
      "character":1
      }
    }

```
</details>
</details>


## 用户登出接口

**接口描述**：此接口用于已登录用户的登出，使得用户会话失效

`[PUT] /api/logout`

**请求参数**

| 参数    | 类型 | 说明             |
| ------- | ---- | ---------------- |
| session | str  | 用户的会话标识符 |

无成功响应参数，接口调用成功则用户直接登出，清除用户的sessionId并返回Succeed

**失败响应状态**

| 状态码 | 错误信息                   | 相关说明                                                      |
| ------ | -------------------------- | ------------------------------------------------------------- |
| 2      | 用户的会话标识符信息不正确 | 用户提供的sessionId不符合规范，如长度不为32位，包含特殊字符等 |
| 1      | 用户还未登录               | 根据用户提供的sessionId找不到具体用户                         |

<details>
 <summary>示例</summary>
 <details>
  <summary>请求</summary>

```json
{
  "session": "Rd8Gs0jw0jdbUeJzf7EIBwkwr7aYit74" 
}

```
</details>
<details>
  <summary>响应</summary>

```json
{
  "code":0,
  "info":"Succeed",
}

```
</details>
</details>


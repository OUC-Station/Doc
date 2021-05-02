# API Document

这是中国海洋大学 2020 年软件工程课程设计 iBird 项目的接口文档。

## 总体

以下为对所有接口的总体概述

### 域名

域名为 https://weparallelines.top

**注意：** 使用 HTTPS

### 接口格式

接口的请求格式一般为 JSON 格式，少数为 MultiForm 格式。

接口的响应格式为 JSON 格式。

### 响应字段

响应字段必定包含**状态码 code** 和**状态信息 msg**。

其他额外字段均包含在**数据 data** 字段中。

**注意：** 以下所有接口的响应字段除 code 和 msg 字段均在 data 字段中，为了书写文档简便其他字段与 code 和 msg 字段并列。

### 响应状态码和状态信息

响应状态码 code 和状态信息 msg 一一对应，无重复。

所有状态码和状态信息列表

> - 10000: Debug
> - 20000: 成功
> - 50000: 意外错误
> - 50403: Forbidden
> - 40000: 请求方法错误
> - 40001: JSON 解析错误
> - 40002: 缺少参数
> - 40003: 参数错误
> - 40004: 微信服务器请求失败
> - 40005: code 无效
> - 40006: 需要登陆

## 接口

### 上传图片

**接口功能**

> 上传图片

**URL**

> /api/upload

**请求方式**

> POST

**请求格式**

> MultiForm

**请求字段**

> | 参数 | 必选 | 类型 | 说明                 |
> | :--- | :--- | :--- | -------------------- |
> | img  | true | file | 图片文件（jpg、png） |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |
> | path     | string   | 图片路径 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40003: 参数错误
> 

**示例**

```json
// request MultiForm
{
  "img": "file",
}

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "path": "/media/20210430135155wJ6YykfxBe.jpg"
    }
}
```

---

### 获取位置列表

**接口功能**

> 获取位置列表

**URL**

> /api/location/get_locations_list

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段           | 字段类型 | 说明         |
> | :----------------- | :------- | :----------- |
> | code               | int      | 状态码       |
> | msg                | string   | 状态信息     |
> | locations          | list     | 位置列表     |
> | location_id        | int      | 位置 ID      |
> | location_name      | string   | 位置名       |
> | location_icon      | string   | 位置图标 URL |
> | location_longitude | float    | 经度         |
> | location_latitude  | float    | 纬度         |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误

**示例**

```json
// request
// GET /api/location/get_locations_list

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "locations": [
            {
                "location_id": 1,
                "location_name": "第一食堂",
                "location_icon": "/media/202104301407519CDCAUCi0v.jpg",
                "location_longitude": 11.11,
                "location_latitude": 11.11
            },
            {
                "location_id": 2,
                "location_name": "第二食堂",
                "location_icon": null,
                "location_longitude": 22.22,
                "location_latitude": 22.22
            }
        ]
    }
}
```

---

### 获取位置详细信息

**接口功能**

> 获取位置详细信息

**URL**

> /api/location/get_location_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数        | 必选 | 类型 | 说明    |
> | :---------- | :--- | :--- | ------- |
> | location_id | true | int  | 位置 ID |
>

**响应格式**

> JSON

**响应字段**

> | 返回字段              | 字段类型 | 说明         |
> | :-------------------- | :------- | :----------- |
> | code                  | int      | 状态码       |
> | msg                   | string   | 状态信息     |
> | location_id           | int      | 位置 ID      |
> | location_name         | string   | 位置名       |
> | location_introduction | string   | 介绍         |
> | location_remark       | string   | 备注         |
> | location_icon         | string   | 位置图标 URL |
> | location_image        | string   | 背景图       |
> | location_address      | string   | 地址表述     |
> | location_longitude    | float    | 经度         |
> | location_latitude     | float    | 纬度         |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
>
> - 40003: 参数错误

**示例**

```json
// request Query
// GET /api/location/get_location_detail?location_id=1

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "location_id": 1,
        "location_name": "第一食堂",
        "location_introduction": "第一食堂第一食堂第一食堂第一食堂",
        "location_remark": "",
        "location_icon": "/media/202104301407519CDCAUCi0v.jpg",
        "location_image": "/media/20210430140751GYEbz4Y5vq.jpg",
        "location_address": "第一食堂",
        "location_longitude": 11.11,
        "location_latitude": 11.11
    }
}
```

---

### 获取活动列表

**接口功能**

> 获取活动列表

**URL**

> /api/activity/get_activities_list

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数    | 必选  | 类型 | 说明                  |
> | :------ | :---- | :--- | --------------------- |
> | current | false | int  | 第几页（不填，默认1） |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明           |
> | :---------- | :------- | :------------- |
> | code        | int      | 状态码         |
> | msg         | string   | 状态信息       |
> | current     | int      | 当前第几页     |
> | total       | int      | 总页数         |
> | num         | int      | 当前页活动数量 |
> | activity_id | int      | 活动 ID        |
> | title       | string   | 活动标题       |
> | cover       | string   | 封面 URL       |
> | start_time  | string   | 开始时间       |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误

**示例**

```json
// request Query
// GET /api/activity/get_activities_list?current=1

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "activities": [
            {
                "activity_id": 2,
                "title": "讲座",
                "cover": "/media/20210430161537bni2rfdjSj.png",
                "start_time": "2021-04-30 09:12:00"
            },
            {
                "activity_id": 1,
                "title": "比赛活动12312",
                "cover": "/media/2021043015592394PZeAm6OP.jpg",
                "start_time": "2021-04-30 07:59:00"
            }
        ],
        "current": 1,
        "total": 1,
        "num": 2
    }
}
```

---

### 获取活动详细信息

**接口功能**

> 获取活动详细信息

**URL**

> /api/activity/get_activity_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数        | 必选 | 类型 | 说明    |
> | :---------- | :--- | :--- | ------- |
> | activity_id | true | int  | 活动 ID |

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明           |
> | :---------- | :------- | :------------- |
> | code        | int      | 状态码         |
> | msg         | string   | 状态信息       |
> | activity_id | int      | 活动 ID        |
> | title       | string   | 活动标题       |
> | cover       | string   | 封面 URL       |
> | content     | string   | 内容（富文本） |
> | create_time | string   | 创建时间       |
> | start_time  | string   | 开始时间       |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
>
> - 40003: 参数错误

**示例**

```json
// request Query
// GET /api/activity/get_activity_detail?activity_id=1

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "activity_id": 1,
        "title": "比赛活动12312",
        "cover": "/media/2021043015592394PZeAm6OP.jpg",
        "content": "<p>欢迎大家参加比萨</p><p><img src=\"/media/课表_20210430161104_229.jpg\" title=\"\" alt=\"课表.jpg\"/></p>",
        "create_time": "2021-04-30 07:59:23",
        "start_time": "2021-04-30 07:59:00"
    }
}
```

---

### 登录

**接口功能**

> 登录

**URL**

> /api/account/login

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数 | 必选 | 类型   | 说明             |
> | :--- | :--- | :----- | ---------------- |
> | code | true | string | 微信用户登录凭证 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40003: 参数错误
> - 40004: 微信服务器请求失败
> - 40005: code 无效

**示例**

```json
// request JSON
{
    "code": ""
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

---

### 获取用户状态

**接口功能**

> 获取用户状态

**URL**

> /api/account/get_status

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段  | 字段类型 | 说明                           |
> | :-------- | :------- | :----------------------------- |
> | code      | int      | 状态码                         |
> | msg       | string   | 状态信息                       |
> | is_login  | bool     | 是否登录                       |
> | nick_name | string   | 用户微信昵称（登录时有此字段） |
> | avatar    | string   | 用户微信头像（登录时有此字段） |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误

**示例**

```json
// request 
// GET /api/account/get_status

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "is_login": true,
        "nick_name": "Hello",
        "avatar": null
    }
}
```

---

### 更新用户信息

**接口功能**

> 新用户信息

**URL**

> /api/account/update_user_info

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数          | 必选 | 类型   | 说明                                  |
> | :------------ | :--- | :----- | ------------------------------------- |
> | encryptedData | true | string | wx.getUserInfo() 返回的 encryptedData |
> | iv            | true | string | wx.getUserInfo() 返回的 iv            |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40003: 参数错误
> - 40006: 需要登陆

**示例**

```json
// request JSON
{
    "encryptedData": "",
    "iv": ""
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

---

### 发表意见

**接口功能**

> 发表意见

**URL**

> /api/suggestion/post_suggestion

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数    | 必选 | 类型   | 说明     |
> | :------ | :--- | :----- | -------- |
> | content | true | string | 意见内容 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40006: 需要登陆

**示例**

```json
// request JSON
{
    "content": "123"
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

---

### 获取我的意见

**接口功能**

> 获取我的意见

**URL**

> /api/suggestion/get_my_suggestions

**请求方式**

> GET

**请求格式**

> None

**请求字段**

> None

**响应格式**

> JSON

**响应字段**

> | 返回字段    | 字段类型 | 说明     |
> | :---------- | :------- | :------- |
> | code        | int      | 状态码   |
> | msg         | string   | 状态信息 |
> | content     | string   | 意见内容 |
> | create_time | string   | 创建时间 |
> | reply       | string   | 回复     |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40006: 需要登陆

**示例**

```json
// request 
// GET /api/account/get_status

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "suggestions": [
            {
                "content": "333",
                "create_time": "2021-05-02 08:59:21",
                "reply": ""
            },
            {
                "content": "333",
                "create_time": "2021-05-02 08:58:52",
                "reply": ""
            },
            {
                "content": "123",
                "create_time": "2021-05-02 08:58:35",
                "reply": ""
            }
        ]
    }
}
```

---

### 发表主题

**接口功能**

> 发表主题

**URL**

> /api/bbs/post_topic

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型   | 说明     |
> | :-------- | :--- | :----- | -------- |
> | title     | true | string | 标题     |
> | content   | true | string | 内容     |
> | anonymous | true | bool   | 是否匿名 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40006: 需要登陆

**示例**

```json
// request JSON
{
    "title": "222222",
    "content": "22222",
    "anonymous": true
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

---

### 获取主题列表

**接口功能**

> 获取主题列表

**URL**

> /api/bbs/get_topics

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数    | 必选  | 类型 | 说明                  |
> | :------ | :---- | :--- | --------------------- |
> | current | false | int  | 第几页（不填，默认1） |

**响应格式**

> JSON

**响应字段**

> | 返回字段         | 字段类型 | 说明           |
> | :--------------- | :------- | :------------- |
> | code             | int      | 状态码         |
> | msg              | string   | 状态信息       |
> | current          | int      | 当前第几页     |
> | total            | int      | 总页数         |
> | num              | int      | 当前页活动数量 |
> | topic_id         | int      | 主题 ID        |
> | anonymous        | bool     | 是否匿名       |
> | account_nickname | string   | 发布者昵称     |
> | account_avatar   | string   | 发布者头像 URL |
> | title            | string   | 标题           |
> | content          | string   | 内容           |
> | create_time      | string   | 创建时间       |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误

**示例**

```json
// request Query
// GET /api/bbs/get_topics?current=1

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "topics": [
            {
                "topic_id": 2,
                "anonymous": true,
                "account_nickname": "匿名用户",
                "account_avatar": null,
                "title": "222222",
                "content": "22222",
                "create_time": "2021-05-02 09:14:42"
            },
            {
                "topic_id": 1,
                "anonymous": false,
                "account_nickname": "Hello",
                "account_avatar": null,
                "title": "1111",
                "content": "111111",
                "create_time": "2021-05-02 09:14:31"
            }
        ],
        "current": 1,
        "total": 1,
        "num": 2
    }
}
```

---

### 获取主题详细信息

**接口功能**

> 获取主题详细信息

**URL**

> /api/bbs/get_topic_detail

**请求方式**

> GET

**请求格式**

> Query

**请求字段**

> | 参数     | 必选 | 类型 | 说明    |
> | :------- | :--- | :--- | ------- |
> | topic_id | true | int  | 活动 ID |

**响应格式**

> JSON

**响应字段**

> | 返回字段                   | 字段类型 | 说明               |
> | :------------------------- | :------- | :----------------- |
> | code                       | int      | 状态码             |
> | msg                        | string   | 状态信息           |
> | topic_id                   | int      | 主题 ID            |
> | anonymous                  | bool     | 是否匿名           |
> | account_nickname           | string   | 发布者昵称         |
> | account_avatar             | string   | 发布者头像 URL     |
> | title                      | string   | 标题               |
> | content                    | string   | 内容               |
> | create_time                | string   | 创建时间           |
> | comments                   | list     | 评论列表           |
> | comments: anonymous        | bool     | 评论是否匿名       |
> | comments: account_nickname | string   | 评论发布者昵称     |
> | comments: account_avatar   | string   | 评论发布者头像 URL |
> | comments: content          | string   | 评论内容           |
> | comments: create_time      | string   | 评论创建时间       |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40003: 参数错误

**示例**

```json
// request Query
// GET /api/bbs/get_topic_detail?topic_id=1

// response JSON
{
    "code": 20000,
    "msg": "成功",
    "data": {
        "topic_id": 1,
        "anonymous": false,
        "account_nickname": "Hello",
        "account_avatar": null,
        "title": "1111",
        "content": "111111",
        "create_time": "2021-05-02 09:14:31",
        "comments": [
            {
                "anonymous": true,
                "account_nickname": "匿名用户",
                "account_avatar": null,
                "content": "你好",
                "create_time": "2021-05-02 09:22:12"
            },
            {
                "anonymous": false,
                "account_nickname": "Hello",
                "account_avatar": null,
                "content": "啦啦啦",
                "create_time": "2021-05-02 09:23:02"
            }
        ]
    }
}
```

---

### 发表评论

**接口功能**

> 发表评论

**URL**

> /api/bbs/post_comment

**请求方式**

> POST

**请求格式**

> JSON

**请求字段**

> | 参数      | 必选 | 类型   | 说明     |
> | :-------- | :--- | :----- | -------- |
> | topic_id  | true | int    | 主题 ID  |
> | content   | true | string | 内容     |
> | anonymous | true | bool   | 是否匿名 |

**响应格式**

> JSON

**响应字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | code     | int      | 状态码   |
> | msg      | string   | 状态信息 |

**响应状态码与状态信息**

> - 20000: 成功
> - 50000: 意外错误
> - 40000: 请求方法错误
> - 40002: 缺少参数
> - 40006: 需要登陆

**示例**

```json
// request JSON
{
    "topic_id": 1,
    "content": "啦啦啦",
    "anonymous": false
}

// response JSON
{
    "code": 20000,
    "msg": "成功"
}
```

---

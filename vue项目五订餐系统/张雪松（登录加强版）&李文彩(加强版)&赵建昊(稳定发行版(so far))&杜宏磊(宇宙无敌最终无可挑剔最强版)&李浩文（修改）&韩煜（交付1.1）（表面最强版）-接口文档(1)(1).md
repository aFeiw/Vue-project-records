# 公共信息

**基础路径**：（跟谁对接口先用谁的地址）

**基础返回结构**

> | 参数    | 类型    | 说明                                               |
> | :------ | :------ | -------------------------------------------------- |
> | code    | Integer | 调用状态码：200成功，400/500失败（其它code码待定） |
> | message | String  | 接口调用情况                                       |
> | content | T       | 内容(任意类型)                                     |

**基础返回示例**

```json
{
    "code": 0,
    "message": "成功信息",
    "content": {
    }
}
```

**header信息说明**

> 除了登录接口外，其他接口都需要认证，所以header中需要带token

**一些枚举值对应信息**

> * **菜品**
>   * 0 ------ 单品
>   * 1 ------ 套餐
> * **图片对应**
>   * 0 ------ 列表页
>   * 1 ------ 详情页
> * **餐别**
>   * 0 ------ 早
>   * 1 ------ 中
>   * 2 ------ 晚
>   * 01 ------ 早中
>   * 02 ------ 早晚
>   * 12 ------ 中晚
>   * 012 ------ 早中晚
> * **套餐状态**
>   * 0 ------ 已下架
>   * 1 ------ 未下架
> * **员工状态**
>   * 0 ------ 未被禁用
>   * 1 ------ 已被禁用
> * **客户类型**
>   * 0 ------ 员工
>   * 1 ------ 病人
> * **订单状态**
>   * 0 ------ 成功
>   * 1 ------ 失败
> * **菜品类型**
>   * 0 ------ 主食
>   * 1 ------ 热菜
>   * 2 ------ 凉菜
> * **菜品状态**
>   * 0 ------ 已下架
>   * 1 ------ 未下架
> * **角色**
>   * 1 ------ 超级管理员
>   * 2 ------ 内勤
>   * 3 ------ 配送员
>   * 4 ------ 客户
> * **前端页面状态显示（订单管理2）**
>   * 0 ------ 显示
>   * 1 ------ 不显示
> * **取餐方式（订单管理2）**
>   * 0 ------ 外卖
>   * 1 ------ 自提
> * **订单状态**
>   * 0 ------ 付款中
>   * 1 ------ 付款失败
>   * 2 ------ 已付款
>   * 3 ------ 制作中
>   * 4 ------ 制作完成
>   * 5 ------ 配送中
>   * 6 ------ 已送达
>   * 7 ------ 已自提
>   * 8 ------ 退款失败
>   * 9 ------ 退款成功
>   
>   

# 张雪松的接口

## 员工管理

#### ip地址：

192.168.9.43

#### 端口：

8081

### 1.员工新增

#### 接口地址

/customer/addCustomer

#### 请求方式

POST

#### 请求参数

| 请求字段     | 字段类型 | 说明     | 是否必须 | 备注         |
| ------------ | -------- | -------- | -------- | ------------ |
| EbizCustomer | body     | 员工对象 | true     |              |
| └name        | String   | 姓名     | true     |              |
| └phone       | String   | 手机号   | true     | 11位数字     |
| └password    | String   | 密码     | true     | 字母数字6-10 |

#### 请求示例

```
{
	"name"："中学生"，
	"phone"："15100001202"，
	"password"："abc1234"
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```
{
    "code"：200，
    "message"：“新增成功”
    "content"：null
}
```

### 2.员工编辑

#### 接口地址

/customer/updateCustomer

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明     | 是否必须 | 备注         |
| ------------ | -------- | -------- | -------- | ------------ |
| EbizCustomer | body     | 员工对象 | true     |              |
| └no          | String   | 职工号   | false    | 六位数字     |
| └name        | String   | 姓名     | false    |              |
| └phone       | String   | 手机号   | false    | 11位数字     |
| └password    | String   | 密码     | false    | 字母数字6-10 |

#### 请求示例

```json
{
	"no":"123456",
	"name":"中学生",
	"phone":"15100001202",
	"password":"abc1234"
}
```





#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"更新成功",
    "content":null
}
```



### 3.查询全部员工

#### 接口地址

/customer/querryAll

#### 请求方式

post

#### 请求参数

| 请求字段      | 字段类型 | 说明         | 是否必须 | 备注     |
| ------------- | -------- | ------------ | -------- | -------- |
| StaffParamDTO | body     | 员工查询对象 | true     |          |
| pageNum       | int      | 页码         | true     | >=1      |
| pageSize      | int      | 数量         | true     | >=1      |
| └no           | String   | 职工号       | false    | 六位数字 |
| └name         | String   | 姓名         | false    |          |

#### 请求示例

```json
{
    "pageNum":1,
    "pageSize":2,
    "no":"123",
    "name":"中学"
}
```



#### 返回字段

| 返回字段 | 字段类型 | 说明                 |
| -------- | -------- | -------------------- |
| id       | int      | 主键id               |
| no       | String   | 工号                 |
| name     | String   | 姓名                 |
| phone    | String   | 11位数字             |
| password | String   | 密码                 |
| status   | int      | 0-未被禁用，1-已禁用 |

```json
{
    "code": 200,
    "message": "success",
    "content": {
        "result": [
            {
                "id": 3,
                "no": "db518426cfa6",
                "name": "大学生",
                "phone": "15100001202",
                "password": "abc1234",
                "status": null
            },
            {
                "id": 5,
                "no": "d7dcf25cbef0",
                "name": "中学生23",
                "phone": "15100001202",
                "password": "abc1234",
                "status": null
            }
        ],
        "total": 5
    }
}
```

### 4.通过工号查询员工

#### 接口地址

/customer/selectCustomerById

#### 请求方式

post

#### 请求参数

| 请求字段 | 字段类型 | 说明   | 是否必须 | 备注 |
| -------- | -------- | ------ | -------- | ---- |
| id       | string   | 员工号 | true     |      |

#### 请求示例

```json
/customer/selectCustomerById?id=1
```



#### 返回字段

| 返回字段 | 字段类型 | 说明                 |
| -------- | -------- | -------------------- |
| id       | int      | 主键id               |
| no       | String   | 工号                 |
| name     | String   | 姓名                 |
| phone    | String   | 11位数字             |
| password | String   | 密码                 |
| status   | int      | 0-未被禁用，1-已禁用 |

#### 返回值示例

```json
{
    “code”:200，
    “message”:“更新成功”
    ”content“:{	
    			"id":1,
                "no":"123",
                "name":"中学",
                "phone":"123456",
                "password":"34586756",
                "status":0
	}
}
```



### 5.员工禁用

#### 接口地址

/customer/updateStatusById

#### 请求方式

get

#### 请求参数

| 请求字段 | 字段类型 | 说明   | 是否必须 | 备注 |
| -------- | -------- | ------ | -------- | ---- |
| id       | int      | 员工id | true     |      |

#### 请求示例

/customer/Disable?id=1

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"禁用/启用成功",
    "content":null
}
```

### 6.员工删除

#### 接口地址

customer/delete

#### 请求方式

get

#### 请求参数

| 请求字段 | 字段类型 | 说明   | 是否必须 | 备注 |
| -------- | -------- | ------ | -------- | ---- |
| id       | int      | 员工id | true     |      |

#### 请求示例

/customer/delete?id=1

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"删除成功",
    "content":null
}
```

## 手机端

### 1.用户登录

#### 接口地址

customer/cusLogin

#### 请求方式

post

#### 请求参数

| 请求字段 | 是否必须 | 类型   | 说明   |
| -------- | -------- | ------ | ------ |
| phone    | 是       | 手机号 | 手机号 |
| captcha  | 是       | 手机号 | 验证码 |

#### 请求示例

```json
{
    "phone":"13116598546",
    "captcha":6398
}
```

#### 返回参数

| 返回字段 | 字段类型 | 说明                 |
| -------- | -------- | -------------------- |
| phone    | String   | 当前登录用户的手机号 |

#### 返回示例

```json
{
    "code": 200,
    "message": "登录成功",
    "content": {
        "phone": "13109466486",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6Mjg2NywiZXhwIjoxNjMxNjg5ODMwLCJ1c2VybmFtZSI6IjEzMTA5NDY2NDg2In0.9KCvEqM0ugwB0JvNtTxyqi4y3LvjFAdr3rGJztC1WhA"
    }
}
```

### 2.验证码

#### 接口地址

/captcha

#### 请求方式

post

#### 请求参数

| 字段  | 是否必传 | 类型   | 说明   |
| ----- | -------- | ------ | ------ |
| phone | 是       | String | 手机号 |

#### 请求示例

```json
{
    "phone":"13116598546"
}
```

#### 返回参数

| 返回字段 | 字段类型 | 说明   |
| -------- | -------- | ------ |
| phone    | String   | 手机号 |
| captcha  | int      | 验证码 |

#### 返回示例

```json
{
    "code": 200,
    "message": "success",
    "content": {
        "phone": "13116598546",
        "captcha": 4604
    }
}
```

### 3.员工登录

#### 接口地址

/customer/workerLogin

#### 请求方式

post

#### 请求参数

| 请求字段 | 字段类型 | 说明 | 是否必须 | 备注 |
| -------- | -------- | ---- | -------- | ---- |
| no       | int      | 工号 | true     |      |
| password | String   | 密码 | true     |      |

#### 请求示例

```json
{
    "no":1001,
    "password":"12345678"
}
```



#### 返回参数

| 返回字段 | 字段类型 | 说明   |
| -------- | -------- | ------ |
| id       | int      | 员工id |
| token    | String   | token  |

#### 返回示例

```json
{
    "code": 200,
    "message": "登录成功",
    "content": {
        "id": 1,
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwiZXhwIjoxNjMxNjg5NjAwLCJ1c2VybmFtZSI6IuW8oOS4iSJ9._niMHNtYW2IoyNcevAkt34W10q6rlOF5iiGTKDUaZb4"
    }
}
```

### 4.默认查询工号和手机号

#### 接口地址

/customer/matching

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明         | 是否必须 | 备注     |
| ------------ | -------- | ------------ | -------- | -------- |
| EbizCustomer | body     | 员工查询对象 | true     |          |
| └no          | String   | 工号         | true     | 6位数字  |
| └phone       | String   | 手机号       | true     | 11位数字 |

#### 请求示例

```json
{
    "no":"123456",
    "phone":"12345678910"
}
```



#### 返回参数

null

#### 返回示例

null

### 5.提交新密码

#### 接口地址

/customer/updatepw

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明         | 是否必须 | 备注         |
| ------------ | -------- | ------------ | -------- | ------------ |
| EbizCustomer | body     | 员工查询对象 | true     |              |
| └captcha     | String   | 验证码       | true     | 4位数字      |
| └password    | String   | 新密码       | true     | 字母数字6-10 |

#### 请求示例

```json
{
    "captcha":"1234",
    "phone":"abc4321"
}
```



#### 返回参数

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回示例

```json
{
    "code":200,
    "message":"修改成功",
    "content":null
}
```

# 李文彩的接口

## 套餐管理

### 1.添加套餐信息

> 描述：添加套餐图片

**URL**

> /dishPackage/addDishPack

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：JSON

> | 参数         | 必选 | 字段类型 | 说明                                                         |
> | ------------ | ---- | -------- | ------------------------------------------------------------ |
> | mealType     | 是   | int      | 商品类别：0菜品，1套餐。                                     |
> | name         | 是   | string   | 套餐名称                                                     |
> | price        | 是   | double   | 套餐价格                                                     |
> | type         | 是   | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | 否   | string   | 套餐描述                                                     |
> | meal         | 是   | List     | 菜品id的List                                                 |
> | └ id         | 是   | int      | 菜品id                                                       |
> | └ num        | 是   | int      | 菜品数量                                                     |
> | listImage    | 是   | int      | id                                                           |
> | detailImages | 是   | List     | 详情页id                                                     |

**参数实例**

```json
{	
    "mealType":1,
    "name":小鸡炖小鸭,
    "price":22.2,
    "type":"012",
    "desc":"野性碰撞",
    "meal":[
    	{"id":201943,"num":1},
		{"id":299943,"num":2}
	],
    "listImage":12345678,
	"detailImages":[1234,3435,4565,39945]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明             |
> | -------- | -------- | ---------------- |
> | code     | int      | 状态码           |
> | message  | string   | 返回信息         |
> | content  | int      | 返回的添加的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 2.删除套餐

> 描述：删除套餐

**URL**

> /dishPackage/deleteDishPack

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 字段类型 | 说明   |
> | ---- | ---- | -------- | ------ |
> | id   | 是   | int      | 图片id |

**参数实例**

```json
/dishPackage/deleteDishPack?id=1234467
```

**返回字段**

> | 返回字段 | 字段类型 | 说明           |
> | -------- | -------- | -------------- |
> | code     | int      | 状态码         |
> | message  | string   | 返回信息       |
> | content  | int      | 返回删除的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 3.编辑套餐信息

> 描述：添加套餐图片

**URL**

> /dishPackage/updateDishPack

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：JSON

> | 参数         | 必选 | 字段类型 | 说明                                                         |
> | ------------ | ---- | -------- | ------------------------------------------------------------ |
> | id           | 是   | int      | 套餐id                                                       |
> | mealType     | 是   | int      | 商品类别：0菜品，1套餐。                                     |
> | name         | 是   | string   | 套餐名称                                                     |
> | price        | 是   | double   | 套餐价格                                                     |
> | type         | 是   | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | 否   | string   | 套餐描述                                                     |
> | meal         | 是   | List     | 菜品id的List                                                 |
> | └ id         | 是   | int      | 菜品id                                                       |
> | └ num        | 是   | int      | 菜品数量                                                     |
> | listImage    | 是   | int      | id                                                           |
> | detailImages | 是   | List     | 详情页id                                                     |

**参数实例**

```json
{	
   "mealType":1,
   "id":124456789,
   "name":小鸡炖小鸭,
   "price":22.2,
   "type":"012",
   "desc":"野性碰撞",
   "meal":[
    	{"id":201943,"num":1},
		{"id":299943,"num":2}
	],
    "listImage":12345678,
	"detailImages":[1234,3435,4565,39945]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明             |
> | -------- | -------- | ---------------- |
> | code     | int      | 状态码           |
> | message  | string   | 返回信息         |
> | content  | int      | 返回的添加的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 4.通过餐别查询菜品信息

> 描述：通过餐别查询菜品

**URL**

> /dishPackage/selectMealIdAndNameByType

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数 | 必选 | 类型        | 说明             |
> | ---- | ---- | ----------- | ---------------- |
> | list | 是   | list string | 餐别（用餐时间） |

**参数实例**

```json
{
    "list":["","1","2"]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | id       | int      | 套餐id   |
> | name     | string   | 套餐名称 |
> | price    | double   | 价格     |
> | num      | int      | 数量     |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        {
        	"id":1234,
            "name":"美味鸡腿饭",
        	"price":12,
        	"num":2
    	},
        {
			"id":1234,
       	 	"name":"美味鸡腿饭2",
   			"price":12,
        	"num":2
        }
    }
}
```

### 5.查询全部套餐信息接口(PC)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectAllPC

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型   | 说明     |
> | -------- | ---- | ------ | -------- |
> | pageNum  | 是   | int    | 分页页码 |
> | pageSize | 是   | int    | 数量     |
> | type     | 否   | string | 餐别     |
> | name     | 否   | string | 餐名     |

**参数实例**

```json
{
    "pageNum":2,
    "pageSize":2,
    "type":"012",
    "name":"小鸡"
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明                                                         |
> | :------- | :------- | :----------------------------------------------------------- |
> | id       | int      | 套餐id                                                       |
> | name     | string   | 套餐名称                                                     |
> | price    | double   | 套餐价格                                                     |
> | type     | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | status   | int      | 套餐状态，0-已下架，1-未下架                                 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content":
        "result":
    	[{
        {
        	"id":1234,
            "name":"美味鸡腿饭",
        	"price":12.5,
        	"type":"012",
       	    "status":0
    	},
        {
			"id":1234,
       	 	"name":"美味鸡腿饭2",
       	 	"price":12.5,
       	 	"type":"012",
       	 	"status":0	
        }],
    	"total":10
}
```

### 6.查询全部套餐信息接口(Phone)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectAllPhone

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型   | 说明     |
> | -------- | ---- | ------ | -------- |
> | pageNum  | 是   | int    | 分页页码 |
> | pageSize | 是   | int    | 数量     |
> | type     | 否   | string | 餐别     |

**参数实例**

```json
{
    "pageNum":2,
    "pageSize":2,
    "type":"0"
}
```

**返回字段**

> | 返回字段   | 字段类型 | 说明                                                         |
> | :--------- | :------- | :----------------------------------------------------------- |
> | id         | int      | 套餐id                                                       |
> | name       | string   | 套餐名称                                                     |
> | price      | double   | 套餐价格                                                     |
> | type       | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc       | string   | 套餐描述                                                     |
> | meals      | List     | 菜品                                                         |
> | id         | String   | 菜品id                                                       |
> | └ mealName | string   | 菜品名称                                                     |
> | └ price    | double   | 菜品价格                                                     |
> | └ num      | int      | 该菜在套餐中的数量                                           |
> | listImage  | string   | 列表页图片                                                   |
> | └ id       | int      | 列表页图片id                                                 |
> | └ url      | string   | 列表页图的url                                                |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": [
        {
            "id":1234,
            "name":"美味鸡腿饭",
            "price":12.5,
            "type":"012",
            "desc":"好吃！"
            "meals":[
            {
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            },
 			{
                "mealName":"小鸡炖蘑菇2",
                "price":10.0,
                "num":1
            }
        	],
       	    "listImage":{
                "id":12323434567,
                "url":"192.168.11.128:8080//c:iamges/399343.jpg" 
    		},
        	{
             "id":1234,
             "name":"美味鸡腿饭",
             "price":12.5,
             "type":"012",
             "desc":"好吃！"
             "meals":[
            {	
    			"id":123456,
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            },
 			{
                "id":1235621,
                "mealName":"小鸡炖蘑菇2",
                "price":10.0,
                "num":1
            }
            ],
      	    "listImage":{
                "id":1232343437,
                "url":"192.168.11.128:8080//c:iamges/3993425223.jpg"
            } 
        }
    ]
}
```

### 7.通过id查询套餐信息接口(PC,Phone)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 类型 | 说明   |
> | ---- | ---- | ---- | ------ |
> | id   | 是   | int  | 套餐id |

**参数实例**

```json
/dishPackage/selectById?id=12
```

**返回字段**

> | 返回字段     | 字段类型 | 说明                                                         |
> | :----------- | :------- | :----------------------------------------------------------- |
> | id           | int      | 套餐id                                                       |
> | name         | string   | 套餐名称                                                     |
> | price        | double   | 套餐价格                                                     |
> | type         | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | string   | 套餐描述                                                     |
> | meals        | List     | 菜品                                                         |
> | └ mealName   | string   | 菜品名称                                                     |
> | └ price      | double   | 菜品价格                                                     |
> | └ num        | int      | 该菜在套餐中的数量                                           |
> | listImage    | string   | 列表页图片                                                   |
> | └ id         | int      | 列表页图片id                                                 |
> | └ url        | string   | 列表页图的url                                                |
> | detailImages | List     | 详情页                                                       |
> | └ id         | int      | 详情页的图片id                                               |
> | └ url        | string   | 详情页的图片url                                              |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "id":1234,
        "name":"美味鸡腿饭",
        "price":12.5,
        "type":"012",
        "status":0,
        "desc":"非常好吃的鸡腿饭",
        "meals":[
            {	
                "id":1253,
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            }
        ],
        "listImage":"192.168.11.128:8080//c:iamges/399343.jpg",
        "detailImages":[
            {
                id:1
                url:"192.168.11.128:8080//c:iamges/3993432343.jpg"
            },
             {
                id:2
                url:"192.168.11.128:8080//c:iamges/12399343.jpg"
            }
        ]       
    }
}
```

### 8.上下架

> 描述：修改餐品的状态

**URL**

> /dishPackage/updateStatus

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 类型    | 说明   |
> | ---- | ---- | ------- | ------ |
> | id   | 是   | Integer | 套餐id |

**参数实例**

```json
/dishPackage/updateStatus?id=12
```

**返回字段**

> | 返回字段 | 字段类型 | 说明               |
> | -------- | -------- | ------------------ |
> | code     | int      | 状态码             |
> | message  | string   | 返回信息           |
> | content  | int      | 返回的上下架的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

# 赵建昊的接口

## 公共信息

**基础路径 `http://192.168.11.28:8081`**

## 订单接口

### 1.查询全部订单信息（PC端）

> 描述：查询全部订单信息，分页

#### **URL**

> /conorder/selectAllOrderList

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数           | 必选 | 类型    |                             说明                             |
| :------------- | :--- | :------ | :----------------------------------------------------------: |
| pageSize       | 是   | Integer |                           分页页长                           |
| pageNum        | 是   | Integer |                           当前页码                           |
| orderNo        | 否   | String  |                            订单号                            |
| dishPackType   | 否   | String  | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
| orderStatus    | 否   | Integer | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
| customerStatus | 否   | Integer |                    类型（0-单品，1-套餐）                    |

#### **参数示例**

```json
{
    "pageSize":5,
    "pageNum":1,
    "orderNo":"",
    "dishPackType":"",
    "orderStatus":"",
    "customerStatus":""
}
```

#### **返回字段**

> | 返回字段             | 字段类型   | 说明                                                         |
> | :------------------- | :--------- | :----------------------------------------------------------- |
> | id                   | Integer    | 自增主键id                                                   |
> | ebizCustomerId       | Integer    | 客户id                                                       |
> | orderNo              | String     | 订单号                                                       |
> | takeFoodWay          | Integer    | 取餐方式（0-外卖，1-自提）                                   |
> | price                | BigDecimal | 总价格                                                       |
> | orderStatus          | Integer    | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | deliveryMan          | String     | 送餐人                                                       |
> | placeOrderTime       | date       | 下单时间                                                     |
> | requiredDeliveryTime | date       | 要求送餐时间                                                 |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询全部订单信息成功",
    "content": {
        "total": 5，
        "list":{
        	（上面的字段组成的对象）
    	}
    }
}
```

### 2.批量导出（PC端）

> 描述：把订单表批量导出到EXCEL中

#### **URL**

> /conorder/exportSelectAll

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数        | 必选 | 类型        |          说明          |
| :---------- | :--- | :---------- | :--------------------: |
| integerList | 是   | Integer数组 | 一个Interger类型的数组 |

#### **参数示例**

```json
{
    "integerList":[1,2,3,4,5]
}
```

#### **返回字段**

> | 返回字段 | 字段类型 | 说明                               |
> | :------- | :------- | :--------------------------------- |
> |          |          | 会根据当前浏览器默认地址，直接下载 |

#### **返回值示例**

```json

```

### 3.单个导出（PC端）

> 描述：把选中的订单信息（单选）打印出一个小票样式的文件

#### **URL**

> /conorder/exportSelectOne

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数 | 必选 | 类型    |     说明     |
| :--- | :--- | :------ | :----------: |
| id   | 是   | Integer | 当前订单的id |

#### **参数示例**

```json
{
    "id":1
}
```

#### **返回字段**

> | 返回字段 | 字段类型 | 说明                               |
> | :------- | :------- | :--------------------------------- |
> |          |          | 会根据当前浏览器默认地址，直接下载 |

#### **返回值示例**

```json

```

### 4.订单详情（PC端）

> 描述：根据订单id查询订单详情信息

#### **URL**

> /conorder/selectByebizCustomerId

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数 | 必选 | 类型    |    说明    |
| :--- | :--- | :------ | :--------: |
| id   | 是   | Integer | 主键自增id |

#### **参数示例** 

```json
{
    id:"2"
}
```

#### **返回字段**

> | 返回字段             | 字段类型            | 说明                                                         |
> | :------------------- | :------------------ | :----------------------------------------------------------- |
> | id                   | Integer             | 自增主键id                                                   |
> | ebizCustomerId       | Integer             | 客户id                                                       |
> | orderNo              | String              | 订单号                                                       |
> | orderPhone           | String              | 手机号                                                       |
> | orderUser            | String              | 订餐人                                                       |
> | takeFoodWay          | Integer             | 取餐方式（0-外卖，1-自提）                                   |
> | price                | BigDecimal          | 总价格                                                       |
> | orderStatus          | Integer             | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | deliveryMan          | String              | 送餐人                                                       |
> | deliveryAddress      | String              | 送餐地址                                                     |
> | remarks              | String              | 备注                                                         |
> | placeOrderTime       | date                | 下单时间                                                     |
> | requiredDeliveryTime | date                | 要求送餐时间                                                 |
> | productionTime       | date                | 制作时间                                                     |
> | producer             | String              | 制作人                                                       |
> | completedTime        | date                | 制作完成时间                                                 |
> | deliveryTime         | date                | 送餐时间                                                     |
> | forwardingTime       | date                | 送达时间                                                     |
> | ebizsjdqbDTO         | List<EbizsjdqbDTO>  |                                                              |
> | └id                  | Integer             | 订单id                                                       |
> | └packName            | String              | 套餐名                                                       |
> | └packNum             | Integer             | 套餐数量                                                     |
> | └ebizsjdqb2DTO       | List<Ebizsjdqb2DTO> |                                                              |
> | └└dishNames          | String              | 单品名                                                       |
> | └└dishNums           | Integer             | 单品数量                                                     |
> | ebizsjdqb1DTO        | List<Ebizsjdqb1DTO> |                                                              |
> | └dishName            | String              | 单品名                                                       |
> | └dishNum             | Integer             | 单品数量                                                     |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total": 1,
        "list": [
            {
                "id": 2,
                "ebizCustomerId": 2,
                "orderNo": "10000002",
                "orderUser": "刘远辉",
                "orderPhone": "18522608634",
                "statusDisplay": 0,
                "takeFoodWay": 1,
                "price": 30,
                "orderStatus": 4,
                "deliveryMan": "张三",
                "deliveryAddress": "一号楼",
                "refundReason": "别找我我没退款",
                "remarks": "实打实大四大所",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-25 14:00:00",
                "productionTime": "2021-08-25 12:34:22",
                "producer": "王师傅",
                "completedTime": "2021-08-25 12:25:48",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "id": 2,
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            }
        ]
    }
}
```

### 5.查指定时间段订单详情（PC端）

> 描述：查指定时间段订单详情并且显示,并且只显示2-4的状态，超出之后就不显示

#### **URL**

> /conorder/selectAllByTimeType

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数        | 必选 | 类型    |   说明   |
| :---------- | :--- | :------ | :------: |
| pageSize    | 是   | Integer | 分页页长 |
| pageNum     | 是   | Integer | 当前页码 |
| orderStatus | 否   | Integer | 订单状态 |

#### **参数示例** 

```json
{
    "pageSize":5,
    "pageNum":1,
    "orderStatus":""
}
```

#### **返回字段**

> | 返回字段             | 字段类型            | 说明                                                         |
> | :------------------- | :------------------ | :----------------------------------------------------------- |
> | id                   | Integer             | 自增主键id                                                   |
> | ebizCustomerId       | Integer             | 客户id                                                       |
> | orderNo              | String              | 订单号                                                       |
> | takeFoodWay          | Integer             | 取餐方式（0-外卖，1-自提）                                   |
> | orderStatus          | Integer             | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | deliveryMan          | String              | 送餐人                                                       |
> | placeOrderTime       | date                | 下单时间                                                     |
> | requiredDeliveryTime | date                | 要求送餐时间                                                 |
> | deliveryTime         | date                | 送餐时间                                                     |
> | ebizsjdqbDTO         | List<EbizsjdqbDTO>  |                                                              |
> | └id                  | Integer             | 订单id                                                       |
> | └packName            | String              | 套餐名                                                       |
> | └packNum             | Integer             | 套餐数量                                                     |
> | └ebizsjdqb2DTO       | List<Ebizsjdqb2DTO> |                                                              |
> | └└dishNames          | String              | 单品名                                                       |
> | └└dishNums           | Integer             | 单品数量                                                     |
> | ebizsjdqb1DTO        | List<Ebizsjdqb1DTO> |                                                              |
> | └dishName            | String              | 单品名                                                       |
> | └dishNum             | Integer             | 单品数量                                                     |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total": 2,
        "list": [
            {
                "id": 1,
                "ebizCustomerId": 1,
                "orderNo": "10000001",
                "takeFoodWay": 0,
                "orderStatus": 2,
                "deliveryMan": "张三",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-27 13:00:00",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    null
                ],
                "ebizsjdqb1DTO": [
                    {
                        "dishName": "鱼香肉丝",
                        "dishNum": 1
                    },
                    {
                        "dishName": "米饭",
                        "dishNum": 1
                    }
                ]
            },
            {
                "id": 2,
                "ebizCustomerId": 2,
                "orderNo": "10000002",
                "takeFoodWay": 1,
                "orderStatus": 3,
                "deliveryMan": "张三",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-27 14:00:00",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    },
                    {
                        "packName": "套餐B",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "螃蟹",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            }
        ]
    }
}
```

### 6.点击订单当前按钮修改状态（PC端）

> 描述：点击订单当前按钮修改状态

#### **URL**

> /conorder/updateButtomStatus

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数        | 必选 | 类型    |   说明   |
| :---------- | :--- | :------ | :------: |
| id          | 是   | Integer |  订单id  |
| orderStatus | 是   | Integer | 订单状态 |
| deliveryMan | 否   | String  |  送餐人  |
| username    | 否   | String  |  用户名  |

#### **参数示例** 

```json
{    "id":5,
 	 "orderStatus":3，
 	 "deliveryMan":"张三"，
 	 "username":"老王"
}
```

#### **返回字段**

> | 返回字段             | 字段类型            | 说明                                                         |
> | :------------------- | :------------------ | :----------------------------------------------------------- |
> | id                   | Integer             | 自增主键id                                                   |
> | ebizCustomerId       | Integer             | 客户id                                                       |
> | orderNo              | String              | 订单号                                                       |
> | takeFoodWay          | Integer             | 取餐方式（0-外卖，1-自提）                                   |
> | orderStatus          | Integer             | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | deliveryMan          | String              | 送餐人                                                       |
> | placeOrderTime       | date                | 下单时间                                                     |
> | requiredDeliveryTime | date                | 要求送餐时间                                                 |
> | deliveryTime         | date                | 送餐时间                                                     |
> | ebizsjdqbDTO         | List<EbizsjdqbDTO>  | ）                                                           |
> | └id                  | Integer             | 订单id                                                       |
> | └packName            | String              | 套餐名                                                       |
> | └packNum             | Integer             | 套餐数量                                                     |
> | └ebizsjdqb2DTO       | List<Ebizsjdqb2DTO> |                                                              |
> | └└dishNames          | String              | 单品名                                                       |
> | └└dishNums           | Integer             | 单品数量                                                     |
> | ebizsjdqb1DTO        | List<Ebizsjdqb1DTO> |                                                              |
> | └dishName            | String              | 单品名                                                       |
> | └dishNum             | Integer             | 单品数量                                                     |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total": 2,
        "list": [
            {
                "id": 1,
                "ebizCustomerId": 1,
                "orderNo": "10000001",
                "takeFoodWay": 0,
                "orderStatus": 2,
                "deliveryMan": "张三",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-27 13:00:00",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    null
                ],
                "ebizsjdqb1DTO": [
                    {
                        "dishName": "鱼香肉丝",
                        "dishNum": 1
                    },
                    {
                        "dishName": "米饭",
                        "dishNum": 1
                    }
                ]
            },
            {
                "id": 2,
                "ebizCustomerId": 2,
                "orderNo": "10000002",
                "takeFoodWay": 1,
                "orderStatus": 3,
                "deliveryMan": "张三",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-27 14:00:00",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    },
                    {
                        "packName": "套餐B",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "螃蟹",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            }
        ]
    }
}
```

### 7.查询全部快递员姓名（PC端）

> 描述：根据人员权限查询全部快递员姓名

#### **URL**

> /conorder/selectByEbizRoleId

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数         | 必选 | 类型    |  说明  |
| :----------- | :--- | :------ | :----: |
| byEbizRoleId | 是   | Integer | 角色id |

#### **参数示例** 

```json
{
    "byEbizRoleId":3
}
```

#### **返回字段**

> | 返回字段 | 字段类型 | 说明         |
> | :------- | :------- | :----------- |
> | 用户名   | username | 快递员用户名 |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": [
        {
            "roleName": "张三"
        }
    ]
}
```

### 8.查询该客户历史订单信息（手机端） 

> 描述：查询该客户历史订单信息（手机端）

#### **URL**

> /conorder/selectByebizCustomerId

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数           | 必选 | 类型    |   说明   |
| :------------- | :--- | :------ | :------: |
| pageSize       | 是   | Integer | 分页页长 |
| pageNum        | 是   | Integer | 当前页码 |
| ebizCustomerId | 是   | Integer |  客户id  |

#### **参数示例** 

```json
{
    "ebizCustomerId":1，
    "pageSize":5,
    "pageNum":1,
}
```

#### **返回字段**

> | 返回字段       | 字段类型            | 说明                                                         |
> | :------------- | :------------------ | :----------------------------------------------------------- |
> | id             | Integer             | 自增主键id                                                   |
> | ebizCustomerId | Integer             | 客户id                                                       |
> | orderNo        | String              | 订单号                                                       |
> | takeFoodWay    | Integer             | 取餐方式（0-外卖，1-自提）                                   |
> | price          | BigDecimal          | 总价格                                                       |
> | orderStatus    | Integer             | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | ebizsjdqbDTO   | List<EbizsjdqbDTO>  |                                                              |
> | └id            | Integer             | 订单id                                                       |
> | └packName      | String              | 套餐名                                                       |
> | └packNum       | Integer             | 套餐数量                                                     |
> | └ebizsjdqb2DTO | List<Ebizsjdqb2DTO> |                                                              |
> | └└dishNames    | String              | 单品名                                                       |
> | └└dishNums     | Integer             | 单品数量                                                     |
> | ebizsjdqb1DTO  | List<Ebizsjdqb1DTO> |                                                              |
> | └dishName      | String              | 单品名                                                       |
> | └dishNum       | Integer             | 单品数量                                                     |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total": 2,
        "list": [
            {
                "id": 2,
                "ebizCustomerId": 2,
                "orderNo": "10000002",
                "orderUser": "刘远辉",
                "orderPhone": "18522608634",
                "statusDisplay": 0,
                "takeFoodWay": 1,
                "price": 30,
                "orderStatus": 4,
                "deliveryMan": "张三",
                "deliveryAddress": "一号楼",
                "refundReason": "别找我我没退款",
                "remarks": "实打实大四大所",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-25 14:00:00",
                "productionTime": "2021-08-25 12:34:22",
                "producer": "王师傅",
                "completedTime": "2021-08-25 12:25:48",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "id": 2,
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            },
            {
                "id": 3,
                "ebizCustomerId": 2,
                "orderNo": "10000003",
                "orderUser": "刘远辉",
                "orderPhone": "18522608634",
                "statusDisplay": 0,
                "takeFoodWay": 1,
                "price": 30,
                "orderStatus": 5,
                "deliveryMan": "张三",
                "deliveryAddress": "一号楼",
                "refundReason": "别找我我没退款",
                "remarks": "实打实大四大所",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-25 14:30:00",
                "productionTime": "2021-08-25 12:34:22",
                "producer": "王师傅",
                "completedTime": "2021-08-25 12:25:48",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "id": 3,
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            }
        ]
    }
}
```

### 9. 按照订单orderNo查询订单信息（手机端） 

> 描述：按照订单id查询订单信息（手机端） 

#### **URL**

> /conorder/selectByebizCustomerId

#### **HTTP请求方式**

> POST请求

#### **请求参数**

> 参数格式：JSON

| 参数    | 必选 | 类型   |  说明  |
| :------ | :--- | :----- | :----: |
| orderNo | 是   | String | 订单号 |

#### **参数示例** 

```json
{
    "orderNo":"10000002"
}
```

#### **返回字段**

> | 返回字段       | 字段类型            | 说明                                                         |
> | :------------- | :------------------ | :----------------------------------------------------------- |
> | id             | Integer             | 自增主键id                                                   |
> | ebizCustomerId | Integer             | 客户id                                                       |
> | orderNo        | String              | 订单号                                                       |
> | orderUser      | String              | 订餐人                                                       |
> | takeFoodWay    | Integer             | 取餐方式（0-外卖，1-自提）                                   |
> | price          | BigDecimal          | 总价格                                                       |
> | orderStatus    | Integer             | 订单状态（0-付款中，1-付款失败，2-已付款，3-制作中，4-制作完成，5-配送中，6-已送达，7-已自提，8-退款失败，9-退款成功） |
> | remarks        | String              | 备注                                                         |
> | placeOrderTime | date                | 下单时间                                                     |
> | deliveryTime   | date                | 送餐时间                                                     |
> | forwardingTime | date                | 送达时间                                                     |
> | ebizsjdqbDTO   | List<EbizsjdqbDTO>  |                                                              |
> | └id            | Integer             | 订单id                                                       |
> | └packName      | String              | 套餐名                                                       |
> | └packNum       | Integer             | 套餐数量                                                     |
> | └ebizsjdqb2DTO | List<Ebizsjdqb2DTO> |                                                              |
> | └└dishNames    | String              | 单品名                                                       |
> | └└dishNums     | Integer             | 单品数量                                                     |
> | ebizsjdqb1DTO  | List<Ebizsjdqb1DTO> |                                                              |
> | └dishName      | String              | 单品名                                                       |
> | └dishNum       | Integer             | 单品数量                                                     |

#### **返回值示例**

```json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total": 1,
        "list": [
            {
                "id": 2,
                "ebizCustomerId": 2,
                "orderNo": "10000002",
                "orderUser": "刘远辉",
                "orderPhone": "18522608634",
                "statusDisplay": 0,
                "takeFoodWay": 1,
                "price": 30,
                "orderStatus": 4,
                "deliveryMan": "张三",
                "deliveryAddress": "一号楼",
                "refundReason": "别找我我没退款",
                "remarks": "实打实大四大所",
                "placeOrderTime": "2021-08-25 08:33:37",
                "requiredDeliveryTime": "2021-08-25 14:00:00",
                "productionTime": "2021-08-25 12:34:22",
                "producer": "王师傅",
                "completedTime": "2021-08-25 12:25:48",
                "deliveryTime": "2021-08-25 12:30:03",
                "forwardingTime": "2021-08-25 13:00:00",
                "ebizsjdqbDTO": [
                    {
                        "id": 2,
                        "packName": "套餐A",
                        "packNum": 1,
                        "ebizsjdqb2DTO": [
                            {
                                "dishNames": "鱼香肉丝",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "拍黄瓜",
                                "dishNums": 1
                            },
                            {
                                "dishNames": "米饭",
                                "dishNums": 1
                            }
                        ]
                    }
                ],
                "ebizsjdqb1DTO": [
                    null
                ]
            }
        ]
    }
}
```

# 杜宏磊的接口

### IP地址

192.168.11.180:8081

### 后台用户登录页面

#### 登录接口

> 描述：登录接口

**URL**

> /user/login

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明   |
> | :------- | :--- | :----- | ------ |
> | username | 是   | String | 用户名 |
> | password | 是   | String | 密码   |

**参数示例**

```json
{
    "username":"zhangsan",
    "password":"12345678"
}
```

**返回字段**

> | 返回字段   | 字段类型     | 说明                |
> | :--------- | :----------- | :------------------ |
> | role       | List<RoleVO> |                     |
> | └ roleName | String       | 角色名称            |
> | id         | int          | 当前登录的用户id    |
> | token      | String       | 登录成功，颁发token |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "role": [
            {
                "roleName": "超级管理员"
            },
            {
                "roleName": "内勤"
            },
            {
                "roleName": "客户"
            }
        ],
        "id": 1,
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwiZXhwIjoxNjMxNDMwMDY0LCJ1c2VybmFtZSI6InpoYW5nc2FuIn0.Nekaqap2QRKg0SXyMP03CgYkdGjs_tYMUyg5hmZ1ARo"
    }
}
```



### 系统管理

#### 用户管理页面

##### 1、用户名模糊查询接口

> 描述：用户名模糊查询接口（查询条件，是否禁用）

**URL**

> /user/listLikeUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | username | 否   | String | 用户名           |
> | pageNum  | 是   | int    | 当前页数（页码） |
> | pageSize | 是   | int    | 每页中的条数     |
>
> **参数示例**

```json
{
    "username":""，
    "pageNum":1,
    "pageSize":10
}
```

**返回字段**

> | 返回字段              | 字段类型          | 说明                       |
> | :-------------------- | :---------------- | :------------------------- |
> | total                 | long              | 查询总条数                 |
> | list                  | List<UserRoleDTO> |                            |
> | └ id                  | int               | 主键id                     |
> | └ username            | String            | 用户名                     |
> | └ desensitizePassword | String            | 密码（脱敏）               |
> | └ password            | String            | 密码                       |
> | └ phone               | String            | 手机号（脱敏）             |
> | └ userStatus          | int               | 用户状态码，0-启用，1-禁用 |
> | └ listRoles           | List<Role>        |                            |
> | └ └ roleName          | String            | 角色名                     |
> | └ createdDate         | datetime          | 用户创建时间               |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 6,
        "list": [
            {
                "id": 1,
                "username": "zhangsan",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "333****",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    },
                    {
                        "roleName": "客户"
                    }
                ],
                "createdDate": "2021-08-24 16:25:15"
            },
            {
                "id": 2,
                "username": "lisi",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****2434",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    }
                ],
                "createdDate": "2021-08-25 11:19:09"
            },
            {
                "id": 3,
                "username": "张三",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": null,
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    }
                ],
                "createdDate": "2021-08-26 19:24:32"
            },
            {
                "id": 4,
                "username": "wangwu",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    }
                ],
                "createdDate": "2021-08-26 19:26:22"
            },
            {
                "id": 5,
                "username": "zhaoliu",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [],
                "createdDate": "2021-08-27 14:31:14"
            },
            {
                "id": 6,
                "username": "赵武",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    },
                    {
                        "roleName": "厨师"
                    }
                ],
                "createdDate": "2021-08-27 14:33:01"
            }
        ]
    }
}
```



##### 2、根据id查询

> 描述：根据id查询

**URL**

> /user/getUserById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数 | 必选 | 类型 | 说明       |
> | :--- | :--- | :--- | ---------- |
> | id   | 是   | int  | 用户当前id |
>
> **参数示例**

```json
http://localhost:8081/user/getUserById?id=1
```

**返回字段**

> | 返回字段            | 字段类型   | 说明                     |
> | :------------------ | :--------- | :----------------------- |
> | id                  | int        | 用户表主键id             |
> | username            | String     | 用户名                   |
> | desensitizePassword | String     | 密码（脱敏）             |
> | password            | String     | 密码                     |
> | phone               | String     | 手机号（脱敏）           |
> | userStatus          | int        | 用户状态，0-启用，1-禁用 |
> | listRole            | List<Role> |                          |
> | └ roleName          | String     | 角色名                   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "id": 1,
        "username": "zhangsan",
        "desensitizePassword": "************",
        "password": "12345678",
        "phone": "333****",
        "userStatus": 0,
        "listRole": [
            {
                "roleName": "超级管理员"
            },
            {
                "roleName": "内勤"
            },
            {
                "roleName": "客户"
            }
        ],
        "createdDate": "2021-08-24 16:25:15"
    }
}
```



##### 3、更新用户数据

> 描述：接收用户所有修改的数据进行更新用户数据（不对密码进行修改）

**URL**

> /user/updateUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型   | 说明         |
> | :------- | :--- | :----- | ------------ |
> | id       | 是   | int    | 用户当前id   |
> | username | 否   | String | 用户名       |
> | password | 否   | String | 密码（脱敏） |
> | phone    | 是   | String | 手机号       |
>
> **参数示例**

```json
{
    "id":1,
    "username":"张三",
    "password":"********",
    "phone":"23456789034"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "更新成功",
    "content": null
}
```



##### 4、新增用户接口

> 描述：新增用户数据

**URL**

> /user/addUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数       | 必选 | 类型       | 说明                                             |
> | :--------- | :--- | :--------- | ------------------------------------------------ |
> | username   | 是   | String     | 用户名                                           |
> | password   | 是   | String     | 密码                                             |
> | phone      | 是   | String     | 手机号                                           |
> | listRole   | 是   | List<Role> |                                                  |
> | └ roleName | 是   | String     | 角色变量，1-超级管理员，2-内勤，3-厨师，4-配送员 |
>
> **参数示例**

```json
{
    "username":"wangwu",
    "password":"12345678",
    "phone":"13113113113",
    "listRole":[
        {
            "roleName":"超级管理员"
        },
        {
            "roleName":"内勤"
        }
    ]
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": null
}
```



##### 5、删除用户接口

> 描述：删除用户数据（需要删除用户表中的用户以及和用户关联角色的表中的字段）

**URL**

> /user/delUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/delUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 6、禁用用户接口

> 描述：禁用用户数据

**URL**

> /user/disableUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/disableUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "禁用成功",
    "content": null
}
```





##### 7、启用用户接口

> 描述：启用用户数据

**URL**

> /user/enableUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/enableUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "启用成功",
    "content": null
}
```



##### 8、查询全部角色名称

> 描述：查询全部角色的名称

**URL**

> /role/listUserRoles

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> **参数示例**

```json
http://localhost:8081/role/listUserRoles
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | total      | long       | 查询总条数 |
> | list       | List<Role> |            |
> | └ id       | int        | 角色的id   |
> | └ roleName | String     | 角色名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 4,
        "list": [
            {
                "id": 1,
                "roleName": "超级管理员"
            },
            {
                "id": 2,
                "roleName": "内勤"
            },
            {
                "id": 3,
                "roleName": "厨师"
            },
            {
                "id": 4,
                "roleName": "配送员"
            }
        ]
    }
}
```





#### 角色管理页面



##### 1、查询角色名与其对应的所有用户名（模糊查：角色名称）

> 描述：查询角色名和对应的所有用户名

**URL**

> /role/listLikeRoleAndUsername

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | roleName | 否   | String | 角色名称         |
> | pageNum  | 是   | int    | 当前页数（页码） |
> | pageSize | 是   | int    | 每页中的条数     |
>
> **参数示例**

```json
{
    "roleName":"",
    "pageNum":1,
    "pageSize":10
}
```

**返回字段**

> | 返回字段       | 字段类型      | 说明                   |
> | :------------- | :------------ | :--------------------- |
> | total          | long          | 查询总条数             |
> | list           | List<ReloDTO> |                        |
> | └  roleName    | String        | 角色名称               |
> | └  users       | List<UserVO>  |                        |
> | └  └  username | String        | 当前角色所对应的用户名 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 5,
        "list": [
            {
                "id": 1,
                "roleName": "超级管理员",
                "users": [
                    {
                        "username": "zhangsan"
                    },
                    {
                        "username": "lisi"
                    },
                    {
                        "username": "张三"
                    },
                    {
                        "username": "wangwu"
                    },
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 2,
                "roleName": "内勤",
                "users": [
                    {
                        "username": "zhangsan"
                    },
                    {
                        "username": "张三"
                    },
                    {
                        "username": "wangwu"
                    },
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 3,
                "roleName": "厨师",
                "users": [
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 4,
                "roleName": "配送员",
                "users": []
            },
            {
                "id": 5,
                "roleName": "客户",
                "users": [
                    {
                        "username": "zhangsan"
                    }
                ]
            }
        ]
    }
}
```



##### 2、添加角色

> 描述：添加角色（只添加角色名称）

**URL**

> /role/addRole

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明     |
> | :------- | :--- | :----- | -------- |
> | roleName | 是   | String | 角色名称 |
>
> **参数示例**

```json
{
    "roleName":"后勤"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "添加成功",
    "content": null
}
```



##### 3、删除角色

> 描述：删除角色（删除相关联当前角色的所有用户关联）

**URL**

> /role/delRole

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json

> | 参数   | 必选 | 类型 | 说明     |
> | :----- | :--- | :--- | -------- |
> | roleId | 是   | int  | 角色的id |
>
> **参数示例**

```json
http://localhost:8081/role/delRole?roleId=2
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 4、编辑角色

> 描述：修改角色名称

**URL**

> /role/updateRole

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | id       | 是   | int    | 当前角色id       |
> | roleName | 是   | String | 修改后的角色名称 |
>
> **参数示例**

```json
{
    "id":1,
    "roleName":"管理员"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "修改成功",
    "content": null
}
```



##### 5、为角色分配菜单

> 描述：为角色分配多个菜单（检查当前角色对应的菜单是否存在关系）

**URL**

> /role/distributeMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型       | 说明   |
> | :------- | :--- | :--------- | ------ |
> | roleId   | 是   | int        | 角色id |
> | listMenu | 是   | List<Menu> |        |
> | └ menuId | 是   | int        | 菜单id |

**参数示例**

```json
{
    "roleId":1,
    "listRole":[
        {
            "menuId":1
        },
        {
            "menuId":2
        },
        {
            "menuId":3
        },
        {
            "menuId":4
        },
        {
            "menuId":5
        }
    ]
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": null
}
```



##### 6、根据id查询当前角色下的所有菜单信息

> 描述：查询全部菜单的菜单名称

**URL**

> /menu/listMenusById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json
>
> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | roleId | 是   | int  | 角色id |

**参数示例**

```json
http://localhost:8081/menu/listMenusById?roleId=1
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | listMenu   | List<Menu> |            |
> | └ id       | int        | 角色的id   |
> | └ parentId | int        | 角色的父id |
> | └ menuName | String     | 菜单名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "listMenu": [
            {
                "id": 2,
                "parentId": 1,
                "menuName": "用户管理"
            }
        ]
    }
}
```





#### 菜单管理页面

##### 1、查询所有菜单信息

> 描述：查询全部菜单的菜单名称

**URL**

> /menu/listMenus

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型 | 说明       |
> | :------- | :--- | :--- | ---------- |
> | pageNum  | 是   | int  | 页码       |
> | pageSize | 是   | int  | 每页的条数 |

**参数示例**

```json
{
    "pageNum":1,
    "pageSize":10
}
```

**返回字段**

> | 返回字段   | 字段类型     | 说明       |
> | :--------- | :----------- | :--------- |
> | total      | long         | 查询总条数 |
> | listMenu   | List<MenuVO> |            |
> | └ id       | int          | 角色的id   |
> | └ parentId | int          | 角色的父id |
> | └ menuName | String       | 菜单名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 2,
        "listMenu": [
            {
                "id": 1,
                "parentId": null,
                "menuName": "菜单管理"
            },
            {
                "id": 2,
                "parentId": 1,
                "menuName": "用户管理"
            }
        ]
    }
}
```



##### 2、删除菜单信息

> 描述：删除菜单信息

**URL**

> /menu/delMenu

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json
>
> | 参数 | 必选 | 类型 | 说明   |
> | :--- | :--- | :--- | ------ |
> | id   | 是   | int  | 菜单id |

**参数示例**

```json
http://localhost:8081/menu/delMenu?id=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 3、修改菜单信息

> 描述：修改菜单的菜单名称（可批量）

**URL**

> /menu/updateMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数       | 必选 | 类型           | 说明         |
> | :--------- | :--- | :------------- | ------------ |
> | menus      | 是   | List<EbizMenu> |              |
> | └ id       | 是   | int            | id           |
> | └ menuName | 是   | String         | 菜单的新名称 |

**参数示例**

```json
{
    "menus":[
        {
            "id":1,
            "menuName":"01"
        },
        {
            "id":2,
            "menuName":"02"
        }
    ]
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": null
}
```



##### 4、新增菜单信息

> 描述：新增菜单信息

**URL**

> /menu/addMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型   | 说明     |
> | :------- | :--- | :----- | -------- |
> | parentId | 否   | int    | 父id     |
> | menuName | 是   | String | 菜单名称 |

**参数示例**

```json
{
    "parentId":1,
    "menuName":"新增用户管理"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "添加成功",
    "content": null
}
```



#### 修改密码页面

##### 修改密码

> 描述：修改当前用户的密码

**URL**

> /user/updateUserPassword

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数        | 必选 | 类型   | 说明       |
> | :---------- | :--- | :----- | ---------- |
> | id          | 是   | int    | 用户当前id |
> | username    | 否   | String | 用户名     |
> | password    | 是   | String | 原密码     |
> | newPassword | 是   | String | 新密码     |
>
> **参数示例**

```json
{
    "id":1,
    "username":"zhangsan",
    "password":"12345678",
    "newPassword":"23456789034"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "密码修改成功",
    "content": null
}
```



# 李浩文接口

## 参数管理

### 1.参数管理-查询所有父配置接口

#### URL

/config/selectAllFather

#### HTTP请求方式

POST

#### 请求参数

无

##### 请求示例

```
{

}
```

#### 返回字段

| 返回字段   | 字段类型        | 说明       |
| ---------- | --------------- | ---------- |
| configList | List<ConfigDTO> | 父配置List |

**ConfigDTO**

| 返回字段         | 字段类型 | 说明                       |
| ---------------- | -------- | -------------------------- |
| id               | int      | 主键id                     |
| configType       | String   | 类型                       |
| configValueCode1 | String   | 类型值1                    |
| configValueCode2 | String   | 类型值2                    |
| isConfig         | int      | 是否可配，0-不可配，1-可配 |
| remarks          | String   | 备注                       |
| parentId         | int      | 父ID                       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"content":{
		"configList":[{
			"id":1,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":
		},
		{
			"id":2,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":
		}]
	}
}
```

### 2.参数管理-根据父id查询所有配置接口

#### URL

/config/selectAll

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明           |
| ---- | ---- | ---- | -------------- |
| id   | 是   | int  | 父配置(标签)id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段           | 字段类型                | 说明       |
| ------------------ | ----------------------- | ---------- |
| configChildrenList | List<ConfigChildrenDTO> | 子配置List |

**ConfigChildrenDTO**

| 返回字段         | 字段类型                | 说明                       |
| ---------------- | ----------------------- | -------------------------- |
| id               | int                     | 主键id                     |
| configType       | String                  | 类型                       |
| configValueCode1 | String                  | 类型值1                    |
| configValueCode2 | String                  | 类型值2                    |
| isConfig         | int                     | 是否可配，0-不可配，1-可配 |
| remarks          | String                  | 备注                       |
| parentId         | int                     | 父ID                       |
| Childrens        | List<ConfigChildrenDTO> | 当前配置的子配置列表       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"content":{
		"configChildrenList":[{
			"id":2,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":1，
			"Childrens":[]
		},
		{
			"id":3,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":1,
			"Childrens":[]
		}]
	}
}
```



### 3.参数管理-根据id查询接口

#### URL

/config/selectById

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明   |
| ---- | ---- | ---- | ------ |
| id   | 是   | int  | 配置id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段         | 字段类型 | 说明                       |
| ---------------- | -------- | -------------------------- |
| id               | int      | 主键id                     |
| configType       | String   | 类型                       |
| configValueCode1 | String   | 类型值1                    |
| configValueCode2 | String   | 类型值2                    |
| isConfig         | int      | 是否可配，0-不可配，1-可配 |
| remarks          | String   | 备注                       |
| parentId         | int      | 父ID                       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询成功"
	"content":{
		"id":1,
		"configType":"1",
		"configValueCode1":"1",
		"configValueCode2":"1",
		"isConfig":1,
		"remarks":"1",
		"parentId":
	}
}
```

### 4.参数管理-删除接口

#### URL

/config/deleteById

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明   |
| ---- | ---- | ---- | ------ |
| id   | 是   | int  | 配置id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 删除结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"删除成功"
}
```

### 5.参数管理-修改接口

#### URL

/config/updateById

#### HTTP请求方式

POST

#### 请求参数

| 参数             | 必选 | 类型   | 说明                       |
| ---------------- | ---- | ------ | -------------------------- |
| id               | 是   | int    | 配置id                     |
| configType       | 否   | String | 类型                       |
| configValueCode1 | 否   | String | 类型值1                    |
| configValueCode2 | 否   | String | 类型值2                    |
| isConfig         | 否   | int    | 是否可配，0-不可配，1-可配 |
| remark           | 否   | String | 备注                       |
| parentId         | 否   | int    | 父ID                       |

##### 请求示例

```
{
	"id":1,
	"configType":"1",
	"configValueCode1":"1",
	"configValueCode2":"1",
	"isConfig":1,
	"remarks":"1",
	"parentId":
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 修改结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"修改成功"
}
```

### 6.参数管理-增加接口

#### URL

/config/addConfig

#### HTTP请求方式

POST

#### 请求参数

| 参数             | 必选 | 类型   | 说明                       |
| ---------------- | ---- | ------ | -------------------------- |
| configType       | 是   | String | 类型                       |
| configValueCode1 | 是   | String | 类型值1                    |
| configValueCode2 | 否   | String | 类型值2                    |
| isConfig         | 是   | int    | 是否可配，0-不可配，1-可配 |
| remark           | 否   | String | 备注                       |
| parentId         | 否   | int    | 父ID                       |

##### 请求示例

```
{
	"configType":"1",
	"configValueCode1":"1",
	"configValueCode2":"1",
	"isConfig":1,
	"remarks":"1",
	"parentId":
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 添加结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"添加成功"
}
```

## 首页统计

### 7.首页统计-查询当日订单统计信息接口

#### URL

/index/statistical

#### HTTP请求方式

POST

#### 请求参数

无

##### 请求示例

```
{

}
```

#### 返回字段

| 返回字段    | 字段类型   | 说明         |
| ----------- | ---------- | ------------ |
| todayOrder  | int        | 今日订单数   |
| waitOrder   | int        | 待制作订单数 |
| makingOrder | int        | 制作中订单数 |
| sendOrder   | int        | 配送中订单数 |
| finishOrder | int        | 已完成订单数 |
| refundOrder | int        | 退款订单数   |
| income      | BigDecimal | 今日收入     |

##### 返回值示例

```
{
	"code":200,
	"message":"查询成功",
	"content":{
		"todayOrder": 10,
    	"waitOrder": 1,
    	"makingOrder": 1,
    	"sendOrder": 3,
    	"finishOrder": 5,
    	"refundOrder": 0,
    	"income": 1000
	}
}
```

## 手机端

### 8.9.手机端-套餐&单品去支付接口（双接口）

ps：套餐使用packageList，单品使用dishList

#### URL

/phone/setOrder

#### HTTP请求方式

POST

#### 请求参数

| 参数        | 必选 | 类型                | 说明                     |
| ----------- | ---- | ------------------- | ------------------------ |
| customerId  | 是   | int                 | 当前登录的用户id         |
| packageList | 否   | List<PackageMsgDTO> | 套餐列表                 |
| dishList    | 否   | List<DishDTO>       | 菜品列表                 |
| name        | 是   | String              | 下单人姓名               |
| phone       | 是   | String              | 下单人手机号             |
| orderType   | 否   | int                 | 取餐方式，0-外卖，1-自提 |
| price       | 是   | int                 | 价格                     |
| address     | 否   | String              | 地址                     |
| time        | 否   | Date                | 送餐时间                 |
| remarks     | 否   | String              | 备注                     |

**DishDTO**

| 参数     | 必选 | 类型   | 说明     |
| -------- | ---- | ------ | -------- |
| dishId   | 是   | int    | 菜品id   |
| dishNum  | 是   | int    | 菜品数量 |
| dishName | 是   | String | 菜品名称 |

**PackageDTO**

| 参数        | 必选 | 类型          | 说明           |
| ----------- | ---- | ------------- | -------------- |
| packageId   | 是   | int           | 套餐id         |
| packageNum  | 是   | int           | 套餐数量       |
| packageName | 是   | String        | 套餐名称       |
| dishList    | 是   | List<DishDTO> | 套餐内菜品列表 |

##### 请求示例

```
{
	"customerId":1,
	"dishList":[{
		"dishId":1,
		"dishNum":1
		"dishName":"aaa"
	},{
		"dishId":2,
		"dishNum":1
		"dishName":"bbb"
	}],
	"packageList":[
	
	],
	"name":"111",
	"phone":"13222222222",
	"orderType":0,
	"price":12,
	"address":"111",
	"time":2020-11-11 11:11:11,
	"remarks":"111"
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 下单结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"下单成功"
	"content":{}
}
```

### 10.手机端-退单接口

#### URL

/phone/deleteOrder

#### HTTP请求方式

POST

#### 请求参数

| 参数    | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| orderId | 是   | String | 订单号   |
| cause   | 否   | String | 退款原因 |

##### 请求示例

```
{
	"orderId":"111",
	"cause":"111"
}
```

#### 返回字段

| 参数    | 类型   | 说明     |
| ------- | ------ | -------- |
| message | String | 退单结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"退款成功"
}
```

### 11.手机端-退单结果接口

#### URL

/phone/deleteOrder

#### HTTP请求方式

POST

#### 请求参数

| 参数    | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| orderId | 是   | String | 订单号   |
| cause   | 否   | String | 退款原因 |

##### 请求示例

```
{
	"orderId":"111",
	"cause":"111"
}
```

#### 返回字段

| 参数  | 类型   | 说明     |
| ----- | ------ | -------- |
| cause | String | 退单原因 |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"cause":"111"
}
```

# 韩煜接口

> **一些枚举值对应信息**
>
> 
>
> - 菜品类型
>   - 0---------->主食
>   - 1---------->热菜
>   - 2----------->凉菜		
> - 餐别类型(数字是String)
>   - 0---------->早
>   - 01--------->早中
>   - 02---------->早晚
>   - 012-------->早中晚
>   - 1------------>中
>   - 12----------->中晚
>   - 2------------->晚
> - 



# 公共信息

**基础路径**：（跟谁对接口先用谁的地址）

**基础返回结构**

> | 参数    | 类型    | 说明                                               |
> | :------ | :------ | -------------------------------------------------- |
> | code    | Integer | 调用状态码：200成功，400/500失败（其它code码待定） |
> | message | String  | 接口调用情况                                       |
> | content | T       | 内容(任意类型)                                     |

**基础返回示例**

```json
{
    "code": 0,
    "message": "成功信息",
    "content": {
    }
}
```

**header信息说明**

> 除了登录接口外，其他接口都需要认证，所以header中需要带token

**一些枚举值对应信息**

> * **菜品**
>   * 0 ------ 单品
>   * 1 ------ 套餐
> * **图片对应**
>   * 0 ------ 列表页
>   * 1 ------ 详情页
> * **餐别**
>   * 0 ------ 早
>   * 1 ------ 中
>   * 2 ------ 晚
>   * 01 ------ 早中
>   * 02 ------ 早晚
>   * 12 ------ 中晚
>   * 012 ------ 早中晚
> * **套餐状态**
>   * 0 ------ 已下架
>   * 1 ------ 未下架
> * **员工状态**
>   * 0 ------ 未被禁用
>   * 1 ------ 已被禁用
> * **客户类型**
>   * 0 ------ 员工
>   * 1 ------ 病人
> * **订单状态**
>   * 0 ------ 成功
>   * 1 ------ 失败
> * **菜品类型**
>   * 0 ------ 主食
>   * 1 ------ 热菜
>   * 2 ------ 凉菜
> * **菜品状态**
>   * 0 ------ 已下架
>   * 1 ------ 未下架
> * **角色**
>   * 1 ------ 超级管理员
>   * 2 ------ 内勤
>   * 3 ------ 配送员
>   * 4 ------ 客户
> * **前端页面状态显示（订单管理2）**
>   * 0 ------ 显示
>   * 1 ------ 不显示
> * **取餐方式（订单管理2）**
>   * 0 ------ 外卖
>   * 1 ------ 自提
> * **订单状态**
>   * 0 ------ 付款中
>   * 1 ------ 付款失败
>   * 2 ------ 已付款
>   * 3 ------ 制作中
>   * 4 ------ 制作完成
>   * 5 ------ 配送中
>   * 6 ------ 已送达
>   * 7 ------ 已自提
>   * 8 ------ 退款失败
>   * 9 ------ 退款成功
> * 

# 张雪松的接口

## 员工管理

#### ip地址：

192.168.9.43

#### 端口：

8081

### 1.员工新增

#### 接口地址

/customer/add

#### 请求方式

POST

#### 请求参数

| 请求字段     | 字段类型 | 说明     | 是否必须 | 备注         |
| ------------ | -------- | -------- | -------- | ------------ |
| EbizCustomer | body     | 员工对象 | true     |              |
| └no          | String   | 职工号   | true     | 六位数字     |
| └name        | String   | 姓名     | true     |              |
| └phone       | String   | 手机号   | true     | 11位数字     |
| └password    | String   | 密码     | true     | 字母数字6-10 |

#### 请求示例

```
{
	"no"："123456"，
	"name"："中学生"，
	"phone"："15100001202"，
	"password"："abc1234"
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```
{
    "code"：200，
    "message"：“新增成功”
    "content"：null
}
```

### 2.员工编辑

#### 接口地址

/customer/modify

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明     | 是否必须 | 备注         |
| ------------ | -------- | -------- | -------- | ------------ |
| EbizCustomer | body     | 员工对象 | true     |              |
| └no          | String   | 职工号   | false    | 六位数字     |
| └name        | String   | 姓名     | false    |              |
| └phone       | String   | 手机号   | false    | 11位数字     |
| └password    | String   | 密码     | false    | 字母数字6-10 |

#### 请求示例

```json
{
	"no":"123456",
	"name":"中学生",
	"phone":"15100001202",
	"password":"abc1234"
}
```





#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"更新成功",
    "content":null
}
```



### 3.员工查询

#### 接口地址

/customer/query

#### 请求方式

post

#### 请求参数

| 请求字段         | 字段类型 | 说明         | 是否必须 | 备注     |
| ---------------- | -------- | ------------ | -------- | -------- |
| CustomerQueryDTO | body     | 员工查询对象 | true     |          |
| └no              | String   | 职工号       | false    | 六位数字 |
| └name            | String   | 姓名         | false    |          |

#### 请求示例

```json
{
    "id":1,
    "no":"123",
    "name":"中学"
}
```



#### 返回字段

| 返回字段 | 字段类型 | 说明   |
| -------- | -------- | ------ |
| id       | int      | 主键id |
| no       | String   | 工号   |
| name     | String   | 姓名   |

#### 返回值示例

```json
{
    “code”:200，
    “message”:“更新成功”
    ”content“:{	
    			"id":1,
				 “no”:“123456”,
   				 “name”:“中学生”
				}
}
```



### 4.员工禁用

#### 接口地址

/customer/Disable

#### 请求方式

get

#### 请求参数

| 请求字段 | 字段类型 | 说明   | 是否必须 | 备注 |
| -------- | -------- | ------ | -------- | ---- |
| id       | int      | 员工id | true     |      |

#### 请求示例

/customer/Disable?id=1

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"禁用/启用成功",
    "content":null
}
```

### 5.员工删除

#### 接口地址

customer/delete

#### 请求方式

get

#### 请求参数

| 请求字段 | 字段类型 | 说明   | 是否必须 | 备注 |
| -------- | -------- | ------ | -------- | ---- |
| id       | int      | 员工id | true     |      |

#### 请求示例

/customer/delete?id=1

#### 返回字段

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回值示例

```json
{
    "code":200,
    "message":"删除成功",
    "content":null
}
```

## 手机端

### 1.用户登录

#### 接口地址

customer/cusLogin

#### 请求方式

post

#### 请求参数

| 请求字段 | 是否必须 | 类型   | 说明   |
| -------- | -------- | ------ | ------ |
| phone    | 是       | 手机号 | 手机号 |
| captcha  | 是       | 手机号 | 验证码 |

#### 请求示例

```json
{
    "phone":"13116598546",
    "captcha":6398
}
```

#### 返回参数

| 返回字段 | 字段类型 | 说明                 |
| -------- | -------- | -------------------- |
| phone    | String   | 当前登录用户的手机号 |

#### 返回示例

```json
{
    "code": 200,
    "message": "登录成功",
    "content": {
        "phone": "13109466486",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6Mjg2NywiZXhwIjoxNjMxNjg5ODMwLCJ1c2VybmFtZSI6IjEzMTA5NDY2NDg2In0.9KCvEqM0ugwB0JvNtTxyqi4y3LvjFAdr3rGJztC1WhA"
    }
}
```

### 2.验证码

#### 接口地址

/captcha

#### 请求方式

post

#### 请求参数

| 字段  | 是否必传 | 类型   | 说明   |
| ----- | -------- | ------ | ------ |
| phone | 是       | String | 手机号 |

#### 请求示例

```json
{
    "phone":"13116598546"
}
```

#### 返回参数

| 返回字段 | 字段类型 | 说明   |
| -------- | -------- | ------ |
| phone    | String   | 手机号 |
| captcha  | int      | 验证码 |

#### 返回示例

```json
{
    "code": 200,
    "message": "success",
    "content": {
        "phone": "13116598546",
        "captcha": 4604
    }
}
```

### 3.员工登录

#### 接口地址

/customer/workerLogin

#### 请求方式

post

#### 请求参数

| 请求字段 | 字段类型 | 说明 | 是否必须 | 备注 |
| -------- | -------- | ---- | -------- | ---- |
| no       | int      | 工号 | true     |      |
| password | String   | 密码 | true     |      |

#### 请求示例

```json
{
    "no":1001,
    "password":"12345678"
}
```

#### 返回参数

| 返回字段 | 字段类型 | 说明   |
| -------- | -------- | ------ |
| id       | int      | 员工id |
| token    | String   | token  |

#### 返回示例

```json
{
    "code": 200,
    "message": "登录成功",
    "content": {
        "id": 1,
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwiZXhwIjoxNjMxNjg5NjAwLCJ1c2VybmFtZSI6IuW8oOS4iSJ9._niMHNtYW2IoyNcevAkt34W10q6rlOF5iiGTKDUaZb4"
    }
}
```



### 4.默认查询工号和手机号

#### 接口地址

/customer/matching

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明         | 是否必须 | 备注     |
| ------------ | -------- | ------------ | -------- | -------- |
| EbizCustomer | body     | 员工查询对象 | true     |          |
| └no          | String   | 工号         | true     | 6位数字  |
| └phone       | String   | 手机号       | true     | 11位数字 |

#### 请求示例

```json
{
    "no":"123456",
    "phone":"12345678910"
}
```



#### 返回参数

null

#### 返回示例

null

### 5.提交新密码

#### 接口地址

/customer/updatepw

#### 请求方式

post

#### 请求参数

| 请求字段     | 字段类型 | 说明         | 是否必须 | 备注         |
| ------------ | -------- | ------------ | -------- | ------------ |
| EbizCustomer | body     | 员工查询对象 | true     |              |
| └captcha     | String   | 验证码       | true     | 4位数字      |
| └password    | String   | 新密码       | true     | 字母数字6-10 |

#### 请求示例

```json
{
    "captcha":"1234",
    "phone":"abc4321"
}
```



#### 返回参数

| 返回字段 | 字段类型 | 说明 |
| -------- | -------- | ---- |
| code     | int      |      |
| message  | String   |      |
| content  | Object   |      |

#### 返回示例

```json
{
    "code":200,
    "message":"修改成功",
    "content":null
}
```

# 李文彩的接口

## 套餐管理

### 1.添加套餐信息图片

> 描述：添加套餐图片信息

**URL**

> /dishPackage/addImage

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：JSON

> | 参数        | 必选 | 类型   | 说明             |
> | ----------- | ---- | ------ | ---------------- |
> | id          | 是   | int    | 图片的id         |
> | imageBase64 | 是   | string | 图片的base64数据 |

**参数实例**

```json
{	
   "imageBase64":"iamgexxxxxxxxxxxxxxxxxxxxx" 
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明                 |
> | -------- | -------- | -------------------- |
> | code     | int      | 状态码               |
> | message  | string   | 返回信息             |
> | content  | int      | 返回的添加的图片的id |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1122445211
}
```

### 2.添加套餐信息

> 描述：添加套餐图片

**URL**

> /dishPackage/addDishPack

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：JSON

> | 参数         | 必选 | 字段类型 | 说明                                                         |
> | ------------ | ---- | -------- | ------------------------------------------------------------ |
> | mealType     | 是   | int      | 商品类别：0菜品，1套餐。                                     |
> | name         | 是   | string   | 套餐名称                                                     |
> | price        | 是   | double   | 套餐价格                                                     |
> | type         | 是   | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | 否   | string   | 套餐描述                                                     |
> | meal         | 是   | List     | 菜品id的List                                                 |
> | └ id         | 是   | int      | 菜品id                                                       |
> | └ num        | 是   | int      | 菜品数量                                                     |
> | listImage    | 是   | int      | id                                                           |
> | detailImages | 是   | List     | 详情页id                                                     |

**参数实例**

```json
{	
    "mealType":1,
    "name":小鸡炖小鸭,
    "price":22.2,
    "type":"012",
    "desc":"野性碰撞",
    "meal":[
    	{"id":201943,"num":1},
		{"id":299943,"num":2}
	],
    "listImage":12345678,
	"detailImages":[1234,3435,4565,39945]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明             |
> | -------- | -------- | ---------------- |
> | code     | int      | 状态码           |
> | message  | string   | 返回信息         |
> | content  | int      | 返回的添加的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 3.删除套餐图片

> 描述：删除套餐图片

**URL**

> /dishPackage/deleteDishPackImage

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 字段类型 | 说明   |
> | ---- | ---- | -------- | ------ |
> | id   | 是   | int      | 图片id |

**参数实例**

```json
/dishPackage/deleteDishPackImage?id=1234467
```

**返回字段**

> | 返回字段 | 字段类型 | 说明           |
> | -------- | -------- | -------------- |
> | code     | int      | 状态码         |
> | message  | string   | 返回信息       |
> | content  | int      | 返回删除的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 4.删除套餐

> 描述：删除套餐

**URL**

> /dishPackage/deleteDishPack

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 字段类型 | 说明   |
> | ---- | ---- | -------- | ------ |
> | id   | 是   | int      | 图片id |

**参数实例**

```json
/dishPackage/deleteDishPack?id=1234467
```

**返回字段**

> | 返回字段 | 字段类型 | 说明           |
> | -------- | -------- | -------------- |
> | code     | int      | 状态码         |
> | message  | string   | 返回信息       |
> | content  | int      | 返回删除的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 5.编辑套餐信息

> 描述：添加套餐图片

**URL**

> /dishPackage/updateDishPack

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：JSON

> | 参数         | 必选 | 字段类型 | 说明                                                         |
> | ------------ | ---- | -------- | ------------------------------------------------------------ |
> | id           | 是   | int      | 套餐id                                                       |
> | mealType     | 是   | int      | 商品类别：0菜品，1套餐。                                     |
> | name         | 是   | string   | 套餐名称                                                     |
> | price        | 是   | double   | 套餐价格                                                     |
> | type         | 是   | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | 否   | string   | 套餐描述                                                     |
> | meal         | 是   | List     | 菜品id的List                                                 |
> | └ id         | 是   | int      | 菜品id                                                       |
> | └ num        | 是   | int      | 菜品数量                                                     |
> | listImage    | 是   | int      | id                                                           |
> | detailImages | 是   | List     | 详情页id                                                     |

**参数实例**

```json
{	
   "mealType":1,
   "id":124456789,
   "name":小鸡炖小鸭,
   "price":22.2,
   "type":"012",
   "desc":"野性碰撞",
   "meal":[
    	{"id":201943,"num":1},
		{"id":299943,"num":2}
	],
    "listImage":12345678,
	"detailImages":[1234,3435,4565,39945]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明             |
> | -------- | -------- | ---------------- |
> | code     | int      | 状态码           |
> | message  | string   | 返回信息         |
> | content  | int      | 返回的添加的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```

### 6.通过餐别查询菜品id和name

> 描述：通过餐别查询菜品

**URL**

> /dishPackage/selectMealIdAndNameByType

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数      | 必选 | 类型   | 说明             |
> | --------- | ---- | ------ | ---------------- |
> | dish_time | 是   | string | 餐别（用餐时间） |

**参数实例**

```json
{
    dish_time:"012"
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明     |
> | :------- | :------- | :------- |
> | id       | int      | 套餐id   |
> | name     | string   | 套餐名称 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        {
        	"id":1234,
            "name":"美味鸡腿饭",
    	},
        {
			"id":1234,
       	 	"name":"美味鸡腿饭2"
        }
    }
}
```

### 7.查询全部套餐信息接口(PC)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectAllPC

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型   | 说明     |
> | -------- | ---- | ------ | -------- |
> | pageNum  | 是   | int    | 分页页码 |
> | pageSize | 是   | int    | 数量     |
> | type     | 否   | string | 餐别     |
> | name     | 否   | string | 餐名     |

**参数实例**

```json
{
    "pageNum":2,
    "pageSize":2,
    "type":"012",
    "name":"小鸡"
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明                                                         |
> | :------- | :------- | :----------------------------------------------------------- |
> | id       | int      | 套餐id                                                       |
> | name     | string   | 套餐名称                                                     |
> | price    | double   | 套餐价格                                                     |
> | type     | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | status   | int      | 套餐状态，0-已下架，1-未下架                                 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        {
        	"id":1234,
            "name":"美味鸡腿饭",
        	"price":12.5,
        	"type":"012",
       	    "status":0
    	},
        {
			"id":1234,
       	 	"name":"美味鸡腿饭2",
       	 	"price":12.5,
       	 	"type":"012",
       	 	"status":0	
        }
    }
}
```

### 8.查询全部套餐信息接口(Phone)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectAllPhone

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型 | 说明     |
> | -------- | ---- | ---- | -------- |
> | pageNum  | 是   | int  | 分页页码 |
> | pageSize | 是   | int  | 数量     |

**参数实例**

```json
{
    "pageNum":2,
    "pageSize":2
}
```

**返回字段**

> | 返回字段   | 字段类型 | 说明                                                         |
> | :--------- | :------- | :----------------------------------------------------------- |
> | id         | int      | 套餐id                                                       |
> | name       | string   | 套餐名称                                                     |
> | price      | double   | 套餐价格                                                     |
> | type       | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc       | string   | 套餐描述                                                     |
> | meals      | List     | 菜品                                                         |
> | └ mealName | string   | 菜品名称                                                     |
> | └ price    | double   | 菜品价格                                                     |
> | └ num      | int      | 该菜在套餐中的数量                                           |
> | listImage  | string   | 列表页图片                                                   |
> | └ id       | int      | 列表页图片id                                                 |
> | └ url      | string   | 列表页图的url                                                |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": [
        {
            "id":1234,
            "name":"美味鸡腿饭",
            "price":12.5,
            "type":"012",
            "desc":"好吃！"
            "meals":[
            {
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            },
 			{
                "mealName":"小鸡炖蘑菇2",
                "price":10.0,
                "num":1
            }
        	],
       	    "listImage":"192.168.11.128:8080//c:iamges/399343.jpg"    
    		},
        	{
             "id":1234,
            "name":"美味鸡腿饭",
            "price":12.5,
            "type":"012",
            "desc":"好吃！"
            "meals":[
            {
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            },
 			{
                "mealName":"小鸡炖蘑菇2",
                "price":10.0,
                "num":1
            }
            ],
      	    "listImage":"192.168.11.128:8080//c:iamges/399343.jpg"
        }
    ]
}
```

### 9.通过id查询套餐信息接口(PC,Phone)

> 描述：通过id查询用户信息

**URL**

> /dishPackage/selectAllPC

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 类型   | 说明   |
> | ---- | ---- | ------ | ------ |
> | id   | 是   | String | 套餐id |

**参数实例**

```json
?id=12
```

**返回字段**

> | 返回字段     | 字段类型 | 说明                                                         |
> | :----------- | :------- | :----------------------------------------------------------- |
> | id           | int      | 套餐id                                                       |
> | name         | string   | 套餐名称                                                     |
> | price        | double   | 套餐价格                                                     |
> | type         | string   | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | desc         | string   | 套餐描述                                                     |
> | meals        | List     | 菜品                                                         |
> | └ mealName   | string   | 菜品名称                                                     |
> | └ price      | double   | 菜品价格                                                     |
> | └ num        | int      | 该菜在套餐中的数量                                           |
> | listImage    | string   | 列表页图片                                                   |
> | └ id         | int      | 列表页图片id                                                 |
> | └ url        | string   | 列表页图的url                                                |
> | detailImages | List     | 详情页                                                       |
> | └ id         | int      | 详情页的图片id                                               |
> | └ url        | string   | 详情页的图片url                                              |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "id":1234,
        "name":"美味鸡腿饭",
        "price":12.5,
        "type":"012",
        "status":0,
        "desc":"非常好吃的鸡腿饭",
        "meals":[
            {
                "mealName":"小鸡炖蘑菇",
                "price":10.0,
                "num":1
            }
        ],
        "listImage":"192.168.11.128:8080//c:iamges/399343.jpg",
        "detailImages":[
            {
                id:1
                url:"192.168.11.128:8080//c:iamges/3993432343.jpg"
            },
             {
                id:2
                url:"192.168.11.128:8080//c:iamges/12399343.jpg"
            }
        ]       
    }
}
```

### 10.上下架

> 描述：修改餐品的状态

**URL**

> /dishPackage/updateStatus

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：String

> | 参数 | 必选 | 类型   | 说明   |
> | ---- | ---- | ------ | ------ |
> | id   | 是   | String | 套餐id |

**参数实例**

```json
/dishPackage/updateStatus?id=12
```

**返回字段**

> | 返回字段 | 字段类型 | 说明               |
> | -------- | -------- | ------------------ |
> | code     | int      | 状态码             |
> | message  | string   | 返回信息           |
> | content  | int      | 返回的上下架的数量 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": 1
}
```



# 杜宏磊的接口

### IP地址

192.168.11.180:8081

### 后台用户登录页面

#### 登录接口

> 描述：登录接口

**URL**

> /user/login

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明   |
> | :------- | :--- | :----- | ------ |
> | username | 是   | String | 用户名 |
> | password | 是   | String | 密码   |

**参数示例**

```json
{
    "username":"zhangsan",
    "password":"12345678"
}
```

**返回字段**

> | 返回字段   | 字段类型     | 说明                |
> | :--------- | :----------- | :------------------ |
> | role       | List<RoleVO> |                     |
> | └ roleName | String       | 角色名称            |
> | token      | String       | 登录成功，颁发token |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "role": [
            {
                "roleName": "超级管理员"
            },
            {
                "roleName": "内勤"
            }
        ],
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwiZXhwIjoxNjMxMzQ3NDI0fQ.Eq4RgDY0k_kBHuD5lVOgYyeciuioh64hhxK48u5I5H4"
    }
}
```



### 系统管理

#### 用户管理页面

##### 1、用户名模糊查询接口

> 描述：用户名模糊查询接口（查询条件，是否禁用）

**URL**

> /user/listLikeUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | username | 否   | String | 用户名           |
> | pageNum  | 是   | int    | 当前页数（页码） |
> | pageSize | 是   | int    | 每页中的条数     |
>
> **参数示例**

```json
{
    "username":""，
    "pageNum":1,
    "pageSize":10
}
```

**返回字段**

> | 返回字段              | 字段类型          | 说明                       |
> | :-------------------- | :---------------- | :------------------------- |
> | total                 | long              | 查询总条数                 |
> | list                  | List<UserRoleDTO> |                            |
> | └ id                  | int               | 主键id                     |
> | └ username            | String            | 用户名                     |
> | └ desensitizePassword | String            | 密码（脱敏）               |
> | └ password            | String            | 密码                       |
> | └ phone               | String            | 手机号（脱敏）             |
> | └ userStatus          | int               | 用户状态码，0-启用，1-禁用 |
> | └ listRoles           | List<Role>        |                            |
> | └ └ roleName          | String            | 角色名                     |
> | └ createdDate         | datetime          | 用户创建时间               |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 6,
        "list": [
            {
                "id": 1,
                "username": "zhangsan",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "333****",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    },
                    {
                        "roleName": "客户"
                    }
                ],
                "createdDate": "2021-08-24 16:25:15"
            },
            {
                "id": 2,
                "username": "lisi",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****2434",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    }
                ],
                "createdDate": "2021-08-25 11:19:09"
            },
            {
                "id": 3,
                "username": "张三",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": null,
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    }
                ],
                "createdDate": "2021-08-26 19:24:32"
            },
            {
                "id": 4,
                "username": "wangwu",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    }
                ],
                "createdDate": "2021-08-26 19:26:22"
            },
            {
                "id": 5,
                "username": "zhaoliu",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [],
                "createdDate": "2021-08-27 14:31:14"
            },
            {
                "id": 6,
                "username": "赵武",
                "desensitizePassword": "************",
                "password": "12345678",
                "phone": "131****3113",
                "userStatus": 0,
                "listRole": [
                    {
                        "roleName": "超级管理员"
                    },
                    {
                        "roleName": "内勤"
                    },
                    {
                        "roleName": "厨师"
                    }
                ],
                "createdDate": "2021-08-27 14:33:01"
            }
        ]
    }
}
```



##### 2、根据id查询

> 描述：根据id查询

**URL**

> /user/getUserById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数 | 必选 | 类型 | 说明       |
> | :--- | :--- | :--- | ---------- |
> | id   | 是   | int  | 用户当前id |
>
> **参数示例**

```json
http://localhost:8081/user/getUserById?id=1
```

**返回字段**

> | 返回字段            | 字段类型   | 说明                     |
> | :------------------ | :--------- | :----------------------- |
> | id                  | int        | 用户表主键id             |
> | username            | String     | 用户名                   |
> | desensitizePassword | String     | 密码（脱敏）             |
> | password            | String     | 密码                     |
> | phone               | String     | 手机号（脱敏）           |
> | userStatus          | int        | 用户状态，0-启用，1-禁用 |
> | listRole            | List<Role> |                          |
> | └ roleName          | String     | 角色名                   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "id": 1,
        "username": "zhangsan",
        "desensitizePassword": "************",
        "password": "12345678",
        "phone": "333****",
        "userStatus": 0,
        "listRole": [
            {
                "roleName": "超级管理员"
            },
            {
                "roleName": "内勤"
            },
            {
                "roleName": "客户"
            }
        ],
        "createdDate": "2021-08-24 16:25:15"
    }
}
```



##### 3、更新用户数据

> 描述：接收用户所有修改的数据进行更新用户数据（不对密码进行修改）

**URL**

> /user/updateUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型   | 说明         |
> | :------- | :--- | :----- | ------------ |
> | id       | 是   | int    | 用户当前id   |
> | username | 否   | String | 用户名       |
> | password | 否   | String | 密码（脱敏） |
> | phone    | 是   | String | 手机号       |
>
> **参数示例**

```json
{
    "id":1,
    "username":"张三",
    "password":"********",
    "phone":"23456789034"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "更新成功",
    "content": null
}
```



##### 4、新增用户接口

> 描述：新增用户数据

**URL**

> /user/addUser

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数     | 必选 | 类型       | 说明                                             |
> | :------- | :--- | :--------- | ------------------------------------------------ |
> | username | 是   | String     | 用户名                                           |
> | password | 是   | String     | 密码                                             |
> | phone    | 是   | String     | 手机号                                           |
> | listRole | 是   | List<Role> |                                                  |
> | └ roleId | 是   | int        | 角色变量，1-超级管理员，2-内勤，3-厨师，4-配送员 |
>
> **参数示例**

```json
{
    "username":"张三",
    "password":"12345678",
    "phone":"13131331313",
    "listRole":[
        {
            "roleId":1
        },
        {
            "roleId":2
        }
    ]
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "新增成功",
    "content": null
}
```



##### 5、删除用户接口

> 描述：删除用户数据（需要删除用户表中的用户以及和用户关联角色的表中的字段）

**URL**

> /user/delUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/delUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 6、禁用用户接口

> 描述：禁用用户数据

**URL**

> /user/disableUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/disableUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "禁用成功",
    "content": null
}
```





##### 7、启用用户接口

> 描述：启用用户数据

**URL**

> /user/enableUser

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | userId | 是   | int  | 用户id |
>
> **参数示例**

```json
http://localhost:8081/user/enableUser?userId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "启用成功",
    "content": null
}
```



##### 8、查询全部角色名称

> 描述：查询全部角色的名称

**URL**

> /role/listUserRoles

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：

> **参数示例**

```json
http://localhost:8081/role/listUserRoles
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | total      | long       | 查询总条数 |
> | list       | List<Role> |            |
> | └ id       | int        | 角色的id   |
> | └ roleName | String     | 角色名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "查询成功",
    "content": {
        "total":2,
        "list":[
            {
                "id":1,
                "roleName":"超级管理员"
            },
            {
                "id":1,
                "roleName":"超级管理员"
            }
        ]
    }
}
```





#### 角色管理页面



##### 1、查询角色名与其对应的所有用户名（模糊查：角色名称）

> 描述：查询角色名和对应的所有用户名

**URL**

> /role/listLikeRoleAndUsername

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | roleName | 否   | String | 角色名称         |
> | pageNum  | 是   | int    | 当前页数（页码） |
> | pageSize | 是   | int    | 每页中的条数     |
>
> **参数示例**

```json
{
    "roleName":"",
    "pageNum":1,
    "pageSize":10
}
```

**返回字段**

> | 返回字段       | 字段类型      | 说明                   |
> | :------------- | :------------ | :--------------------- |
> | total          | long          | 查询总条数             |
> | list           | List<ReloDTO> |                        |
> | └  roleName    | String        | 角色名称               |
> | └  users       | List<UserVO>  |                        |
> | └  └  username | String        | 当前角色所对应的用户名 |

**返回值示例**

``` json
{
    "code": 200,
    "message": "success",
    "content": {
        "total": 5,
        "list": [
            {
                "id": 1,
                "roleName": "超级管理员",
                "users": [
                    {
                        "username": "zhangsan"
                    },
                    {
                        "username": "lisi"
                    },
                    {
                        "username": "张三"
                    },
                    {
                        "username": "wangwu"
                    },
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 2,
                "roleName": "内勤",
                "users": [
                    {
                        "username": "zhangsan"
                    },
                    {
                        "username": "张三"
                    },
                    {
                        "username": "wangwu"
                    },
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 3,
                "roleName": "厨师",
                "users": [
                    {
                        "username": "赵武"
                    }
                ]
            },
            {
                "id": 4,
                "roleName": "配送员",
                "users": []
            },
            {
                "id": 5,
                "roleName": "客户",
                "users": [
                    {
                        "username": "zhangsan"
                    }
                ]
            }
        ]
    }
}
```



##### 2、添加角色

> 描述：添加角色（只添加角色名称）

**URL**

> /role/addRole

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明     |
> | :------- | :--- | :----- | -------- |
> | roleName | 是   | String | 角色名称 |
>
> **参数示例**

```json
{
    "roleName":"后勤"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "添加成功",
    "content": null
}
```



##### 3、删除角色

> 描述：删除角色（删除相关联当前角色的所有用户关联）

**URL**

> /role/delRole

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json

> | 参数   | 必选 | 类型 | 说明     |
> | :----- | :--- | :--- | -------- |
> | roleId | 是   | int  | 角色的id |
>
> **参数示例**

```json
http://localhost:8081/role/delRole?roleId=2
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 4、编辑角色

> 描述：修改角色名称

**URL**

> /role/updateRole

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json

> | 参数     | 必选 | 类型   | 说明             |
> | :------- | :--- | :----- | ---------------- |
> | id       | 是   | int    | 当前角色id       |
> | roleName | 是   | String | 修改后的角色名称 |
>
> **参数示例**

```json
{
    "id":1,
    "roleName":"管理员"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "修改成功",
    "content": null
}
```



##### 5、为角色分配菜单

> 描述：为角色分配多个菜单（检查当前角色对应的菜单是否存在关系）

**URL**

> /role/distributeMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型       | 说明   |
> | :------- | :--- | :--------- | ------ |
> | roleId   | 是   | int        | 角色id |
> | listMenu | 是   | List<Menu> |        |
> | └ menuId | 是   | int        | 菜单id |

**参数示例**

```json
{
    "roleId":1,
    "listRole":[
        {
            "menuId":1
        },
        {
            "menuId":2
        }
    ]
}
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | total      | long       | 查询总条数 |
> | list       | List<Role> |            |
> | └ id       | int        | 角色的id   |
> | └ parentId | int        | 角色的父id |
> | └ menuName | String     | 菜单名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "分配成功",
    "content": null
}
```



##### 6、根据id查询当前角色下的所有菜单信息

> 描述：查询全部菜单的菜单名称

**URL**

> /menu/listMenusById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json
>
> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | roleId | 是   | int  | 角色id |

**参数示例**

```json
http://localhost:8081/menu/listMenusById?roleId=1
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | total      | long       | 查询总条数 |
> | listMenu   | List<Menu> |            |
> | └ id       | int        | 角色的id   |
> | └ parentId | int        | 角色的父id |
> | └ menuName | String     | 菜单名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "修改成功",
    "content": {
        "total":2,
        "listMenu":[
            {
	            "id":2,
		        "parentId":1,
		        "menuName":"用户管理"
            },
            {
                "id":3,
                "parentId":1,
                "menuName":"角色管理"
            }
        ]
    }
}
```





#### 菜单管理页面

##### 1、查询所有菜单信息

> 描述：查询全部菜单的菜单名称

**URL**

> /menu/listMenus

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json

**参数示例**

```json
http://localhost:8081/menu/listMenus
```

**返回字段**

> | 返回字段   | 字段类型   | 说明       |
> | :--------- | :--------- | :--------- |
> | total      | long       | 查询总条数 |
> | listMenu   | List<Menu> |            |
> | └ id       | int        | 角色的id   |
> | └ parentId | int        | 角色的父id |
> | └ menuName | String     | 菜单名称   |

**返回值示例**

``` json
{
    "code": 200,
    "message": "修改成功",
    "content": {
        "total":2,
        "listMenu":[
            {
	            "id":2,
		        "parentId":1,
		        "menuName":"用户管理"
            },
            {
                "id":3,
                "parentId":1,
                "menuName":"角色管理"
            }
        ]
    }
}
```



##### 2、删除菜单信息

> 描述：删除菜单信息

**URL**

> /menu/delMenu

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：json
>
> | 参数   | 必选 | 类型 | 说明   |
> | :----- | :--- | :--- | ------ |
> | menuId | 是   | int  | 菜单id |

**参数示例**

```json
http://localhost:8081/menu/delMenu?menuId=1
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "删除成功",
    "content": null
}
```



##### 3、修改菜单信息

> 描述：修改菜单的菜单名称或父id

**URL**

> /menu/updateMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型   | 说明         |
> | :------- | :--- | :----- | ------------ |
> | menuId   | 是   | int    | 菜单id       |
> | parentId | 否   | int    | 父id         |
> | menuName | 否   | String | 菜单的新名称 |

**参数示例**

```json
{
    "menuId":2,
    "parentId":1,
    "menuName":"用户新管理"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "修改成功",
    "content": null
}
```



##### 4、新增菜单信息

> 描述：新增菜单信息

**URL**

> /menu/addMenu

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：json
>
> | 参数     | 必选 | 类型   | 说明     |
> | :------- | :--- | :----- | -------- |
> | parentId | 否   | int    | 父id     |
> | menuName | 是   | String | 菜单名称 |

**参数示例**

```json
{
    "parentId":1,
    "menuName":"新增用户管理"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "添加成功",
    "content": null
}
```



#### 修改密码页面

##### 修改密码

> 描述：修改当前用户的密码

**URL**

> /user/updateUserPassword

**HTTP请求方式**

> POST

**请求参数**

> 参数格式：

> | 参数        | 必选 | 类型   | 说明       |
> | :---------- | :--- | :----- | ---------- |
> | id          | 是   | int    | 用户当前id |
> | username    | 否   | String | 用户名     |
> | password    | 否   | String | 原密码     |
> | newPassword | 是   | String | 新密码     |
>
> **参数示例**

```json
{
    "id":1,
    "username":"张三",
    "password":"********",
    "newPassword":"23456789034"
}
```

**返回字段**

> 

**返回值示例**

``` json
{
    "code": 200,
    "message": "更新成功",
    "content": null
}
```



# 李浩文接口

## 参数管理

### 1.参数管理-查询所有父配置接口

#### URL

/config/selectAllFather

#### HTTP请求方式

POST

#### 请求参数

无

##### 请求示例

```
{

}
```

#### 返回字段

| 返回字段   | 字段类型        | 说明       |
| ---------- | --------------- | ---------- |
| configList | List<ConfigDTO> | 父配置List |

**ConfigDTO**

| 返回字段         | 字段类型 | 说明                       |
| ---------------- | -------- | -------------------------- |
| id               | int      | 主键id                     |
| configType       | String   | 类型                       |
| configValueCode1 | String   | 类型值1                    |
| configValueCode2 | String   | 类型值2                    |
| isConfig         | int      | 是否可配，0-不可配，1-可配 |
| remarks          | String   | 备注                       |
| parentId         | int      | 父ID                       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"content":{
		"configList":[{
			"id":1,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":
		},
		{
			"id":2,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":
		}]
	}
}
```

### 2.参数管理-根据父id查询所有配置接口

#### URL

/config/selectAll

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明           |
| ---- | ---- | ---- | -------------- |
| id   | 是   | int  | 父配置(标签)id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段           | 字段类型                | 说明       |
| ------------------ | ----------------------- | ---------- |
| configChildrenList | List<ConfigChildrenDTO> | 子配置List |

**ConfigChildrenDTO**

| 返回字段         | 字段类型                | 说明                       |
| ---------------- | ----------------------- | -------------------------- |
| id               | int                     | 主键id                     |
| configType       | String                  | 类型                       |
| configValueCode1 | String                  | 类型值1                    |
| configValueCode2 | String                  | 类型值2                    |
| isConfig         | int                     | 是否可配，0-不可配，1-可配 |
| remarks          | String                  | 备注                       |
| parentId         | int                     | 父ID                       |
| children         | List<ConfigChildrenDTO> | 当前配置的子配置列表       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"content":{
		"configChildrenList":[{
			"id":2,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":1，
			"children":[]
		},
		{
			"id":3,
			"configType":"1",
			"configValueCode1":"1",
			"configValueCode2":"1",
			"isConfig":1,
			"remarks":"1",
			"parentId":1,
			"children":[]
		}]
	}
}
```



### 3.参数管理-根据id查询接口

#### URL

/config/selectById

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明   |
| ---- | ---- | ---- | ------ |
| id   | 是   | int  | 配置id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段         | 字段类型 | 说明                       |
| ---------------- | -------- | -------------------------- |
| id               | int      | 主键id                     |
| configType       | String   | 类型                       |
| configValueCode1 | String   | 类型值1                    |
| configValueCode2 | String   | 类型值2                    |
| isConfig         | int      | 是否可配，0-不可配，1-可配 |
| remarks          | String   | 备注                       |
| parentId         | int      | 父ID                       |

##### 返回值示例

```
{
	"code":200,
	"message":"查询成功"
	"content":{
		"id":1,
		"configType":"1",
		"configValueCode1":"1",
		"configValueCode2":"1",
		"isConfig":1,
		"remarks":"1",
		"parentId":
	}
}
```

### 4.参数管理-删除接口

#### URL

/config/deleteById

#### HTTP请求方式

POST

#### 请求参数

| 参数 | 必选 | 类型 | 说明   |
| ---- | ---- | ---- | ------ |
| id   | 是   | int  | 配置id |

##### 请求示例

```
{
	"id":1
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 删除结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"删除成功"
}
```

### 5.参数管理-修改接口

#### URL

/config/updateById

#### HTTP请求方式

POST

#### 请求参数

| 参数          | 必选 | 类型            | 说明               |
| ------------- | ---- | --------------- | ------------------ |
| configDTOList | 是   | List<ConfigDTO> | 修改的配置信息列表 |

**ConfigDTO**

| 参数             | 必选 | 类型   | 说明                       |
| ---------------- | ---- | ------ | -------------------------- |
| id               | 是   | int    | 配置id                     |
| configType       | 否   | String | 类型                       |
| configValueCode1 | 否   | String | 类型值1                    |
| configValueCode2 | 否   | String | 类型值2                    |
| isConfig         | 否   | int    | 是否可配，0-不可配，1-可配 |
| remark           | 否   | String | 备注                       |
| parentId         | 否   | int    | 父ID                       |

##### 请求示例

```
{
	[{
	"id":1,
	"configType":"1",
	"configValueCode1":"1",
	"configValueCode2":"1",
	"isConfig":1,
	"remarks":"1",
	"parentId":
	}]
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 修改结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"修改成功"
}
```

### 6.参数管理-增加接口

#### URL

/config/addConfig

#### HTTP请求方式

POST

#### 请求参数

| 参数             | 必选 | 类型   | 说明                       |
| ---------------- | ---- | ------ | -------------------------- |
| configType       | 是   | String | 类型                       |
| configValueCode1 | 是   | String | 类型值1                    |
| configValueCode2 | 否   | String | 类型值2                    |
| isConfig         | 是   | int    | 是否可配，0-不可配，1-可配 |
| remark           | 否   | String | 备注                       |
| parentId         | 否   | int    | 父ID                       |

##### 请求示例

```
{
	"configType":"1",
	"configValueCode1":"1",
	"configValueCode2":"1",
	"isConfig":1,
	"remarks":"1",
	"parentId":
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 添加结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"添加成功"
}
```

### 7.手机端-查询楼位置参数

#### URL

/phone/getAddress

#### HTTP请求方式

POST

#### 请求参数

无

##### 请求示例

```
{

}
```

#### 返回字段

| 返回字段 | 字段类型         | 说明           |
| -------- | ---------------- | -------------- |
| content  | List<AddressDTO> | 所有楼位置List |

**AddressDTO**

| 返回字段       | 字段类型     | 说明     |
| -------------- | ------------ | -------- |
| addressList    | List<String> | 楼层List |
| allAddressName | String       | 楼号名   |

##### 返回值示例

```
{
    "code": 200,
    "message": "查询成功",
    "content": [
        {
            "allAddressName": "一号楼",
            "addressList": [
                "7楼",
                "8楼"
            ]
        },
        {
            "allAddressName": "二号楼",
            "addressList": [
                "7楼"
            ]
        }
    ]
}
```

## 首页统计

### 8.首页统计-查询当日订单统计信息接口

#### URL

/index/statistical

#### HTTP请求方式

POST

#### 请求参数

无

##### 请求示例

```
{

}
```

#### 返回字段

| 返回字段    | 字段类型   | 说明         |
| ----------- | ---------- | ------------ |
| todayOrder  | int        | 今日订单数   |
| waitOrder   | int        | 待制作订单数 |
| makingOrder | int        | 制作中订单数 |
| sendOrder   | int        | 配送中订单数 |
| finishOrder | int        | 已完成订单数 |
| refundOrder | int        | 退款订单数   |
| income      | BigDecimal | 今日收入     |

##### 返回值示例

```
{
	"code":200,
	"message":"查询成功",
	"content":{
		"todayOrder": 10,
    	"waitOrder": 1,
    	"makingOrder": 1,
    	"sendOrder": 3,
    	"finishOrder": 5,
    	"refundOrder": 0,
    	"income": 1000
	}
}
```

## 手机端

### 9.10.手机端-套餐&单品去支付接口（双接口）

ps：套餐使用packageList，单品使用dishList

#### URL

/phone/setOrder

#### HTTP请求方式

POST

#### 请求参数

| 参数        | 必选 | 类型                | 说明                            |
| ----------- | ---- | ------------------- | ------------------------------- |
| customerId  | 是   | int                 | 当前登录的用户id                |
| packageList | 否   | List<PackageMsgDTO> | 套餐列表                        |
| dishList    | 否   | List<DishDTO>       | 菜品列表                        |
| name        | 是   | String              | 下单人姓名                      |
| phone       | 是   | String              | 下单人手机号                    |
| orderType   | 否   | int                 | 取餐方式，0-外卖，1-自提        |
| address     | 否   | String              | 地址                            |
| time        | 否   | Date                | 送餐时间                        |
| remarks     | 否   | String              | 备注                            |
| orderStatus | 是   | int                 | 付款状态 1-付款失败  2-付款成功 |

**DishDTO**

| 参数     | 必选 | 类型   | 说明     |
| -------- | ---- | ------ | -------- |
| dishId   | 是   | int    | 菜品id   |
| dishNum  | 是   | int    | 菜品数量 |
| dishName | 是   | String | 菜品名称 |

**PackageDTO**

| 参数        | 必选 | 类型          | 说明           |
| ----------- | ---- | ------------- | -------------- |
| packageId   | 是   | int           | 套餐id         |
| packageNum  | 是   | int           | 套餐数量       |
| packageName | 是   | String        | 套餐名称       |
| dishList    | 是   | List<DishDTO> | 套餐内菜品列表 |

##### 请求示例

```
{
	"customerId":1,
	"dishList":[{
		"dishId":1,
		"dishNum":1
		"dishName":"aaa"
	},{
		"dishId":2,
		"dishNum":1
		"dishName":"bbb"
	}],
	"packageList":[
	
	],
	"name":"111",
	"phone":"13222222222",
	"orderType":0,
	"price":12,
	"address":"111",
	"time":2020-11-11 11:11:11,
	"remarks":"111",
	"orderStatus":2
}
```

#### 返回字段

| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| message  | String   | 下单结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"下单成功"
	"content":{}
}
```

### 11.手机端-退单接口

#### URL

/phone/deleteOrder

#### HTTP请求方式

POST

#### 请求参数

| 参数    | 必选 | 类型   | 说明     |
| ------- | ---- | ------ | -------- |
| orderId | 是   | String | 订单号   |
| cause   | 否   | String | 退款原因 |

##### 请求示例

```
{
	"orderId":"111",
	"cause":"111"
}
```

#### 返回字段

| 参数    | 类型   | 说明     |
| ------- | ------ | -------- |
| message | String | 退单结果 |

##### 返回值示例

```
{
	"code":200,
	"message":"退款成功"
}
```

### 12.手机端-退单结果接口

#### URL

/phone/deleteOrderReason

#### HTTP请求方式

POST

#### 请求参数

| 参数    | 必选 | 类型   | 说明   |
| ------- | ---- | ------ | ------ |
| orderId | 是   | String | 订单号 |

##### 请求示例

```
{
	"orderId":"111"
}
```

#### 返回字段

| 参数  | 类型   | 说明     |
| ----- | ------ | -------- |
| cause | String | 退单原因 |

##### 返回值示例

```
{
	"code":200,
	"message":"查询原因成功",
	"cause":"111"
}
```

# 韩煜接口

> **一些枚举值对应信息**
>
> 
>
> - 菜品类型
>   - 0---------->主食
>   - 1---------->热菜
>   - 2----------->凉菜		
> - 餐别类型(数字是String)
>   - 0---------->早
>   - 01--------->早中
>   - 02---------->早晚
>   - 012-------->早中晚
>   - 1------------>中
>   - 12----------->中晚
>   - 2------------->晚
> - 



## 1.按照名称类型餐别查询菜品

> 描述：按照名称类型查询菜品

**URL**

> http://192.168.8.102:8081/dish/selectByValues

**HTTP请求方式**

> POST请求

**请求参数**

> 参数格式：JSON

| 参数       | 必选 | 类型       | 说明                        |
| :--------- | :--- | :--------- | --------------------------- |
| pageNumber | 是   | String     | 分页页码第几页              |
| pageSize   | 是   | String     | 每页多少条                  |
| id         | 否   | Interegter | 菜品编号                    |
| dishName   | 否   | String     | 菜品名称                    |
| dishTime   | 否   | String     | 餐别0早1中2晚               |
| dishType   | 否   | String     | 菜品类型0主食，1热菜，2凉菜 |

**参数示例**

```json
{

"pageSize":"2",
"pageNumber":"2"

}
```



> **返回值示例**

```json
{
       "code": 200,
       "message": "sucess",
       "content": {
              "total": 5,
              "list": [
                     {
                            "id": 20,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "columnUrl": "http://localhost/6e941a93-d97d-44db-a425-daf98e579f03NBZ.jpg",
                            "imgUrl": [
                                   "http://localhost/5dbae243-175b-4ae6-bb42-6ebfce84ca2ccjwt-right.png",
                                   "http://localhost/e553e80c-8ab3-44c0-871e-5697a18e01cbNBZ.jpg",
                                   "http://localhost/655b6002-c984-4c8f-966f-a81bf2f40778NBZ.jpg"
                            ]
                     },
                     {
                            "id": 22,
                            "dishNames": "芜湖起飞",
                            "dishType": 1,
                            "dishTime": "02",
                            "dishPrice": 12312,
                            "dishDescribe": "阿斯顿撒大撒所",
                            "dishStatus": 1,
                            "columnUrl": null,
                            "imgUrl": [
                                   "http://localhost/0be75910-4e2c-48b8-af41-aec1dfb915de1.jpg",
                                   "http://localhost/27e62f94-4328-48af-8177-bcabc0276ced1.jpg",
                                   "http://localhost/381e459b-d1e9-49b8-9a9a-2b9a786ba4991.jpg"
                            ]
                     },
                     {
                            "id": 23,
                            "dishNames": "测试添加菜品",
                            "dishType": 1,
                            "dishTime": "12",
                            "dishPrice": 123,
                            "dishDescribe": "奥德赛",
                            "dishStatus": 1,
                            "columnUrl": null,
                            "imgUrl": [
                                   "http://localhost/87a123d7-2d32-46d4-8f5c-5c57786aee6e1.jpg",
                                   "http://localhost/579f9035-6656-465c-87a0-070d5c6ef3051.jpg"
                            ]
                     },
                     {
                            "id": 24,
                            "dishNames": "测试添加菜品",
                            "dishType": 1,
                            "dishTime": "12",
                            "dishPrice": 123,
                            "dishDescribe": "奥德赛",
                            "dishStatus": 1,
                            "columnUrl": null,
                            "imgUrl": [
                                   "http://localhost/87a123d7-2d32-46d4-8f5c-5c57786aee6e1.jpg",
                                   "http://localhost/579f9035-6656-465c-87a0-070d5c6ef3051.jpg"
                            ]
                     },
                     {
                            "id": 27,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "columnUrl": "http://localhost/6e941a93-d97d-44db-a425-daf98e579f03NBZ.jpg",
                            "imgUrl": [
                                   "http://localhost/5dbae243-175b-4ae6-bb42-6ebfce84ca2ccjwt-right.png",
                                   "http://localhost/e553e80c-8ab3-44c0-871e-5697a18e01cbNBZ.jpg",
                                   "http://localhost/655b6002-c984-4c8f-966f-a81bf2f40778NBZ.jpg"
                            ]
                     }
              ]
       }
}
```

## 2.查询菜品类型

> 描述：按照id删除

**URL**

> /dish/selectType

**HTTP请求方式**

> get

**请求参数**

无

请求路径样式

http://192.168.8.102:8081/dish/selectType

返回示例

```
{
       "code": 200,
       "message": "sucess",
       "content": {
              "total": 4,
              "list": [
                     {
                            "id": 27,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "imgUrl": "http://localhost/6e941a93-d97d-44db-a425-daf98e579f03NBZ.jpg"
                     },
                     {
                            "id": 27,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "imgUrl": "http://localhost/5dbae243-175b-4ae6-bb42-6ebfce84ca2ccjwt-right.png"
                     },
                     {
                            "id": 27,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "imgUrl": "http://localhost/e553e80c-8ab3-44c0-871e-5697a18e01cbNBZ.jpg"
                     },
                     {
                            "id": 27,
                            "dishNames": "好吃的域",
                            "dishType": 1,
                            "dishTime": "1",
                            "dishPrice": 10,
                            "dishDescribe": "适合加醋",
                            "dishStatus": 1,
                            "imgUrl": "http://localhost/655b6002-c984-4c8f-966f-a81bf2f40778NBZ.jpg"
                     }
              ]
       }
}
```

## 3.菜品批量下架

> 描述：更改菜品状态dishStatus

**URL**

> /dish/updateStatus

**HTTP请求方式**

> post请求 

**请求参数**

> 参数格式：JSON

| 参数类型   | 字段类型 | 说明       |
| :--------- | :------- | :--------- |
| statusList | List     | 菜品唯一id |



**参数示例**

```json
{
"statusList":
       [
             32,34
       ]
}
```

**返回字段**

> | 返回字段   | 字段类型 | 说明                 |
> | :--------- | :------- | :------------------- |
> | dishStatus | int      | 菜品状态0下架1未下架 |

**返回值示例**

```json
{
       "code": 200,
       "message": "success",
       "content": "修改状态成功"
}
```

## 4. 菜品的删除

> 描述：按照菜品的id进行删除

**URL**

> dish/deleteById

**HTTP请求方式**

> GET

**请求参数**

> 参数格式：JSON

> | 参数 | 必选 | 类型 |   说明   |
> | :--: | :--: | :--: | :------: |
> |  id  |  是  | int  | 菜品的id |

**参数示例**

```http
http://localhost:8081/dish/deleteById?id=35
```

**返回字段**

成功or失败消息

> 

**返回值示例**

``` json
{
       "code": 200,
       "message": "success",
       "content": "删除菜品成功"
}
```

## 5.新增菜品

> 描述：更新指定客户信息

**URL**

> /dish/addDish

**HTTP请求方式**

> POST请求 

**请求参数**

> 参数格式：JSON
>
> | 参数类型        | 字段类型   | 说明                                                         |
> | :-------------- | :--------- | :----------------------------------------------------------- |
> | dishNames       | String     | 菜品名称                                                     |
> | dishType        | int        | 菜品类型，0-主食，1-热菜，2-凉菜                             |
> | dishTime        | String     | 餐别，用餐时间，0-早，1-中，2-晚，01-早中，02-早晚，12-中晚，012-早中晚 |
> | dishPrice       | BigDecimal | 价格                                                         |
> | dishDescribe    | String     | 描述                                                         |
> | columnPictureId | int        | 列表图id                                                     |
> | list            | List       | 详情图id集合                                                 |

> 

**参数示例**

```json
       {

    "dishNames":"好吃的域",
    "dishType":1,
    "dishTime":"1",
    "dishPrice":10,
    "dishDescribe":"适合加醋",
    "columnPictureId":37,
    "list":[
       38,39,40
    ]
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明          |
> | :------- | :------- | :------------ |
> | message  | String   | 成功/失败信息 |
> |          |          |               |

**返回值示例**

```json
{
    "code": 200,
    "message": "sucess",
    "content": "添加菜品成功"
}
```

## 6.上传图片

> 描述：异步上传

**URL**

> /dish/uploadPicture

**HTTP请求方式**

> POST请求 

**请求参数**

> 参数格式：JSON

>  

**参数示例**

```json
{
   "imgBase":"base码",
    "basefileName":"NBZ.jpg"
}
```

**返回字段**

> | 返回字段 | 字段类型 | 说明                 |
> | :------- | :------- | :------------------- |
> | id       | int      | 上传图片后数据库的id |

**返回值示例**

```json
{
    "code": 200,
    "message": "sucess",
    "content": "图片的id为：32"
}
```

## 7，查看菜品详情

> 描述：异步上传

**URL**

> /dish/selectById

**HTTP请求方式**

> POST请求 

**请求参数**

> 参数格式：JSON



| 返回字段 | 字段类型 | 说明     |
| -------- | -------- | -------- |
| id       | int      | 商品编号 |



>  list数组

**参数示例**

```json
http://192.168.8.102:8081/dish/selectById?id=32
```

**返回字段**

> | 返回字段     | 字段类型 | 说明               |
> | :----------- | :------- | :----------------- |
> | id           | int      | 商品编号           |
> | dishNames    | String   | 名称               |
> | dishType     | String   | 类型               |
> | dishTime     | String   | 餐别               |
> | dishPrice    | String   | 价格               |
> | dishDescribe | String   | 描述               |
> | dishStatus   | Int      | 菜品状态1上架0下架 |
> | columnUrl    | String   | 列表页地址         |
> | imgUrl       | List     | 详情页地址         |

**返回值示例**

```
{
       "code": 200,
       "message": "success",
       "content": {
              "id": 32,
              "dishNames": "123",
              "dishType": 1,
              "dishTime": "1",
              "dishPrice": 123,
              "dishDescribe": "123",
              "dishStatus": 1,
              "columnUrl": "http://192.168.8.102/2021/08/27/ba596c24-a5d5-4109-8e23-09953f91107d2bc7453d-4b84-422e-be4a-530def078f081.jpg",
              "imgUrl": [
                     "http://192.168.8.102/2021/08/27/c92ae8cd-b316-4ecb-be3a-e624a00f2a652bc7453d-4b84-422e-be4a-530def078f081.jpg"
              ],
              "number": 0
       }
}
```





## 8、图片的删除

> 描述：按照id删除

**URL**

> /dish/deleteImage

**HTTP请求方式**

> get

**请求参数**

> id=34

请求路径样式

http://192.168.8.102:8081/dish/deleteImage?id=34

返回示例

```
{
    "code": 200,
    "message": "sucess",
    "content": "删除成功"
}
```

## 9、菜品的更新

> 描述：进行菜品的更新

**URL**

> dish/updateDish

**HTTP请求方式**

> post

**请求字段**

> | 返回字段     | 字段类型 | 说明       |
> | :----------- | :------- | :--------- |
> | id           | int      | 商品编号   |
> | dishNames    | String   | 名称       |
> | dishType     | String   | 类型       |
> | dishTime     | String   | 餐别       |
> | dishPrice    | String   | 价格       |
> | dishDescribe | String   | 描述       |
> | columnUrl    | String   | 列表页地址 |
> | imgUrl       | List     | 详情页地址 |

**请求参数**

> ```
> {
> 
> "id":"34",
> "dishNames":"好吃的域",
> "dishType":1,
> "dishTime":"1",
> "dishPrice":10,
> "dishDescribe":"适合加醋",
> "columnPictureId":2,
> "list":[
>  38,39,41
> ]
> }
> ```
>
> 

返回示例

```
{
       "code": 200,
       "message": "success",
       "content": "更新成功"
}
```

## 10.菜品上下架

> 描述：更改菜品状态dishStatuss

**URL**

> /dish/updateStatuss

**HTTP请求方式**

> get请求 

**请求参数**

> 参数格式：JSON

| 参数类型 | 字段类型 | 说明       |
| :------- | :------- | :--------- |
| id       | Interger | 菜品唯一id |



**参数示例**

```json
{
"id":"2"
}
```

**返回字段**

```
{
       "code": 200,
       "message": "success",
       "content": "修改状态成功"
}
```


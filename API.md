致力于打造最简单的机器学习平台，把复杂的算法和流程封装成API，使开发者不用建设庞大而复杂的底层架构，也不需要深入理解机器学习原理，轻松实现在自己的应用内集成机器学习引擎。

# API

## 创建引擎
#### URL:
* `http://api.easyrequest.io/engine/create/:name`

#### Method:
* POST

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识
* name
   * 类型: string
   * 必选: true
   * 描述: 引擎名称，可由字母和数字组成。 eg. myengine1
* type
   * 类型: string
   * 必选: true
   * 可选值: bool \ pref
   * 描述: 引擎类型，bool为布尔值引擎，User不需要为Item打分；pref为分值型引擎，User需要对Item打分。 

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/engine/create/myengine1?appkey=yourappkey&type=pref`
   * 以POST的方式提交
   * 创建一个名称为"myengine1"、类型为"pref"的推荐引擎。
   * 返回`{"result": "ok"}`

## 引擎列表
#### URL:
* `http://api.easyrequest.io/engine/list`

#### Method:
* GET

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识

#### 返回方式:
* JSON

#### 示例:
* `http://api.easyrequest.io/engine/list?appkey=yourappkey`

返回
```json
{"engines": [{"name": "eg1", "type": "bool", "version": "2", "records": 22},{"name": "eg2", "type": "pref", "version": "20", "records": 15828}]}
```
* 备注
   * version: 每做一次相似度计算就会升级version，开发者可以根据version判断引擎有没有更新。BTW，引擎更新是周期性的。
   * records: 引擎现有的记录数

## 提交数据到引擎
#### URL:
* `http://api.easyrequest.io/engine/post/:name`

#### Method:
* POST

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识
* name
   * 类型: string
   * 必选: true
   * 描述: 引擎名称，可由字母和数字组成。 eg. myengine1
* user
   * 类型: string
   * 必选: true
   * 描述: 用户ID，只接受由数字组成的字符串。 eg. 1
* items
   * 类型: string
   * 必选: true
   * 描述: 物品ID组成的字符串，由","分隔，物品ID只接受由数字组成的字符串，items分隔的数组最大长度为100。 eg. 101, 102, 103 
* prefs
   * 类型: string
   * 必选: false
   * 描述: 用户对物品打分组成的字符串，由","分隔，分值只接受由浮点数组成的字符串，prefs分隔的数组最大长度为100。该项需要与否取决于引擎的类型，如引擎类型是分值型(pref)，则必须提供prefs参数，而且必须保证prefs和items的分隔数组长度一致，用户数组的排序和用户对物品打分数组的排序必须一致。 eg. 1.0, 1.02, 10.3

#### 返回方式:
* JSON

#### 示例:
* `http://api.easyrequest.io/engine/post/myengine1?appkey=yourappkey&user=1&items=101,102,103&prefs=1.0,1.02,10.3`
   * 以POST的方式提交
   * 这里表示为: 用户"1"对物品"101"的打分是"1.0"，对物品"102"的打分是"1.02"，对物品"103"的打分是"10.3"。
   * 如果用户重复提交相同的数据，则取最后一条纪录做计算，也就是说，可以改变用户对物品的打分，但我们不推荐这种做法。
   * 返回`{"result": "ok"}`

## 用户获得物品推荐
#### URL:
* `http://api.easyrequest.io/recommender`

#### Method:
* GET

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识
* engine
   * 类型: string
   * 必选: true
   * 描述: 引擎名称，可由字母和数字组成。 eg. myengine1
* user
   * 类型: string
   * 必选: true
   * 描述: 用户ID，只接受由数字组成的字符串。 eg. 1
* top
   * 类型: string
   * 必选: false
   * 描述: 获取推荐的条数，默认为10条，最大为100条。

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/recommender?appkey=yourappkey&engine=myengine1&user=1&top=3`
```json
{
    "user": "1",
    "recommenderItems": [
        "107:2.4670174",
        "106:2.359963",
        "105:2.3046758"
    ]
}
```
* 这里表示在引擎myengine1中获得用户ID为"1"的物品推荐，指定条目数为3条。
   * recommenderItems是一个数组，由"itemID:得分"组成，结果由得分从高到低排序。这里的物品推荐结果是107、106、105，得分是2.4670174、2.359963、2.3046758。

## 相似物品推荐
#### URL:
* `http://api.easyrequest.io/similarity`

#### Method:
* GET

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识
* engine
   * 类型: string
   * 必选: true
   * 描述: 引擎名称，可由字母和数字组成。 eg. myengine1
* item
   * 类型: string
   * 必选: true
   * 描述: 物品ID，只接受由数字组成的字符串。 eg. 101
* top
   * 类型: string
   * 必选: false
   * 描述: 获取推荐的条数，默认为10条，最大为100条。

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/similarity?appkey=yourappkey&engine=myengine1&item=101&top=3`
```json
{
    "item": 101,
    "similarities": [
        "105:0.2531794607639313",
        "102:0.25103703141212463",
        "106:0.1828850954771042"
    ]
}
```
* 这里表示在引擎myengine1中获得物品ID为"101"的相似物品推荐，指定条目数为3条。
   * similarities是一个数组，由"itemID:得分"组成，结果由得分从高到低排序。这里的相似物品推荐结果是105、102、106,得分是0.2531794607639313、0.25103703141212463、0.1828850954771042。

## 一组物品最相似推荐
#### URL:
* `http://api.easyrequest.io/mostsimilarity`

#### Method:
* GET

#### 参数:
* appkey
   * 类型: string
   * 必选: true
   * 描述: 注册时发送到邮箱的身份标识
* engine
   * 类型: string
   * 必选: true
   * 描述: 引擎名称，可由字母和数字组成。 eg. myengine1
* items
   * 类型: string
   * 必选: true
   * 描述: 物品ID组成的字符串，由","分隔，物品ID只接受由数字组成的字符串，items分隔的数组最大长度为100。 eg. 101, 102, 103 


#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/mostsimilarity?appkey=yourappkey&engine=myengine1&items=101,105,106,109`
```json
{
    "similarities": [
        "101:105",
        "105:101",
        "106:101"
    ]
}
```
* 这里表示在引擎myengine1中获得物品ID为101、105、106、109的最相似物品推荐。
   * similarities是一个数组，由"itemID:最相似itemID"组成。这里表示物品"101"的最相似物品为"105"，物品"105"的最相似物品为"101"，物品"106"的最相似物品为"101"，物品"109"没有相似的物品。
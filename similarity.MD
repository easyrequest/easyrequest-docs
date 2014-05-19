## 相似物品/用户推荐
#### 描述:
* 引擎算法为itembased，则有item的相似度列表。
* 引擎算法为userbased，则有user的相似度列表。
* 引擎算法为als，则没有任何的相似度列表。

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
   * 类型: int
   * 必选: false。 如果引擎的算法是itembased，则必选为true。
   * 描述: 物品ID
* user
   * 类型: int
   * 必选: false。 如果引擎的算法是userbased，则必选为true。
   * 描述: 用户ID
* top
   * 类型: int
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
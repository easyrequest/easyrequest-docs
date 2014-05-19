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
   * 类型: int
   * 必选: true
   * 描述: 用户ID
* top
   * 类型: int
   * 必选: false
   * 描述: 获取推荐的条数，默认为10条，最大为100条。

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/recommender?appkey=yourappkey&engine=myengine1&user=1&top=3`
```json
{
    "user": "1",
    "recommendItems": [
        "107:2.4670174",
        "106:2.359963",
        "105:2.3046758"
    ]
}
```
* 这里表示在引擎myengine1中获得用户ID为"1"的物品推荐，指定条目数为3条。
   * recommendItems是一个数组，由"itemID:得分"组成，结果由得分从高到低排序。这里的物品推荐结果是107、106、105，得分是2.4670174、2.359963、2.3046758。
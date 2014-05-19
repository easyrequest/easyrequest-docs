## 一组物品/用户最相似推荐
#### 描述:
* 引擎算法为itembased，则有items的最相似列表。
* 引擎算法为userbased，则有users的最相似列表。
* 引擎算法为als，则没有任何的最相似列表。

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
   * 类型: int数组
   * 必选: false。 如果引擎的算法是itembased，则必选为true。
   * 描述: 物品ID数组，由","分隔，数组最大长度为100。 eg. 101, 102, 103 
* users
   * 类型: int数组
   * 必选: false。 如果引擎的算法是userbased，则必选为true。
   * 描述: 用户ID数组，由","分隔，数组最大长度为100。 eg. 1, 2, 3 


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
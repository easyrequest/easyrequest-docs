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
   * 类型: int
   * 必选: true
   * 描述: 用户ID
* items
   * 类型: int数组
   * 必选: true
   * 描述: 物品ID数组，由","分隔，数组最大长度为100。 eg. 101, 102, 103 
* prefs
   * 类型: float数组
   * 必选: false
   * 描述: 用户对物品打分数组，由","分隔，数组最大长度为100。该项需要与否取决于引擎的类型，如引擎类型是分值型(pref)，则必须提供prefs参数，而且必须保证prefs和items的分隔数组长度一致，用户数组的排序和用户对物品打分数组的排序必须一致。 eg. 1.0, 1.02, 10.3

#### 返回方式:
* JSON

#### 示例:
* `http://api.easyrequest.io/engine/post/myengine1?appkey=yourappkey&user=1&items=101,102,103&prefs=1.0,1.02,10.3`
   * 以POST的方式提交
   * 这里表示为: 用户"1"对物品"101"的打分是"1.0"，对物品"102"的打分是"1.02"，对物品"103"的打分是"10.3"。
   * 如果用户重复提交相同的数据，则取最后一条纪录做计算，也就是说，可以改变用户对物品的打分，但我们不推荐这种做法。
   * 返回`{"result": "ok"}`
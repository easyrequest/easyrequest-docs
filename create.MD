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
* algo
   * 类型: string
   * 必选: false
   * 可选值: userbased \ itembased \ als
   * 默认值: itembased
   * 描述: 引擎使用的算法。
* measure
   * 类型: string
   * 必选: false
   * 可选值: cityblock \ cosine \ euclidean \ loglikelihood \ pearson \ tanimoto
   * 默认值: 如果type类型为bool，则默认值为loglikelihood，如果type类型为pref，则默认值为cosine。
   * 描述: userbased和itembased算法使用的度量方法，可通过update接口改变。
* k
   * 类型: int
   * 必选: false
   * 默认值: 10
   * 最大值: 100
   * 描述: 生成推荐结果时最大的可推荐个数，可通过update接口改变。
* features
   * 类型: int
   * 必选: false。 如algo为als时，则必选为true。
   * 默认值: 10
   * 最大值: 100
   * 描述: als算法特有参数（引擎维度），可通过update接口改变。
* iterations
   * 类型: int
   * 必选: false
   * 默认值: 10
   * 最大值: 50
   * 描述: als算法特有参数（迭代次数），可通过update接口改变。
* lambda
   * 类型: float
   * 必选: false
   * 默认值: 0.065
   * 描述: als算法特有参数（regularization parameter），可通过update接口改变。
* alpha
   * 类型: float
   * 必选: false
   * 默认值: 20.0
   * 描述: als算法特有参数（confidence parameter），可通过update接口改变。
* maxrating
   * 类型: float
   * 必选: false
   * 默认值: 5.0
   * 描述: als算法特有参数（available rating），可通过update接口改变。

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/engine/create/myengine1?appkey=yourappkey&type=pref`
   * 以POST的方式提交
   * 创建一个名称为"myengine1"、类型为"pref"的推荐引擎。
   * 返回`{"result": "ok"}`
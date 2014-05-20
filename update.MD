## 更新引擎
#### URL:
* `http://api.easyrequest.io/engine/update/:name`

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
* measure
   * 类型: string
   * 必选: false
   * 可选值: cityblock \ cosine \ euclidean \ loglikelihood \ pearson \ tanimoto
   * 描述: userbased和itembased算法使用的度量方法
* k
   * 类型: int
   * 必选: false
   * 最大值: 100
   * 描述: 生成推荐结果时最大的可推荐个数
* features
   * 类型: int
   * 必选: false
   * 最大值: 100
   * 描述: als算法特有参数（引擎维度）
* iterations
   * 类型: int
   * 必选: false
   * 最大值: 50
   * 描述: als算法特有参数（迭代次数）
* lambda
   * 类型: float
   * 必选: false
   * 描述: als算法特有参数（regularization parameter）
* alpha
   * 类型: float
   * 必选: false
   * 描述: als算法特有参数（confidence parameter）
* maxrating
   * 类型: float
   * 必选: false
   * 描述: als算法特有参数（available rating）

#### 返回方式:
* JSON   

#### 示例:
* `http://api.easyrequest.io/engine/update/myengine1?appkey=yourappkey&measure=cityblock&k=100`
   * 以POST的方式提交
   * 更新名称为"myengine1"的引擎参数，把度量方法更新为cityblock，把最大的可推荐个数更新为100。
   * 返回`{"result": "ok"}`
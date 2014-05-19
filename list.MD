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
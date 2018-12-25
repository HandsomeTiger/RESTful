# API接口

## 业务接口

### 
#### 获取列表
* Uri:  
`GET` `/zoos/{id}`  
* Method:  
`GET`
* Request Body:
```
{
	"code": "axxx" // 微信返回的 code
}
```

* Response Body: 返回内容为员工本人相关信息和`token`
```
{
	"ID": 123,
	"name": "xx",
	"...": "...",
	"token": "token", // 其它每个请求都需要带上的 header 内容
}
```


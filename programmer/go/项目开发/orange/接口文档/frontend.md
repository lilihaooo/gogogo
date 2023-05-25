### 登陆

http请求方式: POST（请使用https协议） https://localhost:xxxx/login

| 参数      | 是否必须 | 说明 |
| -------- | -------- | ---- |
| phone    | 是       | 电话 |
| password | 是       | 密码 |



成功返回:

```
{
   "msg":"登录成功",
	"result":{
	"uname":"你登录的用户名",
	"pwd":"你登录的密码"
	},
	"code":1
}
```





### 注册

http请求方式: POST（请使用https协议） https://localhost:xxxx/zhuce

| 参数     | 是否必填 | 说明 |
| -------- | -------- | ---- |
| phone    | 是       | 电话 |
| password | 是       | 密码 |
| name     | 是       | 姓名 |
| sex      | 否       | 性别 |


PERM元模型

Policy策略: 

Effect影响

Request请求

Matchers匹配规则





请求参数R与策略P通过匹配规则M来匹配获得一个影响E,进到影响的表达式返回一个bool



人话: 请求和策略, 在匹配规则中能否找到一个E





PERM元模型

Policy策略: 

​	sub: 访问实体(谁请求)

​	obj: 访问的资源

​	act: 访问的方法

​	eft: 策略结果, 一般为空, 默认指定allow  (allow, deny)

​	定义:

	[policy_definition]
	p = sub, obj, act



Effect影响

| Policy effect定义                                            | 意义             | 示例                                                         |
| ------------------------------------------------------------ | ---------------- | ------------------------------------------------------------ |
| some(where (p.eft == allow))                                 | allow-override   | [ACL, RBAC, etc.](https://casbin.org/zh/docs/supported-models#examples) |
| !some(where (p.eft == deny))                                 | deny-override    | [拒绝改写](https://casbin.org/zh/docs/supported-models#examples) |
| some(where (p.eft == allow)) && !some(where (p.eft == deny)) | allow-and-deny   | [同意与拒绝](https://casbin.org/zh/docs/supported-models#examples) |
| priority(p.eft) \|\| deny                                    | priority         | [优先级](https://casbin.org/zh/docs/supported-models#examples) |
| subjectPriority(p.eft)                                       | 基于角色的优先级 | [主题优先级](https://casbin.org/zh/docs/supported-models#examples) |

Request请求

​	sub: 访问实体(谁请求)

​	obj: 访问的资源

​	act: 访问的方法

​	定义:

	[request_definition]
	r = sub, obj, act



Matchers匹配规则

```
[matchers]
m = r.sub == p.sub && r.obj == p.obj && r.act == p.act
// 或者写正则
// 或者自定义方法
```





role_definition 角色域

​	g = _, _表示以角色为基础 (这个用户, 是那个角色)

​	g = _, _, _表示以域为基础(多商户模式)   (这个用户, 是那个角色, 属于那个商户)
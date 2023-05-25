## 行为

```
当请求到达控制器时，Yii2 框架会按照以下顺序处理：

行为验证（Behaviors validation）：请求首先经过控制器中定义的行为。行为可以执行访问控制、请求方法过滤、数据处理等验证操作。行为可以根据其配置和规则对请求进行拦截，如果请求不满足行为的验证条件，行为可以选择阻止请求继续传递给具体的方法。

具体方法执行：如果请求通过了行为的验证，Yii2 将继续执行控制器中具体的方法。这是请求的最终目的地，具体的方法将执行实际的业务逻辑和响应。

所以，在控制器中行为是最先被执行的，行为验证通过后，请求才能到达具体的方法中执行。行为提供了在请求到达控制器方法之前进行验证和预处理的机制，以实现更灵活的请求处理流程。

需要注意的是，行为的执行顺序可以通过在 behaviors 方法返回数组中的定义顺序进行控制。按照数组中的顺序，行为将按顺序应用它们的功能和验证。
```









## 组件 and bootstrap

```
User
components中的其他组件为什么不需要放到bootstrap中在启动时自动加载呢
ChatGPT
在 Yii2 框架中，components 配置项用于定义应用程序的各种组件，如数据库连接、缓存组件、邮件发送器等。这些组件在应用程序运行期间可能会被多次使用，而不仅仅是在应用程序启动时。

相比之下，bootstrap 配置项用于指定在应用程序启动时自动加载的组件或模块。它通常用于那些需要在应用程序启动时执行一些特定操作或初始化过程的模块或组件。

原因是，不是所有的组件或模块都需要在应用程序启动时自动加载。有些组件可能只在特定的请求或场景中才需要被实例化和使用。将所有组件都放在 bootstrap 中加载，可能会增加应用程序启动的时间和资源消耗，尤其是对于一些复杂的组件或模块。

另外，Yii2 框架的组件是延迟加载的，即它们在实际使用之前不会被实例化。这意味着即使将组件定义在 components 配置中，它们也不会在应用程序启动时自动加载。相反，它们会在需要时按需加载。

通过将组件放在 components 配置中，你可以在整个应用程序中访问和使用它们，而不仅仅是在应用程序启动时。这使得组件的加载更加灵活，并且可以根据需要进行延迟加载。

总结起来，components 配置项用于定义和配置应用程序的各种组件，而 bootstrap 配置项用于指定在应用程序启动时自动加载的特定组件或模块，以执行一些初始化操作。这种区分使得应用程序能够更加灵活地管理和加载组件，以满足不同的需求和场景。
```









## 过滤器

常用过滤器: yii/filters命名空间下

1. AccessControl AccessControl 提供基于 [rules](https://www.yiichina.com/doc/api/2.0/yii-filters-accesscontrol#$rules-detail) 规则的访问控制

   ```
   use yii\filters\AccessControl;
   
   public function behaviors()
   {
       return [
           'access' => [
               'class' => AccessControl::className(),
               'only' => ['create', 'update'],
               'rules' => [
                   // 允许认证用户
                   [
                       'allow' => true,
                       'roles' => ['@'],
                   ],
                   // 默认禁止其他用户
               ],
           ],
       ];
   }
   ```

2. 认证方法过滤器通过 [HTTP Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication) 或 [OAuth 2](http://oauth.net/2/) 来认证一个用户，认证方法过滤器类在 `yii\filters\auth` 命名空间下。

   ```
   use yii\filters\auth\HttpBasicAuth;
   
   public function behaviors()
   {
       return [
           'basicAuth' => [
               'class' => HttpBasicAuth::className(),
           ],
       ];
   }
   ```

3. ContentNegotiator 支持响应内容格式处理和语言处理。 通过检查 `GET` 参数和 `Accept` HTTP 头部来决定响应内容格式和语言。

   ```
   use yii\filters\ContentNegotiator;
   use yii\web\Response;
   
   public function behaviors()
   {
       return [
           [
               'class' => ContentNegotiator::className(),
               'formats' => [
                   'application/json' => Response::FORMAT_JSON,
                   'application/xml' => Response::FORMAT_XML,
               ],
               'languages' => [
                   'en-US',
                   'de',
               ],
           ],
       ];
   }
   ```

   

## 电话注册

1. 输入电话号码, 获取验证码   

   api: sys/actionGetRegisterVerifyCode

2. 生成验证码将验证码保存到数据库VerifyCode表中

3. 利用阿里云发送验证码到用户手机

4. 用户输入验证码, 从数据库查找该(where phone and code) 验证码是否存在或者过期

5. 注册成功

   
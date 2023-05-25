字符串约束
excludesall：不包含参数中任意的 UNICODE 字符，例如excludesall=ab；

excludesrune：不包含参数表示的 rune 字符，excludesrune=asong；

startswith：以参数子串为前缀，例如startswith=hi；

endswith：以参数子串为后缀，例如endswith=bye。

contains=：包含参数子串，例如contains=email；

containsany：包含参数中任意的 UNICODE 字符，例如containsany=ab；

containsrune：包含参数表示的 rune 字符，例如`containsrune=asong；

excludes：不包含参数子串，例如excludes=email；

范围约束
范围约束的字段类型分为三种：

对于数值，我们则可以约束其值
对于切片、数组和map，我们则可以约束其长度
对于字符串，我们则可以约束其长度
常用tag介绍：

ne：不等于参数值，例如 ne=5；
gt：大于参数值，例如 gt=5；
gte：大于等于参数值，例如 gte=50；
lt：小于参数值，例如 lt=50；
lte：小于等于参数值，例如 lte=50；
oneof：只能是列举出的值其中一个，这些值必须是数值或字符串，以空格分隔，如果字符串中有空格，将字符串用单引号包围，例如 oneof=male female。
eq：等于参数值，注意与 len不同。对于字符串， eq约束字符串本身的值，而 len约束字符串长度。例如 eq=10；
len：等于参数值，例如 len=10；
max：小于等于参数值，例如 max=10；
min：大于等于参数值，例如 min=10
Fields约束
eqfield：定义字段间的相等约束，用于约束同一结构体中的字段。例如： eqfield=Password
eqcsfield：约束统一结构体中字段等于另一个字段（相对），确认密码时可以使用，例如： eqfiel=ConfirmPassword
nefield：用来约束两个字段是否相同，确认两种颜色是否一致时可以使用，例如： nefield=Color1
necsfield：约束两个字段是否相同（相对）
常用约束
unique：指定唯一性约束，不同类型处理不同：

对于map，unique约束没有重复的值
对于数组和切片，unique没有重复的值
对于元素类型为结构体的碎片，unique约束结构体对象的某个字段不重复，使用 unique=field指定字段名
email：使用email来限制字段必须是邮件形式，直接写eamil即可，无需加任何指定。

omitempty：字段未设置，则忽略

-：跳过该字段，不检验；

|：使用多个约束，只需要满足其中一个，例如rgb|rgba；

required：字段必须设置，不能为默认值；
————————————————
版权声明：本文为CSDN博主「Sunshine-松」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_39397165/article/details/108173108
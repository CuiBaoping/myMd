# 一、隐式函数或者Lambda

~~~kotlin
val lambdaFun1: (String) -> String = { name ->
	"name:$name"
}
// 单个参数时，默认参数为 it 
val lambdaFun11: (String) -> String = { 
    "name:$it"
}
val lambdaFun111 = { name: String ->
	"name:$name"
}

val lambdaFun2: (String, Int) -> String  = { name, age ->
    "name:$name, age:$age"
}
val lambdaFun22 = { name: String, age: Int ->
    "name:$name, age:$age"
}

val lambdaFun: ((String) -> String)? = { name ->
    "name:$name"
}
//lambdaFun?("Kotlin") 			//语法错误
lambdaFun?.invoke("Kotlin")		// 正确
lambdaFun?.let{ it("Kotlin") } 	// 正确
lambdaFun!!("Kotlin")			// 正确
~~~

# 二、显示函数

~~~kotlin
fun fun1(age: Int) : String {
    return "fun1 age:$age"
}
fun fun2(name: String, f: (Int) -> String, age: Int) : String {
    return "fun2 name:$name, ${f(age)}"
}
// value = "Fun:fun2 name:Kotlin, fun1 age:88"
val value = fun2("Kotlin", ::fun1, 88) //双冒号操作符 将一个函数当做一个个方法使用
~~~

# 三、Kotlin中 ?、!!、?:、:: 、->、== 符号的简单说明

详见：[Kotlin中 ?、!!、?:、:: 、->、== 符号的简单说明](https://blog.csdn.net/Sindyue/article/details/99625012)

# 四、let、with、run、apply、also函数的使用

详见：[Kotlin系列之let、with、run、apply、also函数的使用](https://blog.csdn.net/u013064109/article/details/78786646)

# 五、生成随机数

~~~kotlin
// (0..1000).shuffled() 生成1001个0~1000的随机数
val number1 = (0..1000).shuffled().first()   
// Math.random()生成 0~1 之间的double型随机数
val number2 = (Math.random()* 1000).toInt()
~~~

# 六、主构造和次构造

~~~kotlin
class Class() {	//主构造
    init {		// 主构造默认初始化
        println("Class")
    }
    constructor(name: String) : this() {	// 第一次构造
        println("name:$name")
    }
    constructor(name: String, age: Int) : this() {	// 第二次构造
        println("name:$name, age:$age")
    }
}
~~~

# 七、Kotlin和Java相互调用规则

## 1、Kotlin调用Java，需要显示规定类型

Kotlin调用Java时，默认为 "XXX!" ，会有崩溃隐患！

~~~java
// Java定义
public class Class{
    public String getInfo1() {
        return "Info1";
    }
    public String getInfo2() {
        return null;
    }
}
~~~

~~~kotlin
// Kotlin调用 
val info1 = Class().info1	// info1 默认为 String!
val info2 = Class().info2
println("${info1.length}")
println("${info2.length}")	//崩溃 因为info2为null

val info1s: String? = Class().info1 // info1 为 String?
val info2s: String? = Class().info2
println("${info1s.length}")
println("${info2s.length}")		//不会崩溃，打印"null"
~~~

# Kotlin中Int十六进制输入

~~~kotlin
val int: Int = 255
println("${int.toString(16)}")	// 输出FF
~~~


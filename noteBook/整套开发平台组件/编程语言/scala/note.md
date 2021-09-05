学习scala
	1. 新建一个package，
	2. object 类，java有 public ，scala 没有public
	3. scala 一定要有main 方法  def main(args: Array[String]): Unit = {} //会转成 java 的main 方法
	4. scala 在编译时 会生成两个 class 方法，$方法文件，因为是完全面向对象，所以需要引入一个静态的类，模拟静态方法
	5. $的类，一般称之为 伴生对象，都可以直接通过 类名访问
	6. 伴生类型的语法 规则 未object 开始
	7. scala 没有 public 方法 默认所有方法都是 public 
	8. scala 没有 void 关键字， 采用特殊对象模拟 unit
	9. scala 生命 方法 用 def 来声明
	10. scala  参数名: 类型
	11. scala 方法声明 和 方法体 用 =   号分割
	12. Scala 推荐 不写 ; 但是可以使用
	13. 拼接字符串三种 风格， 使用+ , printf(%s,name)  %s 字符串 %d 数值， 插值字符串饭是 (s"name=${name},") f"name=${age}%2.f" f 代表可以格式化 raw 原始值是什么就是什么
	14. scala 注释 和java 一样
	15. scala 声明 变量 var  var s : String ="avc"
	16. scala 声明变量 赋值
	17. var val 的区别 var 就是普通的变量，val 变量是不许改变的
	18. 一般会使用 val 一旦定义，不需要更改
	19. scala 数据类型分成两种类 ，avnyal anyref
	20. scala  null nothing Unit

标识符
	1. 和java类似，不过可以用符号作为开头
	2. scala _他有特殊的作用，不能独立使用
	3. 可以用反引号`` 也可以使用名字

运算符
	1. 算数运算符 和java类似
	2. scala 没有++  -- 操作
	3. 没有三元运算符
	4. 和java全部类似
	5. 赋值 =  是有结果 为 unit （）

逻辑运算符
	1. if (){}
	2. if () {} else{}
	3. if(){} else if(){} else{}

For循环     1to5     1until5    Range(1,5,3)    For {}{}    For(I <-1 to 3 ; j =xxxx)    For (I <- 1 to 3 if xxx)    Yield 可以把每次结果存起来

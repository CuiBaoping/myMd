# 这里是本人的学习笔记

## 官网网址

[Android Studio 官网](https://developer.android.google.cn/docs?authuser=0)

学习网址：[示例工程地址]( https://gitee.com/rustfisher/AndroidTutorial)，[文档地址](https://an.rustfisher.com)

# kotlin中的空指针

~~~kotlin
var str: String? = null  // str为空指针
// ?.表示str不为空则进行length操作，为空则什么也不做；?:表示左表达式非空则返回，否则返回有表达式
var i = str?.length ?: 0
var l = str!!.length	// 不检测str是否非空，都进行length操作
~~~

### let辅助工具

let并不是关键字,也不是操作符,而是一个函数. 这个函数提供了函数式API的编程接口, 并且将原始调用对象作为参数传递到Lambda表达式中.

~~~kotlin
fun doStudy(study: Study?) {
        study?.readBooks()
        study?.doHomeWork()
}
~~~

~~~kotlin
fun doStudy(study: Study?) {
    study?.let { study ->
        study.readBooks()
        study.doHomeWork()
    }
}
~~~

~~~kotlin
fun doStudy(study: Study?) {
    study?.let { 
        it.readBooks()
        it.doHomeWork()
    }
}
~~~



# TextView显示跑马灯

在xml文件中设置

~~~xml
android:singleLine="true"
android:ellipsize="marquee"
android:marqueeRepeatLimit="marquee_forever"
~~~

永久滚动，在kt文件中设置如下：

~~~kotlin
// tvMarquee 为TextView控件名称
findViewById<TextView>(R.id.tvMarquee).isSelected = true
~~~

# 获得焦点

## 默认获得焦点

在xml文件中

~~~xml
android:focusable="true"
android:focusableInTouchMode="true"
~~~

或者 在kt文件中

~~~kotlin
tvTitle.isFocusable = true
tvTitle.isFocusableInTouchMode = true
~~~

## 再次获得焦点

在kt文件中

~~~kotlin
tvTitle.requestFocus()
tvTitle.requestFocusFromTouch()
~~~

# 资源文件注意点

## 1，资源文件名称不能出现大写字符

## 2，字符串调用
~~~xml
<!-- .\src\res\valuas\strings.xml -->
<string name="tv_title">Hello World</string>
<string name="tv1_test">按了%1$d次</string>
~~~
[转义详见](# XML文件中转义字符)

### Kotlin调用

~~~kotlin
var i: Int = 2
getString(R.string.tv1_test, i) //结果 "按了2次"
~~~
### xml调用
~~~xml
android:text="@string/tv_title"
~~~

## 3、颜色调用
~~~xml
<!-- .\src\res\valuas\colors.xml -->
<color name="myRed">#FFFF0000</color>
~~~
### Kotlin调用
~~~kotlin
val color: Int = getColor(R.color.myRed)
~~~
### xml调用
~~~xml
android:shadowColor="@color/myRed"
~~~

## 4、图片调用

### 添加图片

复制待添加图片文件，然后在项目中的待添加位置选择粘贴（注意：一般为.\src\res\drawable\位置）

~~~xml
.\src\res\drawable\draw1.png
.\src\res\drawable\draw2.jpg
~~~
### Kotlin调用
~~~kotlin
val bitmap: Bitmap = BitmapFactory.decodeResource(resources, R.drawable.draw2)
val drawable: Drawable = getDrawable(R.drawable.draw2)!!
~~~
### xml调用
~~~xml
android:drawableLeft="@drawable/draw1"
~~~

## 5、界面调用
~~~xml
.\src\res\layout\activity_alert_view.xml
~~~
### Kotlin调用
~~~kotlin
val view: View = layoutInflater.inflate(R.layout.activity_alert_view, null)
~~~

# ImageView设置

保持图片比例，在xml文件中设置

~~~mxl
android:maxWidth="200dp"
android:maxHeight="400dp"
android:adjustViewBounds="true"
~~~

设置图片显示类型（默认为“fitCenter”）

~~~xml
android:scaleType="fitCenter"
~~~

## 控件置顶

在kt文件中

~~~kotlin
vw.bringToFront() // 控件置顶 vm为控件
~~~

## 非主线程运行UI控件

```kotlin
runOnUiThread{ view.text="XXX" }		// UI控件函数需要在{}中
```

~~~kotlin
view.post{ view.text="XXX" }			// UI控件函数需要在{}中
~~~



## 窗口(Activity)切换

在本窗口中需要的地方(如按键点击事件)调用如下：

~~~kotlin
// OtherActivity 为另一个窗口class
val intent: Intent = Intent(this, OtherActivity::class.java)
this.startActivity(intent)
~~~

注意：参考[Activity(活动)](https://blog.csdn.net/qq_35507234/article/details/82718794)

# XML文件中忽略错误提示

~~~xml
tools:ignore="MissingConstraints"
~~~

# 调用系统提示

~~~kotlin
// Toast.LENGTH_SHORT 短时间提示
// Toast.LENGTH_LONG 长时间提示
Toast.makeText(this, "这是系统提示", Toast.LENGTH_SHORT).show()
// 非主任务调用
Toast.makeText(applicationContext, "这是系统提示", Toast.LENGTH_SHORT).show()
~~~

# registerForActivityResult常规用法

详见：[registerForActivityResult常规用法](https://blog.csdn.net/Yu1441/article/details/118614812?spm=1001.2014.3001.5501)

# XML文件中转义字符

### 输入特殊字符如@ %等会报错,有两种解决办法
~~~xml
1.添加转意符号 \ .
2.如果你的字符串不需要格式化，可以在你的<string 标签上增加一个属性:formatted="false"例如 <string name="test" formatted="false">% test %</string> 即可.
~~~

### %1$s,%1$d等的用法
%n$ms：代表输出的是字符串，n代表是第几个参数，设置m的值可以在输出之前放置空格 
%n$md：代表输出的是整数，n代表是第几个参数，设置m的值可以在输出之前放置空格，也可以设为0m,在输出之前放置m个0 
%n$mf：代表输出的是浮点数，n代表是第几个参数，设置m的值可以控制小数位数，如m=2.2时，输出格式为00.00 
也可简单写成：
%d  （表示整数）
%f   （表示浮点数）
%s  （表示字符串）

[字符串调用方法详见](#2，字符串调用)

# 匿名函数的定义与调用

## 普通匿名定义调用：

定义：

~~~kotlin
class MyAdapter(var list: List<Bean>, var context: Context) : RecyclerView.Adapter<MyViewHolder>() {
    var onItemClickListener : OnRecyclerViewClickListener? = null

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyViewHolder {
        val view = View.inflate(context, R.layout.recycler_view_item, null)
        return MyViewHolder(view)
    }

    override fun onBindViewHolder(holder: MyViewHolder, position: Int) {
        holder.textView.text = list[position].name
        holder.textView.setOnClickListener {
            onItemClickListener?.onRecyclerViewClick(position)
        }
    }

    override fun getItemCount(): Int {
        return list.count()
    }
}

class MyViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
    val textView: TextView = itemView.findViewById(R.id.tv)
}

interface OnRecyclerViewClickListener {
    fun onRecyclerViewClick(position: Int)
}
~~~

调用：

~~~kotlin
val myAdapter = MyAdapter(data, this)
myAdapter.onItemClickListener = object : OnRecyclerViewClickListener {
	override fun onRecyclerViewClick(position: Int) {
		println("onRecyclerItemClick: $position")
	}
}
~~~

## lambda定义调用

定义：

~~~kotlin
class MyAdapter(var list: List<Bean>, var context: Context) :
    RecyclerView.Adapter<MyAdapter.MyViewHolder>() {

    private var mOnItemMultipleClickListener: OnRecyclerItemMultipleClickListener? = null

    private var mOnItemClickListener: OnClickListener? = null
    private var mOnItemLongClickListener: OnClickListener? = null
    private var mOnItemTouchListener: OnTouchListener? = null

    private var mOnItemLambdaClickListener: ((Int) -> Unit)? = null
    private var mOnItemLambdaLongClickListener: ((Int) -> Unit)? = null
    private var mOnItemLambdaTouchListener: ((Int, MotionEvent) -> Unit)? = null

    @SuppressLint("ClickableViewAccessibility") // 忽略setOnTouchListener的警告
    inner class MyViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        var textView: TextView = itemView.findViewById(R.id.tv)

        init {
            textView.setOnClickListener {
                mOnItemClickListener?.onMyClick(absoluteAdapterPosition)
                mOnItemMultipleClickListener?.onItemClick(absoluteAdapterPosition)
//                mOnItemLambdaClickListener?.let { it(absoluteAdapterPosition) }
                mOnItemLambdaClickListener?.invoke(absoluteAdapterPosition)
            }

            textView.setOnLongClickListener {
                mOnItemLongClickListener?.onMyClick(absoluteAdapterPosition)
                mOnItemMultipleClickListener?.onItemLongClick(absoluteAdapterPosition)
                mOnItemLambdaLongClickListener?.invoke(absoluteAdapterPosition)
                true
            }

            textView.setOnTouchListener { v: View, event: MotionEvent ->
                mOnItemTouchListener?.onMyTouch(absoluteAdapterPosition, event)
                mOnItemMultipleClickListener?.onItemTouch(absoluteAdapterPosition, event)
                mOnItemLambdaTouchListener?.invoke(absoluteAdapterPosition, event)
                false
            }
        }
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): MyViewHolder {
        val view: View = View.inflate(context, R.layout.recycler_view_item, null)
        return MyViewHolder(view)
    }

    override fun onBindViewHolder(holder: MyViewHolder, position: Int) {
        println("onBindViewHolder:$position")
        holder.textView.text = list[position].name
    }

    override fun getItemCount(): Int {
        return list.size
    }

    /*************** 一个接口多个实现，不推荐使用 ***************/
    fun setOnRecyclerItemMultipleClickListener(listener: OnRecyclerItemMultipleClickListener) {
        mOnItemMultipleClickListener = listener
    }
    interface OnRecyclerItemMultipleClickListener{
        fun onItemClick(position: Int)
        fun onItemLongClick(position: Int)
        fun onItemTouch(position: Int, event: MotionEvent)
    }

    /*************** 一个接口一个实现，推荐使用 ***************/
    fun setOnRecyclerItemClickListener(listener: OnClickListener) {
        mOnItemClickListener = listener
    }
    fun setOnRecyclerItemLongClickListener(listener: OnClickListener) {
        mOnItemLongClickListener = listener
    }
    interface OnClickListener {
        fun onMyClick(position: Int)
    }
    fun setOnRecyclerItemTouchListener(linstener: OnTouchListener) {
        mOnItemTouchListener = linstener
    }
    interface OnTouchListener {
        fun onMyTouch(position: Int, event: MotionEvent)
    }

    /*************** lambda调用 ***************/
    fun setOnRecyclerItemLambdaClickListener(listener: (position: Int) -> Unit) {
        mOnItemLambdaClickListener = listener
    }
    fun setOnRecyclerItemLambdaLongClickListener(listener: (position: Int) -> Unit) {
        mOnItemLambdaLongClickListener = listener
    }
    fun setOnRecyclerItemLambdaTouchListener(linstener: (position: Int, event: MotionEvent) -> Unit) {
        mOnItemLambdaTouchListener = linstener
    }
}
~~~

一个接口多实现调用：

~~~kotlin
        // 一接口多实现调用
        myAdapter.setOnRecyclerItemMultipleClickListener(
            object : MyAdapter.OnRecyclerItemMultipleClickListener  {
            override fun onItemClick(position: Int) {
                println("onItemMultipleClick: $position")
            }
            override fun onItemLongClick(position: Int) {
                println("onItemMultipleLongClick: $position")
            }
            override fun onItemTouch(position: Int, event: MotionEvent) {
                println("OnRecyclerItemMultipleTouch:$position ${event.action}")
                when (event.action) {
                    MotionEvent.ACTION_DOWN -> {}
                    MotionEvent.ACTION_UP -> {}
                    MotionEvent.ACTION_MOVE -> {}
                }
            }
        })
~~~

一个接口一个实现调用：

~~~kotlin
        // 一接口一个实现调用
        myAdapter.setOnRecyclerItemClickListener(object : MyAdapter.OnClickListener {
            override fun onMyClick(position: Int) {
                println("onRecyclerItemClick: $position")
            }
        })
        myAdapter.setOnRecyclerItemLongClickListener(object : MyAdapter.OnClickListener {
            override fun onMyClick(position: Int) {
                println("OnRecyclerItemLongClick: $position")
            }
        })
        myAdapter.setOnRecyclerItemTouchListener(object : MyAdapter.OnTouchListener{
            override fun onMyTouch(position: Int, event: MotionEvent) {
                println("OnRecyclerItemTouch:$position ${event.action}")
                when (event.action) {
                    MotionEvent.ACTION_DOWN -> {}
                    MotionEvent.ACTION_UP -> {}
                    MotionEvent.ACTION_MOVE -> {}
                }
            }
        })
~~~



lambda调用：

~~~kotlin
        // lambda调用
        myAdapter.setOnRecyclerItemLambdaClickListener { 
            position: Int ->
            println("onRecyclerItemLambdaClick: $position")
        }
        myAdapter.setOnRecyclerItemLambdaLongClickListener { 
            position: Int ->
            println("onRecyclerItemLambdaLongClick: $position")
        }
        myAdapter.setOnRecyclerItemLambdaTouchListener { 
            position: Int, event: MotionEvent ->
            println("OnRecyclerItemLambdaTouch:$position ${event.action}")
            when (event.action) {
                MotionEvent.ACTION_DOWN -> {}
                MotionEvent.ACTION_UP -> {}
                MotionEvent.ACTION_MOVE -> {}
            }
        }
~~~

# Kotlin中使用List

Kotlin中List是不可变的需要使用MutableList代替：

~~~kotlin
//var viewList: List<View> = ArrayList<View>() // List不可变，不能使用add增加成员
var viewList: MutableList<View> = arrayListOf()
viewList.add(view1)
~~~

# ImageView控件具有透明通道的图片(如.png)换颜色

xml文件

~~~xml
app:tint="@color/red"	// 这里可以使用selector
~~~

Kotlin文件

~~~kotlin
val iv = findViewById<ImageView>(R.id.iv)	// iv为ImageView控件
iv.setColorFilter(R.color.red)
~~~

## XML文件中的 android、app与tools

参考1：[xml中的android、app、tools你真的了解吗 - 简书 (jianshu.com)](https://www.jianshu.com/p/910685a8ea91)

~~~xml
<!-- 系统命名空间：调用系统属性 -->
<Layout xmlns:android="http://schemas.android.com/apk/res/android" > </Layout>

<!-- 自定义命名空间：使用包或者自定义属性 -->
<Layout xmlns:app="http://schemas.android.com/apk/res-auto"> </Layout>

<!-- 工具命令空间：仅IDE界面使用，APP运行时忽略。可和系统命名空间重叠 -->
<Layout xmlns:tools="http://schemas.android.com/tools" > </Layout>

<!-- 注意：3种命名可任意共存 -->
<Layou xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools">
</Layou>
~~~


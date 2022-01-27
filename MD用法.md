# md的用法

参考：[菜鸟Markdown教程](https://www.runoob.com/markdown/md-tutorial.html)

## 添加标题

~~~markdown
# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题
~~~

## 列表

* 第一项
* 第二项
+ 第一项
+ 第二项
- 第一项
- 第二项
1. 第一项
2. 第二项

## 字体

*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___

## 脚注
创建脚注格式类似这样[^要注明的文本]

## 分隔线

***

___

# 区块

> 最外层
>
> > 第一层嵌套
> >
> > > 第二层嵌套

## 转义

**文本加粗**

\*\*正常显示\*\*

## 代码段

### c语言

~~~ c
 void main(void)
 {
     printf("Hello World!");
 }
~~~

### kotlin 语言

~~~ kotlin
package hello                      //  可选的包头
 
fun main(args: Array<String>) {    // 包级可见的函数，接受一个字符串数组作为参数
   println("Hello World!")         // 分号可以省略
}
~~~

## 链接

这个是一个链接[菜鸟教程](https://www.runoob.com)

这个链接用 1 作为网址变量[菜鸟教程][1]

这个链接用 runoob作为网址变量 [菜鸟教程][runoob]

这个链接用 菜鸟教程 作为网址变量 [菜鸟教程][菜鸟教程]

这是一个文件里链接 [md的用法](# md的用法)

这是一个文件里二级目录链接[添加标题](# 添加标题)

**注意：链接URL地址见文尾**

## 图片
![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "菜鸟网址图标")

![MD 本地图标](.\Image\iconfinder_markdown_20211210.png "MD图标")

## 表格
| 默认左对齐 | 左对齐 | 右对齐 | 居中对齐 |
| - | :-| -: | :-: |
| 单元格 | 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 | 单元格 |



## 公式

$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
${$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$

## 流程图

1. 横向流程图源码格式：
   ```mermaid
   graph LR
   A[方形] -->B(圆角)
       B --> C{条件a}
       C -->|a=1| D[结果1]
       C -->|a=2| E[结果2]
       F[横向流程图]
   ```

2. 竖向流程图源码格式：
   ```mermaid
   graph TD
   A[方形] --> B(圆角)
       B --> C{条件a}
       C --> |a=1| D[结果1]
       C --> |a=2| E[结果2]
       F[竖向流程图]
   ```

3. 标准流程图源码格式：
   ```flow
   st=>start: 开始框
   op=>operation: 处理框
   cond=>condition: 判断框(是或否?)
   sub1=>subroutine: 子流程
   io=>inputoutput: 输入输出框
   e=>end: 结束框
   st->op->cond
   cond(yes)->io->e
   cond(no)->sub1(right)->op
   ```

4. 标准流程图源码格式（横向）：
   ```flow
   st=>start: 开始框
   op=>operation: 处理框
   cond=>condition: 判断框(是或否?)
   sub1=>subroutine: 子流程
   io=>inputoutput: 输入输出框
   e=>end: 结束框
   st(right)->op(right)->cond
   cond(yes)->io(bottom)->e
   cond(no)->sub1(right)->op
   ```

5. UML时序图源码样例：
   ```sequence
   对象A->对象B: 对象B你好吗?（请求）
   Note right of 对象B: 对象B的描述
   Note left of 对象A: 对象A的描述(提示)
   对象B-->对象A: 我很好(响应)
   对象A->对象B: 你真的好吗？
   ```

6. UML时序图源码复杂样例：
   ```sequence
   Title: 标题：复杂使用
   对象A->对象B: 对象B你好吗?（请求）
   Note right of 对象B: 对象B的描述
   Note left of 对象A: 对象A的描述(提示)
   对象B-->对象A: 我很好(响应)
   对象B->小三: 你好吗
   小三-->>对象A: 对象B找我了
   对象A->对象B: 你真的好吗？
   Note over 小三,对象B: 我们是朋友
   participant C
   Note right of C: 没人陪我玩
   ```

7. UML标准时序图样例：
   ```mermaid
   %% 时序图例子,-> 直线，-->虚线，->>实线箭头
     sequenceDiagram
       participant 张三
       participant 李四
       张三->王五: 王五你好吗？
       loop 健康检查
           王五->王五: 与疾病战斗
       end
       Note right of 王五: 合理 食物 <br/>看医生...
       李四-->>张三: 很好!
       王五->李四: 你怎么样?
       李四-->王五: 很好!
   ```

8. 甘特图样例：
   ```mermaid
   %% 语法示例
           gantt
           dateFormat  YYYY-MM-DD
           title 软件开发甘特图
           section 设计
           需求                      :done,    des1, 2014-01-06,2014-01-08
           原型                      :active,  des2, 2014-01-09, 3d
           UI设计                     :         des3, after des2, 5d
       未来任务                     :         des4, after des3, 5d
           section 开发
           学习准备理解需求                      :crit, done, 2014-01-06,24h
           设计框架                             :crit, done, after des2, 2d
           开发                                 :crit, active, 3d
           未来任务                              :crit, 5d
           耍                                   :2d
           section 测试
           功能测试                              :active, a1, after des3, 3d
           压力测试                               :after a1  , 20h
           测试报告                               : 48h
   ```

[1]: https://www.runoob.com
[runoob]: https://www.runoob.com "菜鸟教程"
[菜鸟教程]: https://www.runoob.com "菜鸟教程"
> [*语法参考（繁体）*](https://github.com/othree/markdown-syntax-zhtw/tree/master)
> 
> [Markdown 官方教程](https://markdown.com.cn/extended-syntax/tables.html)
>
> [Markdown 教程(菜鸟)](https://www.runoob.com/markdown/md-tutorial.html)

下面是 类 Setext 风格的标题

这是一级标题
==============
这是二级标题
------------
这是正文

	这里是一个代码块

-------
上面是一条分割线

下面是 类 atx 风格的标题

	# 一级标题
	## 二级标题
	### 三级标题
	#### 四级标题
	##### 五级标题
	###### 六级标题

展示：

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

这里是正文: 

*斜体* 

**加粗** 

`inlinecode` `行内代码`

~~删除的内容~~

\*  在特殊字符`*`前插入反斜杠(`\`)来表示该字符本身

1. 有序列表
2. 有序列表
1. 有序
1. 有序

- 无序列表
    * 下一级列表 
* 无序列表
+ 无序列表


> 这里引言
>> 这里是引言的引言

```java
// 这里是Java代码
public class A(){
	/** Add 
	* @param a
	* @param b
	* @return
	*/
	static int add(int a,int b) {
		return a + b;
	}
	
	/**
	* @param args
	*/
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		System.out.println("out:");
		System.out.println(add(1,2));
	}
}
```
表格
----
|表头|表头|表头|
|---   |---|---|
|单元格|单元格|单元格|


|   	|   	|   	|   	|   	|
|---	|---	|---	|---	|---	|
|   	|   	|   	|   	|   	|
|   	|   	|   	|   	|   	|
|   	|   	|   	|   	|   	|

[表格生成器](https://www.tablesgenerator.com/markdown_tables)

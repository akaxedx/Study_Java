# JavaSE

## 包机制

包的本质就是文件夹

一般运用公司域名的倒置作为包名

www.baidu.com→com.baidu.www

```java
import package;//写在package下
```

import package;//写在package下

## Doc注释

### 参数信息

@author 作者名

@version 版本号

@since 指明需要最早使用的jdk版本

@param 参数名

@return 返回值情况

@throws异常抛出情况

```java
/**
	* @Author wfj
	* @version 1.0
	* @since 1.8
	*/

public class Doc{
	String name;
/**
	*@param name
	*@return
	*@throws Exception
	*/
	public String test(String name){
		return name;
	}

}
```

### 作用

在文件夹打开，使用cmd命令行打开

```shell
javadoc -encoding UTF-8 -charset UTF-8 name.java
```

编码中文并会生成index.html帮助文档

### IDEA生成javaDoc

工具（tool）→ 生成JavaDoc（Generate JavaDoc）

## Java流程控制

### 用户交互Scanner

Scanner类可以获取用户输入

```java
//基本语法
Scanner s = new Scanner(System.in);
```

通过Scanner类的next()与nextLine()方法获取输入的字符串，在读取前，我们一般需要使用hasNext()与hasNextLine()判断是否还有输入的数据

```java
Scanner scanner = new Scanner(System.in);
if(scanner.hasNext()){
	String str = scanner.next();
System.out.println("输出内容为:"+str);
}
scanner.close();//关闭io流是一个好习惯
```

hasNext（scanner.next()）识别到空格会返回true，一定会读取到有效字符，不能得到带有空格的字符串

hasNextLine（scanner.nextLine()）直到回车，识别一行，可以获得空白

```java
Scanner scanner = new Scanner(System.in);
int i = 0;
float t = -0.0f;
System.out.println("请输入整数：");
if(scanner.hasNextInt()){
	i = scanner.nextInt();
	System.out.println("整数数据："+i);
}else{
	System.out.println("输入的数据不是整数数据！");
}

System.out.println("请输入小数：");
if(scanner.hasNextFloat()){
	i = scanner.nextFloat();
	System.out.println("小数数据："+i);
}else{
	System.out.println("输入的数据不是小数数据！");
}
scanner.close();
```

### 练习

```java
//我们可以输入多个数字，并求其总和与平均数，每输入一个和数字用回车确认
//通过输入非数字来结束输入并在输出执行结果
Scanner scanner = new Scanner(System.in);

double sum = 0;
int m = 0;
while(scanner.hasNextDouble()){
	double x = scanner.nextDouble();
	m = m + 1；
	sum = sum + x;
	System.out.println("你输入了第"+m+"个数据，然后当前结果sum="+sum);
}
System.out.println(m+"个数的和为"+sum);
System.out.println(m+"个数的平均值是"+(sum/m));
scanner.close();
```

## 增强for循环

```java
int[] numbers = [10,20,30,40,50];

for(int i = 0;i<5;i++){
	System.out.println(numbers[i])
}

//增强for循环，遍历数组、数组
for(int x:numbers){
	System.out.println(x);
}
```

## Java方法

### 何谓方法

JAVA方法是语句的集合，它们在一起执行一个功能

方法是解决一类问题的步骤的有序组合

方法包含于类或对象中

方法在程序中被创建，在其他地方被引用

### 方法的定义以及调用

方法应具有原子性即一个方法完成一个功能

```java
psvm(){
	int sum = add(1,2);
	System.out.println(sum);//3
}


public static int add(int a,int b){
	return a+b;
}
```

当方法返回一个值的时候，方法调用通常被当作一个值

当方法返回值是void时，方法调用一定是一条语句

```java
int larger = max(30,40);
System.out.println(max(30,40));
```

### 方法重载

重载就是在一个类中，有相同的函数名称，但是参数不同

```java
psvm(){
	int sum = add(1,2);
	System.out.println(sum);//3
}


public static int add(int a,int b){
	return a+b;
}

public static double add(double a,double b){
	return a+b;
}
```

方法名称相同

参数列表不同

### 命令行传参

```java
public class Commandline{
	public static void main(String args[]){
		for(int i = 0;i < args.length; i++){
			System.out.println("args[" + i + "]:"+args[i]);
		}
	}
}
```

### 可变参数

也成为不定向参数

在参数后增加省略号，一个参数只能添加一个可变参数

```java

public void test(int... i){
	System.out.println(i[0]);//本质就是数组
}
```

### 递归

递归就是方法自己调用自己

递归头：什么时候不调用自己，结束递归

递归体：什么时候调用自己

```java
public static int f(int n){
	if(n==1){
		return 1;
	}else{
		return n*f(n-1);
	}
}
```

## 数组

### 数组的定义

数组是相同类型数据的有序集合

数组描述的是相同类型的若干个数据，按照一定的先后次序排列组合而成

其中，每一个数据称作一个数组元素，每个数组元素可以通过一个下标来访问它们

### 数组的声明与创建

```java
int[] nums;//定义
int nums[];//不是首选，来源于c与c++
```

使用new操作符来创建

```java
nums = new int[10];//大小为10，可存放10个int类型数据
```

给数组中元素赋值

```java
nums[0] = 1;
nums[1] = 2;
nums[2] = 3;
//默认值为0
```

声明创建组合

```java
int[] nums = new int[10];
```

.length获取数组长度

### 静态初始化

```java
int[] a = {1,2,3,4,5,6,7,8};//数组大小确定了
Man[] mans = {new Man(),new Man()}//引用类型
```

### 动态初始化：包含默认初始化（都为0）

```java
int[] b = new int[10];
```

### 数组的四个基本特点

长度确定，一旦被创建，大小不可改变

元素类型相同

元素可以是任何数据类型

数组变量属于引用类型，数组中每个元素相当于该对象的成员变量

数组对象本身是在堆中的

ArrayIndexOutOfBoundsException数组下标异常

### 数组的使用

```java
int[] arrays = {1,2,3,4,5};
//打印全部元素
for(i = 0; i < arrays.length; i++){
	System.out.println(arrays[1]);
}//可以使用增强for循环
```

### 多维数组

```java
int[][] array = {{1,2},{2,3},{4,5}};
sout(array[0][0]);
```

### Arrays类

```java
import java.util.Arrays

public class ArrayDemo{
	public static void main(String[] args){
		int[] a = {1,2,3,4};
		sout(a);//类
    sout(Arrays.toString(a));//[1,2,3,4]
		Arrays.sort(a);//排序方法,升序
		Arrays.fill(a,0);//用0填充
	}
}

```

## 内存分析

### 堆

存放new的对象和数组

可以被所有的线程共享，不会存放别的对象引用

### 栈

存放基本变量类型（包含这个基本类型的具体数值）

引用对象的变量（会存放这个引用在堆里的具体地址）

### 方法区

可被所有线程共享

包含了所有的class和static变量

### 过程

声明数组

```java
int[] array = null;
```

栈中存入array

创建数组

```java
array = new int[10];
```

堆中开辟内存，10个空间

给数组赋值

```java
arrays[0] = 0;
...
...
...
```

开辟的空间中放入数字

## 排序

### 选择排序

### 插入排序

### 快速排序

### 归并排序

### 希尔排序

### 堆排序

### 基数排序

### 冒泡排序

```java
public static void sort(int[] array){
	for(int i = 0; i < array.length-1; i++){
		for(int j = 0; j < array.length-1-i; j++){
				if(array[j+1]<array[j]){
					temp = array[j];
					array[j] = array[j+1];
					array[j+1] = temp;
				}
			}	
		}
}
```

## 多态

实际类型确定，引用类型可以不确定，父类的引用指向子类

```java
Student s1 = new Student();
Person s2 = new Student();//无法调用子类独有的方法，可执行子类重写的方法
Object s3 = new Student();
```

### 注意事项

多态是方法的多态

父类和子类，有联系，类型转换异常，ClassCastException

存在条件：继承关系，方法需要重写，父类引用指向子类对象

不能重写的方法：

static方法属于类，不属于实例

final常量

private方法

### instanceof关键字

```java
//Object > String
//Object > Person > Teacher
//Object > Person > Student

psvm(){
	Object object = new Student();
	sout(object instanceof Student);//true
	sout(object instanceof Person);//true
	sout(boject instanceof Object);//true
	sout(object instanceof Teacher);//false
	sout(object instanceof String);//false

}
```

子类转化父类可能会丢失一些方法

父类转化子类需要强制转换

## Static关键字详解

```java
class Student{
	private static int age;//静态变量
	private double score;//非静态变量
}
sout(Student.age);
sout(Student.score);//报错
```

静态属性在内存中只有一个

可以直接通过类名使用

非静态方法可以直接调用静态方法

### 静态代码块

```java
public class Person{
	//2赋初始值
	{
			//匿名代码块
			System.out.println("匿名");//比构造器还早一步执行
	}
	//1只执行一次
	static {
			//静态代码块，只执行一次，与类同时加载
			System.out.println("静态");
	}
	//3
public Person(){
			sout("构造");

	}
}
```

### 静态导入包

```java
import static java.lang.Math random;

psvm(){
	random();
}
```

## 抽象类与接口

### 抽象类：类，只能单继承

```java
public abstract class Action{
	//约束~让别人来实现
	//abstract，抽象方法，只有方法名字，没有方法的实现
	public abstract void doSomething();

}
```

抽象类不能new出来，只能继承，抽象方法只能在抽象类中

```java
//抽象类的方法必须由子类重写
public class A extends Action{
	@Override
	public void doSomething(){}

}
```

### 接口：只有规范，专业的约束，实现约束与实现分离

接口的本质是契约

接口中的所有定义都是抽象的，public abstract

```java
public interface UserService{
	void add(String name);
	void delete(String name);
	void update(String name);
	void query(String name);
}
```

```java
public interface TimeService{
	void timer();
}
```

```java
public class UserServiceImpl implements UserService,TimeService{
	@override
	...
	...
	...
	
}
```

实现类必须重写所有方法，通过接口实现多继承

## 内部类

```java
public class Outer{
	private int id = 10;
	public void out(){
		sout("外部类的方法")	
	}
	public class Inner{		public void in(){
				sout("内部类方法")
		}
		//可以获得外部类私有属性、方法
		//静态内部类无法访问非静态属性

		public void getID(){
			sout(id);
		}
	}
}
```

```java
psvm(){
	Outer outer = new Outer();
	//通过外部类来实例化内部类
	Outer.Inner inner = outer.new Inner();
	inner.in();
}
```

一个java类中可以有多个class，只能有一个public class

### 局部内部类

```java
public class Outer{
	public void method(){
		class Inner{
			public void in(){}
		}
	}
}
```

### 匿名内部类

```java
public class Test{
	psvm(){
		//没有名字初始化类，不用将实例保存到变量中
		new Apple().eat();
	}
}
class Apple{
	public void eat(){}
}
```

## 异常机制

```java
psvm(){
	int a = 1;
  int b = 0;
	try{//监控区域
		sout(a/b);
	}catch(ArithmeticException e){
		sout("异常，。。。");
	}finally{//处理善后
		sout("finally");
		
	}
}
```

error与exception等级不同，error通过Throwable或者Error捕获

catch从上到下范围扩大

```java
e.printStackTrace();//打印错误的栈信息
```

```java
throw new Exception();
//主动抛出异常，一般在方法中使用，假设这个方法无法处理，方法上抛出异常
//将该方法的调用放在try中即可捕获
```

### 自定义异常

```java
public class MyException extends Exception{
	//传递数字>10
	private int detail;
	public MyException(int a){
		this.detail = a;
	}
//异常的打印信息
	@Override
	public String toString(){
		return "MyException{" + "detail=" + detail + '}';
	}
}
```

```java
public class Test{

	static void test(int a) throws MyException{
		Sout("传递的参数为"+a);
		if(a > 10){
			throw new MyException(a);
		}
	}

	psvm(){
		try{test(11);}
		catch(ME e){
			//增加处理异常的方法
			sout(e);
		}
	}
}
```










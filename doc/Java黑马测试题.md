# Java黑马测试题

标签：Java

---

## 一、Java面向对象

### 1.面向对象都有哪些特性以及你对这些特性的理解 

抽象（共有特征，只关注有什么行为和属性，不关注具体的行为） 继承 封装（类，对数据和数据的操作封装，只提供外界接口） 多态

### 3.clone 对象的使用

- clone常见用法
```
Person p1=new Person(01,"xiaowang");
Person p2=p1;//这是浅拷贝，p1=p2
Person p3=(Person)p1.clone();//这是深拷贝，p1!=p2
```
- 深拷贝：除了对对象进行拷贝，对对象的所有属性也进行拷贝；再操作上主要是通过setMail(getName()...);对对象中的类/对象也进行clone()
- 浅拷贝：指向同一对象

---

## 二、JavaSE 语法

### 4. 两个对象值相同 (x.equals(y) == true) ，但却可有不同的hashCode，这句话对不对？

- equals同hashcode同，hashcode同equals不一定同
```
比如说你用身份证判断equal, hashcode = 身份证每一位的数字的综合。
甲的身份证是 12345
乙的身份证是 54321
这样甲和乙的hashcode 都是以一样的 1 + 2+ 3+ 4+ 5 = 15
但是 12345 不equals 54321
```

### 5. 是否可以继承String 

- String是final类，不可以继承

### 6. 当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并 可返回变化后的结果，那么这里到底是值传递还是引用传递?

- java只有值传递，对象属性可通过参数传递在方法内被更改

### 10. 抽象类(abstract class)和接口(interface)有什么异同？

- 思路：从类声明、成员变量、成员方法等逐步对比，包括到自身构造、调用他人、他人调用其等阐述
- 注意：实现接口和继承abstract类时，若不完全实现需声明abstract

### 14. break和continue的区别？

- break跳出当前循环体
- continue跳出本次循环

---

## 五、JavaSE常用API

### switch 是否能作用在 byte 上，是否能作用在 long 上，是否能作用在 String上?

- Java5以前switch(expr)中，expr 只能是 byte、short、char、int。从 Java 5 开始，Java 中引入了枚举类型，expr 也可以是 enum 类型。
- 所以不能是long以上的和String等

### 4. String 、StringBuilder 、StringBuffer的区别？

- String 字符串常量
StringBuffer 字符串变量（线程安全）
StringBuilder 字符串变量（非线程安全）
- Java.lang.StringBuffer线程安全的可变字符序列。这是因为Stringbuffer中方法大都采用了synchronized的关键字修饰
- StringBuilder是Java5中引入的，它和 StringBuffer的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方法都没有被synchronized修饰，因此它的效率理论上也比StringBuffer要高

### 5. 什么情况下用“+”运算符进行字符串连接比调用StringBuffer/StringBuilder 对象的append方法连接字符串性能更好？

- 代码较简单时+ 相当于StringBuilder；但若在循环语句中，循环+ 会每次 循环构造一个StringBuilder对象，导致系统资源浪费，而循环中使用StringBuilder对象的append方法进行连接字符串，只会在for循环外生成一个StringBuilder对象，更优
- 以上通过反编译进行分析判断，也不建议+ 和StringBuidler混用；另外，JDK1.4一下编译需将StringBuidler改为StringBuffer
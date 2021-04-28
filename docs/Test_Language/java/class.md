# 类和方法
## 成员变量
```
/**
 * 成员变量
 */

public class Day01 {
    private  String  name;
    //成员方法
    public String getName(){
        int id =0;  //局部变量
        setName("java");
        return id +this.name;
    }
    //成员方法
    private void setName(String name) {
        //this关键字 这里的this代表本类的一个对象
        this.name = name;
    }
    //使用成员方法
    public Day01 getBook(){
        return this;
    }
}
```
## 类的构造方法
构造方法是一种与类同名的方法，对象的创建就是通过构造方法来完成
```
public class Day02 {

    //构造方法【无参】
    public Day02(){
        //this可以调用有参的构造方法，但是只能在无参构造方法中使用，而且必须是第一句
        this("this调用无参构造方法");
        System.out.println("调用无参构造方法");
    }

    //有参数的构造方法
    public Day02(String name) {
        System.out.println("有参数的构造方法");
    }

    public static void main(String[] args) {
       Day02 day02 = new Day02();

    }

}
```
### 静态变量、常量、方法、主方法
 * 学习之前需要了解一下关键字 static ，应为被static修饰的变量、常量、方法被称为静态变量、常量、方法
 * 静态数据和静态方法的作用通常是为了提供共享数据和方法的一种实现，以static声明的对象和方法，使用时直接用类名调用这些静态成员
 * 注意：

 1、静态方法中不可以使用this关键字

 2、静态方法中不可以直接调用非静态的方法

 主方法，程序的入口 使用关键字main定义
```
public  class Day03 {
    static double PI= 3.1415;   //静态成员变量
    static  int  id;
    //静态方法
    public  static  void method1(){
        System.out.println("我是一个静态方法");
    }
    //调用静态变量和方法
    public void  method2(){
        System.out.println(Day03.PI);
        System.out.println(Day03.id);
        Day03.method1();
    }
    //主方法，程序的入口
    public static void main(String[] args) {
        Day03 day03 = new Day03();
        day03.method2();
    }

}
```
## 对象
* Java的在世界，完全可以为你自己new一个对象出来
 * new 操作符创建对象，同时会自主调用构造方法中的代码
 * 对象的销毁
 * java提供fianlize（）方法。来回收一些不是被new出来的对象，java自己回收机制不受人为控制，所以时间不确定
 * 当然我们也可以指直接调用system.gc()方法强制启动垃圾回收机制
 ```
 public class Day04 {
    public Day04(){
        System.out.println("我是一个构造方法，你可以通过new来让我给你造个对象");
    }

    public static void main(String[] args) {
        new Day04();
    }
}
 ```
# 面向对象
## 类的祖宗
 类的祖宗object
 所有的类都默认继承Object
 常用方法：
 * clone（）
 * finalize（）
 * equals（）
 * toString()

 ### 例子
```
public class Day02 {
    //重写tostring方法
    @Override
    public String toString() {
        return "在"+getClass().getName()+"类中重写tostring（）";
    }

    public static void main(String[] args) {
        System.out.println(new Day02());
    }
}
```
## 继承
 * 继承的关键字extends
 * 子类继承父类的非私有的成员变量、方法
 * 通过关键字super来调用父类的构造方法
 * 子类继承父类之后可以重写父类的方法
 
 ### 例子
```
//父类
public class Day01 {
    //构造方法
    public Day01(){
        System.out.println("父类构造方法");
    }
    //成员方法
    protected void doSomething(){
        System.out.println("这是一个成员方法");
    }
    //返回类型的方法
    protected  Day01 dolt(){
        return new Day01();  //返回一个新对象会调用构造方法
    }

}
//子类，继承了父类
class Day01_sun extends  Day01{
    public Day01_sun(){
        //调用父类的构造方法
        super();
        super.doSomething();
    }
    //新建子类的方法
    public void doSomethingNew(){
        System.out.println("这是一个子类的方法");
    }
    //重写父类的方法
    @Override
    protected void doSomething() {
        super.doSomething();
    }
    //重写父类的方法，返回值为Day01_sun
    protected  Day01_sun dolt(){
        return new Day01_sun();
    }
//主方法
public static void main(String[] args) {
    Day01_sun day01_sun = new Day01_sun(); //创建对象之后调用父类的构造方法
    day01_sun.doSomethingNew(); //执行子类自有方法
    day01_sun.doSomething(); //调用重写父类的doSomething
    day01_sun.dolt(); //调用子类构造方法
    }

}
```
## 方法的重载
方法的重载：为了实现方法名相同形参不同的构造方法同时存在

使用场景，可能同一方法会通过不同的参数来实现不同的业务
### 例子
```
public class Day03 {
        //定义一个方法
    public static  int add(int a,int b){
        return  a+b;
    }
        //不同参数方法
    public static double add(double a, double b){
        return  a+b;
    }

    public static  int add(int a){
        return  a;
    }
    public static int add(int a,double b){
        return 1;
    }

    public  static  int  add(double a,int b){
        return 1;
    }
    //不定长参数方法
    public  static  int add(int ... a){
        int s =0;
        for (int i=0; i<a.length;i++){
            System.out.println("执行第"+i+"次的值为："+a[i]);
            s +=a[i];

        }
        return s;
    }
    public static void main(String[] args) {
        System.out.println("调用add(int,int)方法:"+add(1,2));
        System.out.println("调用add(double,double)方法:"+add(2.5,3.5));
        System.out.println("调用add（int）方法:"+add(2));
        System.out.println("调用不定长参数:"+add(1,2,3,4,5,6,7,8,9));
    }

}
```
## 多态
多态的目的是程序具有良好的扩展性
```
public class Day04 {
    //实例话保存四边形数组对象
    private Day04[] quet = new Day04[6];
    private int nextIndex=0;
    public void draw(Day04 q){
        while (true){
        if (nextIndex < quet.length){
            quet[nextIndex] = q;
            System.out.println("存储到下标:"+nextIndex+"中");
            nextIndex++;
        }else {
            nextIndex=0;
            break;
        }
        }
    }

    public static void main(String[] args) {
        Day04 q = new Day04();
         //以正方形对象为参数调用draw（） ，这里会先调用 Square()构造方法，之后执行draw（）方法
        q.draw(new Square());
        q.draw(new ParalleLogarmgle());//调用方式与上方同理
    }
    
}
class Square extends  Day04{
    public  Square(){
        System.out.println("画一个正方形");
    }
}

class ParalleLogarmgle extends  Day04{
    public ParalleLogarmgle(){
        System.out.println("画一个菱形");
    }
}
```
## 抽象类
抽象类的关键字abstract，实际过程中我们一般将父类定义为抽象了，用来继承和多态处理
抽象类中只有抽象方法，抽象方法除非被重写，否者没有任何意义
```
public abstract class Day05 {
    abstract  void test(Day05 t);
}


class  test1 extends  Day05 {
    public  test1(){
        System.out.println("这里会输出tst1构造方法");
    }
    //重写父类的抽象方法实现子类的多态
    @Override
    void test(Day05 t) {
        System.out.println("这里会输出tst1");
    }
}

class test2 extends  Day05{
    //构造方法
    public  test2(){
        System.out.println("这里会输出tst2构造方法");
    }
    //重写父类的抽象方法实现子类的多态
    @Override
    void test(Day05 t) {
        System.out.println("这里会输出tst2");
    }
}

class  test3 {
    public static void main(String[] args) {
        test1 test1 =new test1();
        test1.test(new test1());

        test2 test2 = new test2();
        test2.test(new test1());
    }

}
```
## 接口
接口的关键字 interface ，接口可以看成是抽象类的衍生，接口中只有方法，没有方法体
```
//定义一个接口
interface  drawTest{
        public void draw(); //接口中方法

}
//父类
public class Day06 {

    public  void doAnything(){
        System.out.println("我是父级的doAnything方法");
    }

}
//子类
class  Day06_sum extends Day06 implements drawTest{
    //重写接口
    @Override
    public void draw() {
        System.out.println("重写了接口中的方法");
    }
    //继承于父类，重写父类的方法
    @Override
    public void doAnything() {
        super.doAnything();
    }

    public static void main(String[] args) {
        Day06_sum day06_sum = new Day06_sum();
        day06_sum.doAnything();
        day06_sum.draw();
    }
}
```
## 内部类(需要好好看)

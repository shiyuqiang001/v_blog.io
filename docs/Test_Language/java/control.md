# 控制器
## 循环
### for循环
#### 语法1：

  for（表达式1；表达式2；表达式3）{

      执行语句

  }

#### 语法2：

 for（元素变量：遍历对象）{

     执行语句

 }
 #### 例子
 ~~~
 public class For_Test {
    public static void main(String[] args) {
        System.out.println("语法1的实践");
        for(int i = 0;i<10;i++){
            System.out.println("i的结果小于10，i现在的值是："+i);
        }

        System.out.println("语法2的实践");
        int [] a = {1,2,3,4,5,6};
        System.out.println("数组a的值："+a+" 为啥是这玩意呢，对象就是这样存在内存中的");
        for (int x:a){
            System.out.println("遍历输出数组a的值："+x);
        }

    }
}
 ~~~
### if循环
#### 语法：

if(布尔表带式1){

      布尔表带式1结果为true：执行语句

 }eles if（布尔表带式2）{

     布尔表带式2结果为true：执行语句

 }else{

     不满足上诉条件执行语句

 }
 #### 例子
 ```
 public class If_Test {
    //简单的if条件语句
    public void if_Case(){
        int a =100;
            if (a==100){
                System.out.println("a的值是100");
            }
    }
    ////一般的if条件语句
    public void if_Else_Case(){
        int a =100;
        int b =50;
        if (a==100){
            System.out.println("a的值是100");
        }else{
            System.out.println("a的值是啥我也不知道");
        }
        if (b>a){
            System.out.println("b的值大于a");
        }else{
            System.out.println("b的值小于a");
        }
    }
    //if_elseif_else
    public void if_Elseif_Else_Case(){
        int b =70;
        if (b>=100){
            System.out.println("成绩优秀");
        }else if((60<b)&&(b<80)){
            System.out.println("成绩及格");
        }else{
            System.out.println("成绩不及格");
        }

    }

    public static void main(String[] args) {
        If_Test if_test = new If_Test(); //实例化一个类对象
        if_test.if_Case();   //调用if_Case方法
        if_test.if_Else_Case(); //调用if_Else_Case方法
        if_test.if_Elseif_Else_Case(); //调用if_Elseif_Else_Case方法
    }
}
 ```
 ## 分支
 ### swith分支
 #### 语法：
 switch（表带式）{

     case 常量1：
          执行语句块；
          break；

     case 常量2：
          执行语句块；
          break；
 }
 #### 例子
 ```
 public class Switch_Test {
    public static void main(String[] args) {
        int a =80;
        switch (a){
            case 10:
                System.out.println("a的值是10");
                break;
            case 20:
                System.out.println("a的值是20");
                break;
            case 80:
                System.out.println("a的值是80");
                break;
        }
    }
}
 ```
### while分支
#### 语法1：
 while（条件表达式）{

     执行语句

 }
 #### 语法2：
 do{

    执行语句

 }while（条件表达式）
#### 例子
```
public class While_Test {
    public static void main(String[] args) {
        System.out.println("语法1的执行实践");
        int a =0;
        while(a<10){
             System.out.println("a现在的值小于10,a现在的值是"+a);
             a++;
        }
        System.out.println("语法2的执行实践");
        int b=0;
        do{
            System.out.println("b现在的值小于10,b现在的值是"+b);
            b++;
        }while(b<10);
    }

}
```
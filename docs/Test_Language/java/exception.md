# 异常
## 语法
```
 try {
        代码块

        }catch (Exception e){

            e.printStackTrace();  
        }
```
## 代码
```
public class Thundering {
    public static void main(String[] args) {
        try {
            String str ="iiil";
            System.out.println(str+"年龄是：");
            int age = Integer.parseInt("20L");
            System.out.println(age);
        }catch (Exception e){
            e.printStackTrace();
        }
        System.out.println("抛出异常后执行输出了本部本");
    }
}
```
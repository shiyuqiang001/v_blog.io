# 字符串
字符串的特性不可变
## 连接字符串
字符串使用“+”来进行字符串拼接
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好");
        String  str2 = new String("java");
        //字符串拼接
        String str = str1+str2;
        System.out.println(str);
    }
}

```

## 获取字符串的信息
### 获取字符串的长度
语法：str.length()
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好");
        System.out.println(str1.length());
    }
}
```
### 字符串查找
语法：str.indexOf( String substr)
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好");
        System.out.println(str1.indexOf("好"));
    }
}
```
### 获得索引处的字符
语法：str.charAt(int index)
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好");
        System.out.println(str1.charAt(1));
    }
}
```
## 字符串操作
### 获取子字符串
语法：str.substring(int beginIndex) ，当然也可以加结束的索引str.substring(int beginIndex, int endIndex)
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好,java");
        System.out.println(str1.substring(1));
    }
}
```
### 去除空格
语法：str.trim()
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好,   java");
        System.out.println("未去空格前字符串长度="+str1.lenght());
        System.out.println("去空格后字符串长度="+str1.trim.lenght());
    }
}
```
### 字符串替换
语法：str.replace(char oldChar,char newChar)
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好,   java");
        str1.replace('a','e')
        System.out.println("替换后的字符串："str1);
    }
}
```
### 判断字符串的开始和结尾
语法：
- str.startsWith("str")
- str.endsWith("str")
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好,   java");
        System.out.println("字符串的开头是你："str1.startsWith("你"));
        System.out.println("字符串的开头是好："str1.startsWith("好"));
        System.out.println("字符串的开头是你："str1.endsWith("你"));
         System.out.println("字符串的开头是a："str1.endsWith("a"));
    }
}
```
### 判断字符串是否相等
语法 str == str1
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("你好,   java");
        String  str2 = new String("你好,   python");
        System.out.println("字符串str1和str2相等吗："+str1==str2);
    }
}
```
### 按字段顺序比较两个字符串
语法：str.compareTo(String others)

按字典顺序此String对象位于参数字符串之前，比较结果为负数。此String对象位于参数字符串之后，比较结果为正数，字符串相等，结果为0
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("a");
        String  str2 = new String("b");c
        String  str3 = new String("c");
        System.out.println(str1+"compareTo"+str2+":"str1.compareTo(str2));
        System.out.println(str3+"compareTo"+str2+":"str3.compareTo(str2));
        System.out.println(str2+"compareTo"+str2+":"str2.compareTo(str2));
    }
}
```
### 字母大小写转换
语法：
- toLowerCase() :转换为小写
- toUpperCase() :转换为大写
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("abcd");
        String newStr = str1.toUpperCase();
        System.out.println(newStr);
        String newStr = str1.toLowerCase();
        System.out.println(newStr);
    }
}
```
### 字符串分割
语法：split(String sign) :根据给定的分割符对字符串进行分割
```
public class string {
    public static void main(String[] args) {
        String  str1 = new String("ab,cd");
        System.out.println(str1.split(','));
    }
}
```
## 字符串生成器
可变的字符串序列StringBuilder
### 追加
方法： append()
### 插入
方法：insert(int offset ,arg)
### 删除
方法： delete(int start ,int end)
```
public class string {
    public static void main(String[] args) {
        StringBuffer sb =new StringBuffer("hello"); //创建字符串生成器
        sb.append(",java");   //尾部追加
        System.out.println(sb);
        sb.insert(5,"?"); //第5位下标处插入
        System.out.println(sb);
        sb.delete(2,6);//删除2-6下标内容
        System.out.println(sb);
    }
}
```

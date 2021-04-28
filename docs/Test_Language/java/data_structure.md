# 知识点
基础知识点适用于多语言，主要是一些普遍的概念性东西。
## 数据结构
java语言提供了8种数据类型
### 整数
整数类型有三种short、int和long
- short

short 数据类型是 16 位、有符号的以二进制补码表示的整数
最小值是 -32768（-2^15）；
最大值是 32767（2^15 - 1）；
Short 数据类型也可以像 byte 那样节省空间。一个short变量是int型变量所占空间的二分之一；
默认值是 0；
- int

int 数据类型是32位、有符号的以二进制补码表示的整数；
最小值是 -2,147,483,648（-2^31）；
最大值是 2,147,483,647（2^31 - 1）；
一般地整型变量默认为 int 类型；
默认值是 0 
- long

long 数据类型是 64 位、有符号的以二进制补码表示的整数；
最小值是 -9,223,372,036,854,775,808（-2^63）；
最大值是 9,223,372,036,854,775,807（2^63 -1）；
这种类型主要使用在需要比较大整数的系统上；
默认值是 0L；
### 浮点
浮点类型根据精度分为float和double两种
- float

float 数据类型是单精度、32位、符合IEEE 754标准的浮点数；
float 在储存大型浮点数组的时候可节省内存空间；
默认值是 0.0f；
- double

double 数据类型是双精度、64 位、符合 IEEE 754 标准的浮点数；
浮点数的默认类型为 double 类型；
默认值是 0.0d；
### 字符
- char类型是一个单一的 16 位 Unicode 字符；
- 最小值是 \u0000（即为 0）；
- 最大值是 \uffff（即为 65535）；
- char 数据类型可以储存任何字符；
### 布尔
boolean数据类型表示一位的信息，只有两个取值：true 和 false
- 默认值是false
## 常量与变量
变量是可变的参数、常量是不可变的参数
他们都是通过声明类型在内存种划分对应的存储区间，下面是一些声明实例
```
int a, b, c;         // 声明三个int型整数：a、 b、c
int d = 3, e = 4, f = 5; // 声明三个整数并赋予初值
byte z = 22;         // 声明并初始化 z
String s = "runoob";  // 声明并初始化字符串 s
double pi = 3.14159; // 声明了双精度浮点型变量 pi
char x = 'x';        // 声明变量 x 的值是字符 'x'。
```
### 变量的类型
- 类变量：
独立于方法之外的变量，用 static 修饰
- 实例变量：
独立于方法之外的变量，不过没有 static 修饰
- 局部变量：
类的方法中的变量
```
public class Variable{
    static int allClicks=0;    // 类变量
 
    String str="hello world";  // 实例变量
 
    public void method(){
 
        int i =0;  // 局部变量
 
    }
}
```
### 局部变量的生命周期
- 局部变量声明在方法、构造方法或者语句块中；
- 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
- 访问修饰符不能用于局部变量；
- 局部变量只在声明它的方法、构造方法或者语句块中可见；
- 局部变量是在栈上分配的。
- 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
### 实例变量的生命周期
- 实例变量声明在一个类中，但在方法、构造方法和语句块之外；
- 当一个对象被实例化之后，每个实例变量的值就跟着确定；
- 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
- 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
- 实例变量可以声明在使用前或者使用后；
- 访问修饰符可以修饰实例变量；
- 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
- 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
- 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。
### 类变量（静态变量）
- 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。
- 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
- 静态变量除了被声明为常量外很少使用，静态变量是指声明为 public/private，final 和 static 类型的变量。静态变量初始化后不可改变。
- 静态变量储存在静态存储区。经常被声明为常量，很少单独使用 static 声明变量。
- 静态变量在第一次被访问时创建，在程序结束时销毁。
- 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为 public 类型。
- 默认值和实例变量相似。数值型变量默认值是 0，布尔型默认值是 false，引用类型默认值是 null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
- 静态变量可以通过：ClassName.VariableName的方式访问。
- 类变量被声明为 public static final 类型时，类变量名称一般建议使用大写字母。如果静态变量不是 public 和 final 类型，其命名方式与实例变量以及局部变量的命名方式一致。
### 常量
java 语言使用 final 关键字来定义一个常量
## 运算符
### 赋值运算符
| 操作符        | 描述   |  例子  |
| --------   | -----  | :----:  |
=	|简单的赋值运算符，将右操作数的值赋给左侧操作数	|C = A + B将把A + B得到的值赋给C
+ =	|加和赋值操作符，它把左操作数和右操作数相加赋值给左操作数	|C + = A等价于C = C + A
- =	|减和赋值操作符，它把左操作数和右操作数相减赋值给左操作数	|C - = A等价于C = C - A
* =	|乘和赋值操作符，它把左操作数和右操作数相乘赋值给左操作数	|C * = A等价于C = C * A
/ =	|除和赋值操作符，它把左操作数和右操作数相除赋值给左操作数	|C / = A，C 与 A 同类型时等价于 C = C / A
（％）=	|取模和赋值操作符，它把左操作数和右操作数取模后赋值给左操作数	|C％= A等价于C = C％A
<< =	|左移位赋值运算符	|C << = 2等价于C = C << 2
>> =	|右移位赋值运算符	|C >> = 2等价于C = C >> 2
＆=	|按位与赋值运算符	|C＆= 2等价于C = C＆2
^ =	|按位异或赋值操作符	|C ^ = 2等价于C = C ^ 2
| =	|按位或赋值操作符	|C | = 2等价于C = C | 2

### 算术运算符
| 操作符        | 描述   |  例子  |
| --------   | -----  | :----:  |
| +    |加法 - 相加运算符两侧的值 |  A + B 等于 30    |
| -    |减法 - 左操作数减去右操作数   |  A – B 等于 -10  |
| *      |乘法 - 相乘操作符两侧的值    | 	A * B等于200  |
| /     |除法 - 左操作数除以右操作数 | B / A等于2   |
| %        |取余 - 左操作数除以右操作数的余数   |  B%A等于0  |

### 自增自减
| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| ++     | 自增: 操作数的值增加1 |  B++ 或 ++B 等于 21（区别详见下文）    |
| --     |  自减: 操作数的值减少1   |   B-- 或 --B 等于 19（区别详见下文）   |
### 比较运算符
| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | \$1600 |   5     |
| 手机        |   \$12   |   12   |
| 管线        |    \$1    |  234  |
### 逻辑运算符
| 操作符        | 描述   |  例子  |
| --------   | -----  | :----:  |
| &&    |称为逻辑与运算符。当且仅当两个操作数都为真，条件才为真。|  （A && B）为假。    |
| 或   |称为逻辑或操作符。如果任何两个操作数任何一个为真，条件为真。   | （A 或 B）为真.  |
| ！    |称为逻辑非运算符。用来反转操作数的逻辑状态。如果条件为true，则逻辑非运算符将得到false。 | 	！（A && B）为真。  |
### 三元运算符
variable x = (expression) ? value if true : value if false
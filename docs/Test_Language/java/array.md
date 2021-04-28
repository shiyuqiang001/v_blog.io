# 数组
数组作为对象，允许使用new进行内存分配
## 一维数组
### 声明方式
- 数组元素类型 数组名[ ]
- 数组元素类型 [ ] 数组名
```
int array []
或
int [] arrayr
```
### 分配内存空间
其实就是定义数组长度，定义长度之后就可以访问，虽然元素为null
```
int array [5]
```
### 数组初始化
数组初始化可以初始化数组中的每一个元素
```
int array [] = new int[]{1,2,3,4}
或者
int array1 = {1,2,3,4}
```
### 一维数组的使用
```
public class GetDay {
    //一维数组
    public static void main(String[] args) {
        int day[] = new int[]{31,28,31,30,31,30,31,31,30,31,30,31};
        for (int i =0;i<day.length;i++){
            System.out.println((i+1)+"月有"+day[i]+"天"
            );
        }
    }
}
```
## 二维数组
### 声明方式
- 数组元素类型 数组名[][]
- 数组元素类型 [][] 数组名
```
int array [][]
或
int [][] arrayr
```
### 分配内存空间
其实就是定义数组长度，定义长度之后就可以访问，虽然元素为null
```
int array [5][6]
```
### 数组初始化
数组初始化可以初始化数组中的每一个元素
```
int array [][] = new int[][]{{11,22},1,2,3,4}
或者
int array1 = {{11,22},1,2,3,4}
```
### 二维数组的使用
```
public class GetDay {
    //一维数组
    public static void main(String[] args) {
         int a[][] = new int[3][4];
        for(int i =0; i<a.length; i++){
            for (int j=0;j<a[i].length; j++){
                System.out.print(a[i][j]);
            }
            System.out.println();
        }
    }
}
```
### 数组的遍历、查询、排序
```
public class GetDay {
    //一维数组
    public static void main(String[] args) {
        static class Meatch{
        int arr[] = new int[]{4,25,32};
        public int binarySecrch(int a){
            Arrays.sort(arr);
            int index = Arrays.binarySearch(arr,a);
            return index;
        }

        public int[] getArr(int a []) {

            return arr;
        }

        //遍历数组的foreach
        int arr2[][] ={{4,3},{1,2}};
        System.out.println("数组中的元素是"+arr2);
        for(int x[]:arr2){
            for (int e :x){
                    System.out.print(e);
            }
            System.out.println();
        }

        //查询
        Meatch m = new Meatch();
        int value=4;
        int index =m.binarySecrch(value);
        System.out.println(value+"的下标值是"+ index);
        for (int arry: m.arr){
            System.out.println(arry);
        }

         //排序
        Meatch m1 = new Meatch();
        int arr1[] = new int[]{4,52,32};
        int arr3[] = m1.getArr(arr1);
        for (int arry1: arr3){
            System.out.print("arr1的排序结果："+arry1);
        } 
    }
}

```
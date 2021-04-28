# 数据结构
## list集合
list集合接口  :实现可变数组，可以保存任何类型元素

ArrayList ：随机插入和访问处理快

LinkList：链式存储，向集合中插入、删除效率比较快

常用方法：
 - get（index i） 获取下标位元素
 - set（index i ,Element e) 修改下标位元素
### 例子
```
public class List_Test {
    public static void main(String[] args) {
        //创建集合对象
        //<>指集合的类型
        System.out.println("********************arraylist**************");
        List<String> list = new ArrayList(); //创建结合对象
        list.add("张三"); //添加元素
        list.add("李四"); //添加元素
        list.add("王五"); //添加元素
        // list.add(111); 这里我试着添加int类型，提示只能添加String
        list.remove(2);//删除元素，这里注意下标值从0开始
        for(int i=0;i<list.size();i++){
            System.out.println(list.get(i)); //使用get方法获取参数
        }
        System.out.println("------------快乐分解线---------------");
        list.set(0,"修改张三"); //修改参数
        for(int i=0;i<list.size();i++){
            System.out.println(list.get(i)); //使用get方法获取参数
        }

        System.out.println("********************Linkedlist**************");
        List<String> list1 = new LinkedList<>();
        list1.add("张三");
        list1.add(0,"李四");
        for(int i=0;i<list1.size();i++){
            System.out.println(list1.get(i)); //使用get方法获取参数
        }
    }
}

```
## map集合
map接口提供将key映射到值得对象
 * 常用方法：
 * put（K key, V value）：向集合添加key和value的映射关系
 * get（Object key）: 如果存在指定key对象，返回该对象的对应值，否则返回null
 * keySet（）：返回该对象中所有key对象形成的集合
 * values（）：返回该集合中所有值对象形成的Collection集合
 ### 例子
 ```
 public class Map_Test {
    public static void main(String[] args) {
        //创建map集合对象
        Map<String, Object> map = new HashMap<>();

        List list = new ArrayList();
        list.add("a");
        list.add("b");
        list.add("c");

        List list1 = new ArrayList();
        list1.add("张三");
        list1.add("李四");
        list1.add("王五");

        //将数据添加到map集合
        map.put("01",list);
        map.put("02",list1);

        //通过键获取值
        System.out.println(map.get("01"));
        System.out.println(map.get("02"));
        System.out.println(map.get("03"));

        //解析值中得数组
        List list_ruslt = (List) map.get("01");
        for (int i=0;i<list_ruslt.size();i++){
            System.out.println(list_ruslt.get(i));
        }

        //提取键得集合
        Set<String> set =map.keySet();
        Iterator iterator = set.iterator();
        System.out.println("KEY集合中得元素：");
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }

        //提取Vlaues值集合
        Collection cool = map.values();
        iterator=cool.iterator();
        System.out.println("VALUE集合中得元素：");
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
 ```
## set集合
set集合无序、不能重复

常用方法：
 * first() :返回此Set中当前第一个元素
 * last（）：返回此Set中当前第一个元素
 * headSet(E toElement):截取排在某个对象前面的的集合
 * subSet(E fromElement ,E toElement):截取排在某两个之间的对象的的集合,截取时前半部是包含，后半部不包含
 * tailSet（E fromElement）:截取某个对象及后面面的的集合

### 例子
```
import java.util.Iterator;
import java.util.TreeSet;

public class Set_Test<mian> implements Comparable {

    private String name;
    private long id;
    public Set_Test(String name,long id){
        this.id =id;
        this.name=name;

    }


    @Override
    public int compareTo(Object o) {
        Set_Test set_test =(Set_Test) o;
        int result = id>set_test.id?1:(id==set_test.id?0:-1);
        return result;
    }

    public static void main(String[] args) {
        Set_Test set_test1 = new Set_Test("李同学",01011);
        Set_Test set_test2 = new Set_Test("张同学",01012);
        Set_Test set_test3 = new Set_Test("王同学",01013);

        TreeSet<Set_Test> tree = new TreeSet<>();
        tree.add(set_test1);
        tree.add(set_test2);
        tree.add(set_test3);
        //返回此Set中当前第一个元素
        System.out.println(tree.first().getId()+" "+tree.first().getName());
        //返回此Set中当前最后一个元素
        System.out.println(tree.last().getId()+" "+tree.last().getName());
        //使用迭代器迭代对象
        Iterator<Set_Test> iterator = tree.iterator();
        System.out.println("Set集合中所有的元素：");
        while(iterator.hasNext()){
            Set_Test st = (Set_Test) iterator.next();
            System.out.println(st.getId()+" "+st.getName());
        }
        //截取排在某个对象前面的的集合
        iterator = tree.headSet(set_test2).iterator();
        System.out.println("截取排在某个对象前面的的集合：");
        while (iterator.hasNext()){
            Set_Test st = (Set_Test)iterator.next();
            System.out.println(st.getId()+" "+st.getName());
        }
        //截取排在某两个之间的对象的的集合,截取时前半部是闭区间，后半部分开区间
        iterator = tree.subSet(set_test1,set_test3).iterator();
        System.out.println("截取排在某两个之间的对象的的集合,截取时前半部是闭区间，后半部分开区间：");
        while (iterator.hasNext()){
            Set_Test st = (Set_Test)iterator.next();
            System.out.println(st.getId()+" "+st.getName());
        }
        //截取某个对象及后面面的的集合
        iterator = tree.tailSet(set_test1).iterator();
        System.out.println("截取排在某个对象后面面的的集合：");
        while (iterator.hasNext()){
            Set_Test st = (Set_Test)iterator.next();
            System.out.println(st.getId()+" "+st.getName());
        }

    }

//可以封装base类
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

}
```
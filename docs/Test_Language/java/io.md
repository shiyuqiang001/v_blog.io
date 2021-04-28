# 输入输出
## 创建删除文件
### 常用方法：
* File（String Pathname）
* File（String parent ， String child）
* File（File f  ，String child）
* file .exists() ：查询文件是否存在
* file .delete() : 删除文件
* file .createNewFile() :创建新文件

### 例子
```
public class Creat_File {
    public static void main(String[] args) {
       File file = new File("D:/Java脚本/src/io_home","1.txt");
       if (file.exists()){
           file.delete();
           System.out.println("删除已存在的文件");
       }else{
           try {
               file.createNewFile();
               System.out.println("文件创建成功");
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
    }

}
```
## 获取文件
### 常用方法
* getName()
 * canRead()
 * canWrite()
 * exits()
 * length()
 * getAbsolutePath()
 * getParent()
 * isFile()
 * isDirectory()
 * isHidden()
 * lastModified()
 ### 例子
 ```
 public class Get_File {
    public static void main(String[] args) {
        File file = new File("D:/Java脚本/src/io_home/1.txt"); //实例文件对象
        if (file.exists()){   //判断文件是不是存在
            String name = file.getName();   // 获取文件名称
            long length = file.length(); //获取文件长度
            boolean hidden = file.isHidden(); //判断文件是否隐藏
            boolean canRead = file.canRead();  //判断是否可读
            System.out.println("查询的文件名称："+name+"，\n文件的长度是："+length+"，\n文件的隐藏属性是："+hidden+"，\n文件的可读属性是："+canRead);
            System.out.println("******其他方法可以按同样的操作测试******");
        }else {
            System.out.println("文件不存在！");
        }
    }
}
```
### 小实战 
实现通过界面编辑，写入文件，点击按钮获取文件
```
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;

public class FileReader_or_Writer extends JFrame {
    private static  final long seriaVersionUID=1L;
    private  JPanel jCPanel =null; //创建面板对象
    private  JTextArea jTextArea = null; //创建文本域对象
    private  JPanel CPanel =null; //创建面板对象
    private  JButton openButton = null ;
    private  JButton stopButton = null;

    //FileReader_or_Writer构造方法
    protected FileReader_or_Writer(){
        super();
        init();


    }

    //初始化数据
    private void init() {
        this.setSize(300,600);
        this.setContentPane(getjCPanel());
        this.setTitle("JFrame");
    }
    //写入文件按钮+事件
    private  JButton getOpenButton(){
        if (openButton==null){
            openButton =new JButton();
            openButton.setText("写入文件");
            openButton.addActionListener(new ActionListener() {
                @Override
                public void actionPerformed(ActionEvent e) {
                    File file = new File("word.txt");
                    try {
                        FileWriter out = new FileWriter(file);
                        String s = jTextArea.getText();
                        out.write(s);
                        out.close();

                    }catch (Exception e1){
                        e1.printStackTrace();
                    }
                }
            });

        }

        return openButton;
    }
    //读取文件按钮+事件
    private  JButton getStopButton(){
        if (stopButton==null){
            stopButton =new JButton();
            stopButton.setText("读取文件");
            stopButton.addActionListener(new ActionListener() {
                @Override
                public void actionPerformed(ActionEvent e) {
                    File file = new File("word.txt");
                    try {
                        FileReader in = new FileReader(file);
                        char byt[] = new char[1024];
                        int len =in.read(byt);
                        jTextArea.setText(new String(byt,0,len));
                        in.close();

                    }catch (Exception e1){
                        //在抛异常的时候界面弹出提示框
                        class MyJDialog extends JDialog{
                           public  MyJDialog (Frame frame){
                               super(frame,"友情提示",true);
                               Container container = getContentPane();
                               container.add(new JLabel("系统库为空请先写入文件！"));
                               this.setBounds(30,30,200,80);
                           }
                        }
                        class MyFrame extends JFrame{
                            public MyFrame(){
                                Container container = new Container();
                                container.setLayout(null);
                                JLabel jLabel =new JLabel("提示：");
                                jLabel.setHorizontalAlignment(SwingConstants.CENTER);
                                container.add(jLabel);
                                new MyJDialog(MyFrame.this).setVisible(true);
                            }
                        }
                        new MyFrame();
                        System.out.println("系统库为空请先写入文件！");
                        e1.printStackTrace();

                    }
                }
            });

        }

        return stopButton;
    }
    //主面板控件
    private  JPanel getjCPanel(){
        if(jCPanel==null){
            jCPanel =new JPanel();
            jCPanel.setLayout(new BorderLayout());
            jCPanel.add(getJTextArea(),BorderLayout.CENTER);
            jCPanel.add(getCPanel(),BorderLayout.SOUTH);

        }
        return jCPanel;
    }
    //子面板控件
    private JPanel getCPanel() {
        CPanel = new JPanel();
        CPanel.add(getOpenButton());
        CPanel.add(getStopButton());
        return CPanel;
    }
    //子面板输入框
    private JTextArea getJTextArea() {
        jTextArea = new JTextArea(10,20);

        return jTextArea;
    }
    //主方法
    public static void main(String[] args) {
        FileReader_or_Writer o = new FileReader_or_Writer();
        o.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        o.setVisible(true);
    }

}

```
## 流
文件的输入输出流,用来操作磁盘文件。适用于读取需求比较简单的场景
 * 输入流：FileInputStream 继承于InputStream 类 ,传输的字节流
 * 常用的构造方法：
 * FileInputStream（String name）
 * FileInputStream (File file)
 ```
 public class FileInput_or_OutputStream {
    public FileInput_or_OutputStream(File file) {
    }

    public static void main(String[] args) {
        File file = new File("D:/Java脚本/src/io_home/1.txt"); //实例文件对象

        //将字节流写入文件
        try {
            FileOutputStream fileOutputStream = new FileOutputStream(file); //创建FileInputStream对象
            byte[] bytes = "你偷走了他的心，怎么还能留下".getBytes();
            fileOutputStream.write(bytes);
            fileOutputStream.close();
        } catch (FileNotFoundException e) {  //文件未找到类型异常
            e.printStackTrace();
        } catch (IOException e) { //IO流类型异常
            e.printStackTrace();
        }

        //将字节流从文件写出
        try {
            FileInputStream fileIntputStream = new FileInputStream(file); //创建FileInputStream对象
            byte[] bytes = new byte[1024] ; //创建bytes数组
            int len = fileIntputStream.read(bytes);
            //将文件中的信息输出
            System.out.println("文件中的信息是："+ new String(bytes,0,len));
            fileIntputStream.close();  //关闭流

        } catch (Exception e) {

        }


    }

}
 ```
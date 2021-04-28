# 网络请求
webshocket 编程通过套接字协议，通过指定的ip和端口进行网络传递

网络传递协议：tcp udp

## TCP
MyClien类  客户端
```
public class MyClien extends JFrame {
    private PrintWriter writer;
    Socket socket;
    private  JTextArea textArea =new JTextArea();
    private  JTextField textField = new JTextField();
    Container cc;

    //创建传统UI窗口 ，及页面数据写入
    public  MyClien(String title){
        super(title);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        cc=this.getContentPane();
        final JScrollPane scrollPane =new JScrollPane();
        scrollPane.setBorder(new BevelBorder(BevelBorder.RAISED));
        getContentPane().add(scrollPane,BorderLayout.CENTER);
        scrollPane.setViewportView(textArea);
        cc.add(textField,"South");
        textField.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                writer.println(textField.getText());
                textArea.append(textField.getText()+'\n');
                textArea.setSelectionEnd(textArea.getText().length());
                textField.setText("");
            }
        });
    }
    //创建socker连接
    private void connect(){
        textArea.append("尝试连接\n");
        try{
            socket = new Socket("127.0.0.1",8998);
            writer=new PrintWriter(socket.getOutputStream(),true);
            textArea.append("连接成功\n");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        MyClien clien = new MyClien("开始向服务器发送数据");
        clien.setSize(200,200);
        clien.setVisible(true);
        clien.connect();
    }
}
```
MyTcp 服务端
```
public class MyTcp {
    private  BufferedReader reader;
    private  ServerSocket serverSocket;
    private  Socket socket;
    void getserver(){
        try{
            serverSocket= new ServerSocket(8998);
            System.out.println("服务器套接字创建成功");
            while(true){
                System.out.println("等待客户机的连接");
                socket=serverSocket.accept();
                reader= new BufferedReader(new InputStreamReader(socket.getInputStream()));
                getClientMessage();
            }
        } catch (Exception e) {
            e.printStackTrace();

        }finally {
            System.out.println("客户机已死亡，启动自毁程序");
        }
    }

    private void getClientMessage() {
        try{
            while (true){
                //获得客户端信息
                System.out.println("客户机说："+reader.readLine());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        try{
            if(reader != null){
                reader.close();
            }
            if(socket != null){
                socket.close();
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }


    public static void main(String[] args) {
        MyTcp tcp = new MyTcp();  //创建本类方法
        tcp.getserver();     //调用主方法
    }
}

```
## UDP
广播类 Weather
```
import java.io.IOException;
import java.net.*;

public class Weather extends Thread {
    String weather = "节目预报：八点有大型晚会，请收听！";
    int port=9898;
    InetAddress inetAddress =null;
    MulticastSocket socket =null;
    Weather(){
        try {
            inetAddress =InetAddress.getByName("224.225.10.0");
            socket =new MulticastSocket(port);
            socket.setTimeToLive(1);
            socket.joinGroup(inetAddress);
        } catch (UnknownHostException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public void run(){
        while (true) {
            DatagramPacket packet = null;  //声明DatagramPacket对象
            byte data[] = weather.getBytes();  //声明字节组
            packet = new DatagramPacket(data, data.length, inetAddress, port);
            System.out.println(new String(data));
            try {
                socket.send(packet);
                sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        Weather weather = new Weather();
        weather.start();
    }
}
```
接收类 Receive 
```
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.InetAddress;
import java.net.MulticastSocket;

public class Receive extends JFrame implements Runnable, ActionListener {
    int port; //定义端口变量
    InetAddress group = null; //声明对象
    MulticastSocket socket = null;
    JButton ince = new JButton("开始接收");  //开始接收按钮
    JButton stop = new JButton("停止接收");  //停止接收按钮
    JTextArea inceAr = new JTextArea(10,10); //文本域大小
    JTextArea inced = new JTextArea(10 ,10);
    Thread thread;
    boolean b =false;

    public Receive(){
        super("广播数据报");
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        thread = new Thread(this);
        ince.addActionListener(this);
        stop.addActionListener(this);
        inceAr.setForeground(Color.blue);
        JPanel north = new JPanel();
        north.add(ince);
        north.add(stop);
        add(north,BorderLayout.NORTH);
        JPanel center = new JPanel();
        center.setLayout(new GridLayout(1,2));
        center.add(inceAr);
        center.add(inced);
        add(center,BorderLayout.CENTER);
        validate();
        port=9898;
        try{
            group=InetAddress.getByName("224.225.10.0");
            socket = new MulticastSocket(port);
            socket.joinGroup(group);
        } catch (Exception e) {
            e.printStackTrace();
        }
        setBounds(100,50,360,380);
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource()==ince){
            ince.setBackground(Color.red);
            stop.setBackground(Color.yellow);
            if(!(thread.isAlive())){
                thread =new Thread(this);
            }
            thread.start();
            b=false;
        }
        if (e.getSource()==stop){
            ince.setBackground(Color.yellow);
            stop.setBackground(Color.red);
            b=true;
        }
    }

    @Override
    public void run() {
        while (true){
            byte data[] = new byte[1024];
            DatagramPacket packet =null;
            packet = new DatagramPacket(data,data.length,group,port);
            try{
                socket.receive(packet);
                String message =new String (packet.getData(),0,packet.getLength());
                inceAr.setText("正在接收8点档：\n"+message);
                inced.append(message+"\n");
            } catch (IOException e) {
                e.printStackTrace();
            }
            if (b==true){
                break;
            }

        }

    }

    public static void main(String[] args) {
        Receive receive =  new Receive();
        receive.setSize(460,200);
    }
}

```

# IO流学习

## 存储和读取数据的解决方案

将程序中的数据保存到本地 output写

将本地的数据加载到程序当中 input读

## IO流的分类

### 输入流（流向）

读取 

### 输出流（流向）

写出

### 字节流（操作文件类型）

所有类型的文件

### 字符流（操作文件类型）

纯文本文件

## IO流体系

### 字节流

InputStream（抽象类）

FileInputStream 操作本地文件的字节流输入

ObjectInputStream 操作对象的字节流输入

BufferedInputStream 带有缓冲区的字节流输入

OutputStream（抽象类）

File...

Object...

Bu...

#### 字节输出流

创建字节输出流对象

写数据

释放资源

```java
package org.example;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        //1.创建对象
        //写出 输出流 OutputStream
        //本地操作 File
        //没有新建文件会自己创建，但父级路径必须存在
        //文件如果存在会清空文件
        FileOutputStream fos = new  FileOutputStream("D:\\code\\JavaLearn\\a.txt");

        //2.写出数据
        //对应ASCII码，想要写入数字需要使用对应数字的ASCII码
        fos.write(97);
        //3.释放资源
        //不释放资源java将占用相应文件
        fos.close();
    }
}
```

一次写多个数据

```java	
package org.example;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        //创建对象
        FileOutputStream fos = new FileOutputStream("D:\\code\\JavaLearn\\a.txt");
        byte[] bytes = {97,98,99,100,101};
        fos.write(bytes);
        fos.close();
    }
}
//abcde
```

从1索引开始写2个字节

```java
package org.example;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        //创建对象
        FileOutputStream fos = new FileOutputStream("D:\\code\\JavaLearn\\a.txt");
        byte[] bytes = {97,98,99,100,101};
        fos.write(bytes,1,2);
        fos.close();
    }
}
//bc
```

换行写

```java
package org.example;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        //创建对象
        FileOutputStream fos = new FileOutputStream("D:\\code\\JavaLearn\\a.txt");
        String str1 = "hajksdfhjkasdfh";
        byte[] arr1 = str1.getBytes();//字符串变字符数组
        fos.write(arr1);

        //win回车换行 \r\n      (\n or \r)
        //Linux \n
        //Mac \r
        String wrap = "\r\n";
        byte[] bytes = wrap.getBytes();
        fos.write(bytes);

        String str2 = "666";
        byte[] arr2 = str2.getBytes();
        fos.write(arr2);
        
        fos.close();
    }
}

```

续写

```java
package org.example;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        //创建对象
        FileOutputStream fos = new  FileOutputStream("D:\\code\\JavaLearn\\a.txt",true);
        fos.write(87);
    }
}

```

#### 字节输入流

读取ASCII

```java
package org.example;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("D:\\code\\JavaLearn\\a.txt");
        int b1 = fis.read();
        System.out.println(b1);
        fis.close();

    }
}
```

强转字母

```java
package org.example;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamDemo {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new
        //文件不存在直接报错
        FileInputStream("D:\\code\\JavaLearn\\a.txt");
        int b1 = fis.read();
        System.out.println((char)b1);

        int b2 = fis.read();
        System.out.println((char)b2);

        int b3 = fis.read();
        System.out.println((char)b3);

        int b4 = fis.read();
        System.out.println((char)b4);
        fis.close();
    }
}
```



### 字符流

Reader（抽象类）

Writer（抽象类）


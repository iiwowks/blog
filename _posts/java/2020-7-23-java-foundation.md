---
layout:    post
title:     "java foundation"
date:       2020-03-20
category:  Java
author:    iiwowks
published:     true
---

## Java核心类

### Character类

```java
// 原始字符 'a' 装箱到 Character 对象 ch 中
Character ch = 'a';
// 原始字符 'x' 用 test 方法装箱
// 返回拆箱的值到 'c'
char c = test('x');
```

### Scanner类

```java
Scanner scan = new Scanner(System.in);
// 从键盘接收数据
// next方式接收字符串
// 判断是否还有输入
if (scan.hasNext()) {
    String str1 = scan.next();
    System.out.println("输入的数据为：" + str1);
}
scan.close();
```

`next():`

* 1、一定要读取到有效字符后才可以结束输入
* 2、对输入有效字符之前遇到的空白，next() 方法会自动将其去掉
* 3、只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符
* next() 不能得到带有空格的字符串

`nextLine()：`

* 1、以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符
* 2、可以获得空白

## 集合

### List

* `ArrayList`通过使用数组存储，数组满时，会创建一个更大的新数组，然后把旧数组中的所有元素复制到新数组
* `LinkedList`通过链表实现
* `List<E>`接口方法：
  * 在末尾添加一个元素：`void add(E e)`
  * 在指定索引添加一个元素：`void add(int index, E e)`
  * 删除指定索引的元素：`int remove(int index)`
  * 删除某个元素：`int remove(Object e)`
  * 获取指定索引的元素：`E get(int index)`
  * 获取链表大小（包含元素的个数）：`int size()`
  * `List.of()`创建List
  * `get(int)`遍历List
  * `List`实例调用 `iterator()`创建`Iterator`迭代器对象访问List
* `Iterator`对象有两个方法：
  * `boolean hasNext()` 判断是否有下一个元素
  * `E next()` 返回下一个元素
* `Iterable`接口定义了一个`Iterator<E> iterator()`方法，集合类必须返回一个`Iterator`实例
* 把`List`变成`Array`
  * `toArray()`返回一个`Object[]`数组， 会丢失类型信息
  * `toArray(T[])`传入一个类型相同的Array，泛型参数`<T>`
* `List.of(T)``Array`变`List` ,返回一个只读`List`

### Map

* `Map<K, V>`
* `put(K key, V value)`
* `V get(K key)`
* `boolean containsKey(K key)`
* `keySet()`返回`Set`集合
* `entrySet()`返回`key*value`映射

### EnumMap

* `key`对象是`enum`类型
* 内部以一个十分紧凑的数组存储value，据`enum`类型的key直接定位到内部数组的索引，并不需要计算`hashCode()`

### TreeMap

* 内部对`key`排序
* `SortedMap`在遍历时严格按照Key的顺序遍历，最常用的实现类是`TreeMap`；
* 作为`SortedMap`的Key必须实现`Comparable`接口，或者传入`Comparator`；
* 要严格按照`compare()`规范实现比较逻辑，否则，`TreeMap`将不能正常工作。

![image0](https://uploadfiles.nowcoder.com/images/20190917/334190970_1568705196598_5712E31C0DD632882CA35FC6B748EEE5)

## IO

* Input：从外部读入数据到内存
* Output：把数据从内存输出到外部
* IO流以字节为最小单位

IO流是一种流式的数据输入/输出模型：

* 二进制数据以`byte`为最小单位在`InputStream`/`OutputStream`中单向流动；
* 字符数据以`char`为最小单位在`Reader`/`Writer`中单向流动。

Java标准库的`java.io`包提供了同步IO功能：

* 字节流接口：`InputStream`/`OutputStream`；
* 字符流接口：`Reader`/`Writer`。

### File对象

Java的标准库`java.io`提供了`File`对象来操作文件和目录。

```java
File f = new File("C:\\Windows\\notepad.exe");
```

```java
// 假设当前目录是C:\Docs
File f1 = new File("sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File(".\\sub\\javac"); // 绝对路径是C:\Docs\sub\javac
File f3 = new File("..\\sub\\javac"); // 绝对路径是C:\sub\javac
```

可以用`.`表示当前目录，`..`表示上级目录。

File对象有3种形式表示的路径

* 一种是`getPath()`，返回构造方法传入的路径，
* 一种是`getAbsolutePath()`，返回绝对路径，
* 一种是`getCanonicalPath()`，它和绝对路径类似，但是返回的是规范路径，规范路径就是把`.`和`..`转换成标准的绝对路径后的路径：`C:\Windows\notepad.exe`

```java
f.isFile()
f.isDirectory()
f.isFile()
f.isDirectory()
f.isFile()
f.isDirectory()
```

用`File`对象获取到一个文件时，还可以进一步判断文件的权限和大小：

* `boolean canRead()`：是否可读；
* `boolean canWrite()`：是否可写；
* `boolean canExecute()`：是否可执行；
* `long length()`：文件字节大小
* 通过`createNewFile()`创建一个新文件，用`delete()`删除该文件
* 程序需要读写一些临时文件，File对象提供了`createTempFile()`来创建一个临时文件，以及`deleteOnExit()`在JVM退出时自动删除该文件。

```java
File f = File.createTempFile("tmp*", ".txt"); // 提供临时文件的前缀和后缀
f.deleteOnExit(); // JVM退出时自动删除
```

* 当File对象表示一个目录时，可以使用`list()`和`listFiles()`列出目录下的文件和子目录名。

### InputStream

```java
public abstract int read() throws IOException;
//读取输入流的下一个字节，并返回字节表示的int值（0~255）,读到末尾返回*1
```

`FileInputStream`是`InputStream`的一个子类。顾名思义，`FileInputStream`就是从文件流中读取数据。

```java
public void readFile() throws IOException {
    // 创建一个FileInputStream对象:
    InputStream input = new FileInputStream("src/readme.txt");
    for (;;) {
        int n = input.read(); // 反复调用read()方法，直到返回*1
        if (n == *1) {
            break;
        }
        System.out.println(n); // 打印byte的值
    }
    input.close(); // 关闭流
}
```

* `InputStream`并不是一个接口，而是一个抽象类, 是所有输入流的超类。
* 定义了一个方法`int read()`，`InputStream`和`OutputStream`都是通过`close()`方法来关闭流。关闭流就会释放对应的底层资源。

用`try ... finally`来保证`InputStream`在无论是否发生IO错误的时候都能够正确地关闭

更好的写法是利用Java 7引入的新的`try(resource)`的语法，只需要编写`try`语句，让编译器自动为我们关闭资源。

**缓冲**
一次读取多个字节`InputStream`提供了两个重载方法来支持读取多个字节：

* `int read(byte[] b)`：读取若干字节并填充到`byte[]`数组，返回读取的字节数
* `int read(byte[] b, int off, int len)`：指定`byte[]`数组的偏移量和最大填充数

```java
//利用缓冲区一次读取多个字节
public void readFile() throws IOException {
    try (InputStream input = new FileInputStream("src/readme.txt")) {
        // 定义1000个字节大小的缓冲区:
        byte[] buffer = new byte[1000];
        int n;
        while ((n = input.read(buffer)) != *1) { // 读取到缓冲区
            System.out.println("read " + n + " bytes.");
        }
    }
}
```

`read()`方法是阻塞（Blocking）的

* 用`FileInputStream`可以从文件获取输入流，这是`InputStream`常用的一个实现类
* `ByteArrayInputStream`可以在内存中模拟一个`InputStream`
* Java标准库的`java.io.InputStream`定义了所有输入流的超类
* `FileInputStream`实现了文件流输入
* `ByteArrayInputStream`在内存中模拟一个字节流输入
* 总是使用`try(resource)`来保证`InputStream`正确关闭

### OutputStream

* `OutputStream`是Java标准库提供的最基本的输出流。
* `OutputStream`也是抽象类，是所有输出类的超类。
* 定义了一个方法`void write(int b)`只会写一个字节，只写入int最低8位表示字节的部分。

```java
public abstract void write(int b) throws IOException;
```

* 还有一个`flush()`方法，将缓冲区的内容真正输出到目的地，缓冲区写满后OutputStream会自动调用，在调用`close()`方法关闭OutputStream之前，会自动调用`flush()`方法

```java
//将若干个字节写入文件流
public void writeFile() throws IOException{
    OutputStream output = new FileOutputStream("out/readme.txt");
    output.write(72);
    output.write(101);
    output.write(108);
    output.write(108);
    output.write(108);
    output.close();
}
```

* `FileOutputStream`
* 用`OutputStream`提供的重载方法`void write(byte[])`来实现一次性写入若干个字节

```java
public void writeFile() throws IOException {
    OutputStream output = new FileOutputStream("out/readme.txt");
    output.write("Hello".getBytes("UTF*8")); // Hello
    output.close();
}
```

### Filter模式

```ascii
                 ┌─────────────┐
                 │ InputStream │
                 └─────────────┘
                       ▲ ▲
┌────────────────────┐ │ │ ┌─────────────────┐
│  FileInputStream   │─┤ └─│FilterInputStream│
└────────────────────┘ │   └─────────────────┘
┌────────────────────┐ │     ▲ ┌───────────────────┐
│ByteArrayInputStream│─┤     ├─│BufferedInputStream│
└────────────────────┘ │     │ └───────────────────┘
┌────────────────────┐ │     │ ┌───────────────────┐
│ ServletInputStream │─┘     ├─│  DataInputStream  │
└────────────────────┘       │ └───────────────────┘
                             │ ┌───────────────────┐
                             └─│CheckedInputStream │
                               └───────────────────┘
```

一类是直接提供数据的基础`InputStream`，例如：

* FileInputStream
* ByteArrayInputStream
* ServletInputStream

一类是提供额外附加功能的`InputStream`，例如：

* BufferedInputStream
* DigestInputStream
* CipherInputStream

## Maven

> 项目目录结构

```ascii
a-maven-project
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       ├── java
│       └── resources
└── target
```

Maven是专门为Java项目打造的管理和构建工具

* 提供了一套标准化的项目结构
* 提供了一套标准化的构建流程（编译，测试，打包，发布……）
* 提供了一套依赖管理机制
* Maven使用`pom.xml`定义项目内容，并使用预设的目录结构
* 在Maven中`<dependency>`声明一个依赖项可以自动下载并导入classpath
* Maven使用`groupId`，`artifactId`和`version`唯一定位一个依赖
* 使用pom.xml定义项目内容,
* maven从中央仓库下载所需的jar包并缓存在本地
* [中央仓库](https://search.maven.org/)
* `lifecycle`相当于java的package,包含一个或多个phase
* `phase`相当于java的class，它包含一个或多个goal,触发goal
* `goal`相当于java的method

| scope      | 说明                                          | 示例            |
| :--------- | :-------------------------------------------- | :-------------- |
| `compile`  | 编译时需要用到该jar包（默认）                 | commons-logging |
| `test`     | 编译Test时需要用到该jar包                     | junit           |
| `runtime`  | 编译时不需要，但运行时需要用到                | mysql           |
| `provided` | 编译时需要用到，但运行时由JDK或某个服务器提供 | servlet-api     |

* `default`内置生命周期:
  * validate
  * initialize
  * ...
  * deploy
* `clean`生命周期:
  * pre-clean
  * clean （注意这个clean不是lifecycle而是phase）
  * post-clean
* 每个phase都是通过插件来执行的
* 标准插件:

| 插件名称 | 对应执行的phase |
| :------- | :-------------- |
| clean    | clean           |
| compiler | compile         |
| surefire | test            |
| jar      | package         |

* 项目打包：
  * maven输出jar包插件：maven-assembly-plugin
  * maven构建web工程：
  * web工程打包：
* 常用命令:
  * `mvn archetype:generate`: 创建maven工程结构
  * `mvn compile`: 编译源代码
  * `mvn test`: 执行测试用例
  * `mvn clean`: 清除产生的项目
  * `mvn package`: 项目打包
  * `mvn install`: 安装至本地仓库

## JDBC

```java
// 1.初始化驱动
Class.forName("com.mysql.jdbc.Driver");
// 2.获取数据库连接
Connection conn = DriverManager.getConnection(JDBC_URL, JDBC_USER, JDBC_PASSWORD);
// 3.操作数据库
Statement stmt = conn.createStatement();
// 4.传入sql语句，获取返回的结果集
ResultSet rs = stmt.executeQuery("SELECT id, grade, name, gender FROM students WHERE gender=0");
```

* `java database connectivity`
* Java标准库自带的JDBC接口其实就是定义了一组接口，而某个具体的JDBC驱动其实就是实现了这些接口的类
* 各数据库厂商使用相同的接口，Java代码不需要针对不同数据库分别开发
* Java程序编译期仅依赖`java.sql`包，不依赖具体数据库的jar包(jdbc驱动)
* 可随时替换底层数据库，访问数据库的Java代码基本不变
* connection相当于一个jdbc连接,相当于java程序到数据库的连接(通常是tcp连接)
* 打开一个Connection时，需要准备URL、用户名和口令，才能成功连接到数据库
* url由厂商指定,mysql :  `jdbc:mysql://<hostname>:<post>/<db>?key1=value1&key2=value2`
* 例子:`jdbc:mysql://localhost:3306/learnjdbc?&useSSL=false&serverTimezone=UTC`

### 查询

* 避免sql注入攻击:
  * 1.对所有字符串参数转义
  * 2.使用`PreparedStatement`

> 使用PreparedStatement

```java
User login(String name, String pass) {
    ...
    String sql = "SELECT * FROM user WHERE login=? AND pass=?";
    PreparedStatement ps = conn.prepareStatement(sql);
    ps.setObject(1, name);
    ps.setObject(2, pass);
    ...
}
```

* 数据类型转换:JDBC在`java.sql.Types`定义了一组常量来表示如何映射SQL数据类型

| SQL数据类型   | Java数据类型             |
| :------------ | :----------------------- |
| BIT, BOOL     | boolean                  |
| INTEGER       | int                      |
| BIGINT        | long                     |
| REAL          | float                    |
| FLOAT, DOUBLE | double                   |
| CHAR, VARCHAR | String                   |
| DECIMAL       | BigDecimal               |
| DATE          | java.sql.Date, LocalDate |
| TIME          | java.sql.Time, LocalTime |

### 更新

```java
try (PreparedStatement ps = conn.prepareStatement(
        "INSERT INTO students (grade, name, gender) VALUES (?,?,?)",
        Statement.RETURN_GENERATED_KEYS)) {
    ps.setObject(1, 1); // grade
    ps.setObject(2, "Bob"); // name
    ps.setObject(3, "M"); // gender
    int n = ps.executeUpdate(); // 1
    try (ResultSet rs = ps.getGeneratedKeys()) {
        if (rs.next()) {
            long id = rs.getLong(1); // 注意：索引从1开始
        }
    }
}
```

* 插入:`PreparedStatement`执行一条sql语句,最后执行`executeUpdate()`
* `获取自增主键`的正确写法是在创建`PreparedStatement`的时候，指定一个`RETURN_GENERATED_KEYS`标志位，表示JDBC驱动必须返回插入的自增主键
  * 调用`prepareStatement()`,第二个参数传入常量`Statement.RETURN_GENERATED_KEYS`,jdbc驱动返回自增主键
  * 执行`executeUpdate()`方法后,必须调用`getGeneratedKeys()`获取一个`ResultSet`对象,
* 使用JDBC执行INSERT、UPDATE和DELETE都可视为更新操作；
* 更新操作使用`PreparedStatement`的`executeUpdate()`进行，返回受影响的行数

### 事务

```java
Connection conn = openConnection();
try{
  // 关闭自动提交
  conn.setAutoCommit(false);
  // 执行多条sql语句
  insert(); update(); delete();
  // 提交事务
  conn.commit();
} catch (SQLException e){
  //回滚事务
  conn.rollback();
} finally {
  // connection对象的状态恢复到初始值
  conn.setAutoCommit(true);
  conn.close();
}
```

* JDBC提供了事务的支持，使用Connection可以开启、提交或回滚事务
* 开启事务
  * 关闭自动提交：`conn.setAutoCommit(false)`
  * 提交事务(事务以commit()方法结束)：`conn.commit()`
  * 回滚事务：`conn.rollback()`
  * connection对象的状态恢复到初始值: `conn.setAutoCommit(true)`
* 设置事务隔离级别为`READ COMMITTED`：`conn.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED)`

### Batch

```java
try (PreparedStatement ps = conn.prepareStatement("insert into students (name, gender, grade, score) values (?, ?, ?,?)")) {
  // 对同一个PreparedStatement反复设置参数并调用addBatch()
  for (String name: names){
    ps.setString(1, name);
    ...
    ps.setInt(4, score);
    ps.addBatch(); //添加到batch
  }
  //执行batch
  int[] ns = ps.exectuteBatch();
  for(int n : ns){
    System.out.println(n + "inserted."); // batch中每个SQL执行的结果数量
  }
}

```

* 批量执行、速度快于循环
* 对同一个PreparedStatement反复设置参数并调用`addBatch()`,相当于给一个sql加上了多组参数
* 调用`executeBatch()`, 返回该组参数执行后影响的结果数量

### 连接池

```java
//创建一个DataSource实例
HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/test");
config.setUsername("root");
config.setPassword("password");
config.addDataSourceProperty("connectionTimeout", "1000"); // 连接超时：1秒
config.addDataSourceProperty("idleTimeout", "60000"); // 空闲超时：60秒
config.addDataSourceProperty("maximumPoolSize", "10"); // 最大连接数：10
DataSource ds = new HikariDataSource(config);
//使用连接池
try (Connection conn = ds.getConnection()){//获取连接}//关闭连接
```

* 避免频繁创建和销毁jdbc连接，通过连接池复用已经创建好的连接
* 连接池标准接口`javax.sql.DataSource`
* `DataSource`实例总是作为一个全局变量存储、贯穿整个应用程序生命周期
* 调用`conn.close()`时，不是关闭连接，而是释放到连接池中，下次获取连接时能直接返回
* 数据库连接池是一种复用Connection的组件，它可以避免反复创建新连接，提高JDBC代码的运行效率
* 可以配置连接池的详细参数并监控连接池

## 正则表达式

* 正则表达式是用字符串描述的一个匹配规则，使用正则表达式可以快速判断给定的字符串是否符合匹配规则。Java标准库`java.util.regex`内建了正则表达式引擎

| 正则表达式 | 规则                              | 可以匹配                       |
| :--------- | :-------------------------------- | :----------------------------- |
| `A`        | 指定字符                          | `A`                            |
| `\u548c`   | 指定Unicode字符，十六进制`\u####` | `和`                           |
| `.`        | 任意字符                          | `a`，`b`，`&`，`0`             |
| `\d`       | 数字0~9                           | `0`~`9`                        |
| `\w`       | 大小写字母，数字和下划线          | `a`~`z`，`A`~`Z`，`0`~`9`，`_` |
| `\s`       | 空格、Tab键                       | 空格，Tab                      |
| `\D`       | 非数字                            | `a`，`A`，`&`，`_`，……         |
| `\W`       | 非\w                              | `&`，`@`，`中`，……             |
| `\S`       | 非\s                              | `a`，`A`，`&`，`_`，……         |
| `A*`       | 任意个数字符                      | 空，`A`，`AA`，`AAA`，……       |
| `A+`       | 至少1个字符                       | `A`，`AA`，`AAA`，……           |
| `A?`       | 0个或1个字符                      | 空，`A`                        |
| `A{3}`     | 指定个数字符                      | `AAA`                          |
| `A{2,3}`   | 指定范围个数字符                  | `AA`，`AAA`                    |
| `A{2,}`    | 至少n个字符                       | `AA`，`AAA`，`AAAA`，……        |


| 正则表达式 | 规则                 | 可以匹配                             |
| :--------- | :------------------- | :----------------------------------- |
| ^          | 开头                 | 字符串开头                           |
| $          | 结尾                 | 字符串结束                           |
| [ABC]      | […]内任意字符        | A，B，C                              |
| [A-F0-9xy] | 指定范围的字符       | `A`，……，`F`，`0`，……，`9`，`x`，`y` |
| [^A-F]     | 指定范围外的任意字符 | 非`A`~`F`                            |

* 用(...)把要提取的规则分组: `learn\\s(java|php|go)`
* `String.matches()`
* `区号-电话号`: `(\d{3,4})\-(\d{6,8})`

```java
Pattern p = Pattern.compile("(\\d{3,4})\\-(\\d{7,8})");
Matcher m = p.matcher("010-12345678");
if (m.matches()) {
    String g1 = m.group(1);
    String g2 = m.group(2);
    System.out.println(g1);
    System.out.println(g2);
} else {
    System.out.println("匹配失败!");
}
```

* 引入`java.util.regex`包，用`Pattern`对象匹配，匹配后获得一个`Matcher`对象，如果匹配成功，就可以直接从`Matcher.group(index)`返回子串
* 正则表达式匹配默认使用贪婪匹配，可以使用`?`表示对某一规则进行非贪婪匹配
* 反向引用匹配到的子串：`$1`, `$2`
* 分割字符串：`String.split()`
* 搜索子串：`Matcher.find()`
* 替换字符串：`String.replaceAll()`

## 设计模式

### 工厂模式

* 工厂模式用于隐藏创建对象的细节
* 工厂类(Factory)分类：
  * 简单工厂:
  * 工厂方法
  * 抽象工厂
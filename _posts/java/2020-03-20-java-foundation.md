---
layout:     post
title:      "java foundation"
date:       2020-03-20
category:   Java
author:     iiwowks
published:  true
photoswipe: true
syntaxhighlight: false
---

> **[Java13 API Document](https://docs.oracle.com/en/java/javase/13/docs/api/index.html)**

### 杂项————用于熟悉API

```java
/* String trim() */
string.trim(); // 去除首尾所有空格


/* substring() */
public String substring(int beginIndex);
public String substring(int beginIndex, int endIndex); // 左闭右开


/* Set */
Set<V> set = new HashSet<>(); // new TreeSet(); // 不重复元素集合
set.add(value);
set.delete(value);
set.hash(value);


/* Map */
Map<K, V> map = new HashMao<>();// new TreeMap(); // key-value对，key
map.set(key, value);
map.get(key);
map.has(key)
map.size();
map.clear();


/* String.valueOf() */
static String valueOf​(Object obj); //Returns the string representation of the Object argument.


/* Stack */
Stack<Character> stack = new Stack<>();


/* StringBuilder */
StringBuilder sb = new StringBuilder();
while (!stack.isEmpty()) {
    sb.append(stack.pop());
}
return sb.reverse().toString();


/* Character类 */
Character ch = 'a'; // 原始字符 'a' 装箱到 Character 对象 ch 中
char c = test('x'); // 原始字符 'x' 用 test 方法装箱  // 返回拆箱的值到 'c'


/* Scanner类 */
Scanner scan = new Scanner(System.in);
if (scan.hasNext()) {
    String str1 = scan.next();
    System.out.println("输入的数据为：" + str1);
}
scan.close();
```


![image0](https://uploadfiles.nowcoder.com/images/20190917/334190970_1568705196598_5712E31C0DD632882CA35FC6B748EEE5)

### 集合-List

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

### 集合-Map

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

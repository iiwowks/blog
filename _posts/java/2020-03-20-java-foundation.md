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

## 杂项————用于熟悉API 记录碰到的不熟悉的库函数

```java
/* entrySet() */
public Set<Map.Entry<K,​V>> entrySet(); // 返回key-value键值Set集合


/* keySet() */
public Set<K> keySet(); // 返回key键值的Set集合


/* getOrDefault(key, value) */
// Returns the value to which the specified key is mapped, or defaultValue if this map contains no mapping for the key.
default V getOrDefault​(Object key, V defaultValue)



/* swap() */
/*
 * @param list list
 * @param i  index
 * @param j  index
 */
public static void swap(List<?> list, int i, int j); // 集合中的元素交换位置


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
Map<K, V> map = new HashMap<>();// new TreeMap(); // key-value对，key
map.set(key, value);
map.get(key);
map.has(key)
map.size();
map.clear();


/* String.valueOf() */
static String valueOf​(Object obj); //Returns the string representation of the Object argument.


/* Stack */
// Java的集合类没有单独的Stack接口，因为有个遗留类名字就叫Stack，出于兼容性考虑，所以没办法创建Stack接口，只能用Deque接口来“模拟”一个Stack
Stack<Character> stack = new Stack<>();
// 现在推荐使用Deque模拟Stack
Deque<Integer> stack = new ArrayDeque<Integer>();


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

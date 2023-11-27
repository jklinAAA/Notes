

**基本语法**

- **类名**：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如 **MyFirstJavaClass** 。

- **方法名**：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。

-   浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

```
(int)23.7 == 23;        
(int)-45.89f == -45
```



##### 基本数据类型

- ###### 自动类型转换

  必须满足转换前的数据类型的位数要低于转换后的数据类型，例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。

- ###### 强制类型转换

1. 条件是转换的数据类型必须是兼容的。

2. 格式：(type)value type是要强制类型转换后的数据类型 int i1 = 123;        byte b = (byte)i1;



##### 常量和静态变量的区别

- 常量通常用于存储一些固定的值，如数学常数、配置信息等，而静态变量通常用于存储可变的数据，如计数器、全局状态等。

  ##### 访问控制修饰符

- **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**

- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。

- **public** ，**default**

  

  ##### 请注意以下方法继承的规则：

- 父类中声明为 public 的方法在子类中也必须为 public。

- 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。

- 父类中声明为 private 的方法，不能够被子类继承。

  

- 前缀自增自减法(++a,--a):** 先进行自增或者自减运算，再进行表达式运算。

- 后缀自增自减法(a++,a--):** 先进行表达式运算，再进行自增或者自减运算 



位运算符

^：如果相对应位值相同，则结果为0，否则为1

\>> ：按位右移运算符。左操作数按位右移右操作数指定的位数。

\>>> :按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。



- #### Java 增强 for 循环

for(声明语句 : 表达式) {   //代码句子 }

**声明语句：**声明新的局部变量，该变量的类型必须和数组元素的类型匹配

**表达式：**表达式是要访问的数组名，或者是返回值为数组的方法。

int [] numbers = {10, 20, 30, 40, 50};     

  for(int x : numbers ){       

  System.out.print( x );      

   System.out.print(",");



- Java switch case 语句

如果 case 语句块中没有 break 语句时，匹配成功后，从<u>当前</u> case 开始，后续所有 case 的值都会输出。如果后续的 case 语句块有 break 语句则会跳出判断。

- Math 类

   System.out.println("90 度的正弦值：" + Math.sin(Math.PI/2));      

   System.out.println("0度的余弦值：" + Math.cos(0));       

   System.out.println("60度的正切值：" + Math.tan(Math.PI/3));       

   System.out.println("1的反正切值： " + Math.atan(1));       

   System.out.println("π/2的角度值：" + Math.toDegrees(Math.PI/2)); 



- Number & Math 类方法

- | 序号 | 方法与描述                                                   |
  | :--- | :----------------------------------------------------------- |
  | 1    | [xxxValue()](https://www.runoob.com/java/number-xxxvalue.html) 将 Number 对象转换为xxx数据类型的值并返回。 |
  | 2    | [compareTo()](https://www.runoob.com/java/number-compareto.html) 将number对象与参数比较。 |
  | 3    | [equals()](https://www.runoob.com/java/number-equals.html) 判断number对象是否与参数相等。 |
  | 4    | [valueOf()](https://www.runoob.com/java/number-valueof.html) 返回一个 Number 对象指定的内置数据类型 |
  | 5    | [toString()](https://www.runoob.com/java/number-tostring.html) 以字符串形式返回值。 |
  | 6    | [parseInt()](https://www.runoob.com/java/number-parseInt.html) 将字符串解析为int类型。 |
  | 7    | [abs()](https://www.runoob.com/java/number-abs.html) 返回参数的绝对值。 |
  | 8    | [ceil()](https://www.runoob.com/java/number-ceil.html) 返回大于等于( >= )给定参数的的最小整数，类型为双精度浮点型。 |
  | 9    | [floor()](https://www.runoob.com/java/number-floor.html) 返回小于等于（<=）给定参数的最大整数 。 |
  | 10   | [rint()](https://www.runoob.com/java/number-rint.html) 返回与参数最接近的整数。返回类型为double。 |
  | 11   | [round()](https://www.runoob.com/java/number-round.html) 它表示**四舍五入**，算法为 **Math.floor(x+0.5)**，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11。 |
  | 12   | [min()](https://www.runoob.com/java/number-min.html) 返回两个参数中的最小值。 |
  | 13   | [max()](https://www.runoob.com/java/number-max.html) 返回两个参数中的最大值。 |
  | 14   | [exp()](https://www.runoob.com/java/number-exp.html) 返回自然数底数e的参数次方。 |
  | 15   | [log()](https://www.runoob.com/java/number-log.html) 返回参数的自然数底数的对数值。 |
  | 16   | [pow()](https://www.runoob.com/java/number-pow.html) 返回第一个参数的第二个参数次方。 |
  | 17   | [sqrt()](https://www.runoob.com/java/number-sqrt.html) 求参数的算术平方根。 |
  | 18   | [sin()](https://www.runoob.com/java/number-sin.html) 求指定double类型参数的正弦值。 |
  | 19   | [cos()](https://www.runoob.com/java/number-cos.html) 求指定double类型参数的余弦值。 |
  | 20   | [tan()](https://www.runoob.com/java/number-tan.html) 求指定double类型参数的正切值。 |
  | 21   | [asin()](https://www.runoob.com/java/number-asin.html) 求指定double类型参数的反正弦值。 |
  | 22   | [acos()](https://www.runoob.com/java/number-acos.html) 求指定double类型参数的反余弦值。 |
  | 23   | [atan()](https://www.runoob.com/java/number-atan.html) 求指定double类型参数的反正切值。 |
  | 24   | [atan2()](https://www.runoob.com/java/number-atan2.html) 将笛卡尔坐标转换为极坐标，并返回极坐标的角度值。 |
  | 25   | [toDegrees()](https://www.runoob.com/java/number-todegrees.html) 将参数转化为角度。 |
  | 26   | [toRadians()](https://www.runoob.com/java/number-toradians.html) 将角度转换为弧度。 |
  | 27   | [random()](https://www.runoob.com/java/number-random.html) 返回一个随机数。 |

######  转义字符

- | \b   | 在文中该处插入一个后退键 |
  | ---- | ------------------------ |
  | \f   | 在文中该处插入换页符     |

##### Character 方法

| 1    | [isLetter()](https://www.runoob.com/java/character-isletter.html) 是否是一个字母 |
| ---- | ------------------------------------------------------------ |
| 2    | [isDigit()](https://www.runoob.com/java/character-isdigit.html) 是否是一个数字字符 |
| 3    | [isWhitespace()](https://www.runoob.com/java/character-iswhitespace.html) 是否是一个空白字符 |
| 4    | [isUpperCase()](https://www.runoob.com/java/character-isuppercase.html) 是否是大写字母 |
| 5    | [isLowerCase()](https://www.runoob.com/java/character-islowercase.html) 是否是小写字母 |
| 6    | [toUpperCase()](https://www.runoob.com/java/character-touppercase.html) 指定字母的大写形式 |
| 7    | [toLowerCase](https://www.runoob.com/java/character-tolowercase.html)() 指定字母的小写形式 |
| 8    | [toString](https://www.runoob.com/java/character-tostring.html)() 返回字符的字符串形式，字符串的长度仅为 |

#### Java String 类

- 字符串长度： int len = site.length();

- 连接字符串：string1.concat(string2);       

  更常用的是使用'+'操作符来连接字符串，如：

  ```
  "Hello," + " runoob" + "!"
  ```

- 创建格式化字符串

  String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

​       String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

如下所示：

System.out.printf("浮点型变量的值为 " +                  

"%f, 整型变量的值为 " +                 

 " %d, 字符串变量的值为 " +                 

 "is %s", floatVar, intVar, stringVar);

你也可以这样写

String fs;

 fs = String.format("浮点型变量的值为 " +                  

 "%f, 整型变量的值为 " +                  

 " %d, 字符串变量的值为 " +                 

  " %s", floatVar, intVar, stringVar);



- String 方法

- | 1    | [char charAt(int index)](https://www.runoob.com/java/java-string-charat.html) 返回指定索引处的 char 值。 |
  | ---- | ------------------------------------------------------------ |
  | 2    | [int compareTo(Object o)](https://www.runoob.com/java/java-string-compareto.html) 把这个字符串和另一个对象比较。 |
  | 3    | [int compareTo(String anotherString)](https://www.runoob.com/java/java-string-compareto.html) 按字典顺序比较两个字符串。 |
  | 4    | [int compareToIgnoreCase(String str)](https://www.runoob.com/java/java-string-comparetoignorecase.html) 按字典顺序比较两个字符串，不考虑大小写。 |
  | 5    | [String concat(String str)](https://www.runoob.com/java/java-string-concat.html) 将指定字符串连接到此字符串的结尾。 |
  | 6    | [boolean contentEquals(StringBuffer sb)](https://www.runoob.com/java/java-string-contentequals.html) 当且仅当字符串与指定的StringBuffer有相同顺序的字符时候返回真。 |
  | 7    | [static String copyValueOf(char[\] data)](https://www.runoob.com/java/java-string-copyvalueof.html) 返回指定数组中表示该字符序列的 String。 |
  | 8    | [static String copyValueOf(char[\] data, int offset, int count)](https://www.runoob.com/java/java-string-copyvalueof.html) 返回指定数组中表示该字符序列的 String。 |
  | 9    | [boolean endsWith(String suffix)](https://www.runoob.com/java/java-string-endswith.html) 测试此字符串是否以指定的后缀结束。 |
  | 10   | [boolean equals(Object anObject)](https://www.runoob.com/java/java-string-equals.html) 将此字符串与指定的对象比较。 |
  | 11   | [boolean equalsIgnoreCase(String anotherString)](https://www.runoob.com/java/java-string-equalsignorecase.html) 将此 String 与另一个 String 比较，不考虑大小写。 |
  | 12   | [byte[\] getBytes()](https://www.runoob.com/java/java-string-getbytes.html)  使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。 |
  | 13   | [byte[\] getBytes(String charsetName)](https://www.runoob.com/java/java-string-getbytes.html) 使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。 |
  | 14   | [void getChars(int srcBegin, int srcEnd, char[\] dst, int dstBegin)](https://www.runoob.com/java/java-string-getchars.html) 将字符从此字符串复制到目标字符数组。 |
  | 15   | [int hashCode()](https://www.runoob.com/java/java-string-hashcode.html) 返回此字符串的哈希码。 |
  | 16   | [int indexOf(int ch)](https://www.runoob.com/java/java-string-indexof.html) 返回指定字符在此字符串中第一次出现处的索引。 |
  | 17   | [int indexOf(int ch, int fromIndex)](https://www.runoob.com/java/java-string-indexof.html) 返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。 |
  | 18   | [int indexOf(String str)](https://www.runoob.com/java/java-string-indexof.html)  返回指定子字符串在此字符串中第一次出现处的索引。 |
  | 19   | [int indexOf(String str, int fromIndex)](https://www.runoob.com/java/java-string-indexof.html) 返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。 |
  | 20   | [String intern()](https://www.runoob.com/java/java-string-intern.html)  返回字符串对象的规范化表示形式。 |
  | 21   | [int lastIndexOf(int ch)](https://www.runoob.com/java/java-string-lastindexof.html)  返回指定字符在此字符串中最后一次出现处的索引。 |
  | 22   | [int lastIndexOf(int ch, int fromIndex)](https://www.runoob.com/java/java-string-lastindexof.html) 返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。 |
  | 23   | [int lastIndexOf(String str)](https://www.runoob.com/java/java-string-lastindexof.html) 返回指定子字符串在此字符串中最右边出现处的索引。 |
  | 24   | [int lastIndexOf(String str, int fromIndex)](https://www.runoob.com/java/java-string-lastindexof.html)  返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。 |
  | 25   | [int length()](https://www.runoob.com/java/java-string-length.html) 返回此字符串的长度。 |
  | 26   | [boolean matches(String regex)](https://www.runoob.com/java/java-string-matches.html) 告知此字符串是否匹配给定的正则表达式。 |
  | 27   | [boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)](https://www.runoob.com/java/java-string-regionmatches.html) 测试两个字符串区域是否相等。 |
  | 28   | [boolean regionMatches(int toffset, String other, int ooffset, int len)](https://www.runoob.com/java/java-string-regionmatches.html) 测试两个字符串区域是否相等。 |
  | 29   | [String replace(char oldChar, char newChar)](https://www.runoob.com/java/java-string-replace.html) 返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。 |
  | 30   | [String replaceAll(String regex, String replacement)](https://www.runoob.com/java/java-string-replaceall.html) 使用给定的 replacement 替换此字符串所有匹配给定的正则表达式的子字符串。 |
  | 31   | [String replaceFirst(String regex, String replacement)](https://www.runoob.com/java/java-string-replacefirst.html)  使用给定的 replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。 |
  | 32   | [String[\] split(String regex)](https://www.runoob.com/java/java-string-split.html) 根据给定正则表达式的匹配拆分此字符串。 |
  | 33   | [String[\] split(String regex, int limit)](https://www.runoob.com/java/java-string-split.html) 根据匹配给定的正则表达式来拆分此字符串。 |
  | 34   | [boolean startsWith(String prefix)](https://www.runoob.com/java/java-string-startswith.html) 测试此字符串是否以指定的前缀开始。 |
  | 35   | [boolean startsWith(String prefix, int toffset)](https://www.runoob.com/java/java-string-startswith.html) 测试此字符串从指定索引开始的子字符串是否以指定前缀开始。 |
  | 36   | [CharSequence subSequence(int beginIndex, int endIndex)](https://www.runoob.com/java/java-string-subsequence.html)  返回一个新的字符序列，它是此序列的一个子序列。 |
  | 37   | [String substring(int beginIndex)](https://www.runoob.com/java/java-string-substring.html) 返回一个新的字符串，它是此字符串的一个子字符串。 |
  | 38   | [String substring(int beginIndex, int endIndex)](https://www.runoob.com/java/java-string-substring.html) 返回一个新字符串，它是此字符串的一个子字符串。 |
  | 39   | [char[\] toCharArray()](https://www.runoob.com/java/java-string-tochararray.html) 将此字符串转换为一个新的字符数组。 |
  | 40   | [String toLowerCase()](https://www.runoob.com/java/java-string-tolowercase.html) 使用默认语言环境的规则将此 String 中的所有字符都转换为小写。 |
  | 41   | [String toLowerCase(Locale locale)](https://www.runoob.com/java/java-string-tolowercase.html)  使用给定 Locale 的规则将此 String 中的所有字符都转换为小写。 |
  | 42   | [String toString()](https://www.runoob.com/java/java-string-tostring.html)  返回此对象本身（它已经是一个字符串！）。 |
  | 43   | [String toUpperCase()](https://www.runoob.com/java/java-string-touppercase.html) 使用默认语言环境的规则将此 String 中的所有字符都转换为大写。 |
  | 44   | [String toUpperCase(Locale locale)](https://www.runoob.com/java/java-string-touppercase.html) 使用给定 Locale 的规则将此 String 中的所有字符都转换为大写。 |
  | 45   | [String trim()](https://www.runoob.com/java/java-string-trim.html) 返回字符串的副本，忽略前导空白和尾部空白。 |
  | 46   | [static String valueOf(primitive data type x)](https://www.runoob.com/java/java-string-valueof.html) 返回给定data type类型x参数的字符串表示形式。 |
  | 47   | [contains(CharSequence chars)](https://www.runoob.com/java/java-string-contains.html) 判断是否包含指定的字符系列。 |
  | 48   | [isEmpty()](https://www.runoob.com/java/java-string-isempty.html) 判断字符串是否为空。 |

- Java StringBuffer 和 StringBuilder 类

  StringBuffer 方法

  | 1    | public StringBuffer append(String s) 将指定的字符串追加到此字符序列。 |
  | ---- | :----------------------------------------------------------- |
  | 2    | public StringBuffer reverse()  将此字符序列用其反转形式取代。 |
  | 3    | public delete(int start, int end) 移除此序列的子字符串中的字符。 |
  | 4    | public insert(int offset, int i) 将 `int` 参数的字符串表示形式插入此序列中。 |
  | 5    | insert(int offset, String str) 将 `str` 参数的字符串插入此序列中。 |
  | 6    | replace(int start, int end, String str) 使用给定 `String` 中的字符替换此序列的子字符串中的字符。 |

| 1    | int capacity() 返回当前容量。                                |
| ---- | :----------------------------------------------------------- |
| 2    | char charAt(int index) 返回此序列中指定索引处的 `char` 值。  |
| 3    | void ensureCapacity(int minimumCapacity) 确保容量至少等于指定的最小值。 |
| 4    | void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin) 将字符从此序列复制到目标字符数组 `dst`。 |
| 5    | int indexOf(String str) 返回第一次出现的指定子字符串在该字符串中的索引。 |
| 6    | int indexOf(String str, int fromIndex) 从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。 |
| 7    | int lastIndexOf(String str) 返回最右边出现的指定子字符串在此字符串中的索引。 |
| 8    | int lastIndexOf(String str, int fromIndex) 返回 String 对象中子字符串最后出现的位置。 |
| 9    | int length()  返回长度（字符数）。                           |
| 10   | void setCharAt(int index, char ch) 将给定索引处的字符设置为 `ch`。 |
| 11   | void setLength(int newLength) 设置字符序列的长度。           |
| 12   | CharSequence subSequence(int start, int end) 返回一个新的字符序列，该字符序列是此序列的子序列。 |
| 13   | String substring(int start) 返回一个新的 `String`，它包含此字符序列当前所包含的字符子序列。 |
| 14   | String substring(int start, int end) 返回一个新的 `String`，它包含此序列当前所包含的字符子序列。 |
| 15   | String toString() 返回此序列中数据的字符串表示形式。         |

- Arrays 类

  | 1    | **public static int binarySearch(Object[] a, Object key)** 用二分查找算法在给定数组中搜索给定值的对象(Byte,Int,double等)。数组在调用前必须排序好的。如果查找值包含在数组中，则返回搜索键的索引；否则返回 (-(*插入点*) - 1)。 |
  | ---- | :----------------------------------------------------------- |
  | 2    | **public static boolean equals(long[] a, long[] a2)** 如果两个指定的 long 型数组彼此*相等*，则返回 true。如果两个数组包含相同数量的元素，并且两个数组中的所有相应元素对都是相等的，则认为这两个数组是相等的。换句话说，如果两个数组以相同顺序包含相同的元素，则两个数组是相等的。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。 |
  | 3    | **public static void fill(int[] a, int val)** 将指定的 int 值分配给指定 int 型数组指定范围中的每个元素。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。 |
  | 4    | **public static void sort(Object[] a)** 对指定对象数组根据其元素的自然顺序进行升序排列。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。 |



#### Java 日期时间

- Date 对象创建以后，可以调用下面的方法。

- | 1    | **boolean after(Date date)** 若当调用此方法的Date对象在指定日期之后返回true,否则返回false。 |
  | :--- | ------------------------------------------------------------ |
  | 2    | **boolean before(Date date)** 若当调用此方法的Date对象在指定日期之前返回true,否则返回false。 |
  | 3    | **Object clone( )** 返回此对象的副本。                       |
  | 4    | **int compareTo(Date date)** 比较当调用此方法的Date对象和指定日期。两者相等时候返回0。调用对象在指定日期之前则返回负数。调用对象在指定日期之后则返回正数。 |
  | 5    | **int compareTo(Object obj)** 若obj是Date类型则操作等同于compareTo(Date) 。否则它抛出ClassCastException。 |
  | 6    | **boolean equals(Object date)** 当调用此方法的Date对象和指定日期相等时候返回true,否则返回false。 |
  | 7    | **long getTime( )** 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
  | 8    | **int hashCode( )**  返回此对象的哈希码值。                  |
  | 9    | **void setTime(long time)**   用自1970年1月1日00:00:00 GMT以后time毫秒数设置时间和日期。 |
  | 10   | **String toString( )** 把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)。 |

- 获取当前日期时间

// 初始化 Date 对象       Date date = new Date();               

// 使用 toString() 函数显示日期时间       System.out.println(date.toString()); 

### Java 日期时间

- 使用printf格式化日期

- %tY：输出四位数的年份，例如：2023

- %ty：输出两位数的年份，例如：23

- %tm：输出两位数的月份，例如：02

- %tB：输出月份的全名，例如：February

- %tb：输出月份的缩写，例如：Feb

- %tA：输出星期的全名，例如：Wednesday

- %ta：输出星期的缩写，例如：Wed

- %td：输出两位数的日期，例如：24

- %te：输出一位或两位数的日期，例如：24 或 02

- %tH：输出24小时制的小时数，例如：23

- %tI：输出12小时制的小时数，例如：11

- %tM：输出分钟数，例如：45

- %tS：输出秒数，例如：30

- %tp：输出上午还是下午，例如：AM 或 PM

- %tZ：输出时区，例如：GMT+08:00

- 

- | %tc  | 包括全部日期和时间信息      | 星期六 十月 27 14:21:20 CST 2007 |
  | ---- | --------------------------- | :------------------------------- |
  | %tF  | "年-月-日"格式              | 2007-10-27                       |
  | %tD  | "月/日/年"格式              | 10/27/07                         |
  | %tr  | "HH:MM:SS PM"格式（12时制） | 02:25:51 下午                    |
  | %tT  | "HH:MM:SS"格式（24时制）    | 14:28:16                         |
  | %tR  | "HH:MM"格式（24时制）       | 14:28                            |

#### Calendar类

- Calendar类对象字段类型

  | Calendar.YEAR         | 年份                           |
  | --------------------- | ------------------------------ |
  | Calendar.MONTH        | 月份                           |
  | Calendar.DATE         | 日期                           |
  | Calendar.DAY_OF_MONTH | 日期，和上面的字段意义完全相同 |
  | Calendar.HOUR         | 12小时制的小时                 |
  | Calendar.HOUR_OF_DAY  | 24小时制的小时                 |
  | Calendar.MINUTE       | 分钟                           |
  | Calendar.SECOND       | 秒                             |
  | Calendar.DAY_OF_WEEK  | 星期几                         |

#### GregorianCalendar类

- 

- | **序号** | **构造函数和说明**                                           |
  | -------- | ------------------------------------------------------------ |
  | 1        | **GregorianCalendar()** 在具有默认语言环境的默认时区内使用当前时间构造一个默认的 GregorianCalendar。 |
  | 2        | **GregorianCalendar(int year, int month, int date)** 在具有默认语言环境的默认时区内构造一个带有给定日期设置的 GregorianCalendar |
  | 3        | **GregorianCalendar(int year, int month, int date, int hour, int minute)** 为具有默认语言环境的默认时区构造一个具有给定日期和时间设置的 GregorianCalendar。 |
  | 4        | **GregorianCalendar(int year, int month, int date, int hour, int minute, int second)**  为具有默认语言环境的默认时区构造一个具有给定日期和时间设置的 GregorianCalendar。 |
  | 5        | **GregorianCalendar(Locale aLocale)** 在具有给定语言环境的默认时区内构造一个基于当前时间的 GregorianCalendar。 |
  | 6        | **GregorianCalendar(TimeZone zone)** 在具有默认语言环境的给定时区内构造一个基于当前时间的 GregorianCalendar。 |
  | 7        | **GregorianCalendar(TimeZone zone, Locale aLocale)**  在具有给定语言环境的给定时区内构造一个基于当前时间的 GregorianCalendar。 |

这里是GregorianCalendar 类提供的一些有用的方法列表：

| **序号** | **方法和说明**                                               |
| -------- | :----------------------------------------------------------- |
| 1        | **void add(int field, int amount)** 根据日历规则，将指定的（有符号的）时间量添加到给定的日历字段中。 |
| 2        | **protected void computeFields()** 转换UTC毫秒值为时间域值   |
| 3        | **protected void computeTime()** 覆盖Calendar ，转换时间域值为UTC毫秒值 |
| 4        | **boolean equals(Object obj)** 比较此 GregorianCalendar 与指定的 Object。 |
| 5        | **int get(int field)** 获取指定字段的时间值                  |
| 6        | **int getActualMaximum(int field)** 返回当前日期，给定字段的最大值 |
| 7        | **int getActualMinimum(int field)** 返回当前日期，给定字段的最小值 |
| 8        | **int getGreatestMinimum(int field)**  返回此 GregorianCalendar 实例给定日历字段的最高的最小值。 |
| 9        | **Date getGregorianChange()** 获得格里高利历的更改日期。     |
| 10       | **int getLeastMaximum(int field)** 返回此 GregorianCalendar 实例给定日历字段的最低的最大值 |
| 11       | **int getMaximum(int field)** 返回此 GregorianCalendar 实例的给定日历字段的最大值。 |
| 12       | **Date getTime()** 获取日历当前时间。                        |
| 13       | **long getTimeInMillis()** 获取用长整型表示的日历的当前时间  |
| 14       | **TimeZone getTimeZone()** 获取时区。                        |
| 15       | **int getMinimum(int field)** 返回给定字段的最小值。         |
| 16       | **int hashCode()** 重写hashCode.                             |
| 17       | **boolean isLeapYear(int year)** 确定给定的年份是否为闰年。  |
| 18       | **void roll(int field, boolean up)** 在给定的时间字段上添加或减去（上/下）单个时间单元，不更改更大的字段。 |
| 19       | **void set(int field, int value)** 用给定的值设置时间字段。  |
| 20       | **void set(int year, int month, int date)** 设置年、月、日的值。 |
| 21       | **void set(int year, int month, int date, int hour, int minute)** 设置年、月、日、小时、分钟的值。 |
| 22       | **void set(int year, int month, int date, int hour, int minute, int second)** 设置年、月、日、小时、分钟、秒的值。 |
| 23       | **void setGregorianChange(Date date)** 设置 GregorianCalendar 的更改日期。 |
| 24       | **void setTime(Date date)** 用给定的日期设置Calendar的当前时间。 |
| 25       | **void setTimeInMillis(long millis)** 用给定的long型毫秒数设置Calendar的当前时间。 |
| 26       | **void setTimeZone(TimeZone value)** 用给定时区值设置当前时区。 |
| 27       | **String toString()** 返回代表日历的字符串。                 |



#### 正则表达式语法



| 字符          | 说明                                                         |
| :------------ | ------------------------------------------------------------ |
| \             | 将下一字符标记为特殊字符、文本、反向引用或八进制转义符。例如， **n**匹配字符 **n**。**\n** 匹配换行符。序列 **\\\\** 匹配 **\\** ，**\\(** 匹配 **(**。 |
| ^             | 匹配输入字符串开始的位置。如果设置了 **RegExp** 对象的 **Multiline** 属性，^ 还会与"\n"或"\r"之后的位置匹配。 |
| $             | 匹配输入字符串结尾的位置。如果设置了 **RegExp** 对象的 **Multiline** 属性，$ 还会与"\n"或"\r"之前的位置匹配。 |
| *             | 零次或多次匹配前面的字符或子表达式。例如，zo* 匹配"z"和"zoo"。* 等效于 {0,}。 |
| +             | 一次或多次匹配前面的字符或子表达式。例如，"zo+"与"zo"和"zoo"匹配，但与"z"不匹配。+ 等效于 {1,}。 |
| ?             | 零次或一次匹配前面的字符或子表达式。例如，"do(es)?"匹配"do"或"does"中的"do"。? 等效于 {0,1}。 |
| {*n*}         | *n* 是非负整数。正好匹配 *n* 次。例如，"o{2}"与"Bob"中的"o"不匹配，但与"food"中的两个"o"匹配。 |
| {*n*,}        | *n* 是非负整数。至少匹配 *n* 次。例如，"o{2,}"不匹配"Bob"中的"o"，而匹配"foooood"中的所有 o。"o{1,}"等效于"o+"。"o{0,}"等效于"o*"。 |
| {*n*,*m*}     | *m* 和 *n* 是非负整数，其中 *n* <= *m*。匹配至少 *n* 次，至多 *m* 次。例如，"o{1,3}"匹配"fooooood"中的头三个 o。'o{0,1}' 等效于 'o?'。注意：您不能将空格插入逗号和数字之间。 |
| ?             | 当此字符紧随任何其他限定符（*、+、?、{*n*}、{*n*,}、{*n*,*m*}）之后时，匹配模式是"非贪心的"。"非贪心的"模式匹配搜索到的、尽可能短的字符串，而默认的"贪心的"模式匹配搜索到的、尽可能长的字符串。例如，在字符串"oooo"中，"o+?"只匹配单个"o"，而"o+"匹配所有"o"。 |
| .             | 匹配除"\r\n"之外的任何单个字符。若要匹配包括"\r\n"在内的任意字符，请使用诸如"[\s\S]"之类的模式。 |
| (*pattern*)   | 匹配 *pattern* 并捕获该匹配的子表达式。可以使用 **$0…$9** 属性从结果"匹配"集合中检索捕获的匹配。若要匹配括号字符 ( )，请使用"\("或者"\)"。 |
| (?:*pattern*) | 匹配 *pattern* 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配。这对于用"or"字符 (\|) 组合模式部件的情况很有用。例如，'industr(?:y\|ies) 是比 'industry\|industries' 更经济的表达式。 |
| (?=*pattern*) | 执行正向预测先行搜索的子表达式，该表达式匹配处于匹配 *pattern* 的字符串的起始点的字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?=95\|98\|NT\|2000)' 匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。 |
| (?!*pattern*) | 执行反向预测先行搜索的子表达式，该表达式匹配不处于匹配 *pattern* 的字符串的起始点的搜索字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?!95\|98\|NT\|2000)' 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。 |
| *x*\|*y*      | 匹配 *x* 或 *y*。例如，'z\|food' 匹配"z"或"food"。'(z\|f)ood' 匹配"zood"或"food"。 |
| [*xyz*]       | 字符集。匹配包含的任一字符。例如，"[abc]"匹配"plain"中的"a"。 |
| [^*xyz*]      | 反向字符集。匹配未包含的任何字符。例如，"[^abc]"匹配"plain"中"p"，"l"，"i"，"n"。 |
| [*a-z*]       | 字符范围。匹配指定范围内的任何字符。例如，"[a-z]"匹配"a"到"z"范围内的任何小写字母。 |
| [^*a-z*]      | 反向范围字符。匹配不在指定的范围内的任何字符。例如，"[^a-z]"匹配任何不在"a"到"z"范围内的任何字符。 |
| \b            | 匹配一个字边界，即字与空格间的位置。例如，"er\b"匹配"never"中的"er"，但不匹配"verb"中的"er"。 |
| \B            | 非字边界匹配。"er\B"匹配"verb"中的"er"，但不匹配"never"中的"er"。 |
| \c*x*         | 匹配 *x* 指示的控制字符。例如，\cM 匹配 Control-M 或回车符。*x* 的值必须在 A-Z 或 a-z 之间。如果不是这样，则假定 c 就是"c"字符本身。 |
| \d            | 数字字符匹配。等效于 [0-9]。                                 |
| \D            | 非数字字符匹配。等效于 [^0-9]。                              |
| \f            | 换页符匹配。等效于 \x0c 和 \cL。                             |
| \n            | 换行符匹配。等效于 \x0a 和 \cJ。                             |
| \r            | 匹配一个回车符。等效于 \x0d 和 \cM。                         |
| \s            | 匹配任何空白字符，包括空格、制表符、换页符等。与 [ \f\n\r\t\v] 等效。 |
| \S            | 匹配任何非空白字符。与 [^ \f\n\r\t\v] 等效。                 |
| \t            | 制表符匹配。与 \x09 和 \cI 等效。                            |
| \v            | 垂直制表符匹配。与 \x0b 和 \cK 等效。                        |
| \w            | 匹配任何字类字符，包括下划线。与"[A-Za-z0-9_]"等效。         |
| \W            | 与任何非单词字符匹配。与"[^A-Za-z0-9_]"等效。                |
| \x*n*         | 匹配 *n*，此处的 *n* 是一个十六进制转义码。十六进制转义码必须正好是两位数长。例如，"\x41"匹配"A"。"\x041"与"\x04"&"1"等效。允许在正则表达式中使用 ASCII 代码。 |
| \*num*        | 匹配 *num*，此处的 *num* 是一个正整数。到捕获匹配的反向引用。例如，"(.)\1"匹配两个连续的相同字符。 |
| \*n*          | 标识一个八进制转义码或反向引用。如果 \*n* 前面至少有 *n* 个捕获子表达式，那么 *n* 是反向引用。否则，如果 *n* 是八进制数 (0-7)，那么 *n* 是八进制转义码。 |
| \*nm*         | 标识一个八进制转义码或反向引用。如果 \*nm* 前面至少有 *nm* 个捕获子表达式，那么 *nm* 是反向引用。如果 \*nm* 前面至少有 *n* 个捕获，则 *n* 是反向引用，后面跟有字符 *m*。如果两种前面的情况都不存在，则 \*nm* 匹配八进制值 *nm*，其中 *n* 和 *m* 是八进制数字 (0-7)。 |
| \nml          | 当 *n* 是八进制数 (0-3)，*m* 和 *l* 是八进制数 (0-7) 时，匹配八进制转义码 *nml*。 |
| \u*n*         | 匹配 *n*，其中 *n* 是以四位十六进制数表示的 Unicode 字符。例如，\u00A9 匹配版权符号 (©)。 |

- #### Matcher 类的方法

  索引方法

  | 1    | **public int start()** 返回以前匹配的初始索引。              |
  | ---- | :----------------------------------------------------------- |
  | 2    | **public int start(int group)**  返回在以前的匹配操作期间，由给定组所捕获的子序列的初始索引 |
  | 3    | **public int end()** 返回最后匹配字符之后的偏移量。          |
  | 4    | **public int end(int group)** 返回在以前的匹配操作期间，由给定组所捕获子序列的最后字符之后的偏移量。 |

​       查找方法

| 1    | **public boolean lookingAt()**  尝试将从区域开头开始的输入序列与该模式匹配。 |
| ---- | :----------------------------------------------------------- |
| 2    | **public boolean find()** 尝试查找与该模式匹配的输入序列的下一个子序列。 |
| 3    | **public boolean find(int start****）** 重置此匹配器，然后尝试查找匹配该模式、从指定索引开始的输入序列的下一个子序列。 |
| 4    | **public boolean matches()** 尝试将整个区域与模式匹配。      |

替换方法

| 1    | **public Matcher appendReplacement(StringBuffer sb, String replacement)** 实现非终端添加和替换步骤。 |
| ---- | ------------------------------------------------------------ |
| 2    | **public StringBuffer appendTail(StringBuffer sb)** 实现终端添加和替换步骤。 |
| 3    | **public String replaceAll(String replacement)**  替换模式与给定替换字符串相匹配的输入序列的每个子序列。 |
| 4    | **public String replaceFirst(String replacement)**  替换模式与给定替换字符串匹配的输入序列的第一个子序列。 |
| 5    | **public static String quoteReplacement(String s)** 返回指定字符串的字面替换字符串。这个方法返回一个字符串，就像传递给Matcher类的appendReplacement 方法一个字面字符串一样工作。 |

- matches 和 lookingAt 方法

matches 和 lookingAt 方法都用来尝试匹配一个输入序列模式。它们的不同是 matches 要求整个序列都匹配，而lookingAt 不要求。

lookingAt 方法虽然不需要整句都匹配，但是需要从第一个字符开始匹配。

- replaceFirst 和 replaceAll 方法

replaceFirst 和 replaceAll 方法用来替换匹配正则表达式的文本。不同的是，replaceFirst 替换首次匹配，replaceAll 替换所有匹配

- PatternSyntaxException 类的方法

  PatternSyntaxException 是一个非强制异常类，它指示一个正则表达式模式中的语法错误。

  PatternSyntaxException 类提供了下面的方法来帮助我们查看发生了什么错误。

| 1    | **public String getDescription()** 获取错误的描述。          |
| ---- | ------------------------------------------------------------ |
| 2    | **public int getIndex()**  获取错误的索引。                  |
| 3    | **public String getPattern()** 获取错误的正则表达式模式。    |
| 4    | **public String getMessage()** 返回多行字符串，包含语法错误及其索引的描述、错误的正则表达式模式和模式中错误索引的可视化指示。 |

### Java 方法

- 方法的命名规则

1.方法的名字的第一个单词应以小写字母作为开头，后面的单词则用大写字母开头写，不使用连接符。例如：**addPerson**。



- 方法的定义

修饰符 返回值类型 方法名(参数类型 参数名){   

 ...    

方法体   

 ...    

return 返回值; }



- 可变参数

方法的可变参数的声明如下所示：

typeName... parameterName



- finalize() 方法

Java 允许定义这样的方法，它在对象被垃圾收集器析构(回收)之前调用，这个方法叫做 finalize( )，它用来清除回收对象。

例如，你可以使用 finalize() 来确保一个对象打开的文件被关闭了。

finalize() 一般格式是：

protected void finalize() {   // 在这里终结代码 }

关键字 protected 是一个限定符，它确保 finalize() 方法不会被该类以外的代码调用。



#### Java 流(Stream)、文件(File)和IO

- 读取控制台输入

  下面是创建 BufferedReader 的基本语法：

  BufferedReader br = new BufferedReader(new   InputStreamReader(System.in));

  BufferedReader 对象创建后，我们便可以使用 read() 方法从控制台读取一个字符，或者用 readLine() 方法读取一个字符串。

- 从控制台读取多字符输入

  int read( ) throws IOException

- FileInputStream

  可以使用字符串类型的文件名来创建一个输入流对象来读取文件：

  InputStream f = new FileInputStream("C:/java/hello");

  也可以使用一个文件对象来创建一个输入流对象来读取文件。我们首先得使用 File() 方法来创建一个文件对象：

  File f = new File("C:/java/hello"); InputStream in = new FileInputStream(f);

创建了InputStream对象，就可以使用下面的方法来读取流或者进行其他的流操作。

| **序号** | **方法及描述**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public void close() throws IOException{}** 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常。 |
| 2        | **protected void finalize()throws IOException {}** 这个方法清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常。 |
| 3        | **public int read(int r)throws IOException{}** 这个方法从 InputStream 对象读取指定字节的数据。返回为整数值。返回下一字节数据，如果已经到结尾则返回-1。 |
| 4        | **public int read(byte[] r) throws IOException{}** 这个方法从输入流读取r.length长度的字节。返回读取的字节数。如果是文件结尾则返回-1。 |
| 5        | **public int available() throws IOException{}** 返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取的字节数。返回一个整数值。 |

- FileOutputStream

| 1    | **public void close() throws IOException{}** 关闭此文件输入流并释放与此流有关的所有系统资源。抛出IOException异常。 |
| ---- | ------------------------------------------------------------ |
| 2    | **protected void finalize()throws IOException {}** 这个方法清除与该文件的连接。确保在不再引用文件输入流时调用其 close 方法。抛出IOException异常。 |
| 3    | **public void write(int w)throws IOException{}** 这个方法把指定的字节写到输出流中。 |
| 4    | **public void write(byte[] w)** 把指定数组中w.length长度的字节写到OutputStream中。 |

#### Java Scanner 类

- 下面是创建 Scanner 对象的基本语法：

  Scanner s = new Scanner(System.in);

- next():

  - 1、一定要读取到有效字符后才可以结束输入。
  - 2、对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。
  - 3、只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
  - next() 不能得到带有空格的字符串。

  nextLine()：

  - 1、以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。
  - 2、可以获得空白。



### Java 异常处理

- Java 内置异常类

- Java 的非检查性异常

- | **异常**                        | **描述**                                                     |
  | :------------------------------ | :----------------------------------------------------------- |
  | ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
  | ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
  | ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
  | ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
  | IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
  | IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
  | IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
  | IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
  | IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
  | NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
  | NullPointerException            | 当应用程序试图在需要对象的地方使用 `null` 时，抛出该异常     |
  | NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
  | SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
  | StringIndexOutOfBoundsException | 此异常由 `String` 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
  | UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

- 检查性异常类

  | ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
  | -------------------------- | ------------------------------------------------------------ |
  | CloneNotSupportedException | 当调用 `Object` 类中的 `clone` 方法克隆对象，但该对象的类无法实现 `Cloneable` 接口时，抛出该异常。 |
  | IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
  | InstantiationException     | 当试图使用 `Class` 类中的 `newInstance` 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
  | InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
  | NoSuchFieldException       | 请求的变量不存在                                             |
  | NoSuchMethodException      | 请求的方法不存在                                             |

- 异常方法（Throwable 类的主要方法:）

| 1    | **public String getMessage()** 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| ---- | ------------------------------------------------------------ |
| 2    | **public Throwable getCause()** 返回一个 Throwable 对象代表异常原因。 |
| 3    | **public String toString()** 返回此 Throwable 的简短描述。   |
| 4    | **public void printStackTrace()** 将此 Throwable 及其回溯打印到标准错误流。。 |
| 5    | **public StackTraceElement [] getStackTrace()** 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| 6    | **public Throwable fillInStackTrace()** 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

- 捕获异常

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```



- 多重捕获块

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。



- throws/throw 关键字

在Java中， **throw** 和 **throws** 关键字是用于处理异常的。

**throw** 关键字用于在代码中抛出异常，而 **throws** 关键字用于在方法声明中指定可能会抛出的异常类型。





### Java 继承

- 类的继承格式

在 Java 中通过 extends 关键字可以申明一个类是从另外一个类继承而来的，一般形式如下：

class 父类 { }

  class 子类 extends 父类 { }

- 需要注意的是 Java 不支持多继承，但支持多重继承

- 继承关键字

  extends关键字：在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类

​       implements关键字：使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

super关键字：我们可以通过super关键字来实现对父类成员的访问，用来引用当前对象的父类

this关键字：指向自己的引用

final 关键字：final 可以用来修饰变量（包括类属性、对象属性、局部变量和形参）、方法（包括类方法和对象方法）和类。

final 含义为 "最终的"。

使用 final 关键字声明类，就是把类定义定义为最终类，不能被继承，或者用于修饰方法，该方法不能被子类重写：

- 声明类：

  ```
  final class 类名 {//类体}
  ```

- 声明方法：

  ```
  修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
  ```

**注：** final 定义的类，其中的属性、方法不是 final 的。



- 构造器

  子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 **super** 关键字调用父类的构造器并配以适当的参数列表。

  如果父类构造器没有参数，则在子类的构造器中不需要使用 **super** 关键字调用父类构造器，系统会自动调用父类的无参构造器。





### Java 重写(Override)与重载(Overload)

- 重写(Override)

![image-20231031155224335](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031155224335.png)

在上面的例子中可以看到，尽管 b 属于 Animal 类型，但是它运行的是 Dog 类的 move方法（<u>**编译看左边，运行看右边**</u>）



- Java 重写(Override)与重载(Overload)

1. 参数列表与被重写方法的参数列表必须完全相同。
2. 返回类型与被重写方法的返回类型可以不相同，但是必须是父类返回值的派生类（java5 及更早版本返回类型要一样，java7 及更高版本可以不同）。
3. 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为 public，那么在子类中重写该方法就不能声明为 protected。
4. 父类的成员方法只能被它的子类重写。
5. 声明为 final 的方法不能被重写。
6. 声明为 static 的方法不能被重写，但是能够被再次声明。
7. 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为 private 和 final 的方法。
8. 子类和父类不在同一个包中，那么子类只能够重写父类的声明为 public 和 protected 的非 final 方法。
9. 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。
10. 构造方法不能被重写。
11. 如果不能继承一个类，则不能重写该类的方法。



- Super 关键字的使用

当需要在子类中调用父类的被重写方法时，要使用 super 关键字。



- 重载(Overload)

1. 重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同
2. **重载规则:**

- 被重载的方法必须改变参数列表(参数个数或类型不一样)；
- 被重载的方法可以改变返回类型；
- 被重载的方法可以改变访问修饰符；
- 被重载的方法可以声明新的或更广的检查异常；
- 方法能够在同一个类中或者在一个子类中被重载。
- 无法以返回值类型作为重载函数的区分标准。



- 重写与重载之间的区别

| 区别点   | 重载方法 | 重写方法                                       |
| :------- | :------- | :--------------------------------------------- |
| 参数列表 | 必须修改 | 一定不能修改                                   |
| 返回类型 | 可以修改 | 一定不能修改                                   |
| 异常     | 可以修改 | 可以减少或删除，一定不能抛出新的或者更广的异常 |
| 访问     | 可以修改 | 一定不能做更严格的限制（可以降低限制）         |

- 总结

  方法的重写(Overriding)和重载(Overloading)是java多态性的不同表现，重写是父类与子类之间多态性的一种表现，重载可以理解成多态的具体表现形式。

  - (1)方法重载是一个类中定义了多个方法名相同,而他们的参数的数量不同或数量相同而类型和次序不同,则称为方法的重载(Overloading)。
  - (2)方法重写是在子类存在方法与父类的方法的名字相同,而且参数的个数与类型一样,返回值也一样的方法,就称为重写(Overriding)。
  - (3)方法重载是一个类的多态性表现,而方法重写是子类与父类的一种多态性表现。



### Java 多态

- 多态存在的三个必要条件
  - 继承
  - 重写
  - 父类引用指向子类对象：**Parent p = new Child();**

- 虚函数

  虚函数的存在是为了多态。

  Java 中其实没有虚函数的概念，它的普通函数就相当于 C++ 的虚函数，动态绑定是Java的默认行为。如果 Java 中不希望某个函数具有虚函数特性，可以加上 final 关键字变成非虚函数。



- 多态的实现方式

  方式一：重写：

  方式二：接口

  - 生活中的接口最具代表性的就是插座，例如一个三接头的插头都能接在三孔插座中，因为这个是每个国家都有各自规定的接口规则，有可能到国外就不行，那是因为国外自己定义的接口类型。
  - java中的接口类似于生活中的接口，就是一些方法特征的集合，但没有方法的实现。具体可以看 [java接口](https://www.runoob.com/java/java-interfaces.html) 这一章节的内容。
  
  方式三：抽象类和抽象方法





### Java 抽象类

- 如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类
- 由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。在 Java 中抽象类表示的是一种继承关系，一个类只能继承一个抽象类，而一个类却可以实现多个接口。



- 抽象类

  在 Java 语言中使用 abstract class 来定义抽象类



- 抽象方法

1. 如果你想设计这样一个类，该类包含一个特别的成员方法，该方法的具体实现由它的子类确定，那么你可以在父类中声明该方法为抽象方法。
2. Abstract 关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。
3. 抽象方法没有定义，方法名后面直接跟一个分号，而不是花括号![image-20231031200209734](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031200209734.png)

声明抽象方法会造成以下两个结果：

- <u>如果一个类包含抽象方法，那么该类必须是抽象类</u>。

- 任何子类必须重写父类的抽象方法，或者声明自身为抽象类。

- 继承抽象方法的子类必须重写该方法。否则，该子类也必须声明为抽象类。最终，必须有子类实现该抽象方法，否则，从最初的父类到最终的子类都不能用来实例化对象。

  如果Salary类继承了Employee类，那么它必须实现computePay()方法：

![image-20231031200540431](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031200540431.png)

- 抽象类总结规定
  - 抽象类不能被实例化(初学者很容易犯的错)，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
  - 抽象类中不一定包含抽象方法，但是<u>有抽象方法的类必定是抽象类</u>。
  - 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。
  -  构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
  - 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。





### Java 封装

- 实现Java封装的步骤

  1.修改属性的可见性来限制对属性的访问（一般限制为private）

​        2.每个值属性提供对外的公共方法访问，也就是创建一对赋取值方法，用于对私有属性的访问  

- 任何要访问类中私有成员变量的类都要通过这些getter和setter方法



### Java 接口

- 是抽象方法的集合，接口通常以interface来声明
- 除非实现接口的类是抽象类，否则该类要定义接口中的所有方法
- 接口无法被实例化，但是可以被实现。一个实现接口的类，必须实现接口内所描述的所有方法，否则就必须声明为抽象类



- 接口与类的区别：
  - 接口不能用于实例化对象。
  - 接口没有构造方法。
  - 接口中所有的方法必须是抽象方法，Java 8 之后 接口中可以使用 default 关键字修饰的非抽象方法。
  - 接口不能包含成员变量，除了 static 和 final 变量。
  - 接口不是被类继承了，而是要被类实现。
  - 接口支持多继承。



- 接口特性
  - 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract**（只能是 public abstract，其他修饰符都会报错）。
  - 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public，用 private 修饰会报编译错误）。
  - 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。



- 抽象类和接口的区别
  -  抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
  -  抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
  -  接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
  -  一个类只能继承一个抽象类，而一个类却可以实现多个接口。
  - ![image-20231031205952097](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031205952097.png)



- 接口的声明

  ![image-20231031210112275](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031210112275.png)

- 接口有以下特性：
  - 接口是隐式抽象的，当声明一个接口的时候，不必使用**abstract**关键字。
  - 接口中每一个方法也是隐式抽象的，声明时同样不需要**abstract**关键字。
  - 接口中的方法都是公有的。



- 接口的实现

  类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。

  类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。

- 接口语法：

  ...implements 接口名称[, 其他接口名称, 其他接口名称..., ...] ...



- 接口的继承

接口的继承使用extends关键字，子接口继承父接口的方法



- 通过使用 `default` 关键字，可以在接口中实现默认方法。

![image-20231031213141075](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231031213141075.png)



- 接口的多继承

在接口的多继承中extends关键字只需要使用一次，在其后跟着继承接口。 如下所示：

public interface Hockey <u>extends</u> Sports, Event



- 标记接口

1. 最常用的继承接口是没有包含任何方法的接口。

2. 标记接口是没有任何方法和属性的接口.它仅仅表明它的类属于一个特定的类型,供其他代码来测试允许做一些事情。

3. 标记接口作用：简单形象的说就是给某个对象打个标（盖个戳），使对象拥有某个或某些特权。

   

   标记接口主要用于以下两种目的：

   - 建立一个公共的父接口：

     正如EventListener接口，这是由几十个其他接口扩展的Java API，你可以使用一个标记接口来建立一组接口的父接口。例如：当一个接口继承了EventListener接口，Java虚拟机(JVM)就知道该接口将要被用于一个事件的代理方案。

   - 向一个类添加数据类型：

     这种情况是标记接口最初的目的，实现标记接口的类不需要定义任何接口方法(因为标记接口根本就没有方法)，但是该类通过多态性变成一个接口类型。


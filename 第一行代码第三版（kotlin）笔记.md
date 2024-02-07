#### 四大组件

Android系统四大组件分别是*Activity、Service、BroadcastReceiver*和*ContentProvider*。

- 其中Activity是所有Android应用程序的门面，凡是在应用中你看得到的东西，都是放在

Activity中的。

- 而Service就比较低调了，你无法看到它，但它会在后台默默地运行，即使用户退出了应用，Service仍然是可以继续运行的。

- BroadcastReceiver允许你的应用接收来自各处的广播消息，比如电话、短信等，当然，你的应用也可以向外发出广播消息。

- ContentProvider则为应用程序之间共享数据提供了可能，比如你想要读取系统通讯录中的联系人，就需要通过ContentProvider来实现

  

##### **Project**模式的项目结构

**AndroidManifest.xml**：程序中定义的所有四大组件都

需要在这个文件里注册，另外还可以在这个文件中给应用程序添加权限声明。（这个文件以后会经常用到）

![image-20240117163722244](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117163722244.png)

这段代码表示对MainActivity进行注册，没有在AndroidManifest.xml里

注册的Activity是不能使用的。其中intent-filter里的两行代码非常重要，<action android:name="android.intent.action.MAIN"/>和<category android:name="android.intent.category.LAUNCHER" />表示MainActivity是这个项目的主Activity，在手机上点击应用图标，首先启动的就是这个Activity.

![image-20240117170858517](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117170858517.png)

应用图标就是通过android:icon属性指定的，

应用的名称则是通过android:label属性指定的。



###### **res**目录下的结构:

所有以“mipmap”开头的目录都是用来放应用图标的，

所有以“values”开头的目录都是用来放字符串、样式、颜色等配置的，

所有以“layout”开头的目录都是用来放布局文件的。

打开res/values/strings.xml文件

##### ![image-20240117170437347](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240117170437347.png)

这里定义了一个应用程序名的字符串，我们有以下两种方式来引用它。

- 在代码中通过R.string.app_name可以获得该字符串的引用。
- 在XML中通过@string/app_name可以获得该字符串的引用。

基本的语法就是上面这两种方式，其中string部分是可以替换的，如果是引用的图片资源就可以替换成drawable，如果是引用的应用图标就可以替换成mipmap，如果是引用的布局文件就可以替换成layout，以此类推。



#### 使用Android的日志工具Log

- 在Android开发中，Log工具是一种常用的调试工具，用于输出程序运行时的日志信息。
- 通过Log，可以在开发阶段方便地追踪代码执行流程、变量值等信息，帮助定位和解决问题。
- 在四大组件中的Activity、Service、BroadcastReceiver、ContentProvider等，都可以使用Log工具记录相关日志。
- Log的使用方法包括：
  - `Log.d(TAG, message)`: 输出调试信息。
  - `Log.i(TAG, message)`: 输出一般信息。
  - `Log.w(TAG, message)`: 输出警告信息。
  - `Log.e(TAG, message)`: 输出错误信息。
- `TAG`一般是一个标签，用于标识日志的来源，方便过滤和查看。
- 在Android开发中，通过Log工具可以更有效地进行调试和监测应用程序的运行状态。



#### 继承与构造函数

##### 继承

- **继承**是面向对象编程的核心概念，允许一个类（子类）继承另一个类（父类）的属性和方法。

- 在Kotlin中使用 `: `关键字实现继承。

- 子类可以访问父类的属性和方法，同时可以重写父类的方法以适应特定需求。

- 示例：

  ```
  // 父类
  open class Animal(val name: String) {
      open fun makeSound() {
          println("Animal makes a sound.")
      }
  }
  
  // 子类继承父类
  class Dog(name: String) : Animal(name) {
      override fun makeSound() {
          println("Dog barks.")
      }
  }
  
  // 创建子类对象
  val myDog = Dog("Buddy")
  myDog.makeSound()  // 输出: Dog barks.
  ```

- `open` 关键字用于标识可被继承的类和方法，子类通过 `override` 关键字重写父类的方法。

##### 构造函数

- **构造函数**是用于创建类实例的特殊方法，负责对象的初始化工作。

- 在Kotlin中，类可以有一个主构造函数和一个或多个次构造函数。

- 主构造函数可以在类头部声明，次构造函数使用 `constructor` 关键字声明。

- 示例：

  ```
  // 类声明主构造函数
  class Person(val name: String, val age: Int) {
      // 次构造函数
      constructor(name: String) : this(name, 0)
  
      fun introduce() {
          println("Hello, my name is $name and I am $age years old.")
      }
  }
  
  // 创建类的实例
  val person1 = Person("Alice", 30)
  val person2 = Person("Bob")
  
  person1.introduce()  // 输出: Hello, my name is Alice and I am 30 years old.
  person2.introduce()  // 输出: Hello, my name is Bob and I am 0 years old.
  ```

- 主构造函数直接在类头部声明属性，次构造函数使用 `this` 关键字调用主构造函数。

- 使用次构造函数可以提供更多的初始化选项，但最终仍然需要调用主构造函数完成对象的初始化。

#### 

#### 2.5.4 数据类与单例类

##### 数据类（Data Class）

- 数据类是Kotlin语言中用于封装数据的特殊类。

- 使用 `data class` 关键字声明，不需要显式实现 toString、equals、hashCode等方法，Kotlin会自动生成。

- 数据类主要用于存储数据，典型应用包括表示实体对象，如用户、商品等。

- 示例：

  ```
  data class Person(val name: String, val age: Int)
  
  // 创建数据类对象
  val person = Person("Alice", 25)
  
  // 自动生成toString方法
  println(person)  // 输出: Person(name=Alice, age=25)
  
  // 自动生成equals方法
  val anotherPerson = Person("Alice", 25)
  println(person == anotherPerson)  // 输出: true
  ```

##### 单例类（Singleton Class）

- 单例类确保一个类只有一个实例，Kotlin中使用 `object` 关键字声明单例类。

- 单例类适用于全局唯一的实例，例如配置管理、资源管理等。

- 示例：

  ```
  object MySingleton {
      fun doSomething() {
          println("Doing something in singleton.")
      }
  }
  
  // 调用单例类的方法
  MySingleton.doSomething()
  ```

- 使用 `object` 声明的类即为该类的单一实例，不需要额外的实例化步骤。

### 2.6 Lambda编程

- Lambda表达式是Kotlin中引入的一项重要特性，用于简化匿名函数的语法。

- Lambda表达式的语法形式为：![image-20240126180025311](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126180025311.png)

- 主要用于函数式编程，可以在集合操作、回调等场景中简化代码。

- 示例：

  ```
  // Lambda表达式作为参数传递给函数
  val list = listOf(1, 2, 3, 4, 5)
  val squaredList = list.map { it * it }
  
  // Lambda表达式作为函数的参数
  fun operateOnNumber(num: Int, operation: (Int) -> Int): Int {
      return operation(num)
  }
  
  val result = operateOnNumber(5) { it * 2 }
  ```

- Lambda表达式可以带有参数，也可以作为参数传递给其他函数。

#### 集合的创建与遍历

- Kotlin专门提供了一个内置的listOf()函数来简化初始化集合的写法，如下所示：

`val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")`



![image-20240126175332682](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175332682.png)

- 这里先使用mutableListOf()函数创建一个可变的集合，然后向集合中

添加了一个新的水果，最后再使用for-in循环对集合进行遍历。

- Set集合的用法几乎与此一模一样，只是将创建集合的方式换成了setOf()和mutableSetOf()函数而已。大致代码如下![image-20240126175446348](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175446348.png)

（需要注意，Set集合中是不可以存放重复元素的，如果存放了多个相同的元素，只会保留其中一份，这是和List集合最大的不同之处。）

- Map集合的用法

  传统的Map用法是先创建一个HashMap的实例，然后将一个个键值对数据添加到Map中。比如这里我们给每种水果设置一个对应的编号，就可以这样写：![image-20240126175626882](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175626882.png)

但更加推荐使用一种类似于数组下标的语法结构，比如向Map中添加一条数据就可以这么写：

![image-20240126175706824](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175706824.png)

Kotlin毫无疑问地提供了一对mapOf()和mutableMapOf()函数来继续简化Map的用法。在mapOf()函数中，我们可以直接传入初始化的键值对组合来完成对Map集合的创建：（to并不是关键字，而是一个infix函数）

![image-20240126175755429](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240126175755429.png)

#### 集合的函数式API

- Kotlin的集合库提供了强大的函数式编程 API，可以用于处理集合数据。
- 函数式编程的优势在于简化代码、提高可读性，并允许更方便地进行链式操作。
- Kotlin中集合的函数式API包括 `map`、`filter`、`reduce` 等常见的函数。

##### map

- `map` 函数用于将集合中的每个元素映射为另一个元素，返回一个新的集合。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 将集合中的每个元素平方
val squaredNumbers = numbers.map { it * it }

// 输出: [1, 4, 9, 16, 25]
println(squaredNumbers)
```

##### filter

- `filter` 函数用于根据指定的条件过滤集合中的元素，返回一个新的集合。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 过滤出偶数
val evenNumbers = numbers.filter { it % 2 == 0 }

// 输出: [2, 4]
println(evenNumbers)
```

##### reduce

- `reduce` 函数用于将集合中的元素进行累加、合并或其他操作，返回一个单一的值。

```
codeval numbers = listOf(1, 2, 3, 4, 5)

// 将集合中的元素累加
val sum = numbers.reduce { acc, num -> acc + num }

// 输出: 15
println(sum)
```

##### forEach

- `forEach` 函数用于遍历集合中的每个元素，并对其执行指定的操作。

```
 codeval numbers = listOf(1, 2, 3, 4, 5)

// 输出每个元素的平方
numbers.forEach { println(it * it) }
```

#### 字符串内嵌表达式

- Kotlin中字符串内嵌表达式的语法规则：![image-20240129230931202](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129230931202.png)

（当表达式中仅有一个变量的时候，还可以将两边的大括号省略）![image-20240129231001120](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129231001120.png)

###### **Activity**状态

- 运行状态
- 暂停状态
- 停止状态
- 销毁状态

#### **Activity**的生存期

- onCreate()。这个方法你已经看到过很多次了，我们在每个Activity

中都重写了这个方法，它会在Activity第一次被创建的时候调用。你应

该在这个方法中完成Activity的初始化操作，比如加载布局、绑定事件

等。

- onStart()。这个方法在Activity由不可见变为可见的时候调用。

- onResume()。这个方法在Activity准备好和用户进行交互的时候调

用。此时的Activity一定位于返回栈的栈顶，并且处于运行状态。

onPause()。这个方法在系统准备去启动或者恢复另一个Activity的

时候调用。我们通常会在这个方法中将一些消耗CPU的资源释放掉，

以及保存一些关键数据，但这个方法的执行速度一定要快，不然会影

响到新的栈顶Activity的使用。

- onStop()。这个方法在Activity完全不可见的时候调用。它和

- onPause()方法的主要区别在于，如果启动的新Activity是一个对话

框式的Activity，那么onPause()方法会得到执行，而onStop()方

法并不会执行。

- onDestroy()。这个方法在Activity被销毁之前调用，之后Activity

的状态将变为销毁状态。

- onRestart()。这个方法在Activity由停止状态变为运行状态之前调

用，也就是Activity被重新启动了。

##### 标准函数**with**、**run**和**apply**

with函数会在Lambda表达式中提供第一个参数对象的上下文，并使用Lambda表达式中的最后一行代码作为返回值返回。示例代码如下![image-20240129232631537](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232631537.png)

run：

![image-20240129232808241](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232808241.png)

apply：

![image-20240129232834682](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240129232834682.png)

#### 常用控件

- TextView（文本视图）

- Button

- EditText（文本输入框）

  通过android:maxLines指定了EditText的最大行数(当输入的内容超过两行时，文本就会向上滚动，EditText则不会再继续拉伸)

- **ImageView**

- ProgressBar（进度条）

可以通过android:visibility进行指定，可选值有3种：visible、invisible和gone。

1.visible表示控件是可见的，这个值是默认值，不指定android:visibility时，控件都是可见的。

2.invisible表示控件不可见，但是它仍然占据着原来的位置和大小，可以理解成控件变成透明状态了

3.gone则表示控件不仅不可见，而且]不再占用任何屏幕空间。

![image-20240206103217505](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206103217505.png)

通过style属性可以将它指定成水平进度条

android:max属性给进度条设置一个最大值

- **AlertDialog**

![image-20240206103340999](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206103340999.png)



#### 基本布局

- **LinearLayout**（线性布局）

- **RelativeLayout（相对布局）**

  android:layout_alignParentLeft、

  android:layout_alignLeft表示让一个控件的左边缘和另一个控件的

  左边缘对齐

- **FrameLayout**（帧布局）

- 引入布局![image-20240206104712906](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206104712906.png)

#### **ListView**

1.在 XML 布局文件中添加 `ListView` 控件![image-20240206105300031](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206105300031.png)

2.创建数据源

一般情况下，我们需要通过数组或集合等数据结构来存储要显示的数据。这里我们创建一个字符串数组作为数据源，如：

```
kotlinCopy Codeval data = listOf("Apple", "Banana", "Cherry", "Durian", "Grape", "Honeydew")
```

3.创建适配器

适配器（Adapter）负责将数据源中的数据与视图绑定起来，并在 `ListView` 中进行显示。Android 框架提供了多个内置的适配器类，如 `ArrayAdapter`、`SimpleAdapter` 等，也可以自定义适配器。这里我们使用 `ArrayAdapter` 来实现一个简单的适配器，代码如下：

```
val adapter = ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, data)
```

其中，第一个参数 `this` 表示上下文对象，第二个参数 `android.R.layout.simple_list_item_1` 是一个内置的布局文件，用于显示一行简单的文本内容，第三个参数是数据源。

4.设置适配器

将创建好的适配器设置到 `ListView` 中，代码如下：

```
val listView: ListView = findViewById(R.id.list_view)
listView.adapter = adapter
```

这样，`ListView` 就已经可以正确地显示数据了。我们也可以对适配器进行更多的设置，如设置自定义布局、添加点击事件等。

5.添加点击事件

为了让用户能够与列表中的项进行交互，我们需要为 `ListView` 中的每一项添加点击事件。可以通过 `setOnItemClickListener` 方法来实现，代码如下：

```
listView.setOnItemClickListener { parent, view, position, id ->
    val item = adapter.getItem(position)
    Toast.makeText(this, item, Toast.LENGTH_SHORT).show()
}
```

#### **RecyclerView**

![image-20240206110812527](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206110812527.png)

为RecyclerView准备一个适配器，新建FruitAdapter类，让这个适配器继承自RecyclerView.Adapter，并将泛型指定FruitAdapter.ViewHolder。其中，ViewHolder是我们在FruitAdapter中定义的一个内部类，代码如下所示：

![image-20240206110912615](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206110912615.png)

适配器准备好了之后，我们就可以开始使用RecyclerView了，修改

MainActivity中的代码，如下所示：![image-20240206111028341](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111028341.png)

![image-20240206111038222](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111038222.png)

使用了一个同样的initFruits()方法，用于初始化所有的水果数据。接着在onCreate()方法中先创建了一个LinearLayoutManager对象，并将它设置到RecyclerView当中。LayoutManager用于指定RecyclerView的布局方式，这里使用的LinearLayoutManager是线性布局的意思，可以实现和ListView类似的效果。接下来我们创建了FruitAdapter的实例，并将水果数据传入FruitAdapter的构造函数中，最后调RecyclerViewsetAdapter()方法来完成适配器设置，这样RecyclerView和数据之间的关联就建立完成了。

- 实现横向滚动和瀑布流布局![image-20240206111312897](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111312897.png)

![image-20240206111346259](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111346259.png)

- 实现一下效果更加炫酷的瀑布流布局

  首先还是来修改一下fruit_item.xml中的代码，如下所示：

![image-20240206111550343](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111550343.png)

这里做了几处小的调整，首先将LinearLayout的宽度由80 dp改成了match_parent，因为瀑布流布局的宽度应该是根据布局的列数来自动适配的，而不是一个固定值。其次我们使用了layout_margin属性来让子项之间互留一点间距，这样就不至于所有子项都紧贴在一些。最后还将TextView的对齐属性改成了居左对齐，因为待会我们会将文字的长度变长，如果还是居中显示就会感觉怪怪的

接着修改MainActivity中的代码，如下所示：![image-20240206111806309](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111806309.png)

![image-20240206111817838](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206111817838.png)

这里我们把眼光聚焦到getRandomLengthString()这个方法上，这个方法中调用了Range对象的random()函数来创造一个1到20之间的随机数，然后将参数中传入的字符串随机重复几遍。在initFruits()方法中，每个水果的名字都改成调用getRandomLengthString()这个方法来生成，这样就能保证各水果名字的长短差距比较大，子项的高度也就各不相同了。



#### 延迟初始化和密封类

##### 对变量延迟初始化

1.  在Kotlin中，我们可以使用`lateinit`关键字来标记一个变量，表示该变量将会在稍后的某个时刻进行初始化。被`lateinit`修饰的变量必须是非空类型，并且不能是原生类型（如Int、Boolean等）。

   ```kotlin
   lateinit var name: String
   ```

   在上面的例子中，我们声明了一个延迟初始化的字符串变量`name`。

2. 延迟初始化的使用限制： 延迟初始化的变量有一些使用限制，需要注意：

   - 只能用于可变变量（var），不能用于只读变量（val）。
   - 延迟初始化的变量不能有自定义的setter和getter。
   - 在使用延迟初始化变量之前，必须进行初始化，否则会抛出`UninitializedPropertyAccessException`异常。

##### 使用密封类优化代码

密封类的关键字是sealed class，它的用法同样非常简单，我们可以轻

松地将Result接口改造成密封类的写法：

![image-20240206114558828](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206114558828.png)



![image-20240206114819072](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206114819072.png)

![image-20240206114834831](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206114834831.png)

getResultMsg()方法中的else条件已经不再需要了。这是因为当在when语句中传入一个密封类变量作为条件时，Kotlin编译器会自动检查该密封类有哪些子类，并强制要求你将每一个子类所对应的条件全部处理。这样就可以保证，即使没有编写else条件，也不可能会出现漏写条件分支的情况。

#### **Fragment**

1.新建fragment

![image-20240206115713211](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206115713211.png)

代码文件：

![image-20240206115652222](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206115652222.png)

2.编写主布局文件![image-20240206115822944](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206115822944.png)

![image-20240206115833289](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206115833289.png)

- 动态添加到Activity当中

修改activity_main.xml，代码如下所示：

![image-20240206120020850](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120020850.png)

在代码中向FrameLayout里添加内容，从而实现动态添加

Fragment的功能。修改MainActivity中的代码，如下所示：![image-20240206120058366](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120058366.png)

![image-20240206120106887](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120106887.png)

动态添加Fragment主要分为5步:

(1) 创建待添加Fragment的实例。

(2) 获取FragmentManager，在Activity中可以直接调用

getSupportFragmentManager()方法获取。

(3) 开启一个事务，通过调用beginTransaction()方法开启。

(4) 向容器内添加或替换Fragment，一般使用replace()方法实现，需

要传入容器的id和待添加的Fragment实例。

(5) 提交事务，调用commit()方法来完成

##### 在**Fragment**中实现返回栈

FragmentTransaction中提供了一个addToBackStack()方法，可以用于将一个事务添加到返回栈中.修改MainActivity中的代

码，如下所示：![image-20240206120408746](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120408746.png)

![image-20240206120419423](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120419423.png)

![image-20240206120435175](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120435175.png)

##### **Fragment**和**Activity**之间的交互

1.

![image-20240206120551286](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120551286.png)

![image-20240206120559863](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120559863.png)

类似于findViewById()方法，kotlin-android-extensions插件也对findFragmentById()方法进行了扩展，允许我们直接使用布局文件中定义的Fragment id名称来自动获取相应的Fragment实例，如下所示：(推荐使用)

![image-20240206120628151](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120628151.png)

2.在每个Fragment中都可以通过调用getActivity()方法来得到和当前Fragment相关联的Activity实例，代码如下所示：

![image-20240206120836889](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120836889.png)

##### **Fragment**的状态和回调

1. 运行状态

当一个Fragment所关联的Activity正处于运行状态时，该Fragment

也处于运行状态。

2. 暂停状态

当一个Activity进入暂停状态时（由于另一个未占满屏幕的Activity被

添加到了栈顶），与它相关联的Fragment就会进入暂停状态。

3. 停止状态

当一个Activity进入停止状态时，与它相关联的Fragment就会进入停

止状态，或者通过调用FragmentTransaction的remove()、

replace()方法将Fragment从Activity中移除，但在事务提交之前

调用了addToBackStack()方法，这时的Fragment也会进入停止状

态。总的来说，进入停止状态的Fragment对用户来说是完全不可见

的，有可能会被系统回收。

4. 销毁状态Fragment总是依附于Activity而存在，因此当Activity被销毁时，与

它相关联的Fragment就会进入销毁状态。或者通过调用

FragmentTransaction的remove()、replace()方法将Fragment

从Activity中移除，但在事务提交之前并没有调用

addToBackStack()方法，这时的Fragment也会进入销毁状态。

![image-20240206120949497](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206120949497.png)

![image-20240206121027784](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206121027784.png)

#### 

##### 大有用途的扩展函数

- 扩展函数表示即使在不修改某个类的源码的情况下，仍然可以打开这个类，向该类添加新的函数。

- 当我们需要统计某个字符串中的字母数量时，只需要编写如下代码

即可：

![image-20240206124835683](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206124835683.png)

- 定义扩展函数的语法结构如下所示：![image-20240206124922056](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206124922056.png)

相比于定义一个普通的函数，定义扩展函数只需要在函数名的前面加上一

个ClassName.的语法结构，就表示将该函数添加到指定类当中了。

- **![image-20240206125953855](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206125953855.png)**

![image-20240206130004128](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206130004128.png)

![image-20240206130018601](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206130018601.png)

##### 有趣的运算符重载

- 运算符重载使用的是operator关键字，只要在指定函数的前面加上operator关键字，就可以实现运算符重载的功能了。

![image-20240206130154208](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206130154208.png)

![image-20240206130207541](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206130207541.png)

语法糖表达式和实际调用函数对照表

![image-20240206130248529](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206130248529.png)

##### 广播机制简介

- Android中的广播主要可以分为两种类型：标准广播和有序

  广播。

- 标准广播（normal broadcasts）是一种完全异步执行的广播，在广

  播发出之后，所有的BroadcastReceiver几乎会在同一时刻收到这条

  广播消息，因此它们之间没有任何先后顺序可言。这种广播的效率会

  比较高，但同时也意味着它是无法被截断的。

![image-20240206160534040](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206160534040.png)

- 有序广播（ordered broadcasts）则是一种同步执行的广播，在广播

  发出之后，同一时刻只会有一个BroadcastReceiver能够收到这条广

  播消息，当这个BroadcastReceiver中的逻辑执行完毕后，广播才会

  继续传递。所以此时的BroadcastReceiver是有先后顺序的，优先级

  高的BroadcastReceiver就可以先收到广播消息，并且前面的BroadcastReceiver还可以截断正在传递的广播，这样后面的

  BroadcastReceiver就无法收到广播消息了。

![image-20240206160602273](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206160602273.png)



##### 接收系统广播

###### 动态注册监听时间变化

- 创建一个BroadcastReceiver：
- 新建一个类，让它继承自BroadcastReceiver，并重写父类的onReceive()方法就行了。这样当有广播到来时，onReceive()方法就会得到执行，具体的逻辑就可以在这个方法中处理。![image-20240206160919606](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206160919606.png)

![image-20240206160928837](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206160928837.png)

###### 静态注册实现开机启动

###### （让程序在未启动的情况下也能接收广播）

右击com.example.broadcasttest包→New→Other→Broadcast

Receiver，会弹出如图6.4所示的窗口。

![image-20240206161417982](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161417982.png)

修改BootCompleteReceiver中的代码，如下所示：![image-20240206161344220](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161344220.png)

对AndroidManifest.xml文件进行修改才行，如下所示：![image-20240206161439057](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161439057.png)



##### 发送自定义广播

###### 发送标准广播

- 在发送广播之前，我们还是需要先定义一个BroadcastReceiver来准备接收此广播，因此新建一个MyBroadcastReceiver，并在onReceive()方法中加入如下代码：![image-20240206161849783](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161849783.png)

- 然后在AndroidManifest.xml中对这个BroadcastReceiver进行修改![image-20240206161925599](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161925599.png)

![image-20240206161934674](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206161934674.png)

- 接下来修改activity_main.xml中的代码，如下所示：![image-20240206162003818](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162003818.png)

- 这里在布局文件中定义了一个按钮，用于作为发送广播的触发点。然后修改MainActivity中的代码，如下所示：![image-20240206162036573](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162036573.png)

###### 发送有序广播

- 和标准广播不同，有序广播是一种同步执行的广播，并且是可以被截断的。

- 重新回到BroadcastTest项目，然后修改MainActivity中的代

  码，如下所示：![image-20240206162314194](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162314194.png)

![image-20240206162320313](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162320313.png)

可以看到，发送有序广播只需要改动一行代码，即将sendBroadcast()

方法改成sendOrderedBroadcast()方法。

- 该如何设定BroadcastReceiver的先后顺序呢？当然是在注册的时候进行设定了，修改AndroidManifest.xml中的代码，如下所示：![image-20240206162421608](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162421608.png)

![image-20240206162427889](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162427889.png)

![image-20240206162448731](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162448731.png)

- 已经获得了接收广播的优先权，那么MyBroadcastReceiver就可以选

  择是否允许广播继续传递了。修改MyBroadcastReceiver中的代码如下所示

![image-20240206162532302](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206162532302.png)

如果在onReceive()方法中调用了abortBroadcast()方法，就表示将

这条广播截断，后面的BroadcastReceiver将无法再接收到这条广播。

#### **Kotlin**课堂：高阶函数详解

###### 定义高阶函数

- 定义：如果一个函数接收另一个函数作为参数，或者返回值的类型是另一个函数，那么该函数就称为高阶函数。

- 不同于定义一个普通的字段类型，函数类型的语法规则是有点特殊的，基本规则如下：

![image-20240206163008481](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163008481.png)

- 既然是定义一个函数类型，那么最关键的就是要声明该函数接收什么参数，以及它的返回值是什么。因此，->左边的部分就是用来声明该函数接收什么参数的，多个参数之间使用逗号隔开，如果不接收任何参数，写一对空括号就可以了。而->右边的部分用于声明该函数的返回值是什么类型，如果没有返回值就使用Unit，它大致相当于Java中的void。现在将上述函数类型添加到某个函数的参数声明或者返回值声明上，那么这个函数就是一个高阶函数了，如下所示：

![image-20240206163045662](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163045662.png)

这里的example()函数接收了一个函数类型的参数，因此example()函数就是一个高阶函数。而调用一个函数类型的参数，它的语法类似于调用一个普通的函数，只需要在参数名的后面加上一对括号，并在括号中传入必要的参数即可。

###### 内联函数的作用

- 内联函数的用法非常简单，只需要在定义高阶函数时加上inline关键字的声明即可，如下所示：

![image-20240206163232730](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163232730.png)

- 下面通过图例的方式来详细说明内联函数的代码替换过程。

![image-20240206163405994](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163405994.png)

![image-20240206163426801](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163426801.png)

- **noinline**与**crossinline**

如果我们只想内联其中的一个Lambda表达式该怎么办呢？这时就

可以使用noinline关键字了，如下所示：![image-20240206163526324](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240206163526324.png)

##### 文件存储

- 比较适合存储一些简单的文本数据或二进制数据

  

  ###### 将数据存储到**SharedPreferences**中

- Context类中提供了一个`openFileOutput()`方法，可以用于将数据存储到指定的文件中。

- 如何在Android项目中使用文件存储的技术，

  首先创建一个FilePersistenceTest项目，并修改activity_main.xml中的代码，如下所示：

![image-20240207111323734](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207111323734.png)

这里只是在布局中加入了一个EditText，用于输入文本内容。

修改MainActivity中的代码，如下所示：![image-20240207111353380](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207111353380.png)

- Context类中还提供了一个`openFileInput()`方法，用于从文件中读取数据。

- 以下是一段简单的代码示例，展示了如何从文件中读取文本数据：![image-20240207114654609](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207114654609.png)

##### **SharedPreferences**存储

- Android中主要提供了以下两种方法用于得到SharedPreferences对象：

1. **Context**类中的**getSharedPreferences()**方法
2. **Activity**类中的**getPreferences()**方法

- 得到了SharedPreferences对象之后，就可以开始向

  SharedPreferences文件中存储数据了，主要可以分为3步实现：

  (1) 调用SharedPreferences对象的edit()方法获取一个

  SharedPreferences.Editor对象。

  (2) 向SharedPreferences.Editor对象中添加数据，比如添加一

  个布尔型数据就使用putBoolean()方法，添加一个字符串则使用

  putString()方法，以此类推。

  (3) 调用apply()方法将添加的数据提交，从而完成数据存储操作。

- SharedPreferences存储的用法：

  修改activity_main.xml中的代码，如下所示：![image-20240207115313797](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207115313797.png)

修改MainActivity中的代码，如下所示：

![image-20240207115335595](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207115335595.png)

![image-20240207115344154](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207115344154.png)



###### 从**SharedPreferences**中读取数据

- 通过例子来实际体验一下，还是在上面的项目上

  修改activity_main.xml中的代码，如下所示：![image-20240207115815593](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207115815593.png)

这里增加了一个还原数据的按钮，我们希望通过点击这个按钮来从

SharedPreferences文件中读取数据。修改MainActivity中的代码，如下

所示：![image-20240207115838766](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207115838766.png)



##### **SQLite**数据库存储

###### 创建数据库

- SQLiteOpenHelper帮助类，借助这个类可以非常简单地对数据库进行创建和升级。
- SQLiteOpenHelper是一个抽象类，这意味着如果我们想要使用它，就需要创建一个自己的帮助类去继承它。SQLiteOpenHelper中有两个抽象方法：onCreate()和onUpgrade()。

- SQLiteOpenHelper中还有两个非常重要的实例方法：

  getReadableDatabase()和getWritableDatabase()。这两个方法都可以创建或打开一个现有的数据库（如果数据库已存在则直接打开，否

  则要创建一个新的数据库），并返回一个可对数据库进行读写操作的对象。不同的是，当数据库不可写入的时候（如磁盘空间已满），getReadableDatabase()方法返回的对象将以只读的方式打开数据库，而getWritableDatabase()方法则将出现异常。

- 具体的例子：

  创建一个名为BookStore.db的数据库，然后在这个数据库中新建一张Book表，表中有id（主键）、作者、价格、页数和书名等列。Book表的建表语句如下所示：![image-20240207120921855](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207120921855.png)

新建MyDatabaseHelper类继承自SQLiteOpenHelper，代码如下所示：

![image-20240207120947260](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207120947260.png)

修改activity_main.xml中的代码，如下所示：

![image-20240207121003443](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207121003443.png)

加入了一个按钮，用于创建数据库

修改MainActivity中的代码，如下所示：![image-20240207121047781](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207121047781.png)



###### 升级数据库

- MyDatabaseHelper中onUpgrade()方法是用于对数据库进行升级的

- 添加一张Category表用于记录图书的分类，Category表中有id（主键）、分类名和分类代码这几个列，那么建表语句就可以写成：

![image-20240207121621951](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207121621951.png)

将这条建表语句添加到MyDatabaseHelper中，代码如下所

示：![image-20240207121641142](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207121641142.png)

现在我们重新运行一下程序，并点击“Create

Database”按钮，没有弹出创建成功的提示。原因：因为此时BookStore.db数据库已经存在了，之后不管我们怎样点击“Create Database”按钮，MyDatabaseHelper中的onCreate()方法都不会再次执行，因此新添加的表也就无法得到创建了。

*解决这个问题的办法也相当简单，只需要先将程序卸载，然后重新运行*（极端）

- 其实我们只需要巧妙地运用SQLiteOpenHelper的升级功能，就可以很轻松地解决这个问题。修改MyDatabaseHelper中的代码，如下所示：

![image-20240207122122469](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207122122469.png)

我们在onUpgrade()方法中执行了两条DROP语句，如果发现

数据库中已经存在Book表或Category表，就将这两张表删除，然后调用

onCreate()方法重新创建。这里先将已经存在的表删除，是因为如果在

创建表时发现这张表已经存在了，就会直接报错

修改MainActivity中的代码，如下所示：

![image-20240207122249153](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207122249153.png)

之前我们传入的是1，现在只要传入一个比1大的数，就可以

让onUpgrade()方法得到执行了。



###### 添加数据

- SQLiteDatabase中提供了一个`insert()`方法，专门用于添加数据。它接收3个参数：第一个参数是表名，我们希望向哪张表里添加数据，这里就传入该表的名字；第二个参数用于在未指定添加数据的情况下给某些可为空的列自动赋值NULL，一般我们用不到这个功能，直接传入null即可；第三个参数是一个ContentValues对象，它提供了一系列的put()方法重载，用于向ContentValues中添加数据，只需要将表中的每个列名以及相应的待添加数据传入即可

- 修改activity_main.xml中的代码，如下所示：![image-20240207122549953](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207122549953.png)

新增了一个按钮，稍后就会在这个按钮的点击事件里编写添加数据的逻辑。

修改MainActivity中的代码，如下所示：

![image-20240207122609616](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207122609616.png)



###### 更新数据

- SQLiteDatabase中提供了一个非常好用的update()方法，用于对数据进行更新。这个方法接收4个参数：第一个参数和insert()方法一样，也是表名，指定更新哪张表里的数据；第二个参数ContentValues对象，要把更新数据在这里组装进去；第三、第四个参数用于约束更新某一行或某几行中的数据，不指定的话默认会更新所有行。

- 修改activity_main.xml中的代码，如下所示：

![image-20240207123005207](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123005207.png)

添加了一个用于更新数据的按钮。然后修改MainActivity中的代码，如下所示：![image-20240207123023120](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123023120.png)

![image-20240207123033370](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123033370.png)



###### 删除数据

- SQLiteDatabase中提供了一个delete()方法，专门用于删除数据。这个方法接收3个参数：第一个参数仍然是表名，这个没什么好说的；第二、第三个参数用于约束删除某一行或某几行的数据，不指定的话默认会删除所有行。

- 修改activity_main.xml中的代码，如下所示：

![image-20240207123210905](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123210905.png)

添加了一个按钮，用于删除数据。然后修改MainActivity中的代码，如下所示：

![image-20240207123224836](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123224836.png)



###### 查询数据

- SQLiteDatabase中还提供了一个query()方法用于对数据进行查询。这个方法的参数非常复杂，最短的一个方法重载也需要传入7个参数。那我们就先来看一下这7个参数各自的含义吧。第一个参数不用说，当然还是表名，表示我们希望从哪张表中查询数据。第二个参用于指定去查询哪几列，如果不指定则默认查询所有列。第三、第四个参数用于约束查询某一行或某几行的数据，不指定则默认查询所有行的数据。第五个参数用于指定需要去group by的列，不指定则表示不对查询结果进行group by操作。第六个参数用于对group by之后的数据进行进一步的过滤，不指定则表示不进行过滤。第七个参数用于指定查询结果的排序方式，不指定则表示使用默认的排序方式。

- **query()**方法参数的详细解释

![image-20240207123343226](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123343226.png)

![image-20240207123351577](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123351577.png)

- 修改activity_main.xml中的代码，如下所示：

![image-20240207123416050](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123416050.png)

![image-20240207123421652](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123421652.png)

添加了一个按钮用于查询数据。然后修改MainActivity中的代码，如下所示：

![image-20240207123440638](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123440638.png)



###### 使用**SQL**操作数据库

- 直接使用SQL来完成前面几个小节中学过的CRUD操作。

添加数据：![image-20240207123537415](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123537415.png)

更新数据：

![image-20240207123548988](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123548988.png)

删除数据：

![image-20240207123603965](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123603965.png)

查询数据：

![image-20240207123614577](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123614577.png)

以上演示的几种方式的执行结果会和前面我们学习的CRUD操作的结果完全相同，选择使用哪一种方式就看你个人的喜好了。



###### 升级数据库的最佳写法

- 模拟一个数据库升级的案例，还是由MyDatabaseHelper类对数据库进行管理。第1版的程序要求非常简单，只需要创建一张Book表。MyDatabaseHelper中的代码如下所示：

![image-20240207123932866](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123932866.png)

![image-20240207123940484](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207123940484.png)

需要向数据库中再添加一张Category表。于是，修改MyDatabaseHelper中的代码，如下所示：

![image-20240207124013492](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124013492.png)

在onCreate()方法里我们新增了一条建表语句，然后又在onUpgrade()方法中添加了一个if判断，如果用户数据库的旧版本号小于等于1，就只会创建一张Category表。

没过多久，新的需求又来了，这次要给Book表和Category表之间建立关联，需要在Book表中添加一个category_id字段。再次修改MyDatabaseHelper中的代码，如下所示：

![image-20240207124104422](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124104422.png)

![image-20240207124110816](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124110816.png)

这里请注意一个非常重要的细节：每当升级一个数据库版本的时候，onUpgrade()方法里都一定要写一个相应的if判断语句。为什么要这么做呢？这是为了保证App在跨版本升级的时候，每一次的数据库修改都能被全部执行。比如用户当前是从第2版升级到第3版，那么只有第二条判断语句会执行，而如果用户是直接从第1版升级到第3版，那么两条判断语句都会执行。使用这种方式来维护数据库的升级，不管版本怎样更新，都可以保证数据库的表结构是最新的，而且表中的数据完全不会丢失。





#### **Kotlin**课堂：高阶函数的应用

###### 简化**SharedPreferences**的用法

- 使用高阶函数简化SharedPreferences的用法，新建一个SharedPreferences.kt文件，然后在里面加入如下代码：

![image-20240207124307067](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124307067.png)

定义好了open函数之后，我们以后在项目中使用SharedPreferences存储数据就会更加方便了，写法如下所示：

![image-20240207124338824](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124338824.png)

- 我们实际上可以直接在项目中使用如下写法来向

  SharedPreferences存储数据：

![image-20240207124434760](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124434760.png)

其实就是将open函数换成了edit函数，但是edit函数的语义性明显要更好一些。当然，我前面命名成open函数，主要是为了防止和KTX的edit函数同名，以免你在理解的时候产生混淆。



###### 简化**ContentValues**的用法

- ContentValues的基本用法在7.4节中已经学过了，它主要用于结合SQLiteDatabase的API存储和修改数据库中的数据，具体的用法示例如下：

![image-20240207124532096](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124532096.png)

- 新建一个ContentValues.kt文件，然后在里面定义一个cvOf()方法，如下所示：

![image-20240207124551740](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124551740.png)

首先，cvOf()方法接收了一个Pair参数，也就是使用A to B语法结构创建出来的参数类型，但是我们在参数前面加上了一个vararg关键字，这是什么意思呢？其实vararg对应的就是Java中的可变参数列表，我们允许向这个方法传入0个、1个、2个甚至任意多个Pair类型的参数，这些参数都会被赋值到使用vararg声明的这一个变量上面，然后使用for-in循环可以将传入的所有参数遍历出来。

接下来我们开始为cvOf()方法实现功能逻辑，核心思路就是先创建一个ContentValues对象，然后遍历pairs参数列表，取出其中的数据并填入ContentValues中，最终将ContentValues对象返回即可。思路并不复杂，但是存在一个问题：Pair参数的值是Any?类型的，我们怎样让它和ContentValues所支持的数据类型对应起来呢？这个确实没有什么好的办法，只能使用when语句一一进行条件判断，并覆盖ContentValues所支持的所有数据类型。结合下面的代码来理解应该更加清楚一些：

![image-20240207124733312](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124733312.png)

- 有了这个cvOf()方法之后，我们使用ContentValues时就会变得更加简单了，比如向数据库中插入一条数据就可以这样写：

![image-20240207124841936](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124841936.png)

- 从功能性方面，cvOf()方法好像确实用不到高阶函数的知识，但是从代码实现方面，却可以结合高阶函数来进行进一步的优化。比如借助apply函数，cvOf()方法的实现将会变得更加优雅：

![image-20240207124920148](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124920148.png)

![image-20240207124925947](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124925947.png)

- KTX库中也提供了一个具有同样功能的contentValuesOf()方法，

  用法如下所示：![image-20240207124944891](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207124944891.png)

平时我们在编写代码的时候，直接使用KTX提供的contentValuesOf()

方法就可以了





#### **ContentProvider**

###### **ContentProvider**简介

- ContentProvider主要用于在不同的应用程序之间实现数据共享的功能，它提供了一套完整的机制，允许一个程序访问另一个程序中的数据，同时还能保证被访问数据的安全性。

- ContentProvider可以选择只对哪一部分数据进行共享，从而保证我

  们程序中的隐私数据不会有泄漏的风险

  

###### 运行时权限

到**Android 10**系统为止所有的危险权限

![image-20240207125733337](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207125733337.png)

![image-20240207125751174](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207125751174.png)



###### 在程序运行时申请权限

- 其实表8.1中列出的所有权限都是可以申请的，这里简单起见，我们就使用CALL_PHONE这个权限来作为本小节的示例吧。CALL_PHONE这个权限是编写拨打电话功能的时候需要声明的，因为拨打电话会涉及用户手机的资费问题，因而被列为了危险权限。在Android 6.0系统出现之前，拨打电话功能的实现其实非常简单，修改activity_main.xml布局文件，如下所示：![image-20240207130108744](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130108744.png)

我们在布局文件中只是定义了一个按钮，点击按钮就去触发拨打电话的逻辑。接着修改MainActivity中的代码，如下所示：	

![image-20240207130147895](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130147895.png)

![image-20240207130156626](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130156626.png)

在按钮的点击事件中，我们构建了一个隐式Intent，Intent的action指定为Intent.ACTION_CALL，这是一个系统内置的打电话的动作，然后在data部分指定了协议是tel，号码是10086。

接下来修改AndroidManifest.xml文件，在其中声明如下权限：![image-20240207130328244](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130328244.png)

由于权限被禁止，运行会报错，因为Android 6.0及以上系统在使用危险权限时必须进行运行时权限处理。

尝试修复这个问题，修改MainActivity中的代码，如下所示：

![image-20240207130647472](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130647472.png)

![image-20240207130700824](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207130700824.png)





###### **ContentResolver**的基本用法

- 如果想要访问ContentProvider中共享的数据，就一定要借助ContentResolver类，可以通过Context中的getContentResolver()方法获取该类的实例。ContentResolver中提供了一系列的方法用于对数据进行增删改查操作，其中insert()方法用于添加数据，update()方法用于更新数据，delete()方法用于删除数据，query()方法用于查询数据。SQLiteDatabase中也是使用这几个方法进行增删改查操作的，只不过它们在方法参数上稍微有一些区别。
- 不同于SQLiteDatabase，ContentResolver中的增删改查方法都是不接收表名参数的，而是使用一个Uri参数代替，这个参数被称为内容URI。内容URI最标准的格式如下：

![image-20240207132357305](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132357305.png)

在得到了内容URI字符串之后，我们还需要将它解析成Uri对象才可以作为

参数传入。解析的方法也相当简单，代码如下所示：![image-20240207132436135](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132436135.png)

只需要调用Uri.parse()方法，就可以将内容URI字符串解析成Uri对象了。现在我们就可以使用这个Uri对象查询table1表中的数据了，代码如下所示：![image-20240207132458007](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132458007.png)

表**8.2** **query()**方法的参数说明

![image-20240207132729391](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132729391.png)

查询完成后返回的仍然是一个Cursor对象，这时我们就可以将数据从

Cursor对象中逐个读取出来了。读取的思路仍然是通过移动游标的位置遍

历Cursor的所有行，然后取出每一行中相应列的数据，代码如下所示：

![image-20240207132749125](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132749125.png)

- 如何向table1表中添加一条数据，代码如下所示：

![image-20240207132815078](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132815078.png)

如果我们想要更新这条新添加的数据，把column1的值清空，可以借助

ContentResolver的update()方法实现，代码如下所示：

![image-20240207132850745](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132850745.png)

可以调用ContentResolver的delete()方法将这条数据删除掉，

代码如下所示：![image-20240207132915532](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207132915532.png)



###### 读取系统联系人

- 修改activity_main.xml中的代码，如下所示：

![image-20240207133101641](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133101641.png)

![image-20240207133109262](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133109262.png)

修改MainActivity中的代码，如下所示：![image-20240207133140400](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133140400.png)

![image-20240207133201586](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133201586.png)

读取系统联系人的权限千万不能忘记声明。修改AndroidManifest.xml中的代码，如下所示：![image-20240207133306365](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133306365.png)



###### 创建**ContentProvider**的步骤

- 通过新建一个类去继承ContentProvider的方式来实现ContentProvider类中有6个抽象方法，我们在使用子类继承它的时候，需要将这6个方法全部重写。

![image-20240207134034884](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134034884.png)

![image-20240207134042148](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134042148.png)

修改MyProvider中的代码，如下所示：

- ![image-20240207133937806](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207133937806.png)



完善MyProvider中的内容了，这次来实现getType()方法中的逻辑，代码如下所示：![image-20240207134429487](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134429487.png)

![image-20240207134435442](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134435442.png)



###### 实现跨程序数据共享

在上一章中DatabaseTest项目的基础上继续开发

- 右击com.example.databasetest包→New→Other→Content Provider，会弹出如图8.13所示的窗口。

- ![image-20240207134843659](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134843659.png)

修改DatabaseProvider中的代码，如下所示：![image-20240207134956892](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207134956892.png)

![image-20240207135020359](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135020359.png)

![image-20240207135050223](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135050223.png)

![image-20240207135110551](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135110551.png)

我们是使用Android Studio的快捷方式创建的ContentProvider，因此注册这一步已经自动完成了。打开AndroidManifest.xml文件瞧一瞧，代码如下所示：![image-20240207135329660](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135329660.png)

首先需要将DatabaseTest程序从模拟器中删除，以防止上一章中产生的遗留数据对我们造成干扰。然后运行一下项目，将DatabaseTest程序重新安装在模拟器上。接着关闭DatabaseTest这个项目，并创建一个新项目ProviderTest，我们将通过这个程序去访问DatabaseTest中的数据。

修改activity_main.xml中的代码，如下所示：![image-20240207135416060](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135416060.png)

然后修改MainActivity中的代码，如下所示：![image-20240207135430583](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135430583.png)

![image-20240207135443873](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135443873.png)





#### **Kotlin**课堂：泛型和委托

###### 泛型的基本用法

- 在一般的编程模式下，我们需要给任何一个变量指定一个具体的类型，而泛型允许我们在不指定具体类型的情况下进行编程，这样编写出来的代码将会拥有更好的扩展性。
- 举个例子，List是一个可以存放数据的列表，但是List并没有限制我们只能存放整型数据或字符串数据，因为它没有指定一个具体的类型，而是使用泛型来实现的。也正是如此，我们才可以使用List<Int>、List<String>之类的语法来构建具体类型的列表
- 泛型主要有两种定义方式：一种是定义泛型类，另一种是定义泛型方法，使用的语法结构都是<T>。
- 如果我们要定义一个泛型类，就可以这么写：![image-20240207135810807](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135810807.png)

我们在调用MyClass类和method()方法的时候，就可以将泛型指定成具

体的类型，如下所示：![image-20240207135825989](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135825989.png)

- 而如果我们不想定义一个泛型类，只是想定义一个泛型方法，应该要怎么写呢？也很简单，只需要将定义泛型的语法结构写在方法上面就可以了，如下所示：![image-20240207135849437](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207135849437.png)

- 接下来，我们尝试对本小节所学的泛型知识进行应用。回想一下，在6.5.1小节学习高阶函数的时候，我们编写了一个build函数，代码如下所示：![image-20240207140035780](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140035780.png)

现在我们就通过本小节所学的泛型知识对build函数进行扩展，让它实现和apply函数完全一样的功能。只需要使用<T>将build函数定义成泛型函数，再将原来所有强制指定StringBuilder的地方都替换成T就可以了。新建一个build.kt文件，并编写如下代码：![image-20240207140106976](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140106976.png)



###### 类委托和委托属性

- 委托是一种设计模式，它的基本理念是：操作对象自己不会去处理某段逻辑，而是会把工作委托给另外一个辅助对象去处理。
- 首先来看类委托，它的核心思想在于将一个类的具体实现委托给另一个类去完成。借助于委托模式，我们可以轻松实现一个自己的实现类。比如这里定义一个MySet，并让它实现Set接口，代码如下所示：![image-20240207140318856](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140318856.png)

可以看到，MySet的构造函数中接收了一个HashSet参数，这就相当于一个辅助对象。然后在Set接口所有的方法实现中，我们都没有进行自己的实现，而是调用了辅助对象中相应的方法实现，这其实就是一种委托模式。

- Kotlin中委托使用的关键字是by，我们只需要在接口声明的后面使用by关键字，再接上受委托的辅助对象，就可以免去之前所写的一大堆模板式的代码了，如下所示：![image-20240207140356434](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140356434.png)

这两段代码实现的效果是一模一样的，但是借助了类委托的功能之后，代码明显简化了太多。另外，如果我们要对某个方法进行重新实现，只需要单独重写那一个方法就可以了，其他的方法仍然可以享受类委托所带来的便利，如下所示：

![image-20240207140419585](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140419585.png)



- 我们看一下委托属性的语法结构，如下所示：![image-20240207140437042](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140437042.png)

这种写法就代表着将p属性的具体实现委托给了Delegate类去完成。当调用p属性的时候会自动调用Delegate类的getValue()方法，当给p属性赋值的时候会自动调用Delegate类的setValue()方法。因此，我们还得对Delegate类进行具体的实现才行，代码如下所示：![image-20240207140513437](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140513437.png)



###### 实现一个自己的**lazy**函数

- 新建一个Later.kt文件，并编写如下代码：![image-20240207140652424](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140652424.png)

接着我们在Later类中实现getValue()方法，代码如下所示：

![image-20240207140705228](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140705228.png)

代码写到这里，委托属性的功能就已经完成了。虽然我们可以立刻使用它，不过为了让它的用法更加类似于lazy函数，最好再定义一个顶层函数。这个函数直接写在Later.kt文件中就可以了，但是要定义在Later类的外面，因为只有不定义在任何类当中的函数才是顶层函数。代码如下所示：

![image-20240207140740518](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140740518.png)

现在，我们自己编写的later懒加载函数就已经完成了，你可以直接使用

它来替代之前的lazy函数，如下所示：![image-20240207140759589](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207140759589.png)

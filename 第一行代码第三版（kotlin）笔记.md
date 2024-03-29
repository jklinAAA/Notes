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





##### 使用通知

###### 创建通知渠道

- 首先需要一个NotificationManager对通知进行管理，可以通过调用Context的getSystemService()方法获取。getSystemService()方法接收一个字符串参数用于确定获取系统的哪个服务，这里我们传入Context.NOTIFICATION_SERVICE即可。因此，获取NotificationManager的实例就可以写成：![image-20240207162323679](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162323679.png)

接下来要使用NotificationChannel类构建一个通知渠道，并调用NotificationManager的createNotificationChannel()方法完成创建。由于NotificationChannel类和createNotificationChannel()方法都是Android 8.0系统中新增的API，因此我们在使用的时候还需要进行版本判断才可以，写法如下：

![image-20240207162358837](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162358837.png)

创建一个通知渠道至少需要渠道ID、渠道名称以及重要等级这3个参数，其中渠道ID可以随便定义，只要保证全局唯一性就可以。



###### 通知的基本用法

- 首先需要使用一个Builder构造器来创建Notification对象，使用AndroidX库中提供的兼容API。AndroidX库中提供了一个NotificationCompat类，使用这个类的构造器创建Notification对象，就可以保证我们的程序在所有Android系统版本上都能正常工作了，代码如下所示：![image-20240207162615983](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162615983.png)

- 我们可以在最终的build()方法之前连缀任意多的设置方法来创

  建一个丰富的Notification对象，先来看一些最基本的设置：![image-20240207162657316](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162657316.png)

只需要调用NotificationManager的notify()方法就可以让通知显示出来了。notify()方法接收两个参数：第一个参数是id，要保证为每个通知指定的id都是不同的；第二个参数则是Notification对象，这里直接将我们刚刚创建好的Notification对象传入即可。因此，显示一个通知就可以写成：![image-20240207162818674](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162818674.png)



具体的例子：

- 新建一个NotificationTest项目，并修改activity_main.xml中的代码，如下所示：![image-20240207162948439](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207162948439.png)

修改MainActivity中的代码，如下所示：![image-20240207163027875](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163027875.png)

现在可以来运行一下程序了，其实MainActivity一旦打开之后，通知渠道就已经创建成功了，我们可以进入应用程序设置当中查看。依次点击设置→应用和通知→NotificationTest→通知，如图9.6所示。![image-20240207163126617](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163126617.png)



- 其实要想实现通知的点击效果，我们还需要在代码中进行相应的设置，这就涉及了一个新的概念——PendingIntent。
- PendingIntent倾向于在某个合适的时机执行某个动作。所以，也可以把PendingIntent简单地理解为延迟执行的Intent。
- 首先需要准备好另一个Activity，右击com.example.notificationtest包→New→Activity→Empty Activity，新建NotificationActivity。然后修改activity_notification.xml中的代码，如下所示：![image-20240207163609786](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163609786.png)

![image-20240207163625413](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163625413.png)

修改MainActivity中的代码，给通知加入点击功能，如下所示：![image-20240207163645834](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163645834.png)

现在重新运行一下程序，并点击“Send Notice”按钮，依旧会发出一条通知。然后下拉系统状态栏，点击一下该通知，就会打开NotificationActivity的界面了，如图9.9所示![image-20240207163730375](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163730375.png)



- 如果我们没有在代码中对该通知进行取消，它就会一直显示在系统的状态栏上。解决的方法有两种：一种是在NotificationCompat.Builder中再连缀一个setAutoCancel()方法，一种是显式地调用NotificationManager的cancel()方法将它取消。两种方法我们都学习一下

  第一种方法写法如下：![image-20240207163839727](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163839727.png)

可以看到，setAutoCancel()方法传入true，就表示当点击这个通知的时候，通知会自动取消。

第二种方法写法如下：![image-20240207163901002](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207163901002.png)

这里我们在cancel()方法中传入了1，这个1是什么意思呢？还记得在创建通知的时候给每条通知指定的id吗？当时我们给这条通知设置的id就是1。因此，如果你想取消哪条通知，在cancel()方法中传入该通知的id就行了。



###### 通知的进阶技巧

省略的通知内容![image-20240207164220792](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164220792.png)

- 如果你真的非常需要在通知当中显示一段长文字，Android也是支持

  的，通过setStyle()方法就可以做到，具体写法如下![image-20240207164235556](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164235556.png)

![image-20240207164315929](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164315929.png)

- 除了显示长文字之外，通知里还可以显示一张大图片，具体用法是基本相似的：![image-20240207164340513](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164340513.png)

![image-20240207164402003](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164402003.png)

- 通知渠道的重要等级越高，发出的通知就越容易获得用户的注意。比如高重要等级的通知渠道发出的通知可以弹出横幅、发出声音，而低重要等级的通知渠道发出的通知不仅可能会在某些情况下被隐藏，而且可能会被改变显示的顺序，将其排在更重要的通知之后。

- 开发者只能在创建通知渠道的时候为它指定初始的重要等级，如果用户不认可这个重要等级的话，可以随时进行修改，开发者对此无权再进行调整和变更，因为通知渠道一旦创建就不能再通过代码修改了。

- 创建一个新的通知渠道来测试。修改MainActivity中的代码，如下所示![image-20240207164756154](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164756154.png)

这里我们将通知渠道的重要等级设置成了“高”，表示这是一条非常重要的通知，要求用户必须立刻看到。现在重新运行一下程序，并点击“Sendnotice”按钮，效果如图9.13所示。	![image-20240207164814874](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207164814874.png)

- 可以看到，这次的通知不是在系统状态栏显示一个小图标了，而是弹出了一个横幅，并附带了通知的详细内容，表示这是一条非常重要的通知。不管用户现在是在玩游戏还是看电影，这条通知都会显示在最上方，以此引起用户的注意。





##### 调用摄像头拍照

- 新建一个CameraAlbumTest项目，然后修改activity_main.xml中的代码，如下所示：![image-20240207165003779](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165003779.png)

布局文件中只有两个控件：一个Button和一个ImageView。Button是用于打开摄像头进行拍照的，而ImageView则是用于将拍到的图片显示出来。

然后开始编写调用摄像头的具体逻辑，修改MainActivity中的代码，如下

所示：![image-20240207165115910](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165115910.png)

![image-20240207165126386](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165126386.png)

在AndroidManifest.xml中对它进行注册才行，代码如下所示：![image-20240207165217043](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165217043.png)



右击res目录→New→Directory，创建一个xml目录，接着右击xml目录→New→File，创建一个file_paths.xml文件。然后修改file_paths.xml文件中的内容，如下所示：

![image-20240207165333344](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165333344.png)

external-path就是用来指定Uri共享路径的，name属性的值可以随便填，path属性的值表示共享的具体路径。这里使用一个单斜线表示将整个SD卡进行共享，当然你也可以仅共享存放output_image.jpg这张图片的路径。



##### 从相册中选择图片

- 还是在CameraAlbumTest项目的基础上进行修改，编辑activity_main.xml文件，在布局中添加一个按钮，用于从相册中选择图片，代码如下所示：![image-20240207165535872](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165535872.png)

然后修改MainActivity中的代码，加入从相册选择图片的逻辑，代码如下

所示：![image-20240207165550830](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165550830.png)	![image-20240207165602189](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165602189.png)





##### 播放音频

- 在Android中播放音频文件一般是使用MediaPlayer类实现的，它对多种格式的音频文件提供了非常全面的控制方法，从而使播放音乐的工作变得十分简单。![image-20240207165740554](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165740554.png)

![image-20240207165755167](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165755167.png)

- 梳理一下MediaPlayer的工作流程。首先需要创建一个MediaPlayer对象，然后调用setDataSource()方法设置音频文件的路径，再调用prepare()方法使MediaPlayer进入准备状态，接下来调用start()方法就可以开始播放音频，调用pause()方法就会暂停播放，调用reset()方法就会停止播放。

- 新建一个PlayAudioTest项目，然后修改activity_main.xml中的代码，如下所示：

![image-20240207165835293](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165835293.png)

MediaPlayer可以用于播放网络、本地以及应用程序安装包中的音频。这里简单起见，我们就以播放应用程序安装包中的音频来举例吧。

首先来创建assets目录吧，它必须创建在app/src/main这个目录下面，也就是和java、res这两个目录是平级的。右击app/src/main→New→Directory，在弹出的对话框中输入“assets”，目录就创建完成了。由于我们要播放音频文件，这里我提前准备好了一份music.mp3资源（资源下载方式见前言），将它放入assets目录中即可，如图9.18所示。![image-20240207165956368](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207165956368.png)

然后修改MainActivity中的代码，如下所示：![image-20240207170011253](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170011253.png)

![image-20240207170025017](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170025017.png)



##### 播放视频

- 播放视频文件其实并不比播放音频文件复杂，主要是使用VideoView类来实现的。![image-20240207170140217](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170140217.png)

- 通过一个实际的例子来学习一下吧，新建PlayVideoTest项目，然

  后修改activity_main.xml中的代码，如下所示：![image-20240207170215912](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170215912.png)

VideoView不支持直接播放assets目录下的视频资源，所以我们只能寻找其他的解决方案。res目录下允许我们再创建一个raw目录，像诸如音频、视频之类的资源文件也可以放在这里，并且VideoView是可以直接播放这个目录下的视频资源的。

现在右击app/src/main/res→New→Directory，在弹出的对话框中输入“raw”，完成raw目录的创建，并把要播放的视频资源放在里面。这里我提前准备了一个video.mp4资源（资源下载方式见前言），如图9.20所示，你也可以使用自己准备的视频资源。![image-20240207170335790](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170335790.png)

然后修改MainActivity中的代码，如下所示：![image-20240207170351962](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170351962.png)

![image-20240207170411656](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170411656.png)







##### Kotlin**课堂：使用**infix函数构建更可读的语法

- to并不是Kotlin语言中的一个关键字，之所以我们能够使用A to B
  这样的语法结构，是因为Kotlin提供了一种高级语法糖特性：infix函数。
- infix函数也并不是什么难理解的事物，它只是把编程语言函数调用的语法规则调整了一下而已，比如A to B这样的写法，实际上等价于A.to(B)的写法



- 通过两个具体的例子来学习一下infix函数的用法，先从简单

  的例子看起。![image-20240207170640168](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170640168.png)

首先，除去最前面的infix关键字不谈，这是一个String类的扩展函数。我们给String类添加了一个beginsWith()函数，它也是用于判断一个字符串是否是以某个指定参数开头的，并且它的内部实现就是调用的String类的startsWith()函数。

但是加上了infix关键字之后，beginsWith()函数就变成了一个infix函数，这样除了传统的函数调用方式之外，我们还可以用一种特殊的语法糖格式调用beginsWith()函数，如下所示：![image-20240207170824675](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170824675.png)	从这个例子就能看出，infix函数的语法规则并不复杂，上述代码其实就是调用的" Hello Kotlin "这个字符串的beginsWith()函数，并传入了一个"Hello"字符串作为参数。但是infix函数允许我们将函数调用时的小数点、括号等计算机相关的语法去掉，从而使用一种更接近英语的语法来编写程序，让代码看起来更加具有可读性。另外，infix函数由于其语法糖格式的特殊性，有两个比较严格的限制：首先，infix函数是不能定义成顶层函数的，它必须是某个类的成员函数，可以使用扩展函数的方式将它定义到某个类当中；其次，infix函数必须接收且只能接收一个参数，至于参数类型是没有限制的。只有同时满足这两点，infix函数的语法糖才具备使用的条件

- 再看一个复杂一些的例子。比如这里有一个集合，如果想要判断集合中是否包括某个指定元素，一般可以这样写：![image-20240207170917203](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170917203.png)

很简单对吗？但我们仍然可以借助infix函数让这段代码变得更加具有可读性。在infix.kt文件中添加如下代码：![image-20240207170933128](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207170933128.png)

可以看到，我们给Collection接口添加了一个扩展函数，这是因为Collection是Java以及Kotlin所有集合的总接口，因此给Collection添加一个has()函数，那么所有集合的子类就都可以使用这个函数了。另外，这里还使用了泛型函数的定义方法，从而使得has()函数可以接收任意具体类型的参数。而这个函数内部的实现逻辑就相当简单了，只是调用了Collection接口中的contains()函数而已。也就是说，has()函数和contains()函数的功能实际上是一模一样的，只是它多了一个infix关键字，从而拥有了infix函数的语法糖功能。

现在我们就可以使用如下的语法来判断集合中是否包括某个指定的元素：![image-20240207171024035](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240207171024035.png)





#### **Service**

###### **Service**是什么

- Service是Android中实现程序后台运行的解决方案，它非常适合执行那些不需要和用户交互而且还要求长期运行的任务。Service的运行不依赖于任何用户界面，即使程序被切换到后台，或者用户打开了另外一个应用程序，Service仍然能够保持正常运行。
- Service并不会自动开启线程，所有的代码都是默认运行在主线程当中的。也就是说，我们需要在Service的内部手动创建子线程，并在这里执行具体的任务，否则就有可能出现主线程被阻塞的情况。

##### 

##### **Android**多线程编程

###### 线程的基本用法

- 定义一个线程只需要新建一个类继承自Thread，然后重写父类的run()方法，并在里面编写耗时逻辑即可，如下所示：![image-20240208112830939](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208112830939.png)

- 启动线程只需要创建MyThread的实例，然后调用它的start()方法即可，这样run()方法中的代码就会在子线程当中运行了，如下所示：![image-20240208112927121](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208112927121.png)

- 使用继承的方式耦合性有点高，我们会更多地选择使用实现

  Runnable接口的方式来定义一个线程，如下所示：![image-20240208112959000](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208112959000.png)

如果使用了这种写法，启动线程的方法也需要进行相应的改变，如下所示：![image-20240208113013031](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113013031.png)

- 如果你不想专门再定义一个类去实现Runnable接口，也可以使用Lambda的方式，这种写法更为常见，如下所示：![image-20240208113206181](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113206181.png)

- 而Kotlin还给我们提供了一种更加简单的开启线程的方式，写法如下：![image-20240208113222884](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113222884.png)



###### 在子线程中更新**UI**

- 和许多其他的GUI库一样，Android的UI也是线程不安全的。也就是说，如果想要更新应用程序里的UI元素，必须在主线程中进行，否则就会出现异常。

- 新建一个AndroidThreadTest项目，然后修改activity_main.xml中的代码，如下所示：![image-20240208113448888](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113448888.png)

修改MainActivity中的代码，如下所示：![image-20240208113502560](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113502560.png)

![image-20240208113510836](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208113510836.png)



###### 解析异步消息处理机制

- Android中的异步消息处理主要由4个部分组成：Message、Handler、MessageQueue和Looper。
- **Message**

Message是在线程之间传递的消息，它可以在内部携带少量的信息，用于在不同线程之间传递数据。上一小节中我们使用到了Message的what字段，除此之外还可以使用arg1和arg2字段来携带一些整型数据，使用obj字段携带一个Object对象。

2. **Handler**

Handler顾名思义也就是处理者的意思，它主要是用于发送和处理消息的。发送消息一般是使用Handler的sendMessage()方法、post()方法等，而发出的消息经过一系列地辗转处理后，最终会传递到Handler的handleMessage()方法中。

3. **MessageQueue**

MessageQueue是消息队列的意思，它主要用于存放所有通过Handler发送的消息。这部分消息会一直存在于消息队列中，等待被处理。每个线程中只会有一个MessageQueue对象。

4. **Looper**

Looper是每个线程中的MessageQueue的管家，调用Looper的loop()方法后，就会进入一个无限循环当中，然后每当发现MessageQueue中存在一条消息时，就会将它取出，并传递到Handler的handleMessage()方法中。每个线程中只会有一个Looper对象。

- 整个异步消息处理机制的流程如图10.3所示。![image-20240208114813167](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208114813167.png)



###### 使用**AsyncTask**

- 借助AsyncTask，即使你对异步消息处理机制完全不了解，也可以十分简单地从子线程切换到主线程。

- AsyncTask的基本用法：由于AsyncTask是一个抽象类，所以如果我们想使用它，就必须创建一个子类去继承它。在继承时我们可以为AsyncTask类指定3个泛型参数，这3个参数的用途如下：

  - Params。在执行AsyncTask时需要传入的参数，可用于在后台任务中使用。

  - Progress。在后台任务执行时，如果需要在界面上显示当前的进度，则使用这里指定的泛型作为进度单位。

  - Result。当任务执行完毕后，如果需要对结果进行返回，则使用这里指定的泛型作为返回值类型。

    

    因此，一个最简单的自定义AsyncTask就可以写成如下形式：![image-20240208115253519](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115253519.png)

![image-20240208115319624](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115319624.png)

- 我们还需要重写AsyncTask中的几个方法才能完成对任务的定制。经常需要重写的方法有以下4个。

1. **onPreExecute()**

这个方法会在后台任务开始执行之前调用，用于进行一些界面上的初

始化操作，比如显示一个进度条对话框等。02. **doInBackground(Params...)**

这个方法中的所有代码都会在子线程中运行，我们应该在这里去处理

所有的耗时任务。任务一旦完成，就可以通过return语句将任务的执

行结果返回，如果AsyncTask的第三个泛型参数指定的是Unit，就可

以不返回任务执行结果。注意，在这个方法中是不可以进行UI操作

的，如果需要更新UI元素，比如说反馈当前任务的执行进度，可以调

用publishProgress (Progress...)方法来完成。

3. **onProgressUpdate(Progress...)**

当在后台任务中调用了publishProgress(Progress...)方法后，

onProgressUpdate (Progress...)方法就会很快被调用，该方

法中携带的参数就是在后台任务中传递过来的。在这个方法中可以对

UI进行操作，利用参数中的数值就可以对界面元素进行相应的更新。

4. **onPostExecute(Result)**

当后台任务执行完毕并通过return语句进行返回时，这个方法就很快

会被调用。返回的数据会作为参数传递到此方法中，可以利用返回的

数据进行一些UI操作，比如说提醒任务执行的结果，以及关闭进度条

对话框等。

因此，一个比较完整的自定义AsyncTask就可以写成如下形式：![image-20240208115405455](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115405455.png)

![image-20240208115413141](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115413141.png)

- 简单来说，使用AsyncTask的诀窍就是，在doInBackground()方法中执行具体的耗时任务，在onProgressUpdate()方法中进行UI操作，在onPostExecute()方法中执行一些任务的收尾工作。

  如果想要启动这个任务，只需编写以下代码即可![image-20240208115631750](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115631750.png)





##### **Service**的基本用法

###### 定义一个**Service**

- 新建一个ServiceTest项目，然后右击com.example.servicetest→New→Service→Service，会弹出如图10.4所示的窗口。![image-20240208115743446](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208115743446.png)

将两个属性都勾中，点击“Finish”完成创建。

现在观察MyService中的代码，如下所示：

![image-20240208120034002](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120034002.png)

重写Service中的另外一些方法了，如下所示：![image-20240208120054497](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120054497.png)

这里我们又重写了onCreate()、onStartCommand()和onDestroy()这3个方法，它们是每个Service中最常用到的3个方法了。其中onCreate()方法会在Service创建的时候调用，onStartCommand()方法会在每次Service启动的时候调用，onDestroy()方法会在Service销毁的时候调用。



- 每一个Service都需要在AndroidManifest.xml文件中进行注册才能生效。这是Android四大组件共有的特点。智能的Android Studio早已自动帮我们完成了。打开AndroidManifest.xml文件瞧一瞧，代码如下所示：![image-20240208120312158](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120312158.png)



###### 启动和停止**Service**

- 启动和停止的方法主要是借助Intent来实现的。下面就让我们在ServiceTest项目中尝试启动以及停止MyService。

  首先修改activity_main.xml中的代码，如下所示：![image-20240208120357718](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120357718.png)

这里我们在布局文件中加入了两个按钮，分别用于启动和停止Service。然后修改MainActivity中的代码，如下所示：

![image-20240208120413947](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120413947.png)



###### **Activity**和**Service**进行通信

- 例如在Activity中指挥Service去干什么，Service就去干什么。当然可以，这就需要借助我们刚刚忽略的onBind()方法了。
- 比如说，目前我们希望在MyService里提供一个下载功能，然后在Activity中可以决定何时开始下载，以及随时查看下载进度。实现这个功能的思路是创建一个专门的Binder对象来对下载功能进行管理。修改MyService中的代码，如下所示：![image-20240208120849163](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120849163.png)

首先需要在布局文件里新增两个按钮，修改activity_main.xml中的代码，如下所示：![image-20240208120917032](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208120917032.png)

​	这两个按钮分别是用于绑定和取消绑定Service的

当一个Activity和Service绑定了之后，就可以调用该Service里的Binder提供的方法了。修改MainActivity中的代码，如下所示：

![image-20240208121322836](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208121322836.png)

![image-20240208121334361](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208121334361.png)



##### **Service**的生命周期

- 之前我们学习过了Activity以及Fragment的生命周期。类似地，Service也有自己的生命周期，前面我们使用到的onCreate()、onStartCommand()、onBind()和onDestroy()等方法都是在Service的生命周期内可能回调的方法

  

##### **Service**的更多技巧

###### 使用前台**Service**.

- 从Android 8.0系统开始，只有当应用保持在前台可见状态的情况下，Service才能保证稳定运行，一旦应用进入后台之后，Service随时都有可能被系统回收。而如果你希望Service能够一直保持运行状态，就可以考虑使用前台Service。
- 前台Service和普通Service最大的区别就在于，它一直会有一个正在运行的图标在系统的状态栏显示，下拉状态栏后可以看到更加详细的信息，非常类似于通知的效果，如图10.11所示。![image-20240208121931154](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208121931154.png)



- 如何才能创建一个前台Service吧，其实并不复杂，修改MyService中的代码，如下所示：

![image-20240208122122485](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122122485.png)



从Android 9.0系统开始，使用前台Service必须在AndroidManifest.xml文件中进行权限声明才行，如下所示：![image-20240208122201753](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122201753.png)

现在重新运行一下程序，并点击“Start Service”按钮，MyService就会以前台Service的模式启动了，并且在系统状态栏会显示一个通知图标，下拉状态栏后可以看到该通知的详细内容，如图10.12所示

![image-20240208122226360](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122226360.png)



###### 使用**IntentService**

- Service中的代码都是默认运行在主线程当中的，如果直接在Service里处理一些耗时的逻辑，就很容易出现ANR（Application Not Responding）的情况。

  所以这个时候就需要用到Android多线程编程的技术了，我们应该在Service的每个具体的方法里开启一个子线程，然后在这里处理那些耗时的逻辑。因此，一个比较标准的Service就可以写成如下形式：![image-20240208122427023](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122427023.png)

但是，这种Service一旦启动，就会一直处于运行状态，必须调用stopService()或stopSelf()方法，或者被系统回收，Service才会停止。所以，如果想要实现让一个Service在执行完毕后自动停止的功能，就可以这样写：![image-20240208122619001](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122619001.png)

![image-20240208122625871](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122625871.png)



- 为了可以简单地创建一个异步的、会自动停止的Service，Android专门提供了一个IntentService类，这个类就很好地解决了前面所提到的两种尴尬，下面我们就来看一下它的用法。

  新建一个MyIntentService类继承自IntentService，代码如下所示：![image-20240208122808364](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122808364.png)

接下来修改activity_main.xml中的代码，加入一个用于启动MyIntentService的按钮，如下所示：![image-20240208122834971](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122834971.png)

![image-20240208122843703](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122843703.png)

然后修改MainActivity中的代码，如下所示：![image-20240208122854504](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122854504.png)

最后不要忘记，Service都是需要在AndroidManifest.xml里注册的，如下所示：![image-20240208122914329](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122914329.png)

![image-20240208122927836](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208122927836.png)





#### **Kotlin**课堂：泛型的高级特性

###### 对泛型进行实化

- ![image-20240208123314692](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123314692.png)

可以看到，bar()是一个带有泛型类型的内联函数，foo()函数调用了bar()函数，在代码编译之后，bar()函数中的代码将可以获得泛型的实际类型。这就意味着，Kotlin中是可以将内联函数中的泛型进行实化的。

- 首先，该函数必须是内联函数才行，也就是要用inline关键字来修饰该函数。其次，在声明泛型的地方必须加上reified关键字来表示该泛型要进行实化。示例代码如下：![image-20240208123427541](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123427541.png)

上述函数中的泛型T就是一个被实化的泛型，因为它满足了内联函数和reified关键字这两个前提条件。那么借助泛型实化，到底可以实现什么样的效果呢？从函数名就可以看出来了，这里我们准备实现一个获取泛型实际类型的功能，代码如下所示：![image-20240208123446522](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123446522.png)

虽然只有一行代码，但是这里却实现了一个Java中完全不可能实现的功能：getGenericType()函数直接返回了当前指定泛型的实际类型。T.class这样的语法在Java中是不合法的，而在Kotlin中，借助泛型实化功能就可以使用T::class.java这样的语法了。现在我们可以使用如下代码对getGenericType()函数进行测试：![image-20240208123534304](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123534304.png)

这里给getGenericType()函数指定了两种不同的泛型，由于getGenericType()函数会将指定泛型的具体类型返回，因此这里我们将返回的结果进行打印。现在运行一下main()函数，结果如图10.17所示。![image-20240208123600669](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123600669.png)



###### 泛型实化的应用

- 除了ContentProvider之外，你会发现其余的3个组件有一个共同的特点，它们都是要结合Intent一起使用的。比如说启动一个Activity就可以这么写：![image-20240208123707164](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123707164.png)

如果在没有更好选择的情况下，这种写法也是可以忍受的，但是Kotlin的泛型实化功能使得我们拥有了更好的选择。新建一个reified.kt文件，然后在里面编写如下代码：

![image-20240208123726397](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123726397.png)

现在，如果我们想要启动TestActivity，只需要这样写就可以了：![image-20240208123842608](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208123842608.png)

不过，现在的startActivity()函数其实还是有问题的，因为通常在启用Activity的时候还可能会使用Intent附带一些参数，比如下面的写法：![image-20240208124046634](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124046634.png)

而经过刚才的封装之后，我们就无法进行传参了

只需要借助之前在第6章学习的高阶函数就可以轻松搞定。回到reified.kt文件当中，这里添加一个新的startActivity()函数重载，如下所示：![image-20240208124111666](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124111666.png)

在创建完Intent的实例之后，随即调用该函数类型参数，并把Intent的实例传入，这样调用startActivity()函数的时候就可以在Lambda表达式中为Intent传递参数了，如下所示：![image-20240208124149902](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124149902.png)





###### 泛型的协变

- 在开始学习协变和逆变之前，我们还得先了解一个约定。一个泛型类或者泛型接口中的方法，它的参数列表是接收数据的地方，因此可以称它为in位置，而它的返回值是输出数据的地方，因此可以称它为out位置，如图10.18所示。![image-20240208124244222](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124244222.png)

有了这个约定前提，我们就可以继续学习了。首先定义如下3个类：![image-20240208124301108](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124301108.png)

如果某个方法接收一个List<Person>类型的参数，而我们传入一个List<Student>的实例，这样合不合法呢？看上去好像也挺正确的，但是Java中是不允许这么做的，因为List<Student>不能成为List<Person>的子类，否则将可能存在类型转换的安全隐患。为什么会存在类型转换的安全隐患呢？下面我们通过一个具体的例子进行说明。这里自定义一个SimpleData类，代码如下所示：![image-20240208124435717](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124435717.png)

SimpleData是一个泛型类，它的内部封装了一个泛型data字段，调用set()方法可以给data字段赋值，调用get()方法可以获取data字段的值。接着我们假设，如果编程语言允许向某个接收SimpleData<Person>参数的方法传入SimpleData<Student>的实例，那么如下代码就会是合法的：![image-20240208124616709](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124616709.png)

![image-20240208124626144](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124626144.png)

回到main()方法当中，我们调用SimpleData<Student>的get()方法来获取它内部封装的Student数据，可现在SimpleData<Student>中实际包含的却是一个Teacher的实例，那么此时必然会产生类型转换异常。所以，为了杜绝这种安全隐患，Java是不允许使用这种方式来传递参数的。换句话说，即使Student是Person的子类，SimpleData<Student>并不是SimpleData<Person>的子类。不过，回顾一下刚才的代码，你会发现问题发生的主要原因是我们在handleSimpleData()方法中向SimpleData<Person>里设置了一个Teacher的实例。如果SimpleData在泛型T上是只读的话，肯定就没有类型转换的安全隐患了，那么这个时候SimpleData<Student>可不可以成为SimpleData<Person>的子类呢？

- 讲到这里，我们终于要引出泛型协变的定义了。**假如定义了一个MyClass<T>的泛型类，其中A是B的子类型，同时MyClass<A>又是MyClass<B>的子类型，那么我们就可以称MyClass在T这个泛型上是协变的。**

  但是如何才能让MyClass<A>成为MyClass<B>的子类型呢？如果一个泛型类在其泛型类型的数据上是只读的话，那么它是没有类型转换安全隐患的。而要实现这一点，则需要让MyClass<T>类中的所有方法都不能接收T类型的参数。换句话说，T只能出现在out位置上，而不能出现在in位置上。现在修改SimpleData类的代码，如下所示：![image-20240208124819531](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124819531.png)

经过了这样的修改之后，下面的代码就可以完美编译通过且没有任何安全隐患了：![image-20240208124844826](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208124844826.png)

由于SimpleData类已经进行了协变声明，那么SimpleData<Student>自然就是SimpleData<Person>的子类了，所以这里可以安全地向handleMyData()方法中传递参数。然后在handleMyData()方法中去获取SimpleData封装的数据，虽然这里泛型声明的是Person类型，实际获得的会是一个Student的实例，但由于Person是Student的父类，向上转型是完全安全的，所以这段代码没有任何问题。



###### 泛型的逆变

- 定义：假如定义了一个MyClass<T>的泛型类，其中A是B的子类型，同时MyClass<B>又是MyClass<A>的子类型，那么我们就可以称MyClass在T这个泛型上是逆变的。协变和逆变的区别如图10.19所示。![image-20240208125000288](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208125000288.png)

具体的例子：这里先定义一个Transformer接口，用于执行一些转换操作，代码如下所示：![image-20240208125026944](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208125026944.png)

可以看到，Transformer接口中声明了一个transform()方法，它接收一个T类型的参数，并且返回一个String类型的数据，这意味着参数T在经过transform()方法的转换之后将会变成一个字符串。至于具体的转换逻辑是什么样的，则由子类去实现，Transformer接口对此并不关心。那么现在我们就尝试对Transformer接口进行实现，代码如下所示![image-20240208125055251](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208125055251.png)

这段代码从安全的角度来分析是没有任何问题的，因为Student是Person的子类，使用Transformer<Person>的匿名类实现将Student对象转换成一个字符串也是绝对安全的，并不存在类型转换的安全隐患。但是实际上，在调用handleTransformer()方法的时候却会提示语法错误，原因也很简单，Transformer<Person>并不是Transformer<Student>的子类型。那么这个时候逆变就可以派上用场了，它就是专门用于处理这种情况的。修改Transformer接口中的代码，如下所示：

![image-20240208125127256](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208125127256.png)

![image-20240208125134634](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208125134634.png)





#### 使用网络技术

###### **WebView**的用法

- Android提供了一个WebView控件，借助它我们就可以在自己的应用程序里嵌入一个浏览器，从而非常轻松地展示各种各样的网页。
- WebView的用法也相当简单，下面我们就通过一个例子来学习一下吧。新建一个WebViewTest项目，然后修改activity_main.xml中的代码，如下所示：![image-20240208130627751](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208130627751.png)

我们在布局文件中使用到了一个新的控件：WebView。这个控件就是用来显示网页的

然后修改MainActivity中的代码，如下所示：![image-20240208130652260](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208130652260.png)

![image-20240208130700387](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208130700387.png)

通过WebView的getSettings()方法可以设置一些浏览器的属性，这里我们并没有设置过多的属性，只是调用了setJavaScriptEnabled()方法，让WebView支持JavaScript脚本。接下来是比较重要的一个部分，我们调用了WebView的setWebViewClient()方法，并传入了一个WebViewClient的实例。这段代码的作用是，当需要从一个网页跳转到另一个网页时，我们希望目标网页仍然在当前WebView中显示，而不是打开系统浏览器。最后一步就非常简单了，调用WebView的loadUrl()方法，并将网址传入，即可展示相应网页的内容，这里就让我们看一看百度的首页长什么样吧。![image-20240208131047687](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208131047687.png)

我们还得修改AndroidManifest.xml文件，并加入权限声明，如下所示：![image-20240208131031068](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208131031068.png)



##### 使用**HTTP**访问网络

- 它的工作原理特别简单，就是客户端向服务器发出一条HTTP请求，服务器收到请求之后会返回一些数据给客户端，然后客户端再对这些数据进行解析和处理就可以了。



###### 使用**HttpURLConnection**

- 首先需要获取HttpURLConnection的实例，一般只需创建一个URL对象，并传入目标的网络地址，然后调用一下openConnection()方法即可，如下所示：![image-20240208131941784](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208131941784.png)

在得到了HttpURLConnection的实例之后，我们可以设置一下HTTP请求所使用的方法。常用的方法主要有两个：GET和POST。GET表示希望从服务器那里获取数据，而POST则表示希望提交数据给服务器。写法如下：![image-20240208132007383](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132007383.png)

接下来就可以进行一些自由的定制了，比如设置连接超时、读取超时的毫秒数，以及服务器希望得到的一些消息头等。这部分内容根据自己的实际情况进行编写，示例写法如下：![image-20240208132030155](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132030155.png)

之后再调用getInputStream()方法就可以获取到服务器返回的输入流了，剩下的任务就是对输入流进行读取：![image-20240208132046864](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132046864.png)

最后可以调用disconnect()方法将这个HTTP连接关闭：![image-20240208132101536](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132101536.png)



- 下面就让我们通过一个具体的例子来真正体验一HttpURLConnection的用法。新建一个NetworkTest项目，首先修改activity_main.xml中的代码，如下所示：![image-20240208132945551](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132945551.png)

![image-20240208132954615](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208132954615.png)

接着修改MainActivity中的代码，如下所示：![image-20240208133019843](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133019843.png)

![image-20240208133028560](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133028560.png)

我们在“Send Request”按钮的点击事件里调用了sendRequestWithHttpURLConnection()方法，在这个方法中先是开启了一个子线程，然后在子线程里使用HttpURLConnection发出一条HTTP请求，请求的目标地址就是百度的首页。接着利用BufferedReader对服务器返回的流进行读取，并将结果传入showResponse()方法中。而在showResponse()方法里，则是调用了一个runOnUiThread()方法，然后在这个方法的Lambda表达式中进行操作，将返回的数据显示到界面上。

仍然别忘了要声明一下网络权限。修改AndroidManifest.xml中的代码，如下所示：![image-20240208133115725](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133115725.png)

![image-20240208133123546](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133123546.png)

现在运行一下程序，并点击“Send Request”按钮，结果如图11.2所示![image-20240208133147932](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133147932.png)

没错，服务器返回给我们的就是这种HTML代码，只是通常情况下浏览器会将这些代码解析成漂亮的网页后再展示出来。

那么如果想要提交数据给服务器应该怎么办呢？其实也不复杂，只需要将HTTP请求的方法改成POST，并在获取输入流之前把要提交的数据写出即可。注意，每条数据都要以键值对的形式存在，数据与数据之间用“&”符号隔开。比如说我们想要向服务器提交用户名和密码，就可以这样写：![image-20240208133231411](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208133231411.png)





###### 使用**OkHttp**

- OkHttp的项目主页地址是：https://github.com/square/okhttp。
- 在使用OkHttp之前，我们需要先在项目中添加OkHttp库的依赖。编辑app/build.gradle文件，在dependencies闭包中添加如下内容：![image-20240208141102135](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141102135.png)

- OkHttp的具体用法，首先需要创建一个OkHttpClient

  的实例，如下所示：![image-20240208141126841](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141126841.png)

接下来如果想要发起一条HTTP请求，就需要创建一个Request对象：![image-20240208141137689](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141137689.png)

上述代码只是创建了一个空的Request对象，并没有什么实际作用，我们可以在最终的build()方法之前连缀很多其他方法来丰富这个Request对象。比如可以通过url()方法来设置目标的网络地址，如下所示：![image-20240208141206224](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141206224.png)

之后调用OkHttpClient的newCall()方法来创建一个Call对象，并调用它的execute()方法来发送请求并获取服务器返回的数据，写法如下：![image-20240208141223736](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141223736.png)

Response对象就是服务器返回的数据了，我们可以使用如下写法来得到返回的具体内容：![image-20240208141238780](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141238780.png)

如果是发起一条POST请求，会比GET请求稍微复杂一点，我们需要先构建一个Request Body对象来存放待提交的参数，如下所示：![image-20240208141253995](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141253995.png)	![image-20240208141301915](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141301915.png)

然后在Request.Builder中调用一下post()方法，并将RequestBody对象传入：![image-20240208141319622](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141319622.png)

接下来的操作就和GET请求一样了，调用execute()方法来发送请求并获取服务器返回的数据即可。

- 现在我们先把NetworkTest这个项目改用OkHttp的方式再实现一遍吧。

  由于布局部分完全不用改动，所以直接修改MainActivity中的代码，如下所示：![image-20240208141457801](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141457801.png)

![image-20240208141504844](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208141504844.png)





##### 解析**XML**格式数据

- 在网络上传输数据时最常用的格式有两种：XML和JSON。
- 搭建Web服务器的过程：下面来看Window系统下的搭建过程。首先你需要下载一个Apache服务器的安装包，官方下载地址是：http://httpd.apache.org。下载完成后双击就可以进行安装了，如图11.3所示。![image-20240208142741725](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208142741725.png)

然后一直点击“Next”，会提示让你输入自己的域名，我们随便填一个域名就可以了，如图11.4所示。![image-20240208142807158](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208142807158.png)

接着继续一直点击“Next”，会提示让你选择程序安装的路径，这里我选择安装到C:\Apache目录下。之后继续点击“Next”就可以完成安装了。安装成功后服务器会自动启动，你可以打开浏览器来验证一下。在地址栏输入127.0.0.1，如果出现了如图11.5所示的界面，就说明服务器已经启动成功了。![image-20240208142851379](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208142851379.png)

接下来进入C:\Apache\htdocs目录下，在这里新建一个名为get_data.xml的文件，然后编辑这个文件，并加入如下XML格式的内容。![image-20240208142934119](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208142934119.png)

![image-20240208142945068](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208142945068.png)

这时在浏览器中访问http://127.0.0.1/get_data.xml这个网址，就应该出现如图11.6所示的内容。![image-20240208143010507](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143010507.png)

准备工作到此结束，接下来就让我们在Android程序里去获取并解析这段XML数据吧

- 解析XML格式的数据其实也有挺多种方式的，本节中我们学习比较常用的两种：Pull解析和SAX解析。

  

###### **Pull**解析方式

- 这里仍然是在NetworkTest项目的基础上继续开发

  修改MainActivity中的代码，如下所示：![image-20240208143202240](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143202240.png)

![image-20240208143215746](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143215746.png)

为了能让程序使用HTTP，我们还要进行如下配置才可以。右击res目录→New→Directory，创建一个xml目录，接着右击xml目录→New→File，创建一个network_config.xml文件。然后修改network_config.xml文件中的内容，如下所示：![image-20240208143302818](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143302818.png)

这段配置文件的意思就是允许我们以明文的方式在网络上传输数据，而HTTP使用的就是明文传输方式。

接下来修改AndroidManifest.xml中的代码来启用我们刚才创建的配置文件：![image-20240208143334747](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143334747.png)

这样就可以在程序中使用HTTP了



###### **SAX**解析方式

- 要使用SAX解析，通常情况下我们会新建一个类继承自DefaultHandler，并重写父类的5个方法，如下所示：![image-20240208143535676](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143535676.png)

- 下面就让我们尝试用SAX解析的方式来实现和上一小节同样的功能吧。新建一个ContentHandler类继承自DefaultHandler，并重写父类的5个方法，如下所示：![image-20240208143901779](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143901779.png)

![image-20240208143915883](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208143915883.png)

接下来的工作就非常简单了，修改MainActivity中的代码，如下所示：![image-20240208144009279](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144009279.png)

![image-20240208144023025](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144023025.png)

现在重新运行一下程序，点击“Send Request”按钮后观察Logcat中的打印日志，你会看到和图11.7中一样的结果![image-20240208144144867](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144144867.png)



##### 解析**JSON**格式数据

- 比起XML，JSON的主要优势在于它的体积更小，在网络上传输的时候更省流量。但缺点在于，它的语义性较差，看起来不如XML直观。

- 在开始之前，我们还需要在C:\Apache\htdocs目录中新建一个get_data.json的文件，然后编辑这个文件，并加入如下JSON格式的内容：![image-20240208144256401](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144256401.png)

这时在浏览器中访问http://127.0.0.1/get_data.json这个网址，就应该出现如图11.8所示的内容![image-20240208144333007](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144333007.png)

好了，这样我们就把JSON格式的数据准备好了，下面就开始学习如何在Android程序中解析这些数据吧。



###### 使用**JSONObject**.

- 修改MainActivity中的代码，如下所示：![image-20240208144436472](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144436472.png)

![image-20240208144443760](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144443760.png)

现在重新运行一下程序，并点击“SendRequest”按钮，结果如图11.9所示。![image-20240208144507634](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144507634.png)





###### 使用**GSON**

- 如果想要使用这个功能的话，就必须在项目中添加GSON库的依赖。编辑app/build.gradle文件，在dependencies闭包中添加如下内容：![image-20240208144705893](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144705893.png)

![image-20240208144715740](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144715740.png)

- 它的强大之处就在于可以将一段JSON格式的字符串自动映射成一个对象，从而不需要我们再手动编写代码进行解析了。比如说一段JSON格式的数据如下所示：![image-20240208144748253](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144748253.png)

那我们就可以定义一个Person类，并加入name和age这两个字段，然后只需简单地调用如下代码就可以将JSON数据自动解析成一个Person对象了：![image-20240208144813512](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144813512.png)

如果需要解析的是一段JSON数组，会稍微麻烦一点，比如如下格式的数据：![image-20240208144826778](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144826778.png)

这个时候，我们需要借助TypeToken将期望解析成的数据类型传入fromJson()方法中，如下所示：![image-20240208144843213](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208144843213.png)



- 下面就让我们来真正地尝试一下吧。首先新增一个App类，并加入id、name和version这3个字段，如下所示：![image-20240208145218694](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145218694.png)

然后修改MainActivity中的代码，如下所示：![image-20240208145228269](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145228269.png)

![image-20240208145234957](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145234957.png)

现在重新运行程序，点击“Send Request”按钮后观察Logcat中的打印日志，你会看到和图11.9中一样的结果。



##### 网络请求回调的实现方式

- 通常情况下我们应该将这些通用的网络操作提取到一个公共的类里，并提供一个通用方法，当想要发起网络请求的时候，只需简单地调用一下这个方法即可。比如使用如下的写法：![image-20240208145701510](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145701510.png)

以后每当需要发起一条HTTP请求的时候，就可以这样写：![image-20240208145717753](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145717753.png)

在获取到服务器响应的数据后，我们就可以对它进行解析和处理了。但是需要注意，网络请求通常属于耗时操作，而sendHttpRequest()方法的内部并没有开启线程，这样就有可能导致在调用sendHttpRequest()方法的时候主线程被阻塞。

那么在遇到这种情况时应该怎么办呢？其实解决方法并不难，只需要使用编程语言的回调机制就可以了。下面就让我们来学习一下回调机制到底是如何使用的。

首先需要定义一个接口，比如将它命名成HttpCallbackListener，代码如下所示：![image-20240208145855036](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145855036.png)

可以看到，我们在接口中定义了两个方法：onFinish()方法表示当服务器成功响应我们请求的时候调用，onError()表示当进行网络操作出现错误的时候调用

接着修改HttpUtil中的代码，如下所示：![image-20240208145926972](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145926972.png)

![image-20240208145938320](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208145938320.png)

现在sendHttpRequest()方法接收两个参数，因此我们在调用它的时候还需要将HttpCallbackListener的实例传入，如下所示：	![image-20240208150038990](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208150038990.png)

![image-20240208150046343](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208150046343.png)



不过你会发现，上述使用HttpURLConnection的写法总体来说还是比较复杂的，那么使用OkHttp会变得简单吗？答案是肯定的，而且要简单得多，下面我们来具体看一下。在HttpUtil中加入一个sendOkHttpRequest()方法，如下所示：![image-20240208150120262](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208150120262.png)

OkHttp在enqueue()方法的内部已经帮我们开好子线程了，然后会在子线程中执行HTTP请求，并将最终的请求结果回调到okhttp3.Callback当中。那么我们在调用sendOkHttpRequest()方法的时候就可以这样写：![image-20240208150226208](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208150226208.png)

![image-20240208150233102](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208150233102.png)





##### 最好用的网络库：**Retrofit**

- Retrofit的项目主页地址是：https://github.com/square/retrofit。



###### **Retrofit**的基本用法

- 要想使用Retrofit，我们需要先在项目中添加必要的依赖库。编辑app/build.gradle文件，在dependencies闭包中添加如下内容：![image-20240208191704414](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240208191704414.png)

由于Retrofit是基于OkHttp开发的，因此添加上述第一条依赖会自动将Retrofit、OkHttp和Okio这几个库一起下载，我们无须再手动引入OkHttp库。另外，Retrofit还会将服务器返回的JSON数据自动解析成对象，因此上述第二条依赖就是一个Retrofit的转换库，它是借助GSON来解析JSON数据的，所以会自动将GSON库一起下载下来，这样我们也不用手动引入GSON库了。

由于Retrofit会借助GSON将JSON数据转换成对象，因此这里同样需要新增一个App类，并加入id、name和version这3个字段，如下所示：

![image-20240210131731545](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131731545.png)

新建AppService接口，代码如下所示：![image-20240210131803836](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131803836.png)

修改activity_main.xml中的代码，如下所示：![image-20240210131831404](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131831404.png)

![image-20240210131837754](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131837754.png)

修改MainActivity中的代码，如下所示：![image-20240210131856495](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131856495.png)

接下来就可以进行一下测试了，不过由于这里使用的服务器接口仍然是HTTP，因此我们还要按照11.3.1小节所示的步骤来进行网络安全配置才行。先从NetworkTest项目中复制network_config.xml文件到RetrofitTest项目当中，然后修改AndroidManifest.xml中的代码，如下所示

![image-20240210131926447](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131926447.png)

![image-20240210131934229](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210131934229.png)



###### 处理复杂的接口地址类型

- 为了方便举例，这里先定义一个Data类，并包含id和content这两个字段，如下所示：![image-20240210132015802](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132015802.png)

然后我们先从最简单的看起，比如服务器的接口地址如下所示：![image-20240210132031280](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132031280.png)

这是最简单的一种情况，接口地址是静态的，永远不会改变。那么对应到Retrofit当中，使用如下的写法即可：![image-20240210132052307](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132052307.png)

- 在很多场景下，接口地址中的部分内容可能会是动态变化的，比如如下的接口地址：![image-20240210132126384](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132126384.png)

接口地址对应到Retrofit当中，如下所示：![image-20240210132211504](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132211504.png)

另外，很多服务器接口还会要求我们传入一系列的参数，格式如下：![image-20240210132237919](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132237919.png)

Retrofit针对这种带参数的GET请求，专门提供了一种语法支持：![image-20240210132315522](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132315522.png)



###### **Retrofit**构建器的最佳写法

- 是获取Service接口的动态代理对象实在是太麻烦了。先回顾一下之前的写法吧，大致代码如下所示：![image-20240210132439771](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132439771.png)

- 我们可以将通用的这部分功能封装起来，从而简化获取Service接口动态代理对象的过程。新建一个ServiceCreator单例类，代码如下所示：![image-20240210132515779](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132515779.png)

经过这样的封装之后，Retrofit的用法将会变得异常简单，比如我们想获取一个AppService接口的动态代理对象，只需要使用如下写法即可：![image-20240210132549886](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132549886.png)

利用泛型实化功能，修改ServiceCreator中的代码，如下所示：![image-20240210132656796](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132656796.png)

那么现在我们就又有了一种新的方式来获取AppService接口的动态代理对象，如下所示：![image-20240210132717712](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132717712.png)





#### **Kotlin**课堂：使用协程编写高效的并发程序

###### 协程的基本用法

- 需要先在app/build.gradle文件当中添加如下依赖库：![image-20240210132908936](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132908936.png)

接下来创建一个CoroutinesTest.kt文件，并定义一个main()函数，然后开始我们的协程之旅吧

- 如何开启一个协程？最简单的方式就是使用Global.launch函数，如下所示：![image-20240210132947721](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210132947721.png)

Global.launch函数每次创建的都是一个顶层协程，这种协程当应用程序运行结束时也会跟着一起结束。日志无法打印出来，要解决这个问题也很简单，我们让程序延迟一段时间再结束就行了，如下所示：![image-20240210133046460](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210133046460.png)

那么有没有什么办法能让应用程序在协程中所有代码都运行完了之后再结束呢？当然也是有的，借助runBlocking函数就可以实现这个功能：![image-20240210133201585](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210133201585.png)

那么如何才能创建多个协程呢？很简单，使用launch函数就可以了，如下所示：![image-20240210133215802](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240210133215802.png)



###### 使用协程简化回调的写法

- suspendCoroutine函数必须在协程作用域或挂起函数中才能调用，它接收一个Lambda表达式参数，主要作用是将当前协程立即挂起，然后在一个普通的线程中执行Lambda表达式中的代码。Lambda表达式的参数列表上会传入一个Continuation参数，调用它的resume()方法或resumeWithException()可以让协程恢复执行。
- 了解了suspendCoroutine函数的作用之后，接下来我们就可以借助这个函数来对传统的回调写法进行优化。首先定义一个request()函数，代码如下所示：![image-20240212121449452](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121449452.png)

不管之后我们要发起多少次网络请求，都不需要再重复进行回调实现了。比如说获取百度首页的响应数据，就可以这样写：![image-20240212121531472](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121531472.png)

事实上，suspendCoroutine函数几乎可以用于简化任何回调的写法，比如之前使用Retrofit来发起网络请求需要这样写：![image-20240212121817182](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121817182.png)

定义一个await()函数，代码如下所示：![image-20240212121846943](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121846943.png)

有了await()函数之后，我们调用所有Retrofit的Service接口都会变得极其简单，比如刚才同样的功能就可以使用如下写法进行实现：![image-20240212121912158](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121912158.png)

![image-20240212121919027](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212121919027.png)



#### **Material Design**

###### **Toolbar**

- 修改activity_main.xml中的代码，如下所示：![image-20240212122531678](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212122531678.png)

接下来我们修改MainActivity，代码如下所示：![image-20240212122718425](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212122718425.png)

现在运行一下程序，效果如图12.3所示。![image-20240212122734783](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212122734783.png)

- Toolbar比较常用的功能：

  比如修改标题栏上显示的文字内容。这段文字内容是在AndroidManifest.xml中指定的，如下所示：![image-20240212122829856](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212122829856.png)

这里给activity增加了一个android:label属性，用于指定在Toolbar中显示的文字内容，如果没有指定的话，会默认使用application中指定的label内容，也就是我们的应用名称。

不过只有一个标题的Toolbar看起来太单调了，我们还可以再添加一些action按钮来让Toolbar更加丰富一些。这里我提前准备了几张图片作为按钮的图标，将它们放在了drawable-xxhdpi目录下。现在右击res目录→New→Directory，创建一个menu文件夹。然后右击menu文件夹→New→Menu resource file，创建一个toolbar.xml文件，并编写如下代码：![image-20240212123108208](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123108208.png)

![image-20240212123115409](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123115409.png)

修改MainActivity中的代码，如下所示：![image-20240212123146312](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123146312.png)

现在重新运行一下程序，效果如图12.4所示。![image-20240212123305453](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123305453.png)



##### 滑动菜单

###### **DrawerLayout**

- 首先它是一个布局，在布局中允许放入两个直接子控件：第一个子控件是主屏幕中显示的内容，第二个子控件是滑动菜单中显示的内容。因此，我们就可以对activity_main.xml中的代码做如下修改：![image-20240212123546029](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123546029.png)

![image-20240212123554766](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212123554766.png)

layout_gravity这个属性是必须指定的，因为我们需要告诉DrawerLayout滑动菜单是在屏幕的左边还是右边，指定left表示滑动菜单在左边，指定right表示滑动菜单在右边。这里我指定了start，表示会根据系统语言进行判断，如果系统语言是从左往右的，比如英语、汉语，滑动菜单就在左边，如果系统语言是从右往左的，比如阿拉伯语，滑动菜单就在右边。



Toolbar的最左边加入一个导航按钮，点击按钮也会将滑动菜单的内容展示出来。这样就相当于给用户提供了两种打开滑动菜单的方式。首先我准备了一张导航按钮的图标ic_menu.png，将它放在了drawable-xxhdpi目录下。然后修改MainActivity中的代码，如下所示：![image-20240212124100479](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212124100479.png)

![image-20240212124155704](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212124155704.png)



###### **NavigationView**

- 打开app/build.gradle文件，在dependencies闭包中添
  加如下内容：![image-20240212124301067](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240212124301067.png)

开始使用NavigationView之前，我们还需要准备好两个东西：menu和headerLayout。menu是用来在NavigationView中显示具体的菜单项的，headerLayout则是用来在NavigationView中显示头部布局的。

右击menu文件夹→New→Menu resourcefile，创建一个nav_menu.xml文件，并编写如下代码：![image-20240216125021365](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125021365.png)

接下来应该准备headerLayout了，我们就在headerLayout中放置头像、用户名、邮箱地址这3项内容吧。右击layout文件夹→New→Layout resource file，创建一个nav_header.xml文件。修改其中的代码，如下所示：![image-20240216125128739](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125128739.png)

我们终于可以使用NavigationView了。修改activity_main.xml中的代码，如下所示：![image-20240216125219759](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125219759.png)

修改MainActivity中的代码，如下所示：![image-20240216125330148](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125330148.png)

![image-20240216125339069](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125339069.png)

现在可以重新运行一下程序了，点击一下Toolbar左侧的导航按钮，效果如图12.8所示![image-20240216125408323](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125408323.png)



##### 悬浮按钮和可交互提示

###### **FloatingActionButton**

- 首先仍然需要提前准备好一个图标，这里我放置了一张ic_done.png到drawable-xxhdpi目录下。然后修改activity_main.xml中的代码，如下所示：![image-20240216125524366](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125524366.png)

![image-20240216125537380](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125537380.png)

现在我们就可以运行一下了，效果如图12.9所示

![image-20240216125608537](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125608537.png)

其实我们还可以指定FloatingActionButton的悬浮高度，如下所示：![image-20240216125649220](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125649220.png)

app:elevation属性给FloatingActionButton指定一个高度值。它和普通的Button其实没什么两样，都是调用setOnClickListener()方法来设置按钮的点击事件



###### **Snackbar**

- Snackbar的用法也非常简单，它和Toast是基本相似的，只不过可以额外增加一个按钮的点击事件。修改MainActivity中的代码，如下所示：![image-20240216125929552](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216125929552.png)

重新运行一下程序，并点击悬浮按钮，效果如图12.11所示![image-20240216130021956](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130021956.png)

Snackbar从屏幕底部出现了，上面有我们设置的提示文字，还有一个“Undo”按钮，按钮是可以点击的。过一段时间后，Snackbar会自动从屏幕底部消失。

这个Snackbar竟然将我们的悬浮按钮给遮挡住了。虽说也不是什么重大的问题，因为Snackbar过一会儿就会自动消失，但这种用户体验总归是不友好的。有没有什么办法能解决一下呢？当然有了，只需要借助CoordinatorLayout就可以轻松解决。



###### **CoordinatorLayout**

- CoordinatorLayout可以监听其所有子控件的各种事件，并自动
  帮助我们做出最为合理的响应。举个简单的例子，刚才弹出的Snackbar提示将悬浮按钮遮挡住了，而如果我们能让CoordinatorLayout监听到Snackbar的弹出事件，那么它会自动将内部的FloatingActionButton向上偏移，从而确保不会被Snackbar遮挡。
- 至于CoordinatorLayout的使用也非常简单，我们只需要将原来的FrameLayout替换一下就可以了。修改activity_main.xml中的代码，如下所示：![image-20240216130258453](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130258453.png)

![image-20240216130310211](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130310211.png)

现在重新运行一下程序，并点击悬浮按钮，效果如图12.12所示。![image-20240216130409355](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130409355.png)





##### 卡片式布局

###### **MaterialCardView**

- ![image-20240216130727831](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130727831.png)

这里定义了一个MaterialCardView布局，我们可以通过app:cardCornerRadius属性指定卡片圆角的弧度，数值越大，圆角的弧度也越大。另外，还可以通过app:elevation属性指定卡片的高度：高度值越大，投影范围也越大，但是投影效果越淡；高度值越小，投影范围也越小，但是投影效果越浓。

由于我们还需要用到RecyclerView，因此必须在app/build.gradle文件中声明库的依赖：![image-20240216130905629](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130905629.png)

接下来开始具体的代码实现，修改activity_main.xml中的代码，如下所示：![image-20240216130918942](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130918942.png)

![image-20240216130928881](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130928881.png)

接着定义一个实体类Fruit，代码如下所示：![image-20240216130942997](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130942997.png)

然后需要为RecyclerView的子项指定一个我们自定义的布局，在layout目录下新建fruit_item.xml，代码如下所示![image-20240216130956466](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216130956466.png)

![image-20240216131002974](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131002974.png)

接下来需要为RecyclerView准备一个适配器，新建FruitAdapter类，让这个适配器继承自RecyclerView.Adapter，并将泛型指定为FruitAdapter.ViewHolder，代码如下所示：![image-20240216131030560](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131030560.png)

上述代码相信你一定很熟悉，和我们在第4章中编写的FruitAdapter基本一模一样。唯一需要注意的是，在onBindViewHolder()方法中我们使用了Glide来加载水果图片

最后修改MainActivity中的代码，如下所示：![image-20240216131107389](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131107389.png)

现在重新运行一下程序，效果如图12.13所![image-20240216131139465](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131139465.png)



###### **AppBarLayout**

- AppBarLayout实际上是一个垂直方向的LinearLayout，它在内部做了很多滚动事件的封装，并应用了一些Material Design的设计理念。

- 修改activity_main.xml中的代码，如下所示：![image-20240216131250173](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131250173.png)

![image-20240216131300444](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131300444.png)

现在重新运行一下程序，你就会发现一切都正常了，如图12.14所示。![image-20240216131322692](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131322692.png)

当AppBarLayout接收到滚动事件的时候，它内部的子控件其实是可以指定如何去响应这些事件的，通过app:layout_scrollFlags属性就能实现。修改activity_main.xml中的代码，如下所示：![image-20240216131429397](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131429397.png)

这里在Toolbar中添加了一个app:layout_scrollFlags属性，并将这个属性的值指定成了scroll|enterAlways|snap。其中，scroll表示当RecyclerView向上滚动的时候，Toolbar会跟着一起向上滚动并实现隐藏；enterAlways表示当RecyclerView向下滚动的时候，Toolbar会跟着一起向下滚动并重新显示；snap表示当Toolbar还没有完全隐藏或显示的时候，会根据当前滚动的距离，自动选择是隐藏还是显示。

现在重新运行一下程序，并向上滚动RecyclerView，效果如图12.15所示。![image-20240216131521211](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131521211.png)



##### 下拉刷新

- SwipeRefreshLayout就是用于实现下拉刷新功能的核心类，我们把想要实现下拉刷新功能的控件放置到SwipeRefreshLayout中，就可以迅速让这个控件支持下拉刷新。那么在MaterialTest项目中，应该支持下拉刷新功能的控件自然就是RecyclerView了。
- 使用SwipeRefreshLayout之前首先需要在app/build.gradle文件中添加如下依赖：![image-20240216131620762](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131620762.png)

修改activity_main.xml中的代码，如下所示：![image-20240216131713851](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131713851.png)

![image-20240216131725010](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131725010.png)

由于RecyclerView现在变成了SwipeRefreshLayout的子控件，因此之前使用app:layout_behavior声明的布局行为现在也要移到SwipeRefreshLayout中才行。

不过这还没有结束，虽然RecyclerView已经支持下拉刷新功能了，但是我们还要在代码中处理具体的刷新逻辑才行。修改MainActivity中的代码，如下所示![image-20240216131852633](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131852633.png)

![image-20240216131900831](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216131900831.png)

通常情况下，当触发了下拉刷新事件，应该是去网络上请求最新的数据，然后再将这些数据展示出来。这里简单起见，我们就不和网络进行交互了，而是调用一个refreshFruits()方法进行本地刷新操作。refreshFruits()方法中先是开启了一个线程，然后将线程沉睡两秒钟。之所以这么做，是因为本地刷新操作速度非常快，如果不将线程沉睡的话，刷新立刻就结束了，从而看不到刷新的过程。沉睡结束之后，这里使用了runOnUiThread()方法将线程切换回主线程，然后调用initFruits()方法重新生成数据，接着再调用FruitAdapter的notifyDataSetChanged()方法通知数据发生了变化，最后调用SwipeRefreshLayout的setRefreshing()方法并传入false，表示刷新事件结束，并隐藏刷新进度条。

现在可以重新运行一下程序了，在屏幕的主界面向下拖动，会有一个下拉刷新的进度条出现，松手后就会自动进行刷新了，效果如图12.16所示。![image-20240216132116441](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132116441.png)



##### 可折叠式标题栏

###### **CollapsingToolbarLayout**

- CollapsingToolbarLayout是不能独立存在的，它在设计的时候就
  被限定只能作为AppBarLayout的直接子布局来使用。AppBarLayout
  又必须是CoordinatorLayout的子布局
- 首先我们需要一个额外的Activity作为水果的详情展示界面，右击com.example.materialtest包→New→Activity→Empty Activity，创建一个FruitActivity，并将布局名指定成activity_fruit.xml，然后我们开始编写水果详情展示界面的布局。
- 首先实现标题栏部分，这里使用CoordinatorLayout作为最外层布局，如下所示：![image-20240216132529382](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132529382.png)

![image-20240216132537823](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132537823.png)

接着我们在CoordinatorLayout中嵌套一个AppBarLayout，如下所示：![image-20240216132554333](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132554333.png)

接下来我们在AppBarLayout中再嵌套一个CollapsingToolbarLayout，如下所示：![image-20240216132608887](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132608887.png)

![image-20240216132616551](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132616551.png)

接下来，我们在CollapsingToolbarLayout中定义标题栏的具体内容，如下所示：![image-20240216132635777](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132635777.png)

![image-20240216132653487](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132653487.png)

下面开始编写水果内容详情部分。继续修改activity_fruit.xml中的代码，如下所示：![image-20240216132714220](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132714220.png)

![image-20240216132721329](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132721329.png)

不管是ScrollView还是NestedScrollView，它们的内部都只允许存在一个直接子布局。因此，如果我们想要在里面放入很多东西的话，通常会先嵌套一个LinearLayout，然后再在LinearLayout中放入具体的内容就可以了，如下所示：![image-20240216132813473](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132813473.png)

![image-20240216132822929](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132822929.png)

接下来在LinearLayout中放入具体的内容，这里我准备使用一个TextView来显示水果的内容详情，并将TextView放在一个卡片式布局当中，如下所示：![image-20240216132856216](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132856216.png)

![image-20240216132909463](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132909463.png)

为了做出示范，我就准备在activity_fruit.xml中加入一个悬浮按钮了。这个界面是一个水果详情展示界面，那么我就加入一个表示评论作用的悬浮按钮吧。首先需要提前准备好一个图标，这里我放置了一张ic_comment.png到drawable-xxhdpi目录下。然后修改activity_fruit.xml中的代码，如下所示：![image-20240216132947646](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132947646.png)

![image-20240216132956720](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216132956720.png)

接下来我们开始编写功能逻辑，修改FruitActivity中的代码，如下所示：![image-20240216133048163](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133048163.png)

![image-20240216133055597](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133055597.png)

其实还差最关键的一步，就是处理RecyclerView的点击事件，不然的话，我们根本就无法打开FruitActivity。修改FruitAdapter中的代码，如下所示：![image-20240216133146192](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133146192.png)

![image-20240216133154178](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133154178.png)

见证奇迹的时刻到了，现在重新运行一下程序，并点击界面上的任意一个水果，比如我点击了葡萄，效果如图12.17所示。![image-20240216133227077](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133227077.png)

我们尝试向上拖动水果内容详情，你会发现水果背景图上的标题会慢慢缩小，并且背景图会产生一些错位偏移的效果，如图12.18所示。![image-20240216133335606](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133335606.png)

继续向上拖动，直到标题栏变成完全折叠状态，效果如图12.19所示。![image-20240216133443071](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133443071.png)

可以看到，标题栏的背景图片不见了，悬浮按钮也自动消失了，现在水果标题栏变成了一个最普通的Toolbar。这是由于用户正在阅读具体的内容，我们需要给他们提供最充分的阅读空间。而如果这个时候向下拖动水果内容详情，就会执行一个完全相反的动画过程，最终恢复成图12.17的界面效果。



###### 充分利用系统状态栏空间

- 想要让背景图能够和系统状态栏融合，需要借助android:fitsSystemWindows这个属性来实现。在CoordinatorLayout、AppBarLayout、CollapsingToolbarLayout这种嵌套结构的布局中，将控件的android:fitsSystemWindows属性指定成true，就表示该控件会出现在系统状态栏里。对应到我们的程序，那就是水果标题栏中的ImageView应该设置这个属性了。不过只给ImageView设置这个属性是没有用的，我们必须将ImageView布局结构中的所有父布局都设置上这个属性才可以，修改activity_fruit.xml中的代码，如下所示：![image-20240216133730387](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133730387.png)

![image-20240216133741616](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133741616.png)

即使我们将android:fitsSystemWindows属性都设置好了也没有用，因为还必须在程序的主题中将状态栏颜色指定成透明色才行。指定成透明色的方法很简单，在主题中将android:statusBarColor属性的值指定成@android:color/transparent就可以了。打开res/values/styles.xml文件，对主题的内容进行修改，如下所示：![image-20240216133858618](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133858618.png)

![image-20240216133907224](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133907224.png)

还需要让FruitActivity使用这个主题才可以，修改AndroidManifest.xml中的代码，如下所示：![image-20240216133928889](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133928889.png)

现在重新运行MaterialTest程序，水果详情展示界面的效果就会如图12.20所示。![image-20240216133946988](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216133946988.png)



#### **Kotlin**课堂：编写好用的工具方法

###### 求**N**个数的最大最小值

- 我们之前在第7章的Kotlin课堂中学过vararg关键字，它允许
  方法接收任意多个同等类型的参数，正好满足我们这里的需求。那么我们就可以新建一个Max.kt文件，并在其中自定义一个max()函数，如下所示：![image-20240216134334542](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134334542.png)

这里max()函数的参数声明中使用了vararg关键字，也就是说现在它可以接收任意多个整型参数。接着我们使用了一个maxNum变量来记录所有数的最大值，并在一开始将它赋值成了整型范围的最小值。然后使用for-in循环遍历nums参数列表，如果发现当前遍历的数字比maxNum更大，就将maxNum的值更新成这个数，最终将maxNum返回即可。

现在就可以使用如下的写法来实现：![image-20240216134445921](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134445921.png)

- Java中规定，所有类型的数字都是可比较的，因此必须实现Comparable接口，这个规则在Kotlin中也同样成立。那么我们就可以借助泛型，将max()函数修改成接收任意多个实现Comparable接口的参数，代码如下所示：![image-20240216134538203](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134538203.png)

经过这样的修改之后，我们就可以更加灵活地使用max()函数了，比如说求3个浮点型数字的最大值，同样也变得轻而易举：![image-20240216134603744](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134603744.png)



###### 简化**Toast**的用法

- 首先回顾一下Toast的标准用法吧，如果想要在界面上弹出一段文字提示需要这样写：![image-20240216134722351](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134722351.png)

- 我们可以给String类和Int类各添加一个扩展函数，并在里面封装弹出Toast的具体逻辑。这样以后每次想要弹出Toast提示时，只需要调用它们的扩展函数就可以了。

  新建一个Toast.kt文件，并在其中编写如下代码：![image-20240216134807929](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134807929.png)

那么经过这样的扩展之后，我们以后在使用Toast时可以变得多么简单呢？体验一下就知道了，比如同样弹出一段文字提醒就可以这么写：![image-20240216134847657](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134847657.png)

如果你想弹出一个定义在strings.xml中的字符串资源，也非常简单，写法如下：![image-20240216134908299](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134908299.png)



我们在第2章学习Kotlin基础语法的时候，曾经学过给函数设定参数默认值的功能。只要借助这个功能，我们就可以在不增加showToast()函数使用复杂度的情况下，又让它可以支持动态指定显示时长了。修改Toast.kt中的代码，如下所示：![image-20240216134944365](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216134944365.png)

我们给showToast()函数增加了一个显示时长参数，但同时也给它指定了一个参数默认值。这样我们之前所使用的showToast()函数的写法将完全不受影响，默认会使用Toast.LENGTH_SHORT类型的显示时长。而如果你想要使用Toast.LENGTH_LONG的显示时长，只需要这样写就可以了：![image-20240216135050789](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135050789.png)



###### 简化**Snackbar**的用法

- 先来回顾一下Snackbar的常规用法吧，如下所示：![image-20240216135108904](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135108904.png)

- 由于make()方法接收一个View参数，Snackbar会使用这个View自动查找最外层的布局，用于展示Snackbar。因此，我们就可以给View类添加一个扩展函数，并在里面封装显示Snackbar的具体逻辑。新建一个Snackbar.kt文件，并编写如下代码：![image-20240216135243374](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135243374.png)

![image-20240216135250178](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135250178.png)

现在想要使用Snackbar显示一段文本提示，只需要这样写就可以了：![image-20240216135316942](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135316942.png)

我们可以让showSnackbar()函数再额外接收一个函数类型参数，以此来实现Snackbar的完整功能支持。修改Snackbar.kt中的代码，如下所示：![image-20240216135350998](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135350998.png)

![image-20240216135358516](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135358516.png)

这样showSnackbar()函数就拥有比较完整的Snackbar功能了，比如本小节最开始的那段示例代码，现在就可以使用如下写法进行实现：![image-20240216135425123](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216135425123.png)





#### **Jetpack**

- 简介![image-20240216184740524](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216184740524.png)

新建一个JetpackTest工程，然后开启我们的Jetpack探索之旅吧



##### **ViewModel**

- ViewModel的一个重要作用就是可以帮助Activity分担一部分工作，它是专门用于存放与界面相关的数据的。
- 当手机发生横竖屏旋转的时候，Activity会被重新创建，同时存放在Activity中的数据也会丢失。而ViewModel的生命周期和Activity不同，它可以保证在手机屏幕发生旋转的时候不会被重新创建，只有当Activity退出的时候才会跟着Activity一起销毁。因此，将与界面相关的变量存放在ViewModel当中，这样即使旋转手机屏幕，界面上显示的数据也不会丢失。ViewModel的生命周期如图13.2所示。![image-20240216185022231](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185022231.png)



###### **ViewModel**的基本用法

- 需要在app/build.gradle文件中添加如下依赖：![image-20240216185050058](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185050058.png)

- 比较好的编程规范是给每一个Activity和Fragment都创建一个对应的ViewModel，因此这里我们就为MainActivity创建一个对应的MainViewModel类，并让它继承自ViewModel，代码如下所示：![image-20240216185125698](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185125698.png)

这里我们要实现一个计数器的功能，就可以在ViewModel中加入一个counter变量用于计数，如下所示：![image-20240216185146869](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185146869.png)

现在我们需要在界面上添加一个按钮，每点击一次按钮就让计数器加1，并且把最新的计数显示在界面上。修改activity_main.xml中的代码，如下所示：![image-20240216185202100](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185202100.png)

接着我们开始实现计数器的逻辑，修改MainActivity中的代码，如下所示：![image-20240216185214666](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185214666.png)

我们绝对不可以直接去创建ViewModel的实例，而是一定要通过ViewModelProvider来获取ViewModel的实例，具体语法规则如下![image-20240216185236378](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185236378.png)

现在可以运行一下程序了，效果如图13.3所示。![image-20240216185301693](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185301693.png)

如果你尝试通过侧边工具栏旋转一下模拟器的屏幕，就会发现Activity虽然被重新创建了，但是计数器的数据却没有丢失，如图13.5所示。![image-20240216185322465](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185322465.png)



###### 向**ViewModel**传递参数

借助ViewModelProvider.Factory

- 修改MainViewModel中的代码，如下所示：![image-20240216185415889](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185415889.png)

新建一个MainViewModelFactory类，并让它实现ViewModelProvider.Factory接口，代码如下所示：![image-20240216185455472](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185455472.png)

另外，我们还得在界面上添加一个清零按钮，方便用户手动将计数器清零。修改activity_main.xml中的代码，如下所示：![image-20240216185541288](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185541288.png)

最后修改MainActivity中的代码，如下所示![image-20240216185551457](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185551457.png)

![image-20240216185558148](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185558148.png)

现在重新运行程序，点击数次“Plus One”按钮，然后退出程序并重新打开，你会发现，计数器的值是不会丢失的，如图13.6所示。![image-20240216185700470](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185700470.png)

只有点击“Clear”按钮，计数器的值才会被清零，你可以自己尝试一下。



##### **Lifecycles**

- Lifecycles组件就是为了解决这个问题而出现的，它可以让任何一个类都能轻松感知到Activity的生命周期，同时又不需要在Activity中编写大量的逻辑处理。
- 下面我们就通过具体的例子来学习Lifecycles组件的用法。新建一个MyObserver类，并让它实现LifecycleObserver接口，代码如下所示：![image-20240216185852403](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185852403.png)

LifecycleObserver是一个空方法接口，只需要进行一下接口实现声明就可以了，而不去重写任何方法。

接下来我们可以在MyObserver中定义任何方法，但是如果想要感知到Activity的生命周期，还得借助额外的注解功能才行。比如这里还是定义activityStart()和activityStop()这两个方法，代码如下所示：![image-20240216185933632](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185933632.png)	![image-20240216185939821](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216185939821.png)

代码写到这里还是无法正常工作的，因为当Activity的生命周期发生变化的时候并没有人去通知MyObserver，而我们又不想像刚才一样在Activity中去一个个手动通知。这个时候就得借助LifecycleOwner这个好帮手了，它可以使用如下的语法结构让MyObserver得到通知：![image-20240216190043108](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216190043108.png)

只要你的Activity是继承自AppCompatActivity的，或者你的Fragment是继承自androidx.fragment.app.Fragment的，那么它们本身就是一个LifecycleOwner的实例，这部分工作已经由AndroidX库自动帮我们完成了。也就是说，在MainActivity当中就可以这样写：![image-20240216190117019](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216190117019.png)![image-20240216190121991](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216190121991.png)

只要添加这样一行代码，MyObserver就能自动感知到Activity的生命周期了,不过目前MyObserver虽然能够感知到Activity的生命周期发生了变化，却没有办法主动获知当前的生命周期状态。要解决这个问题也不难，只需要在MyObserver的构造函数中将Lifecycle对象传进来即可，如下所示：![image-20240216190657671](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216190657671.png)

有了Lifecycle对象之后，我们就可以在任何地方调用lifecycle.currentState来主动获知当前的生命周期状态。

lifecycle.currentState返回的生命周期状态是一个枚举类型，一共有INITIALIZED、DESTROYED、CREATED、STARTED、RESUMED这5种状态类型，它们与Activity的生命周期回调所对应的关系如图13.8所示。![image-20240216190733274](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216190733274.png)





 

##### **LiveData**

- LiveData是Jetpack提供的一种响应式编程组件，它可以包含任何类型的数据，并在数据发生变化的时候通知给观察者。LiveData特别适合与ViewModel结合在一起使用，虽然它也可以单独用在别的地方，但是在绝大多数情况下，它是使用在ViewModel当中的。



###### **LiveData**的基本用法

- 修改MainViewModel中的代码，如下所示：![image-20240216191115372](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191115372.png)

接下来开始改造MainActivity，代码如下所示：![image-20240216191152346](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191152346.png)

![image-20240216191159306](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191159306.png)

lifecycle-livedata-ktx就是一个专门为Kotlin语言设计的库，这个库在2.2.0版本中加入了对observe()方法的语法扩展。我们只需要在app/build.gradle文件中添加如下依赖：![image-20240216191304471](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191304471.png)

然后就可以使用如下语法结构的observe()方法了：![image-20240216191314366](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191314366.png)

比较推荐的做法是，永远只暴露不可变的LiveData给外部。这样在非ViewModel中就只能观察LiveData的数据变化，而不能给LiveData设置数据。下面我们就看一下如何改造MainViewModel来实现这样的功能：![image-20240216191337218](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191337218.png)





###### **map**和**switchMap**

- 先来看map()方法，这个方法的作用是将实际包含数据的LiveData和仅用于观察数据的LiveData进行转换。那么什么情况下会用到这个方法呢？比如说有一个User类，User中包含用户的姓名和年龄，定义如下：![image-20240216191422668](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191422668.png)

我们可以在ViewModel中创建一个相应的LiveData来包含User类型的数据，如下所示：![image-20240216191435086](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191435086.png)

如果MainActivity中明确只会显示用户的姓名，而完全不关心用户的年龄，那么这个时候还将整个User类型的LiveData暴露给外部，就显得不那么合适了,而map()方法就是专门用于解决这种问题的，它可以将User类型的LiveData自由地转型成任意其他类型的LiveData，下面我们来看一下具体的用法：![image-20240216191545920](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191545920.png)

- 前面我们所学的所有内容都有一个前提：LiveData对象的实例都是在ViewModel中创建的。然而在实际的项目中，不可能一直是这种理想情况，很有可能ViewModel中的某个LiveData对象是调用另外的方法获取的。下面就来模拟一下这种情况，新建一个Repository单例类，代码如下所示：![image-20240216191643612](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191643612.png)

然后我们在MainViewModel中也定义一个getUser()方法，并且让它调用Repository的getUser()方法来获取LiveData对象：![image-20240216191705060](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191705060.png)

修改MainViewModel中的代码，如下所示：

![image-20240216191732135](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191732135.png)

![image-20240216191738294](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191738294.png)

为了让你能更清晰地理解switchMap()的用法，我们再来梳理一遍它的整体工作流程。首先，当外部调用MainViewModel的getUser()方法来获取用户数据时，并不会发起任何请求或者函数调用，只会将传入的userId值设置到userIdLiveData当中。一旦userIdLiveData的数据发生变化，那么观察userIdLiveData的switchMap()方法就会执行，并且调用我们编写的转换函数。然后在转换函数中调用Repository.getUser()方法获取真正的用户数据。同时，switchMap()方法会将Repository.getUser()方法返回的LiveData对象转换成一个可观察的LiveData对象，对于Activity而言，只要去观察这个LiveData对象就可以了。下面我们就来测试一下，修改activity_main.xml文件，在里面新增一个“Get User”按钮：![image-20240216191814789](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191814789.png)

![image-20240216191821982](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191821982.png)

然后修改MainActivity中的代码，如下所示：![image-20240216191830936](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191830936.png)

现在重新运行程序，并一直点击“Get User”按钮，你会发现界面上的数字会一直在变，如图13.9所示。这是因为我们传入的userId值是随机的，同时也说明switchMap()方法确实已经正常工作了。![image-20240216191903487](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216191903487.png)





##### **Room**

###### 使用**Room**进行增删改查

先来看一下Room的整体结构。它主要由Entity、Dao和Database这3部分组成，每个部分都有明确的职责，详细说明如下。

- Entity。用于定义封装实际数据的实体类，每个实体类都会在数据库中有一张对应的表，并且表中的列是根据实体类中的字段自动生成的。

- Dao。Dao是数据访问对象的意思，通常会在这里对数据库的各项操作进行封装，在实际编程的时候，逻辑层就不需要和底层数据库打交道了，直接和Dao层进行交互即可。

- Database。用于定义数据库中的关键信息，包括数据库的版本号、包含哪些实体类以及提供Dao层的访问实例



继续在JetpackTest项目上进行改造。首先要使用Room，需要在app/build.gradle文件中添加如下的依赖：![image-20240216192026705](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192026705.png)





##### **WorkManager**

###### **WorkManager**的基本用法

- 要想使用WorkManager，需要先在app/build.gradle文件中添加如下的依赖：![image-20240216192131223](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192131223.png)

- WorkManager的基本用法其实非常简单，主要分为以下3步：

- (1) 定义一个后台任务，并实现具体的任务逻辑；

  (2) 配置该后台任务的运行条件和约束信息，并构建后台任务请求；

  (3) 将该后台任务请求传入WorkManager的enqueue()方法中，系统会在合适的时间运行。

  第一步要定义一个后台任务，这里创建一个SimpleWorker类，代码如下所示：![image-20240216192158406](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192158406.png)

接下来可以进入第二步，配置该后台任务的运行条件和约束信息。![image-20240216192310110](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192310110.png)

PeriodicWorkRequest.Builder构造函数中传入的运行周期间隔不能短于15分钟，示例代码如下：![image-20240216192357315](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192357315.png)

最后一步，将构建出的后台任务请求传入WorkManager的enqueue()方法中，系统就会在合适的时间去运行了：![image-20240216192410975](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192410975.png)

- 现在我们来测试一下吧。首先在activity_main.xml中新增一个“Do Work”按钮，如下所示：![image-20240216192427398](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192427398.png)

接下来修改MainActivity中的代码，如下所示![image-20240216192437463](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192437463.png)



###### 使用**WorkManager**处理复杂的任务

- 首先从最简单的看起，让后台任务在指定的延迟时间后运行，只需要借助setInitialDelay()方法就可以了，代码如下所示：![image-20240216192501865](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192501865.png)

可以控制运行时间之后，我们再增加一些别的功能，比如说给后台任务请求添加标签：![image-20240216192515005](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192515005.png)

那么添加了标签有什么好处呢？最主要的一个功能就是我们可以通过标签来取消后台任务请求：![image-20240216192533877](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192533877.png)

除此之外，我们也可以使用如下代码来一次性取消所有后台任务请求：![image-20240216192550156](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192550156.png)

doWork()方法中返回Result.success()和Result.failure()又有什么作用？这两个返回值其实就是用于通知任务运行结果的，我们可以使用如下代码对后台任务的运行结果进行监听![image-20240216192645433](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192645433.png)

接下来，我们再来看一下WorkManager中比较有特色的一个功能——链式任务。假设这里定义了3个独立的后台任务：同步数据、压缩数据和上传数据。现在我们想要实现先同步、再压缩、最后上传的功能，就可以借助链式任务来实现，代码示例如下：![image-20240216192711585](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240216192711585.png)	

.

#### **Kotlin**课堂：使用**DSL**构建专有的语法结构

- DSL的全称是领域特定语言（Domain Specific Language），它是编程语言赋予开发者的一种特殊能力，通过它我们可以编写出一些看似脱离其原始语法结构的代码，从而构建出一种专有的语法结构。.
- 首先新建一个DSL.kt文件，然后在里面定义一个Dependency类，代码如下所示：![image-20240218153453559](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153453559.png)

接下来再定义一个dependencies高阶函数，代码如下所示：![image-20240218153509303](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153509303.png)

经过这样的DSL设计之后，我们就可以在项目中使用如下的语法结构了：

![image-20240218153529837](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153529837.png)

另外，我们也可以通过dependencies函数的返回值来获取所有添加的依赖库，代码如下所示：![image-20240218153543996](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153543996.png)

![image-20240218153552812](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153552812.png)



- 如果你了解一些前端开发的话，应该知道网页的展示都是由浏览器解析HTML代码来实现的。HTML中定义了很多标签，其中<table>标签用于创建一个表格，<tr>标签用于创建表格的行，<td>标签用于创建单元格。将这3种标签嵌套使用，就可以定制出包含任意行列的表格了。这里我们来做个实验吧，首先创建一个test.txt文件，并在其中编写如下HTML代码：![image-20240218153628103](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153628103.png)

![image-20240218153632174](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153632174.png)

这段代码会创建出一个两行三列的表格。那么要如何进行验证呢？很简单，修改一下文件的后缀名就可以了，这里将文件改名成test.html，然后双击文件，使用浏览器打开即可，效果如图13.16所示。

![image-20240218153657493](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153657493.png)

- 那么如果现在有一个需求，要求我们在Kotlin中动态生成表格所对应的HTML代码，你会怎么做呢？最简单直接的方式就是字符串拼接了，但是这种做法显然十分烦琐，而且字符串拼接的代码也难以阅读。

  这个时候DSL又可以大显身手了，借助DSL，我们可以以一种不可思议的语法结构来动态生成表格所对应的HTML代码，仍然是在DSL.kt文件中进行编写，首先定义一个Td类，代码如下所示：![image-20240218153736871](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153736871.png)

完成了Td类，接下来我们再定义一个Tr类，代码如下所示：![image-20240218153745774](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153745774.png)

定义好了Tr类之后，我们现在就可以使用如下的语法格式来构建表格中的一行数据：![image-20240218153803075](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153803075.png)

接下来继续对DSL进行完善，再定义一个Table类，代码如下所示：![image-20240218153823096](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153823096.png)

那么现在，我们就可以使用如下的语法结构来构建一个表格了：![image-20240218153842119](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153842119.png)

这段代码看上去已经相当不错了，不过这仍然不是最终版本，我们还可以再进一步对语法结构进行精简。定义一个table()函数，代码如下所示：![image-20240218153855971](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153855971.png)

编写了这么多代码之后，我们就可以使用如下神奇的语法结构来动态生成一个表格所对应的HTML代码了：![image-20240218153910913](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153910913.png)

.现在我们可以运行一下main()函数，结果如图13.17所示。![image-20240218153954883](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153954883.png)

另外，在DSL中也可以使用Kotlin的其他语法特性，比如通过循环来批量生成<tr>和<td>标签：![image-20240218153926665](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153926665.png)

最终的运行结果如图13.18所示。![image-20240218153940584](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153940584.png)





##### 全局获取**Context**的技巧

- Android提供了一个Application类，每当应用程序启动的时候，系统就会自动将这个类进行初始化。而我们可以定制一个自己的Application类，以便于管理程序内一些全局的状态信息，比如全局Context。

  定制一个自己的Application其实并不复杂，首先需要创建一个MyApplication类继承自Application，代码如下所示![image-20240218151128281](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151128281.png)

将Context设置成静态变量很容易会产生内存泄漏的问题，所以这是一种有风险的做法，因此Android Studio会给出如图14.1所示的警告提示![image-20240218151250733](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151250733.png)

但是由于这里获取的不是Activity或Service中的Context，而是Application中的Context，它全局只会存在一份实例，并且在整个应用程序的生命周期内都不会回收，因此是不存在内存泄漏风险的。那么我们可以使用如下注解，让Android Studio忽略上述警告提示：![image-20240218151314062](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151314062.png)

接下来我们还需要告知系统，当程序启动的时候应该初始化MyApplication类，而不是默认的Application类。这一步也很简单，在AndroidManifest.xml文件的<application>标签下进行指定就可以了，代码如下所示：![image-20240218151331123](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151331123.png)

这样我们就实现了一种全局获取Context的机制，之后不管你想在项目的任何地方使用Context，只需要调用一下MyApplication.context就可以了。



##### 使用**Intent**传递对象

###### **Serializable**方式

- Serializable是序列化的意思，表示将一个对象转换成可存储或可传输的状态。序列化后的对象可以在网络上进行传输，也可以存储到本地。至于序列化的方法非常简单，只需要让一个类去实现Serializable这个接口就可以了。

  比如说有一个Person类，其中包含了name和age这两个字段，如果想要将它序列化，就可以这样写：![image-20240218151934187](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151934187.png)

然后在FirstActivity中只需要这样写：![image-20240218151959898](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218151959898.png)

接下来在SecondActivity中获取这个对象也很简单，写法如下：![image-20240218152015348](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152015348.png)



###### **Parcelable**方式

- 除了Serializable之外，使用Parcelable也可以实现相同的效果，不过不同于将对象进行序列化，Parcelable方式的实现原理是将一个完整的对象进行分解，而分解后的每一部分都是Intent所支持的数据类型，这样就能实现传递对象的功能了。

下面我们来看一下Parcelable的实现方式，修改Person中的代码，如下所示：![image-20240218152105365](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152105365.png)

接下来，在FirstActivity中我们仍然可以使用相同的代码来传递Person对象，只不过在SecondActivity中获取对象的时候需要稍加改动，如下所示：![image-20240218152121551](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152121551.png)

不过，这种实现方式写起来确实比较复杂，为此Kotlin给我们提供了另外一种更加简便的用法，但前提是要传递的所有数据都必须封装在对象的主构造函数中才行。修改Person类中的代码，如下所示：![image-20240218152201641](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152201641.png)





##### 定制自己的日志工具

- 新建一个LogUtil单例类，代码如下所示：![image-20240218152416436](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152416436.png)

![image-20240218152423069](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152423069.png)

这样就把一个自定义的日志工具创建好了，之后在项目里，我们可以像使用普通的日志工具一样使用LogUtil。比如打印一行DEBUG级别的日志可以这样写![image-20240218152445126](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152445126.png)

打印一行WARN级别的日志可以这样写：![image-20240218152454044](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152454044.png)





##### 深色主题

- 右击res目录→New→Directory，创建一个values-v29目录，然后右击values-v29目录→New→Values resource file，创建一个styles.xml文件。接着对这个文件进行编写，代码如下所示![image-20240218152630007](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152630007.png)

现在重新运行MaterialTest项目，效果如图14.11所示。![image-20240218152652497](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152652497.png)



- 首先删除values-v29目录及其目录下的内

  容，然后修改values/styles.xml中的代码，如下所示：![image-20240218152732977](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152732977.png)

现在我们就可以重新运行一下程序，看看使用DayNight主题之后，MaterialTest项目默认的界面效果是什么样的，如图14.12所示。![image-20240218152803491](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152803491.png)

很明显，现在的界面比之前使用Force Dark转换后的界面要好看很多，至少卡片式布局的效果得到了保留。.

然而，虽然现在界面中的主要内容都已经自动切换成了深色主题，但是你会发现标题栏和悬浮按钮仍然保持着和浅色主题时一样的颜色。这是因为标题栏以及悬浮按钮使用的是我们定义在colors.xml中的几种颜色值，代码如下所示：![image-20240218152846512](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152846512.png)

这种指定颜色值引用的方式相当于对控件的颜色进行了硬编码，DayNight主题是不能对这些颜色进行动态转换的。好在解决方案也并不复杂，我们只需要进行一些主题差异型编程就可以了。右击res目录→New→Directory，创建一个values-night目录，然后右击values-night目录→New→Values resource file，创建一个colors.xml文件。接着在这个文件中指定深色主题下的颜色值，如下所示：![image-20240218152906283](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152906283.png)

现在重新运行一下程序，效果如图14.13所示。![image-20240218152916749](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218152916749.png)



##### **Kotlin**课堂：**Java**与**Kotlin**代码之间的转换

- 比如，下面是一段使用Java语言编写的代码：![image-20240218153052161](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153052161.png)

如果想要将这段代码转换成Kotlin版本，其实非常简单，只需要复制这段代码，然后在Android Studio中打开任意一个Kotlin文件，在这里进行粘贴，Android Studio就会弹出如图14.15所示的提示框。![image-20240218153106114](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153106114.png)

这个提示框在询问我们：即将粘贴的是一段Java代码，需要将它转换成Kotlin代码吗？点击“Yes”按钮，Android Studio就会帮我们自动进行代码转换，转换后的结果如图14.16所示。![image-20240218153120240](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153120240.png)

- 依靠这种自动转换工具只能实现基础版的Kotlin语法，细节方面的代码优化还是得靠我们手动完成。比如，使用如下代码来实现同样的功能明显是一种更好的写法：![image-20240218153149467](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153149467.png)

![image-20240218153155062](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153155062.png)

上述方法是将一段Java代码转换成Kotlin代码的方式。另外，我们还可以直接将一个Java文件以及其中的所有代码一次性转换成Kotlin版本。具体操作方法是，首先在Android Studio中打开该Java文件，然后点击导航栏中的Code→Convert Java File to Kotlin File，如图14.17所示。![image-20240218153225302](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20240218153225302.png)

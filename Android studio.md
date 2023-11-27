

## Android studio tips

- 如何在Android Studio中自动生成getter和setter 

  在编辑器中使用Alt + [Insert]

  - 没有圆角语句就在布局开头加
  
  ```
  xmlns:app="http://schemas.android.com/apk/res-auto"
  ```

![image-20231116215909753](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231116215909753.png)

圆角包裹

```
<androidx.cardview.widget.CardView
    android:layout_width="80dp"
    android:layout_height="80dp"
    app:cardCornerRadius="40dp">

<ImageView
    android:layout_width="80dp"
    android:layout_height="80dp"
    android:src="@drawable/qq20231110124608"
    ></ImageView>
    </androidx.cardview.widget.CardView>
```



- 隐藏密码

  android:inputType="textPassword"

- 格式化代码

  CTRL+alt+L
  
  - 颜色设置可以到 color hunt.co找
  
    然后到color.xml去定义
  
  - material组件

![image-20231119095759866](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231119095759866.png)

- 如何统一修改名称：

  双击 右键 ![image-20231122092636361](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231122092636361.png)

### 添加图片

![image-20231115095837643](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115095837643.png)

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115100036511.png)



方法二

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115145723843.png)

![image-20231115145748935](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115145748935.png)

**到****activity_main.xml****文件中设置图标**

![image-20231115150023495](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115150023495.png)

- **res目录**

1. 所有以drawable开头的文件夹都是用来放图片的
2. 所有以mipmap开头的文件夹都是用来放应用图标的
3. 所有以values开头的文件夹都是用来放字符串、样式、颜色等配置的
4. layout文件夹是用来放布局文件的

- ![image-20231108215014482](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231108215014482.png)

- nest.xml 嵌套布局

- 重用布局  

  用<include layout="@layout/nest"></include> 引用

### Android中的Cursor

1. 定义：Cursor就是[游标](https://so.csdn.net/so/search?q=游标&spm=1001.2101.3001.7020)，可以理解为我们在输入文本框闪烁的光标，标记我们要输入的位置
2. 

在我们查看网上的代码例子的时候会发现，使用它之前总会先执行这样一句代码

cursor.moveToNext()

或这样一句代码

cursor.moveToFirst()

在上文说到Cursor的作用就像是光标一样，用来标记我们获取数据的位置，然而刚获取到数据的时候指向的是索引为-1的数据。就像下图所示。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5f313eda67ae40779f7c6033d03ef820.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBATXQuZ2V0SW5zdGFuY2UoKQ==,size_14,color_FFFFFF,t_70,g_se,x_16)

- moveToFirst调用的是moveToPosition（0）
- moveToNext调用的是moveToPosition（mPos+1)
- 第一次调用的话，这两句话的意思是一样的（开始mPos=-1）。下面列举一些Cursor的常用方法

- close()：关闭游标，释放资源

- copyStringToBuffer(int columnIndex, CharArrayBuffer buffer)：在缓冲区中检索请求的列的文本，将将其存储

- getColumnCount()：返回所有列的总数

- getColumnIndex(String columnName)：返回指定列的名称，如果不存在返回-1

- getColumnIndexOrThrow(String columnName)：从零开始返回指定列名称，如果不存在将抛出IllegalArgumentException 异常。

- getColumnName(int columnIndex)：从给定的索引返回列名

- getColumnNames()：返回一个字符串数组的列名

- getCount()：返回Cursor 中的行数

- moveToFirst()：移动光标到第一行

- moveToLast()：移动光标到最后一行

- moveToNext()：移动光标到下一行

- moveToPosition(int position)：移动光标到一个绝对的位置

- moveToPrevious()：移动光标到上一行

  

### LitePal

初始化配置

添加版本号时报错

![image-20231113230520791](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231113230520791.png)

```
implementation ("org.litepal.guolindev:core:3.2.3")
```

![image-20231113230618641](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231113230618641.png)

```
google()
mavenCentral()
jcenter()
maven  (url="https://jitpack.io")
```



### Fragment

Fragment静态使用

1.创建一个Fragment

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210417155557120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xhZGlleg==,size_16,color_FFFFFF,t_70)

### ViewPager2

#### ViewPager+fragment 模拟微信首页

1.定义一个layout用于放置按钮

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115090831212.png)

创建layout

![image-20231115091002244](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115091002244.png)

修改布局为横向  height修改  background定义为gary（或者其他）（报红就创建一个gary.xml或者去color.xml去定义）

![image-20231115093916814](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115093916814.png)

到color.xml去定义颜色

![image-20231115094640805](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115094640805.png)



编写bottom.xml

![image-20231115094730522](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115094730522.png)



由于imageview需要用到点击和不点击时的图片，因此去drawable定义一个（tab_weixin）

![image-20231115094846648](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115094846648.png)

在定义的xml里写如图片

![image-20231115100808087](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115100808087.png)



把组合图片放入bottom.xml的image view的background 后面是drewable的名字

![image-20231115100951752](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115100951752.png)

第一栏编写完毕

![image-20231115101712778](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115101712778.png)



复制粘贴

修改   创建一个draw able目录下的tab_contact

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115150930786.png)

去阿里巴巴矢量图标库找图片加入

重复编辑item（drawable中完成）

![image-20231115154518126](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115154518126.png)



完成后回到bottom.xml 编写

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="horizontal"
    android:layout_width="match_parent"
    android:layout_height="55dp"
    android:background="@color/gray">

    <LinearLayout
        android:id="@+id/id_tab_weixin"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:layout_gravity="center"
        android:gravity="center"
        android:orientation="vertical">
        <ImageView
            android:id="@+id/tab_iv_weixin"
            android:layout_width="32dp"
            android:layout_height="32dp"
            android:background="@drawable/tab_weixin"></ImageView>
        <TextView
            android:id="@+id/text_weixin"
            android:layout_width="32dp"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="微信" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/id_tab_contact"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:layout_gravity="center"
        android:orientation="vertical">
        <ImageView
            android:id="@+id/tab_tv_contact"
            android:layout_width="32dp"
            android:layout_height="32dp"
            android:background="@drawable/tab_contact"></ImageView>
        <TextView
            android:id="@+id/text_contact"
            android:layout_width="48dp"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="通讯录" />
    </LinearLayout>
    <LinearLayout
        android:id="@+id/id_tab_find"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:layout_gravity="center"
        android:orientation="vertical">
        <ImageView
            android:id="@+id/tab_iv_find"
            android:layout_width="32dp"
            android:layout_height="32dp"
            android:background="@drawable/tab_find"></ImageView>
        <TextView
            android:id="@+id/text_find"
            android:layout_width="32dp"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="发现" />
    </LinearLayout>
    <LinearLayout
        android:id="@+id/id_tab_profile"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:gravity="center"
        android:layout_gravity="center"
        android:orientation="vertical">
        <ImageView
            android:id="@+id/tab_iv_profile"
            android:layout_width="32dp"
            android:layout_height="32dp"
            android:background="@drawable/tab_profile"></ImageView>
        <TextView
            android:id="@+id/text_profile"
            android:layout_width="32dp"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:text="我的" />
    </LinearLayout>
</LinearLayout>
```

效果如图![image-20231115154600787](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115154600787.png)



接着编辑源码，相应点击事件



在主函数中运行要在xml里加入include![image-20231115184450091](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115184450091.png)

运行时遇到一个错误，错吧imageview 的id号写成了linerlayout的id号，会导致将linearlayout类型视图强转为imageview导致报错

![image-20231115185732134](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115185732134.png)



出现这种情况报红是因为onClick里面的View v   外面也要是v   把v改为view就可以了

![image-20231115221637731](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231115221637731.png)



### Room

1.room是对sqlite的抽象封装

![image-20231117224739445](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231117224739445.png)



- new 一个类 Student  

![image-20231117225423336](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231117225423336.png)

![image-20231117225554726](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231117225554726.png)

- 加入@Entity  报错   要导入依赖库

  到build.gradle导入

![image-20231118103654697](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118103654697.png)

`/`/ 导入 Room 依赖库

implementation 'androidx.room:room-runtime:2.2.5'

// 导入注解处理器 ( Java )
    annotationProcessor 'androidx.room:room-compiler:2.2.5'`

这样导入会出错  根据新版的Android studio 应该如下

```
implementation("androidx.room:room-runtime:2.6.0")
annotationProcessor("androidx.room:room-compiler:2.6.0")
```

导入之后同步

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231117231215453.png)

- 定义id name  age  并用ALT+Inset 设置get and set

```
@Entity
public class Student {
    //主键唯一   (autoGenerate = true)表示主键自动增长  //@PrimaryKey主键的操作
    @PrimaryKey(autoGenerate = true)
    private  int id ;
    private  String name ;
    private   int  age  ;

    //写set和get函数给他暴露出去
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

为了更好的使用他 给他提供一个构造函数

![image-20231118110019693](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118110019693.png)

```
public Student(int id, String name, int age) {
    this.id = id;
    this.name = name;
    this.age = age;
}
```

为了更好的打印 可以来一个tostring

```
@Override
public String toString() {
    return "Student{" +
            "id=" + id +
            ", name='" + name + '\'' +
            ", age=" + age +
            '}';
}
```

这就是一张表

```
@Entity
public class Student {
    //主键唯一   (autoGenerate = true)表示主键自动增长  //@PrimaryKey主键的操作
    @PrimaryKey(autoGenerate = true)
    private  int id ;
    private  String name ;
    private   int  age  ;

    public Student(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    //写set和get函数给他暴露出去
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

- 对表进行增删改查 （Dao）

Dao不是一个类 而是一个interface接口

所以要把![image-20231118110708892](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118110708892.png)

改为![image-20231118110724769](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118110724769.png)

只需要面向一个Dao 就能增删改查

![image-20231118110822039](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118110822039.png)

```
@Dao//Database access object == 对表进行增删改查
public interface StudentDao {
    //增    写一个insertStudents函数    students是可变参数   要给他一个注解@Insert  这就能完成插入操作
    @Insert
    void  insertStudents(Student ... students);

    //改
    @Update
    void  updateStudents(Student... students);

    //删  条件
    @Delete
    void deleteStudents(Student ...  student);

    //删  所有       @Delete单个删除条件用     删除所有要用 @Query("DELETE FROM Student")
    @Query("DELETE FROM Student")
    void deleteAllStudents();

    //查  所有  涉及所有  用@Query   查询的时候需要根据表id倒序 就用  ORDER BY ID DESC
    @Query("SELECT * FROM Student ORDER BY ID DESC")
    List<Student> getAllStudent();
}
```



- Datebase

![image-20231118113225782](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118113225782.png)

```
//继承了extends RoomDatabase  之后要变成抽象函数
```

```
@Database(entities = {Student.class},version = 1) //注解要传参   记得输入版本号version = 1
public  abstract class StudentDatabase extends RoomDatabase {     //继承了extends RoomDatabase  之后要变成抽象函数
    //用户只需要操作dao  我们必须暴露dao   dao被用户拿到，就能对数据库增删改查
    public  abstract  StudentDao getStudentDao();


    //单例模式  返回 DB
    private  static   StudentDatabase  INSTANCE;
    static  synchronized   StudentDatabase getInstance(Context context){    //Context context 拿到当前的环境
        if (INSTANCE == null){   //context拿到一个环境  getApplicationContext保持环境的一致性   student database 数据库的名字     写完记得构建.build()
            INSTANCE = Room.databaseBuilder
                    (context.getApplicationContext(),StudentDatabase.class,"student database")
                    //如果我们想玩数据库  默认是异步线程
                    //慎用：强制开启 主线程  也可以操作数据库  （测试可以用  真是环境下不要用）
                  //  .allowMainThreadQueries()
                    .build();        //把他们换行了  可以写在一行
        }

        return  INSTANCE;
    }
}
```

![image-20231118115042295](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118115042295.png)

后面实战  要把这个改为 public



### Room实战

在room里来一个管理

![image-20231118114455800](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118114455800.png)

![image-20231118114521759](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118114521759.png)



1.在manager里面写一个引擎![image-20231118114559528](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118114559528.png)

![image-20231118114655233](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118114655233.png)



***这里遇到一个报错   static

![image-20231118153843668](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118153843668.png)

这个括号应该放在上面

![image-20231118153913538](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118153913538.png)





![image-20231118154130848](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118154130848.png)

完整部分（不包括import 上面）

```
//DB的引擎
public class DBEngine {
    private StudentDao   studentDao;
    public DBEngine(Context context){  //需要Context 环境
        StudentDatabase studentDatabase =StudentDatabase.getInstance(context);
        studentDao =  studentDatabase.getStudentDao();   //拿到dao
    }

   //dao增删改查

    //insert 插入
    public void  insertStudents(Student ... students) {
        new InsertAsyncTask(studentDao).execute(students);
    }
    //update 更新
    public  void  updateStudents(Student ... students){
        new  UpdateAsyncTask(studentDao).execute(students);
    }
    //delete 删除 条件
    public  void  deleteStudents(Student ... students){
        new  DeleteAsyncTask(studentDao).execute(students);
    }

    //delete 全部删除
    public  void  deleteAllStudents(Student ... students){
        new  DeleteAllAsyncTask(studentDao).execute();
    }

    //查询全部
    public  void  queryAllStudents(){
        new   QueryAllAsyncTask(studentDao).execute();
    }

        //如果我们想玩数据库  默认是异步线程  ========= 异步操作
        //insert 插入
        static class InsertAsyncTask extends AsyncTask<Student, Void, Void> {
            private StudentDao dao;
            public InsertAsyncTask(StudentDao studentDao) {
                dao =studentDao;
            }

            @Override     //重写异步操作
            protected Void doInBackground(Student... students) {
                dao.insertStudents(students);
                return null;
            }
        }

        //update更新
    static class  UpdateAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public UpdateAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }

        @Override     //重写异步操作
        protected Void doInBackground(Student... students) {
            dao.updateStudents(students);
            return null;
        }
    }

//delete 删除 条件
    static class DeleteAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public DeleteAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }
        @Override     //重写异步操作
        protected Void doInBackground(Student... students) {  //既然传递了student进来，就是条件删除
            dao.deleteStudents(students);
            return null;
        }
    }

//删除  全部删除
    static class DeleteAllAsyncTask extends AsyncTask<Void, Void, Void> { //全部删除全为空 void
        private StudentDao dao;
        public DeleteAllAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }
    @Override
    protected Void doInBackground(Void... voids) {
        dao.deleteAllStudents();
        return null;
    }
}
//全部 查询
   private static class QueryAllAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public QueryAllAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }

    @Override
    protected Void doInBackground(Student... students) {  //为什么不是 Void ... void
        List<Student>allStudent =dao.getAllStudent();
        //遍历全部查询的结构
        for (Student student :allStudent){
            Log.e("Derry","doInBackground:全部 查询 每一项:"+student.toString());
        }
        return null;

    }
}


}
```

2.回到为room创造的Activity 

修改布局

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity4">
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="插入"
        android:onClick="insertAction"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="修改"
        android:onClick="updateAction"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="删除"
        android:onClick="deleteAction"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="插入"
        android:onClick="queryAction"/>
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="全部删除"
        android:onClick="deleteAllAction"/>
</LinearLayout>
```

创建插入的函数

![image-20231118193148450](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118193148450.png)

写这个语句的时候  回到Student![image-20231118193659948](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118193659948.png)

![image-20231118193635552](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118193635552.png)

可以把id删掉  因为它是自增的

![image-20231118193734186](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118193734186.png)



还可以把这个删掉  不传也没关系

![image-20231118194225070](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118194225070.png)



删掉之后成这个

![image-20231118195109963](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118195109963.png)

但是不能这样写，直接全部注释掉

忘记加注解

![image-20231118195455866](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118195455866.png)



![image-20231118200553498](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118200553498.png)

```
public class MainActivity4 extends AppCompatActivity {
    private  DBEngine dbEngine ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main4);
        dbEngine =new DBEngine(this); //初始化   传入环境 context this
    }

    //插入
    public void insertAction(View view) {
        Student student1 =new Student("张三",20);
        Student student2 =new Student("李四",23);
        Student student3 =new Student("王五",27);
        dbEngine.insertStudents(student1,student2,student3);
    }
//修改   修改下标为3   修改成如下
    public void updateAction(View view) {
        Student student =new Student("李元霸",40);
        student.setId(3);
        dbEngine.updateStudents(student);
    }
//删除 条件  下标为3
    public void deleteAction(View view) {
        Student student =new Student(null,0);
        student.setId(3);
        dbEngine.deleteStudents();

    }
//查询
    public void queryAction(View view) {
        dbEngine.queryAllStudents();    //没有条件
    }
//全部删除
    public void deleteAllAction(View view) {
        dbEngine.deleteAllStudents();
    }
}
```



![image-20231118200616683](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231118200616683.png)

```
package com.example.myproject.room.manager;

import android.content.Context;
import android.os.AsyncTask;
import android.util.Log;

import com.example.myproject.room.Student;
import com.example.myproject.room.StudentDao;
import com.example.myproject.room.StudentDatabase;

import java.util.List;

//DB的引擎
public class DBEngine {
    //只要拿到dao  就能对数据库增删改查
    private StudentDao   studentDao;
    public DBEngine(Context context){  //需要Context 环境
        StudentDatabase studentDatabase =StudentDatabase.getInstance(context);
        studentDao =  studentDatabase.getStudentDao();   //拿到dao
    }

   //dao增删改查

    //insert 插入
    public void  insertStudents(Student ... students) {
        new InsertAsyncTask(studentDao).execute(students);
    }
    //update 更新
    public  void  updateStudents(Student ... students){
        new  UpdateAsyncTask(studentDao).execute(students);
    }
    //delete 删除 条件
    public  void  deleteStudents(Student ... students){
        new  DeleteAsyncTask(studentDao).execute(students);
    }

    //delete 全部删除
    public  void  deleteAllStudents(Student ... students){
        new  DeleteAllAsyncTask(studentDao).execute();
    }

    //查询全部
    public  void  queryAllStudents(){
        new   QueryAllAsyncTask(studentDao).execute();
    }

        //如果我们想玩数据库  默认是异步线程  ========= 异步操作
        //insert 插入
        static class InsertAsyncTask extends AsyncTask<Student, Void, Void> {
            private StudentDao dao;
            public InsertAsyncTask(StudentDao studentDao) {
                dao =studentDao;
            }

            @Override     //重写异步操作
            protected Void doInBackground(Student... students) {
                dao.insertStudents(students);
                return null;
            }
        }

        //update更新
    static class  UpdateAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public UpdateAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }

        @Override     //重写异步操作
        protected Void doInBackground(Student... students) {
            dao.updateStudents(students);
            return null;
        }
    }

//delete 删除 条件
    static class DeleteAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public DeleteAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }
        @Override     //重写异步操作
        protected Void doInBackground(Student... students) {  //既然传递了student进来，就是条件删除
            dao.deleteStudents(students);
            return null;
        }
    }

//删除  全部删除
    static class DeleteAllAsyncTask extends AsyncTask<Void, Void, Void> { //全部删除全为空 void
        private StudentDao dao;
        public DeleteAllAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }
    @Override
    protected Void doInBackground(Void... voids) {
        dao.deleteAllStudents();
        return null;
    }
}
//全部 查询
   private static class QueryAllAsyncTask extends AsyncTask<Student, Void, Void> {
        private StudentDao dao;
        public QueryAllAsyncTask(StudentDao studentDao) {
            dao =studentDao;
        }

    @Override
    protected Void doInBackground(Student... students) {  //为什么不是 Void ... void
        List<Student>allStudent =dao.getAllStudent();
        //遍历全部查询的结构
        for (Student student :allStudent){
            Log.e("Derry","doInBackground:全部 查询 每一项:"+student.toString());
        }
        return null;

    }
}


}
```



Can not extract resource from com.android.aaptcompiler.ParsedResource@32d026e5. 这个报错还没解决



#### databinding和viewbinding

- *****\*模块build.gradle\**文件\**android节点\**下添加如下代码****记得同步

```
android{
buildFeatures {

    viewBinding = true
    dataBinding = true
     }
}
```



## Floating action buttons

github

[material-components-android/docs/components/FloatingActionButton.md at master · material-components/material-components-android (github.com)](https://github.com/material-components/material-components-android/blob/master/docs/components/FloatingActionButton.md)

先把布局改了

```
androidx.coordinatorlayout.widget.CoordinatorLayout
```



### xml

```
android:text="@string/no_note"
android:visibility="gone"   //不显示
```

```
android:text="@string/no_note"
android:visibility="invisible"   //中间不显示
```

```
android:text="@string/no_note"
android:visibility="visible"    //中间显示
```



- ```
  android:clickable="true"  //可点击  点击由波纹效果
  ```

- `android:maxLines="2" //最多显示两行`	
  `android:ellipsize="end"  //超出用省略号表示`



#### 如何查看修改之前的代码（用于代码还原）

方法一：

![image-20231125195627293](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231125195627293.png)



方法二：

右键

![image-20231125195658958](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231125195658958.png)

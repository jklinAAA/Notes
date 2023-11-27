### layout-item_note

```
android:maxLines="2" //最多显示两行	
android:ellipsize="end"  //超出用省略号表示
```



- 使用app:icon="@drawable/delete_icon"

​       需要这个xmlns:app="http://schemas.android.com/apk/res-auto"



#### NoteAdapter

- 打印列表需要适配器

![](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121160609009.png)

```
package com.example.logintest14.Adapter;

import android.content.Context;
import android.content.DialogInterface;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import com.example.logintest14.Dao.NoteDao;
import com.example.logintest14.Entity.EntityNoteCard;
import com.example.logintest14.InitDataBase.InitDataBase;
import com.example.logintest14.R;
import com.example.logintest14.Util.UtilMethod;
import com.example.logintest14.fragment.NotePager.AddOrEditNoteActivity;
import com.google.android.material.card.MaterialCardView;
import com.google.android.material.dialog.MaterialAlertDialogBuilder;

import java.util.ArrayList;

public class NoteAdapter extends RecyclerView.Adapter<NoteAdapter.ViewHolder> {
    ArrayList<EntityNoteCard> list;  //列表
    Context context; //上下文
    int deletePosition;   //成员变量，删除的位置
    //删除数据库里卖弄的内容 需要
    InitDataBase initDataBase;
    NoteDao noteDao;
    //更新日记的数量
    CountListen countListen;

    public NoteAdapter(ArrayList<EntityNoteCard> list, Context context, CountListen countListen) {
        this.list = list;
        this.context = context;
        this.countListen = countListen;
        initDataBase = UtilMethod.getInstance(context); //初始化
        noteDao = initDataBase.noteDao();
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {  //创建一个ViewHolder 并返回   //视图绑定
        View view = LayoutInflater.from(context).inflate(R.layout.item_note, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull NoteAdapter.ViewHolder holder, int position) {
        if (position == holder.getLayoutPosition()) {
            holder.username.setText(list.get(position).getUsername());   //holder.username 拿到username控件
            // holder.username.setText(list.get(position).getUsername());
            holder.slogan.setText(list.get(position).getSlogan());
            holder.createTime.setText(list.get(position).getCreateTime());
            holder.title.setText(list.get(position).getTitle());
            holder.content.setText(list.get(position).getContent());
            //点击事件  删除
            holder.delete.setOnClickListener(view -> {
                new MaterialAlertDialogBuilder(context).setTitle("你想要删除这篇日记吗？").setPositiveButton("yes", (dialog, which) -> {
                    deletePosition = holder.getLayoutPosition();    //传值
                    deleteNote();
                }).setNegativeButton("no", null).show();
            });
            //修改的点击事件
            holder.itemCard.setOnClickListener(view->{
                Intent intent = new Intent(context, AddOrEditNoteActivity.class);
                intent.putExtra("isAdd",false);
                intent.putExtra("noteId",list.get(position).getNoteCardId()); //拿到一个CardId
                context.startActivity(intent);    //AddOrEditNoteActivity 默认是添加 不能直接到
            });
        }
    }

    private void deleteNote() {
        noteDao.deleteNoteById(list.get(deletePosition).getNoteCardId());    //删除数据库
        notifyItemRemoved(deletePosition);//通知list更新数据   只是删除了list里面的数据 并没有删除数据库里面的内容

        list.remove(deletePosition);        //删除list里面数据
        countListen.countListen(list.size());   //删除之后把size传进去

    }

    @Override
    public int getItemCount() {

        return list.size();
    }

    //视图绑定  对应那张图片
    public class ViewHolder extends RecyclerView.ViewHolder {
        MaterialCardView itemCard;
        ImageView userAvatar;
        TextView username;
        TextView slogan;
        TextView createTime;
        ImageView cover;
        TextView title;
        TextView content;
        Button delete;

        public ViewHolder(@NonNull View itemView) {

            super(itemView);
            itemCard = itemView.findViewById(R.id.item_card);
            userAvatar = itemView.findViewById(R.id.user_avatar);
            username = itemView.findViewById(R.id.username);
            slogan = itemView.findViewById(R.id.slogan);
            createTime = itemView.findViewById(R.id.create_time);
            cover = itemView.findViewById(R.id.cover);
            title = itemView.findViewById(R.id.title);
            content = itemView.findViewById(R.id.content);
            delete = itemView.findViewById(R.id.delete);

        }
    }

    public interface CountListen {
        void countListen(int count);
    }
}

```

![image-20231121210813979](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121210813979.png)

改为landa表达式

![image-20231121210838778](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121210838778.png)

![image-20231121210849907](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121210849907.png)

### EntityNoteCard

需要实体类对象渲染

![image-20231121161010231](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121161010231.png)

构造，get and set ， to string 三件套

```
package com.example.logintest14.Entity;

public class EntityNoteCard {
    long noteCardId;
    String username;
    String slogan;
    String userAvatar;
    String cover;
    String title;
    String content;
    String createTime;

    public EntityNoteCard() {
    }

    public EntityNoteCard(long noteCardId, String username, String slogan, String userAvatar, String cover, String title, String content, String createTime) {
        this.noteCardId = noteCardId;
        this.username = username;
        this.slogan = slogan;
        this.userAvatar = userAvatar;
        this.cover = cover;
        this.title = title;
        this.content = content;
        this.createTime = createTime;
    }

    public String getCreateTime() {
        return createTime;
    }

    public void setCreateTime(String createTime) {
        this.createTime = createTime;
    }

    public long getNoteCardId() {
        return noteCardId;
    }

    public void setNoteCardId(long noteCardId) {
        this.noteCardId = noteCardId;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getSlogan() {
        return slogan;
    }

    public void setSlogan(String slogan) {
        this.slogan = slogan;
    }

    public String getUserAvatar() {
        return userAvatar;
    }

    public void setUserAvatar(String userAvatar) {
        this.userAvatar = userAvatar;
    }

    public String getCover() {
        return cover;
    }

    public void setCover(String cover) {
        this.cover = cover;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    @Override
    public String toString() {
        return "EntityNoteCard{" +
                "noteCardId=" + noteCardId +
                ", username='" + username + '\'' +
                ", slogan='" + slogan + '\'' +
                ", userAvatar='" + userAvatar + '\'' +
                ", cover='" + cover + '\'' +
                ", title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}

```



- ![image-20231121205014708](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121205014708.png)

编写这个的时候R.id 报错

在开头导入

```
import com.example.logintest14.R;
```



### DiaryFragment

渲染主页



- 尝试用视图绑定 但是报错了不知道怎么回事（已经导入了依赖）


FragmentNoteBinding  noteBinding;   

noteBinding =FragmentNoteBinding.inflate(getLayoutInflater());

![image-20231121215328549](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231121215328549.png)

就先这样了

解决方法 ：FragmentNoteBinding  这个的意思是你的activity所对应的layout文件的名字的下划线命名改成驼峰命名，首字母要大写，最后加上一个Binding

![image-20231122092036153](C:\Users\30327\Desktop\image-20231122092036153.png)

- 我的文件是这样所以应该这样命名               FragmentDiary2Binding



- 写完之后打开发现没有渲染 

  应该在![image-20231122093523389](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231122093523389.png)

返回一个list.size 长度

```
package com.example.logintest14.fragment.NotePager;

import android.content.Intent;
import android.os.Bundle;

import androidx.fragment.app.Fragment;
import androidx.recyclerview.widget.LinearLayoutManager;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import com.example.logintest14.Adapter.NoteAdapter;
import com.example.logintest14.Dao.NoteDao;
import com.example.logintest14.Entity.EntityNote;
import com.example.logintest14.Entity.EntityNoteCard;
import com.example.logintest14.InitDataBase.InitDataBase;
import com.example.logintest14.R;
import com.example.logintest14.Util.UtilMethod;
import com.example.logintest14.databinding.FragmentDiary2Binding;

import java.util.ArrayList;
import java.util.List;


public class DiaryFragment extends Fragment {

    FragmentDiary2Binding binding;
    InitDataBase initDataBase;   //需要数据库的引用
    NoteDao noteDao;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        binding = FragmentDiary2Binding.inflate(getLayoutInflater());
        initMethod(); // 可以用接口回调？
         initList();
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
//        list.add(new EntityNoteCard(1,"czl","My SloganMy SloganMy Slogan",null,null,"The title",getString(R.string.item_content),getString(R.string.item_time)));
        //跳转表达式  加文本
        binding.floatingActionButton.setOnClickListener(view -> {
            startActivity(new Intent(getActivity(), AddOrEditNoteActivity.class));      //上下文 +要去的地方
        });
        return binding.getRoot();

    }

    private void initList() {
        List<EntityNote> localNote = getLocalNote();//查询
        if (localNote != null && localNote.size() > 0) {             //需要的是EntityNoteCard实体类 查询是EntityNote实体类  需要把后者转到前者
            ArrayList<EntityNoteCard> list = noteToCard(localNote);
            NoteAdapter noteAdapter = new NoteAdapter(list, getContext(), count -> {              //内部匿名接口  实现更新日记的数量
                binding.noteAlter.setText(getString(R.string.note_alter, count + ""));
            });
            binding.noteList.setAdapter(noteAdapter);            //渲染
            binding.noteList.setLayoutManager(new LinearLayoutManager(getContext(), LinearLayoutManager.VERTICAL, false));
            binding.noteAlter.setText(getString(R.string.note_alter, list.size() + ""));
        } else {
            binding.noNote.setVisibility(View.VISIBLE);
        }
    }

    private ArrayList<EntityNoteCard> noteToCard(List<EntityNote> list) {
        ArrayList<EntityNoteCard> cards = new ArrayList<>();
        for (EntityNote note : list) {   //到EntityNoteCard给一个无参构造            public EntityNoteCard() {}
            EntityNoteCard entityNoteCard = new EntityNoteCard();
            entityNoteCard.setNoteCardId(note.getNoteId());
            entityNoteCard.setContent(note.getNoteContent());
            entityNoteCard.setTitle(note.getNoteTitle());
            entityNoteCard.setCreateTime(note.getCreateTime());
            entityNoteCard.setCover(note.getNoteImageUrl());
            entityNoteCard.setUsername(getString(R.string.item_username));            //先写死 后面再改成动态
            entityNoteCard.setSlogan(getString(R.string.item_slogan));
            cards.add(entityNoteCard);

        }
        return cards;
    }

    private void initMethod() {
        initDataBase = UtilMethod.getInstance(getContext());
        noteDao = initDataBase.noteDao();
    }

    private List<EntityNote> getLocalNote() {
        List<EntityNote> allNote = noteDao.getAllNote();
        if (allNote.size() > 0) {
            return allNote;
        } else {
            return null;
        }

    }

    @Override
    public void onResume() {
        initList();
        super.onResume();
    }
}
```

### AddOrEditNoteActivity

xml：

文本可能会很长  用这个

![image-20231123104003874](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231123104003874.png)



class 

获取一个实体 room

```
package com.example.logintest14.fragment.NotePager;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.text.Editable;
import android.text.TextWatcher;

import com.example.logintest14.Dao.NoteDao;
import com.example.logintest14.Entity.EntityNote;
import com.example.logintest14.InitDataBase.InitDataBase;
import com.example.logintest14.R;
import com.example.logintest14.Util.UtilMethod;
import com.example.logintest14.databinding.ActivityAddOrEditNoteBinding;

import java.text.SimpleDateFormat;
import java.util.Date;

public class AddOrEditNoteActivity extends AppCompatActivity {
    ActivityAddOrEditNoteBinding binding;
    //获取实体类
    InitDataBase initDataBase;
    NoteDao noteDao;
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd:mm");
    String createTime;
    boolean isAdd = true;
    EntityNote note;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        binding = ActivityAddOrEditNoteBinding.inflate(getLayoutInflater());                  //binding赋值
        // setContentView(R.layout.activity_add_or_edit_note);     // 原来的
        setContentView(binding.getRoot());
        initMethod();  //初始化
        Intent intent = getIntent();
        if (!(intent != null && intent.getBooleanExtra("isAdd", true))) {
            isAdd = false;
            long noteId = intent.getLongExtra("noteId", -1);
            note = noteDao.getNoteById(noteId);
            binding.noteTitle.setText(note.getNoteTitle().length() > 0 ? note.getNoteTitle() : "");       //渲染
            binding.noteContent.setText(note.getNoteContent());
        }
        binding.closeButton.setOnClickListener(view -> {
            finish();
        });
        //保存  封装成一个方法
        binding.saveButton.setOnClickListener(view -> {
            saveNote();
        });
        binding.noteContent.addTextChangedListener(new TextWatcher() {      //日记总字数更新
            @Override
            public void beforeTextChanged(CharSequence s, int start, int count, int after) {

            }

            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
            }

            @Override
            public void afterTextChanged(Editable s) {
                binding.wordsCount.setText(getString(R.string.note_length, s.toString().toString().trim().length()));     //s是他给的参数
            }
        });
    }

    private void initMethod() {  //初始化
        createTime = simpleDateFormat.format(new Date(System.currentTimeMillis()));//成员变量给控件
        binding.createTime.setText(createTime);   //拿时间
        initDataBase = UtilMethod.getInstance(getApplicationContext());
        noteDao = initDataBase.noteDao();
        binding.wordsCount.setText(getString(R.string.note_length, 0));

    }

    private void saveNote() {
        if (isAdd) {
            if (binding.noteContent.getText().toString().trim().isEmpty()) {
                //getText() 内容   toString()整理成字符串trim()去除空字符   isEmpty()判断是否为空
                UtilMethod.showToast(getApplicationContext(), "Content is empty~");  //提示方法  内容为空
            } else {
                noteDao.insertNote(new EntityNote(6, binding.noteTitle.getText().toString().trim(), binding.noteContent
                        .getText().toString().trim(), null, createTime));
                UtilMethod.showToast(getApplicationContext(), "Save note success!");
                finish();
            }
        } else {        //编辑更新
            if (binding.noteContent.getText().toString().trim().isEmpty()) {
                //getText() 内容   toString()整理成字符串trim()去除空字符   isEmpty()判断是否为空
                UtilMethod.showToast(getApplicationContext(), "Content is empty~");  //提示方法  内容为空
            } else {
               String content = binding.noteContent.getText().toString().trim();
               note.setNoteContent(content);
              note.setNoteTitle(binding.noteTitle.getText().toString().trim().length()>0? binding.noteTitle.getText().toString().trim() :"");
              noteDao.updateNote(note);
                UtilMethod.showToast(getApplicationContext(), "保存成功!");
                finish();
            }
        }
    }
}
```

## 报错

-  Room cannot verify the data integrity. Looks like you've changed schema but forgot to update the version number. You can simply fix this by increasing the version number. Expected identity hash: 

修改了user数据![image-20231123223424256](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231123223424256.png)

忘记在版本号+1

![image-20231123223508119](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231123223508119.png)

```
package com.example.logintest14.InitDataBase;

import androidx.room.AutoMigration;
import androidx.room.Database;
import androidx.room.RenameTable;
import androidx.room.RoomDatabase;
import androidx.room.migration.AutoMigrationSpec;

import com.example.logintest14.Dao.NoteDao;
import com.example.logintest14.Entity.EntityNote;

@Database(
        version = 1,
        entities = {EntityNote.class},autoMigrations = {
//        @AutoMigration(from = 1, to = 2)
}
)
public abstract class InitDataBase extends RoomDatabase {
    public abstract NoteDao noteDao();
    @RenameTable(fromTableName = "User", toTableName = "AppUser")
    static class MyAutoMigration implements AutoMigrationSpec { }
}
```



### 图片

导入依赖

1.

```
implementation ( "com.github.bumptech.glide:glide:4.12.0")
```

2.

![image-20231124224737943](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124224737943.png)

给个id

![image-20231124225001433](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124225001433.png)

![image-20231124225638917](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124225638917.png)

也可以改为在线图片  去网页搜索任意一张图片，在新标签页中打开，复制图片的路径

![image-20231124230918289](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124230918289.png)

换到这个地方

![image-20231124230936592](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124230936592.png)

给联网权限（不然用不了网页图片）

![image-20231124231127415](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124231127415.png)



- 图片选择

  官方给了方法  [照片选择器  | Android 开发者  | Android Developers](https://developer.android.com/training/data-storage/shared/photopicker?hl=zh-cn)

  ![image-20231124231820353](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124231820353.png)

  ![image-20231124231901928](C:\Users\30327\AppData\Roaming\Typora\typora-user-images\image-20231124231901928.png)

### 导入的方法

报红可以用： 把光标放在报红位置  按住Alt+回车

### 【前言】

-  **授课内容**：Android开发基础：（基本控件+视图+Toast+监听器+适配器+布局）
- **Android**本意指“仿真机器人”，Google公司将Android的标识设计为一个绿色机器人， 表示Android系统符合环保概念，是一个轻薄短小，功能强大的移动系统，是第一个真正为手机打造的开放性系统。
- **Android系统是基于 <u>Linux</u> 平台开发的系统**

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230712171031890.png" alt="image-20230712171031890" style="zoom: 33%;" />



### 1. Android基本控件

#### 1.1 控件（Widget）

- 控件用于构建用户界面的可视元素，允许用户与应用程序进行交互并提供信息的展示。控件可以是按钮、文本框、滑块等等，它们通常用于用户界面的布局和用户输入的处理。
- 控件是由视图（View）类或其子类实现的，每个控件都有其特定的功能和外观。
- 控件可以在**XML布局文件**中声明，也可以在Java或Kotlin代码中动态创建和配置。
- 常见的Android控件包括：
  - TextView
  - EditText
  - Button
  - ImageButton
  - ImageView
  - CheckBox（复选框）
  - RadioButton（单选按钮）
  - ListView（列表视图）
  - RecyclerView（可循环视图）
  - ProgressBar（进度条）：[(83条消息) Android自定义ProgressBar的样式_android progressbar 自定义样式_殇神马的博客-CSDN博客](https://blog.csdn.net/mq2856992713/article/details/52372177)
  - SeekBar（拖动条）：[(83条消息) android学习SeekBar的使用和自定义样式_android seekbar 样式_qq_36699930的博客-CSDN博客](https://blog.csdn.net/qq_36699930/article/details/81742920)



#### 1.2 常见的控件及其使用方法

##### 1.2.1 TextView（文本视图）

用于显示文本内容，可以设置字体、颜色、大小等属性。

```xml
<TextView
    android:id="@+id/tv_name"		//控件的唯一标识符
    android:layout_width="wrap_content" //宽度
    android:layout_height="wrap_content"//高度
    android:layout_gravity="center"		//在父容器中的位置
    android:gravity="center"			//内容的对齐方式
   	android:text="姓名"				   //文本内容(1.文本 2.strings.xml中声明)
    android:textSize="20sp"				//字体大小		
    android:textStyle="bold"			//字体样式
    android:textColor="@color/black"	//字体颜色
    android:background="@drawable/background"//背景(需要先新建一个背景的xml文件)
	android:paddingLeft="20dp"			//左内边距
    android:paddingRight="20dp"			//右内边距
    android:paddingTop="5dp"			//上内边距
    android:paddingBottom="5dp"		//下内边距
	android:singleLine="true"  			//设置是否只在一行内显示全部内容
    app:layout_constraintBottom_toBottomOf="parent"//使用约束布局时，设置边界约束
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.2"	//使用约束布局时，设置距离水平边界的偏移比例
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

【gravity 和 layout_gravity 的区别】：

- `layout_gravity`用于控制控件**在父容器中**的位置和对齐方式。
- `gravity`用于控制控件内部**内容**的对齐方式。



【padding和margin的区别】：[android:padding和android:margin的区别 - 简书 (jianshu.com)](https://www.jianshu.com/p/ccedb1e609cd)

padding为内边距；margin为外边距。

安卓的view是一块矩形区域，padding是内边距，就是view（里面的内容）永远都至少和边界有一段设定好的距离。margin是外边距，就是外面的view无法完全靠近这个view的边界，至少要间隔一段设置好的距离。



【backgound和src的区别】：

src是图片内容（前景），bg是背景，可以同时使用,同时使用则src在前面，background在后，src会遮住background.



**【background.xml】**

```xml
<?xml version="1.0" encoding="utf-8"?>

<!-- rectangle表示为矩形 -->
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle" >

    <!-- 设置上下左右内边距
         top:上内边距
         bottom:下内边距
         left:左内边距
         right:右内边距
     -->
    <padding
        android:bottom="15dp"
        android:left="15dp"
        android:right="15dp"
        android:top="15dp"
        />

    <!-- 设置圆角矩形
         radius:圆角弧度，核心代码
    -->
    <corners android:radius="20dp" />

    <!-- 设置描边效果
         width:描边宽度
         color:描边颜色
     -->
    <stroke
        android:width="2px"
        android:color="@color/black" />

    <!-- 设置填充效果
         color:填充颜色
     -->
    <solid android:color="#FFFFFF" />

</shape>
```



##### 1.2.2 EditText（编辑文本框）

用于接收用户输入的文本内容。

```xml
<EditText
    android:id="@+id/edt_name"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="20sp"
    android:textStyle="italic"
    android:hint="Enter your name"		//设置提示文本
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.15"
    app:layout_constraintStart_toEndOf="@+id/textView"
    app:layout_constraintTop_toTopOf="parent" />
```

- 如果的文本是账号或密码，需要实现单行输入的功能，添加下面的属性：

  ```xml
  android:lines="1"
  android:inputType="text"
  ```

- 对于密码，需要添加password属性（后面还可以指定其他密码格式）

  ```xml
  android:password="true"
  ```



##### 1.2.3 Button（按钮）

用于触发某个操作或事件。

```xml
<Button
    android:id="@+id/bt_login"
    android:layout_width="265dp"
    android:layout_height="51dp"
    android:text="@string/login"
    android:textSize="18sp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.45"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/edt_name"
    app:layout_constraintVertical_bias="0.08" />
```

设置监听器：

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        //执行点击Button后的操作
    }
});
```

示例：（Toast+Intent）

```java
mbt_login.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        //实现页面跳转
        Intent intent = new Intent();
        intent.setClass(MainActivity.this,Todo.class);          //TODO: 跳转到 Todo页面
        startActivity(intent);

        //显示Toast提示消息
        Toast toast = Toast.makeText(MainActivity.this, "登录成功!", Toast.LENGTH_SHORT);
        toast.show();
    }
});
```



##### 1.2.4 ImageButton（图像按钮）

用于显示图标或图片，并响应用户的点击操作

```xml
<ImageButton
    android:id="@+id/ibt_register"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="@drawable/ic_register"		//ic_register导入的svg资源
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.791" />
```



##### 1.2.5 ImageView（图像视图）

用于显示图像资源。

```xml
<ImageView
    android:id="@+id/iv_bg"
    android:layout_width="match_parent"
    android:layout_height="240dp"
    android:src="@drawable/bg_img"	//指定ImageView显示的图像来源
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.0"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.0" />
```



##### 1.2.6 CheckBox（复选框）

用于选择多个选项。

```xml
<CheckBox
    android:id="@+id/cbox_item1"
    android:layout_width="263dp"
    android:layout_height="47dp"
    android:text="待办事项1"
    android:checked="true"/>	//设置默认选中
```

设置监听器：

```java
checkBox1 = findViewById(R.id.cbox_item1);

checkBox1.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        // 处理选中状态改变的事件
        if (isChecked) {
            Toast.makeText(Todo.this, "待办事项1完成！",Toast.LENGTH_SHORT);
        }
    }
}); 
```



##### 1.2.7 RadioButton（单选按钮）

用于从多个选项中选择一个。

```xml
<RadioGroup
    android:id="@+id/myRadioGroup"
    android:layout_width="290dp"
    android:layout_height="wrap_content"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.545"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.93">

    <RadioButton
        android:id="@+id/radioOption1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Option 1"
        tools:layout_editor_absoluteX="157dp"
        tools:layout_editor_absoluteY="635dp" />

   <RadioButton
        android:id="@+id/radioOption2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Option 2"
        tools:layout_editor_absoluteX="157dp"
        tools:layout_editor_absoluteY="635dp" />

</RadioGroup>
```

【RadioGroup】：

RadioGroup是Android中的一个容器控件，用于组织和管理一组RadioButton控件。它用于创建一组互斥的选择，只允许用户从中选择一个选项。

RadioGroup的特点：

- 互斥选择：当选中一个RadioButton时，其他RadioButton会自动取消选中。
- 单选组合：RadioGroup将一组RadioButton控件视为一个单元，只需为RadioGroup设置监听器即可监听用户的选择事件，而无需为每个RadioButton单独设置监听器。
- 默认选中：RadioGroup可以设置其中一个RadioButton作为默认选中项。



##### 1.2.8 ListView（列表视图）

以**可滚动**的列表的形式展示具体数据内容，并且能够根据数据的长度自适应屏幕显示。

```xml
<ListView
    android:id="@+id/lv_fruit"
    android:layout_width="350dp"
    android:layout_height="370dp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintVertical_bias="0.9" />
```

使用步骤：

（关于适配器）

```java
//1、定义对象
ListView listView;

//2、绑定控件
listView=(ListView) findViewById(R.id.list_view);
    
//准备ListView的数据
String[] data={"菠萝","芒果","石榴","葡萄", "苹果", "橙子", "西瓜"};

//创建适配器 连接数据源和控件的桥梁
//参数 1：当前的上下文环境
//参数 2：当前列表项所加载的布局文件
//(android.R.layout.simple_list_item_1)这里的布局文件是Android内置的，里面只有一个textview控件用来显示简单的文本内容
//参数 3：数据源
ArrayAdapter<String> adapter=new ArrayAdapter<>(Todo.this,android.R.layout.simple_list_item_1,data);

//将适配器加载到控件中
mListView.setAdapter(adapter);

//为列表中选中的项添加单击响应事件
mListView.setOnItemClickListener(new AdapterView.OnItemClickListener()
{
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int i, long l) {
        String result=((TextView)view).getText().toString();
        Toast.makeText(Todo.this,"您选择的水果是："+result,Toast.LENGTH_LONG).show();
    }
});
```



##### 1.2.9 RecyclerView（可循环视图）

用于显示大型数据集的列表或网格。

（1）创建RecyclerView布局：在布局文件中添加`RecyclerView`控件，用于显示整个列表

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ContactUI">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvContact"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

（2）再创建`RecyclerView`的列表项视图：新建一个`list_item.xml`文件，这是RecyclerView中每个项的外观

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/tv_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="29dp"
        android:layout_marginTop="33dp"
        android:text="联系人"
        android:textSize="18sp"
        android:padding="5dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/tv_phone"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:padding="5dp"
        android:text="电话"
        android:textSize="18sp"
        app:layout_constraintStart_toStartOf="@+id/tv_name"
        app:layout_constraintTop_toBottomOf="@+id/tv_name" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

（3）创建ViewHolder：为RecyclerView创建自定义ViewHolder类，用于管理和持有列表项视图的子视图元素。

**ViewHolder：**持有列表项布局中各个视图元素的引用，并在需要时将数据绑定到这些视图元素上，避免频繁地调用`findViewById`来查找和获取视图元素，从而提高了列表的滚动性能和效率

```java
class MyViewHolder extends RecyclerView.ViewHolder{
    TextView contact_name;
    TextView contact_phone_name;

    //构造函数
    public MyViewHolder(@NonNull View itemView){
        super(itemView);
        //通过调用super(itemView)，我们将传递给自定义ViewHolder类的构造函数的itemView参数传递给父类的构造函数，确保父类ViewHolder正确地初始化了ViewHolder对象的内部状态。
        //确保在自定义ViewHolder类中，可以正确地使用父类ViewHolder中提供的方法和属性，如getAdapterPosition()、getItemViewType()等，以及通过getItemView()访问根视图。

        contact_name = itemView.findViewById(R.id.tv_name);
        contact_phone_name = itemView.findViewById(R.id.tv_phone);
    }
}
```

（4）创建Adapter：为RecyclerView创建自定义Adapter类，用于管理数据源和将数据绑定到ViewHolder中的视图元素。

 `Adapter`：主要负责数据和视图之间的桥梁，用于管理和绑定数据到ViewHolder中的视图元素，并提供与RecyclerView的交互。MyAdapter表示使用的是自定义的Adapter类

```java
class MyAdapter extends RecyclerView.Adapter<MyViewHolder>{

    //TODO: onCreateViewHolder：创建RecyclerView的列表项视图
    @NonNull    //@NonNull是一个注解，用于在代码中标记参数、方法返回值或字段不应为null的情况。实现在静态代码分析工具的帮助下，捕获潜在的空指针异常问题
    @Override   //@Override是一个Java注解，用于标记方法覆盖（重写）父类或实现接口中的方法
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType){
        //通过View.inflate()方法将布局文件R.layout.list_item转换为View对象。R.layout.list_item用于指定ViewHolder将显示的视图布局
        View view = View.inflate(ContactUI.this,R.layout.list_item,null);
        MyViewHolder myViewHolder = new MyViewHolder(view); //将先前创建的View对象作为参数传递给构造函数
        return myViewHolder;
    }

    //TODO: onBindViewHolder: 绑定数据到ViewHolder中的视图元素。通过获取特定位置的Contact对象，并将其相应的数据设置到ViewHolder中的TextView视图元素上
    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder,int position){
        Contact contact = mContactList.get(position);
        holder.contact_name.setText(contact.contact_name);
        holder.contact_phone_name.setText(contact.contact_phone_number);
    }

    //TODO: getItemCount: 返回数据源的大小
    @Override
    public int getItemCount(){
        return mContactList.size();
    }
}
```

（5）初始化RecyclerView：

5.1：在相应的class中定义RecyclerView变量：RecyclerView mRecyclerView;

5.2：在Activity或Fragment中，找到RecyclerView并初始化它：findViewById

5.3：创建数据源：mContactList

5.4：实例化适配器，并将Adapter与RecyclerView关联：Adapter

5.5：设置布局管理器，指定RecyclerView的布局方式：layoutManager

```java
//定义RecyclerView变量
RecyclerView mRecyclerView;
//自定义适配器
MyAdapter mMyAdapter;
//定义数据源
List<Contact> mContactList = new ArrayList<>();

@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_contact_ui);

        mRecyclerView = findViewById(R.id.rvContact);

        //构造联系人列表数据源
        for(int i = 0; i < 20; i++){
            Contact contact = new Contact();
            contact.contact_name = "联系人" + i;
            contact.contact_phone_number = "123";
            mContactList.add(contact);
        }

        //实例化适配器
        mMyAdapter = new MyAdapter();
        //设置适配器
        mRecyclerView.setAdapter(mMyAdapter);
        //设置布局管理器，用于指定RecyclerView的布局方式
        LinearLayoutManager layoutManager = new LinearLayoutManager(ContactUI.this);
        mRecyclerView.setLayoutManager(layoutManager);

    }//onCreate
```





### 2. 布局（Layout）

#### 2.1 布局

- 布局是用于定义界面中控件和视图的位置和大小的方式，描述了界面的结构和组织。
- **布局文件以`.xml`结尾，存放在`res/layout`目录下**
- 常用布局：


1. LinearLayout（线性布局）
2. RelativeLayout（相对布局）
3. ConstraintLayout（约束布局）
4. FrameLayout（帧布局）
5. GridLayout（网格布局）



#### 2.2 常用布局

##### 2.2.1 LinearLayout（线性布局）

按照水平或垂直方向线性排列控件，可以设置**权重属性**来控制控件的相对大小。

```xml
<LinearLayout
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.336"
    app:layout_constraintVertical_bias="0.07"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="2dp"
        android:padding="10dp"
        android:text="待办列表"
        android:textSize="20sp"
        android:weight
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.109"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.044" />

    <CheckBox
        android:id="@+id/cbox_item1"
        android:layout_width="301dp"
        android:layout_height="49dp"
        android:checked="true"
        android:text="待办事项1"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.309"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.115" />

    <CheckBox
        android:id="@+id/cbox_item2"
        android:layout_width="298dp"
        android:layout_height="48dp"
        android:text="待办事项2"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.3"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.185" />
</LinearLayout>
```

注意事项：

- `android:orientation`属性决定了布局的方向，可以是`vertical`（垂直）或`horizontal`（水平）。
- 使用`android:layout_weight`属性可以控制子控件的权重，以实现灵活的布局。



##### 2.2.2 RelativeLayout（相对布局）

通过相对于其他控件或父容器的位置关系来摆放控件，可以灵活地调整控件的位置。

```xml
<RelativeLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello" />

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me"
        android:layout_below="@id/textView1" />

</RelativeLayout>
```

注意事项：

- 使用`android:layout_alignParent...`属性可以设置控件相对于父容器的位置关系。
- 使用`android:layout_...To...Of`属性可以设置控件相对于其他控件的位置关系。



##### 2.2.3 ConstraintLayout（约束布局）

使用约束关系来定义控件之间的位置和相对大小，适用于复杂布局和适配不同屏幕尺寸的场景。

```xml
<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me"
        app:layout_constraintTop_toBottomOf="@id/textView1"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

注意事项：

- 使用`app:layout_constraint...`属性可以设置控件之间的约束关系。
- 注意避免出现循环约束和不完整约束的情况，以确保布局的正确性。

【layout_constraintDimensionRatio】：设定长宽比，可以通过设定某一边的长度，来限制另一边的长度



##### 2.2.4 FrameLayout（帧布局）

控件按照层叠的方式排列，后面的控件会覆盖前面的控件，这种显示方式有些类似于堆栈，适用于简单布局和单个控件的情况。

```xml
<FrameLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:src="@drawable/bg_img" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Overlay Text"
        android:layout_gravity="center" />

</FrameLayout>
```

注意事项：

- 子控件会按照添加的顺序进行层叠，后面的控件会覆盖前面的控件。
- 当我们往里面添加控件的时候,会默认把他们放到这块区域的左上角，可以通过layout_gravity属性，指定到其他的位置
- 布局的大小由控件中最大的子控件决定，如果控件的大小一样大的话，那么同一时刻就只能看到最上面的那个组件



##### 2.2.5 GridLayout（网格布局）

按照行列的网格方式排列控件，可以自定义行数、列数和控件之间的间隔。

```xml
<GridLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:columnCount="2">

    <Button
        android:text="Button 1" />

    <Button
        android:text="Button 2" />

    <Button
        android:text="Button 3" />

    <Button
        android:text="Button 4" />

</GridLayout>
```

注意事项：

- 使用`android:columnCount`属性设置**列数**，可以根据需要自定义网格的列数。
- 子控件会按照添加的顺序自动填充到网格中的对应位置。



### 3. 视图（View ）

- **Android 所有的控件和布局都有着一个父类：View** 
- Anroid 通过**继承**的方式，对父类控件进行继承，由此来在父类基础上创造新的控件。


下图是View的主要**继承关系**：

![image-20231004213451549](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231004213451549.png)

- View更完整的继承体系可参见下面这篇博客：

【[(78条消息) Android View的继承体系大全（包含125个view的所有子类）（by 星空武哥）_星空武哥的博客-CSDN博客](https://blog.csdn.net/lsyz0021/article/details/53144273)】



### 4. Toast

Toast是Android中的**消息提示**组件。

使用Toast的基本步骤：

1. 获取当前的上下文（Context）对象。上下文可以是Activity、Service、Application等。

2. 创建Toast对象，并设置要显示的消息内容和持续时间：
   ```java
   Toast toast = Toast.makeText(context, message, duration);
   ```

   - `context`：上下文对象，用于指定Toast显示的上下文环境。
   - `message`：要显示的消息内容，可以是字符串或字符序列。
   - `duration`：Toast的持续时间，可以是`Toast.LENGTH_SHORT`（短暂显示）或`Toast.LENGTH_LONG`（稍长时间显示）。

3. 可选：设置Toast的位置：
   ```java
   toast.setGravity(gravity, xOffset, yOffset);
   ```

   - `gravity`：Toast的位置，可以是`Gravity.TOP`、`Gravity.BOTTOM`、`Gravity.CENTER`等。
   - `xOffset`：Toast在x轴上的偏移量。
   - `yOffset`：Toast在y轴上的偏移量。

4. 调用`show()`方法显示Toast：
   ```java
   toast.show();
   ```

   通过调用`show()`方法，Toast会在屏幕上显示出来。

【使用示例】：
```java
// 登录成功后显示一个短暂的Toast提示消息
Toast toast = Toast.makeText(MainActivity.this, "登录成功!", Toast.LENGTH_SHORT);
toast.show();
```

- 定制Toast：[2.5.7 Toast(吐司)的基本使用 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/android-tutorial-toast.html#:~:text=2.5.7 Toast (吐司)的基本使用 1 1.直接调用Toast类的makeText ()方法创建 这是我们用的最多的一种形式了！ 比如点击一个按钮，然后弹出Toast，用法：,： ... 3 3.示例代码下载 ToastDemo.zip 本节小结： 好的，本节给大家讲解了Toast的基本使用，以及如何自定义Toast，非常简单，大家可以在实际开发中对自己的Toast进行定制~ )



### 5. 监听器（Listener）

监听器是一种用于监听和响应用户交互事件的机制。通过监听器，可以捕获用户的操作，并执行相应的逻辑或处理。

常见的监听器：

1. OnClickListener（点击监听器）：用于捕获View的点击事件。
   ```java
   Button button = findViewById(R.id.button);
   button.setOnClickListener(new View.OnClickListener() {
       @Override
       public void onClick(View v) {
           // 处理点击事件
       }
   });
   ```

2. OnLongClickListener（长按监听器）：用于捕获View的长按事件。
   ```java
   Button button = findViewById(R.id.button);
   button.setOnLongClickListener(new View.OnLongClickListener() {
       @Override
       public boolean onLongClick(View v) {
           // 处理长按事件
           return true; // 返回true表示事件已消费，不再触发其他事件
       }
   });
   ```

3. TextWatcher（文本改变监听器）：用于捕获EditText中文本的变化事件。
   ```java
   EditText editText = findViewById(R.id.editText);
   editText.addTextChangedListener(new TextWatcher() {
       @Override
       public void beforeTextChanged(CharSequence s, int start, int count, int after) {
           // 文本改变前执行
       }
   
       @Override
       public void onTextChanged(CharSequence s, int start, int before, int count) {
           // 文本改变时执行
       }
   
       @Override
       public void afterTextChanged(Editable s) {
           // 文本改变后执行
       }
   });
   ```

4. AdapterView.OnItemClickListener（列表项点击监听器）：用于捕获ListView或GridView等列表视图中列表项的点击事件。
   ```java
   ListView listView = findViewById(R.id.listView);
   listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
       @Override
       public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
           // 处理列表项点击事件
       }
   });
   ```

5. SeekBar.OnSeekBarChangeListener（拖动条改变监听器）：用于捕获SeekBar拖动条的值变化事件。
   ```java
   SeekBar seekBar = findViewById(R.id.seekBar);
   seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
       @Override
       public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
           // 值变化时执行
       }
   
       @Override
       public void onStartTrackingTouch(SeekBar seekBar) {
           // 开始拖动时执行
       }
   
       @Override
       public void onStopTrackingTouch(SeekBar seekBar) {
           // 停止拖动时执行
       }
   });
   ```

6. CheckBox.setOnCheckedChangeListener（复选框状态监听器）：用于捕获复选框的选择状态发生改变的事件。

   ```java
   CheckBox checkBox = findViewById(R.id.checkBox);
   checkBox.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
       @Override
       public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
           // 处理选择状态改变事件
           if (isChecked) {
               // 复选框被选中
           } else {
               // 复选框未选中
           }
       }
   });
   ```




### 6. 适配器（Adapter）

#### 6.1 适配器

- 适配器是一种连接数据和界面元素的桥梁，负责将数据源中的数据逐个绑定到界面上的视图元素，例如ListView、RecyclerView等。

- 常见适配器：


1. ArrayAdapter

2. BaseAdapter

3. RecyclerView.Adapter

- 适配器的基本使用流程：


1. 准备数据源：可以是数组、列表、数据库等数据集合。

2. 创建适配器：根据实际需求，选择合适的适配器，并实例化一个适配器对象。

3. 绑定适配器：将适配器对象绑定到要显示数据的控件上，如ListView、RecyclerView等。

4. 可选：自定义适配器的布局和样式：根据需求，可以自定义适配器的布局文件或视图。

5. 可选：设置事件监听器：根据需要，可以为适配器的视图元素设置点击事件、选择事件等监听器。



#### 6.2 常见的适配器

##### 6.2.1 ArrayAdapter

用于将数据源中的数据逐个地绑定到ListView、Spinner等控件上。

示例：

```java
String[] data = { "Item 1", "Item 2", "Item 3" };
ArrayAdapter<String> adapter = new ArrayAdapter<>(context, android.R.layout.simple_list_item_1, data);
listView.setAdapter(adapter);
```

以上示例中，使用ArrayAdapter将一个String数组中的数据绑定到ListView上，使用了Android内置的simple_list_item_1布局作为列表项的布局。



##### 6.2.2 BaseAdapter

通过继承BaseAdapter来创建自定义的适配器，实现更复杂的数据绑定逻辑。

```java
public class MyAdapter extends BaseAdapter {
    // 自定义适配器的实现
}
```

示例：

```java
public class MyAdapter extends BaseAdapter {
    private List<Item> itemList;
    private LayoutInflater inflater;

    public MyAdapter(Context context, List<Item> itemList) {
        this.itemList = itemList;
        inflater = LayoutInflater.from(context);
    }

    @Override
    public int getCount() {
        return itemList.size();
    }

    @Override
    public Object getItem(int position) {
        return itemList.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View view = convertView;
        ViewHolder holder;

        if (view == null) {
            view = inflater.inflate(R.layout.list_item, parent, false);
            holder = new ViewHolder();
            holder.textView = view.findViewById(R.id.text_view);
            view.setTag(holder);
        } else {
            holder = (ViewHolder) view.getTag();
        }

        Item item = itemList.get(position);
        holder.textView.setText(item.getName());

        return view;
    }

    private static class ViewHolder {
        TextView textView;
    }
}
```

以上示例中，自定义了一个BaseAdapter的子类MyAdapter，重写了相关方法来实现对数据源的管理和视图元素的绑定。



##### 6.2.3 RecyclerView.Adapter

用于将数据源中的数据逐个地绑定到RecyclerView的列表项上。

```java
public class MyAdapter extends RecyclerView.Adapter<MyViewHolder> {
    // 自定义RecyclerView适配器的实现
}
```

示例：

```java
package com.example.myapplication9;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.GridLayoutManager;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.LinearLayout;
import android.widget.TextView;

import java.util.ArrayList;
import java.util.List;

public class ContactUI extends AppCompatActivity {

    //定义
    RecyclerView mRecyclerView;
    //自定义适配器
    MyAdapter mMyAdapter;
    //定义数据源
    List<Contact> mContactList = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_contact_ui);

        mRecyclerView = findViewById(R.id.rvContact);

        //构造联系人列表数据源
        for(int i = 0; i < 20; i++){
            Contact contact = new Contact();
            contact.contact_name = "联系人" + i;
            contact.contact_phone_number = "123";
            mContactList.add(contact);
        }

        //实例化适配器
        mMyAdapter = new MyAdapter();
        //设置适配器
        mRecyclerView.setAdapter(mMyAdapter);
        //设置布局管理器，用于指定RecyclerView的布局方式
        LinearLayoutManager layoutManager = new LinearLayoutManager(ContactUI.this);
        mRecyclerView.setLayoutManager(layoutManager);

    }//onCreate

    //TODO: ViewHolder主要负责持有和管理列表项视图的子视图元素，用于优化列表项的性能。MyViewHolder表示使用的是自定义的ViewHolder类
    class MyViewHolder extends RecyclerView.ViewHolder{
        TextView contact_name;
        TextView contact_phone_name;

        //构造函数
        public MyViewHolder(@NonNull View itemView){
            super(itemView);
            //通过调用super(itemView)，我们将传递给自定义ViewHolder类的构造函数的itemView参数传递给父类的构造函数，确保父类ViewHolder正确地初始化了ViewHolder对象的内部状态。
            //确保在自定义ViewHolder类中，可以正确地使用父类ViewHolder中提供的方法和属性，如getAdapterPosition()、getItemViewType()等，以及通过getItemView()访问根视图。

            contact_name = itemView.findViewById(R.id.tv_name);
            contact_phone_name = itemView.findViewById(R.id.tv_phone);
        }
    }

    //TODO: Adapter主要负责数据和视图之间的桥梁，用于管理和绑定数据到ViewHolder中的视图元素，并提供与RecyclerView的交互。MyAdapter表示使用的是自定义的Adapter类
    class MyAdapter extends RecyclerView.Adapter<MyViewHolder>{

        //TODO: onCreateViewHolder：创建RecyclerView的列表项视图
        @NonNull    //@NonNull是一个注解，用于在代码中标记参数、方法返回值或字段不应为null的情况。实现在静态代码分析工具的帮助下，捕获潜在的空指针异常问题
        @Override   //@Override是一个Java注解，用于标记方法覆盖（重写）父类或实现接口中的方法
        public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType){
            //通过View.inflate()方法将布局文件R.layout.contact_list转换为View对象。R.layout.contact_list用于指定ViewHolder将显示的视图布局
            View view = View.inflate(ContactUI.this,R.layout.list_item,null);
            MyViewHolder myViewHolder = new MyViewHolder(view); //将先前创建的View对象作为参数传递给构造函数
            return myViewHolder;
        }

        //TODO: onBindViewHolder: 绑定数据到ViewHolder中的视图元素。通过获取特定位置的Contact对象，并将其相应的数据设置到ViewHolder中的TextView视图元素上
        @Override
        public void onBindViewHolder(@NonNull MyViewHolder holder,int position){
            Contact contact = mContactList.get(position);
            holder.contact_name.setText(contact.contact_name);
            holder.contact_phone_name.setText(contact.contact_phone_number);
        }

        //TODO: getItemCount: 返回数据源的大小
        @Override
        public int getItemCount(){
            return mContactList.size();
        }
    }
}
```



### 【附录】

- [iconfont-阿里巴巴矢量图标库](https://www.iconfont.cn/)

- ProgressBar：[(83条消息) Android自定义ProgressBar的样式_android progressbar 自定义样式_殇神马的博客-CSDN博客](https://blog.csdn.net/mq2856992713/article/details/52372177)
- SeekBar：[(83条消息) android学习SeekBar的使用和自定义样式_android seekbar 样式_qq_36699930的博客-CSDN博客](https://blog.csdn.net/qq_36699930/article/details/81742920)
- View更完整的继承体系：[(78条消息) Android View的继承体系大全（包含125个view的所有子类）（by 星空武哥）_星空武哥的博客-CSDN博客](https://blog.csdn.net/lsyz0021/article/details/53144273)

- 定制Toast：[2.5.7 Toast(吐司)的基本使用 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/android-tutorial-toast.html#:~:text=2.5.7 Toast (吐司)的基本使用 1 1.直接调用Toast类的makeText ()方法创建 这是我们用的最多的一种形式了！ 比如点击一个按钮，然后弹出Toast，用法：,： ... 3 3.示例代码下载 ToastDemo.zip 本节小结： 好的，本节给大家讲解了Toast的基本使用，以及如何自定义Toast，非常简单，大家可以在实际开发中对自己的Toast进行定制~ )

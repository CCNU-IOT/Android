## Android开发中Ability间的通信问题

Android开发中常常需要进行`Ability`间的通信，比如在一个`Activity`中访问另一个`Activity`中的变量。通常使用以下3种机制实现不同`Ability`间的通信：

1. 使用消息通信机制
2. 使用数据存储机制
3. 使用数据接口机制

本文将根据上面3种机制介绍6种Android开发中用于Ability间通信的解决办法：

1. 基于消息的通信机制 intent
2. 基于外部存储的数据传输 File/SharedPreference/SQLite
3. 借助全局变量
4. 借助类的public static成员变量



### 1. 基于消息的通信机制 intent

**`Intent `是 `Android `四大组件**（`Activity`、`Service`、`BroadcastReceiver`、`ContentProvider`）**之间通信的纽带**，在 `Intent `中携带数据也是四大组件之间数据通信最常用、最普通的方式。使用步骤如下：

#### 1.1 数据发送方

1. 创建用于封装数据的Bundle对象
2. 创建intent对象
3. 将Bundle对象嵌入Intent对象中

```java
// 1.创建用于封装数据的Bundle对象
Bundle bundle = new Bundle();
bundle.putString("name", "WangJie");
bundle.putInt("age", 23);

// 2.创建intent对象
Intent intent = new Intent(MainActivity.this, SecondActivity.class);

// 3.将Bundle对象嵌入Intent对象中
intent.putExtras(bundle);

// 4.执行数据传递
startActivity(intent);
```

或者直接使用以下更简洁的写法：

```java
// 1.创建Intent对象
Intent intent = new Intent(MainActivity.this, SecondActivity.class);

// 2.将数据放入intent中
//程序自动创建Bundle，然后将对Intent添加的数据装载在Bundle中，对用户透明
intent.putExtra("name", "WangJie");
intent.putExtra("age", 23);

// 3.执行数据传递 
startActivity(intent);
```

#### 1.2 数据接收方

使用`intent.getXXXExtra("key-name", default-value)`获取值，其中`XXX`代表数据类型，如果获取的值为空，则设为`default-value`。

```java
// 1.获取intent对象
Intent intent = getIntent();

// 2.获取intent传递的数据
if (intent != null) {
    String name = intent.getStringExtra("key1");
    int age = intent.getIntExtra("key2", 0);
}
```

#### 1.3 示例

##### 1.3.1 `MainActivity.java`

在发送方`MainAcitivity`中创建`Intent`对象并放入要传递的数据

```java
public class MainActivity extends AppCompatActivity {
    private Button btn;
    private String username = "XiaoMing";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btn=findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
				// 1.创建Intent对象
                Intent intent=new Intent(MainActivity.this, SecondActivity.class);
                // 2.将数据放入intent中
                intent.putExtra("username", username);
                // 3.执行数据传递 
                startActivity(intent);
            }
        });
    }
}
```

##### 1.3.2 `SecondActivity.java`

在接收方`SecondActivity `中获取跳转时携带的数据

```java
public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv);
        
		// 1.获取intent对象
        Intent intent = getIntent();
        
		// 2.获取intent传递的数据
        if (intent != null){
            String username = intent.getStringExtra("username");
            tv.setText(username);
        }
    }
}
```



### 2. SharedPreference

`SharedPreferences`是`Android`平台上一个轻量级的存储辅助类，用来**保存应用的一些常用配置**，用作**简单数据的持久化缓存**。提供了`string，set，int，long，float，boolean`六种数据类型。

最终数据是以`xml`形式进行存储，本质是基于`XML`文件存储**`key-value`键值对**数据。

存储的文件在路径`/data/data/<package name>/shared_prefs/`下

主要用途：

1. 保存应用的设置，例如：设置静音，下次进入还是静音
2. 判断是否是第一次登陆
3. 保存登录用户名密码等情形

#### 2.1 写入数据

调用 `getSharedPreferences()` 方法获得 `SharedPreferences `对象，并提供两个参数：**文件名**和**操作模式**。

提供4种操作模式：

- `MODE_PRIVATE`：默认操作模式，代表该文件是私有数据，写入的内容会覆盖原文件的内容，且只能被应用本身访问。
- `MODE_APPEND`：模式会检查文件是否存在，存在就往文件追加内容，否则就创建新文件。
- `MODE_WORLD_READABLE`：表示当前文件可以被其他应用读取；
- `MODE_WORLD_WRITEABLE`：表示当前文件可以被其他应用写入。
  - 由于`MODE_WORLD_READABLE`和`MODE_WORLD_WRITEABLE`存在严重的安全风险，允许其他应用访问和修改应用的`SharedPreferences`数据，因此这两个模式现已被**弃用**

```java
// 1.获取SharedPreferences对象
SharedPreferences sp = getApplication().getSharedPreferences("MyInfo", MODE_PRIVATE);

// 2.获取SharedPreference的Editor对象，经过Editor进行写入
SharedPreferences.Editor editor = sp.edit();
editor.putString("name", "WangJie");
editor.putInt("age", 23);
editor.putBoolean("isStudent", true);

// 3.commit添加的数据，否则不会生效
editor.commit();
```

#### 2.2 读取数据

```java
// 1.获取SharedPreferences对象
SharedPreferences sp = getSharedPreferences("MyInfo",MODE_PRIVATE);

// 2.获取SharedPreferences对象中的数据
String name = sp.getString("name","默认值");
int age = sp.getInt("age",0);
boolean married = sp.getBoolean("married",false);
```

#### 2.3 示例

##### 2.3.1 `MainActivity`

先在`MainActivity`中对`SharedPreferences`写入数据

```java
public class MainActivity extends AppCompatActivity {
    private Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 写入数据
        // 1.获取SharedPreferences对象
        SharedPreferences sp = getApplication().getSharedPreferences("MyInfo", MODE_PRIVATE);
        // 2.获取SharedPreference的Editor对象，经过Editor进行写入
        SharedPreferences.Editor editor = sp.edit();
        editor.putString("name", "WangJie");
        editor.putInt("age", 23);
        editor.putBoolean("isStudent", true);

        // 3.put完成后一定要commit()，否则不会生效
        editor.commit();

        btn=findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 跳转到另一个名为MainActivity2的界面
                Intent intent=new Intent(MainActivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
    }
}
```

##### 2.3.2 `SecondActivity.java`

在`SecondActivity`中从`SharedPreferences`中读取数据

```java
public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv);
		
        // 1.获取SharedPreferences对象
        SharedPreferences sp = getSharedPreferences("MyInfo",MODE_PRIVATE);
        // 2.获取SharedPreferences中的数据
        String name = sp.getString("name","默认值");
        int age = sp.getInt("age",0);
        boolean married = sp.getBoolean("married",false);
        
        tv.setText(name);
    }
}	
```



### 3. SQLite

SQLite是一款轻量级的关系型数据库，它的运算速度非常快，占用资源很少，在存储大量复杂的关系型数据的时可以使用。

- 数据类型：

```
integer:整型
real:浮点型
text:文本类型
blob:二进制类型
```

- 关键字：

```
autoincrement:自增长
primary key:主键
```

- 数据库的文件都存放在`/data/data/<package name>/database/`目录下

#### 3.1 创建数据库帮助类

继承自`SQLiteOpenHelper`，需要重写`onCreate`和`onUpgrade`方法，通常会在构造方法中创建数据库，在`onCreate`方法中创建表。

```java
public class MyDatabaseHelper extends SQLiteOpenHelper {
    private Context mContext;
    public MyDatabaseHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version){
        //在构造方法中创建数据库
        super(context, name, factory, version);
        mContext = context;
    }

    @Override
    public void onCreate(SQLiteDatabase db){
        //通常进行一些建表的操作
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion){
        //更新操作
    }
}
```

#### 3.2 创建帮助类实例、数据库

- `getReadableDatabase`：创建数据库（存在则直接打开），并返回一个可对数据库进行读操作的对象
- `getWritableDatabase`：创建数据库（存在则直接打开），并返回一个可对数据库进行读写操作的对象

```java
// 1.创建帮助类实例
dbHelper = new MyDatabaseHelper(this, <数据库名>, null, 1);

// 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
SQLiteDatabase db = dbHelper.getWritableDatabase();
```

#### 3.3 插入

```java
// 1.创建帮助类实例
dbHelper = new MyDatabaseHelper(this, <数据库名>, null, 1);

// 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
SQLiteDatabase db = dbHelper.getWritableDatabase();

// 3.组装要插入的数据
ContentValues values = new ContentValues();
values.put(<列名1>, <列值1>);
values.put(<列名2>, <列值2>);

// 4.调用insert方法插入数据
db.insert(<表名>, null, values);
values.clear();
```

#### 3.4 更新

`update`方法的参数：

```java
// 1.创建帮助类实例
dbHelper = new MyDatabaseHelper(this, <数据库名>, null, 1);

// 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
SQLiteDatabase db = dbHelper.getWritableDatabase();

// 3.选择要更新的数据
ContentValues values = new ContentValues();
values.put(<列名1>, <列值1>);
values.put(<列名2>, <列值2>);

// 4.调用update方法更新数据
db.update(<表名>, values, <约束条件，相当于where子句，用占位符指定相应的内容>, <占位符对应的参数>);
```

#### 3.5 删除

```java
// 1.创建帮助类实例
dbHelper = new MyDatabaseHelper(this, <数据库名>, null, 1);

// 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
SQLiteDatabase db = dbHelper.getWritableDatabase();

// 3.调用update方法更新数据
db.delete(<表名>, <约束条件，相当于where子句，用占位符指定相应的内容>, <占位符对应的参数>);
```

#### 3.6 查询

```java
// 1.创建帮助类实例
dbHelper = new MyDatabaseHelper(this, <数据库名>, null, 1);

// 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
SQLiteDatabase db = dbHelper.getWritableDatabase();

// 3.查询Book表中的所有数据
Cursor cursor = db.query("Book", null, null, null, null, null,null);
if (cursor.moveToFirst()){
    do {
        //遍历cursor对象
        int name_id = cursor.getColumnIndex("name");
        String name = cursor.getString(name_id);
        int author_id = cursor.getColumnIndex("pages");
        String author = cursor.getString(author_id);
        int pages_id = cursor.getColumnIndex("pages");
        int pages = cursor.getInt(pages_id);
        int price_id = cursor.getColumnIndex("price");
        double price = cursor.getDouble(price_id);
        Log.d("MainActivity", "book name is" + name);
        Log.d("MainActivity", "book author is" + author);
        Log.d("MainActivity", "book pages is" + pages);
        Log.d("MainActivity", "book price is" + price);
    }while(cursor.moveToNext());
    
// 4.关闭cursor
cursor.close();
```

#### 3.7 示例

##### 3.7.1 `MyDatabaseHelper.java`

```java
public class MyDatabaseHelper extends SQLiteOpenHelper {
    public static final String CREATE_BOOK = "create table book ("
            + "id integer primary key autoincrement, "
            + "author text, "
            + "price real, "
            + "pages integer, "
            + "name text)";

    public static final String CREATE_CATEGORY = "create table Category ("
            + "id integer primary key autoincrement, "
            + "category_name text, "
            + "category_code integer)";
    
    private Context mContext;
    public MyDatabaseHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version){
        super(context, name, factory, version);
        mContext = context;
    }

    @Override
    public void onCreate(SQLiteDatabase db){
        db.execSQL(CREATE_BOOK);
        db.execSQL(CREATE_CATEGORY);
        .makeText(mContext, "创建数据库、数据表成功", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion){
        db.execSQL("drop table if exists Book");
        db.execSQL("drop table if exists Category");
        onCreate(db);
    }
}
```

##### 3.7.2 `MainActivity.java`

```java
public class MainActivity extends AppCompatActivity {
    private Button btnUpdate;
    private Button btnAdd;
    private Button btnDelete;
    private Button btnQuery;
    private MyDatabaseHelper dbHelper;
    private static Context mContext;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mContext = this;
        // 1.创建帮助类实例
        dbHelper = new MyDatabaseHelper(this, "BookStore.db", null, 1);

        // TODO:插入数据
        btnAdd=findViewById(R.id.btnAdd);
        btnAdd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
                SQLiteDatabase db = dbHelper.getWritableDatabase();

                // 3.组装要插入的数据
                ContentValues values = new ContentValues();
                values.put("name", "Flower");
                values.put("author", "Lin");
                values.put("pages", 346);
                values.put("price", 23.7);

                // 4.调用insert方法插入数据
                db.insert("Book", null, values);
                Toast.makeText(mContext, "插入数据成功", Toast.LENGTH_SHORT).show();
            }
        });

        // TODO:更新数据
        btnUpdate=findViewById(R.id.btnUpdate);
        btnUpdate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
                SQLiteDatabase db = dbHelper.getWritableDatabase();
                // 3.要更新的数据
                ContentValues values = new ContentValues();
                values.put("price", 100.99);
                // 4.调用update方法更新数据
                db.update("Book", values, "name = ?", new String[] {"Tantt"} );
                Toast.makeText(mContext, "更新数据成功", Toast.LENGTH_SHORT).show();
            }
        });


        // TODO:删除数据
        btnDelete=findViewById(R.id.btnDelete);
        btnDelete.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
               SQLiteDatabase db = dbHelper.getWritableDatabase();
                // 3.调用update方法更新数据
                db.delete("Book", "pages > ?", new String[] {"250"} );
                Toast.makeText(mContext, "删除数据成功", Toast.LENGTH_SHORT).show();
            }
        });

        // TODO:查询数据
        btnQuery = findViewById(R.id.btnQuery);
        btnQuery.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 2.调用getWritableDatabase()方法返回一个可操作的数据库对象
                SQLiteDatabase db = dbHelper.getWritableDatabase();
                // 3.查询Book表中的所有数据
                Cursor cursor = db.query("Book", null, null, null, null, null,null);
                if (cursor.moveToFirst()){
                    do {
                        //遍历cursor对象
                        int name_id = cursor.getColumnIndex("name");
                        String name = cursor.getString(name_id);
                        int author_id = cursor.getColumnIndex("pages");
                        String author = cursor.getString(author_id);
                        int pages_id = cursor.getColumnIndex("pages");
                        int pages = cursor.getInt(pages_id);
                        int price_id = cursor.getColumnIndex("price");
                        double price = cursor.getDouble(price_id);
                        Log.d("MainActivity", "book name is" + name);
                        Log.d("MainActivity", "book author is" + author);
                        Log.d("MainActivity", "book pages is" + pages);
                        Log.d("MainActivity", "book price is" + price);
                    }while(cursor.moveToNext());
                    Toast.makeText(mContext, "查询数据成功", Toast.LENGTH_SHORT).show();
                }
                cursor.close();
            }
        });
    }
}
```



### 4. File

- 文件存储方式是一种较常用的方法，在`Android`中读取/写入文件的方法，与`Java`中实现`I/O`的程序是完全一样的，提供`openFileInput()`和`openFileOutput()`方法来读取设备上的文件。

- 通过文件读写得到的文件存储在路径`/data/data/<package name>/files/`

#### 4.1 将数据存储到文件中

```java
String data = "data to save";
// 1.创建文件输出流对象(需要设置文件名和模式MODE)
FileOutputStream out = openFileOutput("文件名", 覆盖:MODE_PRIVATE 追加:MODE_APPEND);

// 2.创建缓冲区写对象
BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(out));

// 3.调用write方法写入数据
writer.write(data);

// 4.关闭写操作
writer.close();
```

#### 4.2 从文件读取数据

```java
// 1.创建文件输入流对象
FileInputStream in = openFileInput("文件名");

// 2.创建缓冲区读对象
BufferedReader reader = new BufferedReader(new InputStreamReader());

// 3.调用read方法读取数据
StringBuffer content = new StringBuffer();
String line = "";
while ((line = reader.readLine()) != null){
    content.append(line);
}

// 4.关闭读操作
reader.close();
data = content.toString();
```

#### 4.3 示例：

##### 4.3.1 `MainActivity.java`

[使用设备浏览器查看设备上的文件  | Android Studio](https://developer.android.google.cn/studio/debug/device-file-explorer?hl=zh-cn)

```java
public class MainActivity extends AppCompatActivity {
    private Button btn;
    private EditText username;
    private EditText passwd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        username = findViewById(R.id.edit_username);
        passwd = findViewById(R.id.edit_passwd);
        btn=findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent=new Intent(MainActivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
        SetUserInfo();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        String name = username.getText().toString();
        String password = passwd.getText().toString();
        saveToFile( "userinfo", name + ": " +  password + "\n",0);
    }

    public void SetUserInfo(){
        String userinfo = loadFile("userinfo");
        //截取用户名和密码
        int id = userinfo.indexOf(':');
        if (id != -1) {
            String name = userinfo.substring(0, id);
            String password = userinfo.substring(id + 1);
            System.out.println("用户名： " + username);
            System.out.println("密码：" + passwd);

            if (!TextUtils.isEmpty(userinfo)) {
                username.setText(name);
                passwd.setText(password);
                //将光标移动到文本末尾为止以便继续输入
                username.setSelection(name.length());
                passwd.setSelection(password.length());
                Toast.makeText(this, "Restoring Succeeded", Toast.LENGTH_SHORT).show();
            }
        }
    }
    public void saveToFile(String filename, String data, int mode){
        // 1.创建文件输出流对象
        FileOutputStream out = null;
        // 2.创建缓冲区写对象
        BufferedWriter writer = null;
        try{
            out = openFileOutput(filename, mode);
            writer = new BufferedWriter(new OutputStreamWriter(out));
            // 3.调用write方法写入数据
            writer.write(data);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                // 4.关闭写操作
                if (writer != null){
                    writer.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    public String loadFile(String filename){
        // 1.创建文件输入流对象
        FileInputStream in = null;
        // 2.创建缓冲区读对象
        BufferedReader reader = null;
        StringBuilder content = new StringBuilder();
        try {
            in = openFileInput("userinfo");
            reader = new BufferedReader(new InputStreamReader(in));
            String line = "";
            // 3.调用read方法读取数据
            while ((line = reader.readLine()) != null){
                content.append(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // 4.关闭读操作
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        return content.toString();
    }
}
```

##### 4.3.2 `SecondActivity.java`

```java
public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv);
    }
}
```



### 5. 借助全局变量

创建一个专门用于存放共享变量的类，继承自`Application`，因为`Application`在`package`创建的时候就存在了，到所有的`activity`都被`destroy`掉之后才会被释放掉。

**示例**：

#### 5.1 创建全局的`Application`类

`DataApplication.class`

```java
package com.example.myapplication;

import android.app.Application;

public class DataApplication extends Application {
    private String username;

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }
}
```

#### 5.2 在`AndroidManifest.xml`中注册`application`

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:name=".DataApplication" //在application中添加DataApplication的注册信息
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyApplication"
        tools:targetApi="31">
        <activity
            android:name=".SecondActivity"
            android:exported="false" />
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
    
</manifest>
```

#### 5.3 在`MainActivity`中修改`DataApplication`中的变量

相当于共享`MainActivity`中的变量值

```java
public class MainActivity extends AppCompatActivity {
    private Button btn;
    public String username = "XiaoMing";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //1.获得应用程序实例
        DataApplication app = (DataApplication) getApplicationContext();
        //2.修改DataApplication中的变量值
        app.setUsername(username);
			
        btn=findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 跳转到另一个名为MainActivity2的界面
                Intent intent=new Intent(MainActivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
    }
}
```

#### 5.4 在`SecondActivity`中获取`DataApplication`中的变量

相当于获取`MainActivity`中的变量值

```java
public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv);

        //获得应用程序实例
        DataApplication app = (DataApplication) getApplicationContext();
        //取值
        String result = app.getUsername();
        tv.setText(result);
    }
}
```



### 6. 借助类的public static静态成员变量（不推荐）

由于类的静态成员可以通过 “className.fileName” 来访问，故而可以实现 Activity 之间的数据通信。

但是由于静态变量会一直存在于内存中，可能会导致内存泄漏或不必要的资源占用。

**示例**：

#### 6.1 在`MainActivity`中定义public static成员变量

```java
public class MainActivity extends AppCompatActivity {
    private Button btn;
    public static String username = "Xiaoming";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btn=findViewById(R.id.btn);
        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 跳转到SecondActivity的界面
                Intent intent = new Intent(MainActivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
    }
}
```

#### 6.2 在`SecondActivity`中访问`MainActivity`中的成员变量

```java
public class SecondActivity extends AppCompatActivity {
    TextView tv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
        tv = findViewById(R.id.tv);
        
        //访问MainActivity中的public静态变量
        tv.setText(MainActivity.s);
        
        //修改MainActivity中的public静态变量
        MainActivity.s = "Lihua";
    }
}
```



### SQL语句

#### 1 SQL语句介绍

> SQL语言，是一种专门对数据库进行操作的语言。
>
> 像我们刚刚通过右键就能插入一条数据，但其实它的本质就是执行一条SQL语句



#### 2 增删查改语句

##### 2.1 增删查改的意思

- 增：新增记录	


- 删：删除记录


- 查：查询记录


- 改：修改记录

##### 2.2 insert语句

>  insert语句对应的是“增”，也即新增数据

- 基本用法：

```sql
insert into 表名(字段名) values(值);
```

- 例：

```mysql
insert into user(name,age,desc) values('andy',20,'打酱油的');
```

> 代表给user表新增一条数据，name的值为andy，age的值为20。



##### 2.3 delete语句

> delete语句对应的是“删”，也即删除数据

- 用法（慎用）：

```mysql
delete from 表名;
```

- 例：

```mysql
delete from user;
```

- 在执行这条语句前我们user表里有三条数据
![](https://upload-images.jianshu.io/upload_images/9249356-cd12bbc14adb30dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 执行完后，我们发现，数据全没了
![](https://upload-images.jianshu.io/upload_images/9249356-e812d14d49b66f81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>  结论：delete语句默认会删除表格中的所有数据，要 `慎用` 

- 按条件删除，用法：（常用）

```mysql
delete from 表名 where 字段 = 某个值;
```

- 例：

```mysql
delete from user where id = 2;
```

>  说明：这代表删除user表下，id为2的那条记录

- 也可以按范围删除，例：

```mysql
delete from user where id <= 3;
```

> 说明：这代表删除user表下，id小于或等于3的那些记录



##### 2.4 select语句

> select语句对应的是“查”，即查询记录

**指定查询某些字段**

- 用法：

```mysql
select 字段 from 表名;
```

- 例：

```sql
select name,age from user;
```

说明：这会查询出user表下所有数据，只会包含`name`和`age`字段。如果还有其他字段，结果中不会包含。



**查询所有字段**

- 用法：

```sql
select * from 表名;
```

- 例：

```sql
select * from user;
```

>  默认会查询出表中的所有数据，如果想指定条件查询，也可以在后面加  `where`

- 例：

```sql
select * from user where id < 10;
```

>  说明：只查询出id小于10的数据，不包括10



##### 2.5 update语句

> update语句对应的是“改”，也即修改某条数据

- 用法（慎用）：

```sql
update 表名 set 字段 = 新值;
```

- 例：

```sql
update user set name = '黑马一哥';
```

>  说明：把user表中所有数据的name值改为黑马一哥，注意，此操作是修改所有，所以要小心使用！



- 指定条件修改，例：

```sql
update user set name = '黑马一哥' where id = 3;
```

>  只修改id为3的这条数据，把name改成黑马一哥
###  PHP操作数据库

####  为什么需要

>  之前我们学的语句都是在MySQL自己的管理界面上操作，但有的时候我们需要在界面上显示一些数据

- PHP操作数据库，主要分为三大步：
  - 建立数据库连接
  - 操作数据库（增删改查）
  - 关闭数据库连接

  ​


####  建立数据库连接

- 语法：

```php
mysqli_connect('数据库地址','账号','密码','数据名');
```

- 参数解释：

```
参数1：数据库的ip地址
参数2：数据库管理的账号
参数3：数据库管理的密码
参数4：数据库名，因为一个数据库服务器里可能有很多数据库，你需要告诉它连接哪个数据库的
```

- 例：

```php
$link = mysqli_connect('127.0.0.1','root','root','manage');
```

> 使用完此函数后，会有一个返回值，如果返回值为false代表连接失败
>
> 如果返回值不为false，那么会打印一个类似下图的数据

![](https://upload-images.jianshu.io/upload_images/9249356-c5e58ea1559e1508.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个返回值我们一般叫  `连接通道`，这个  `连接通道`  里面的内容是什么我们不需要关心，只需要知道，`连接通道`里包含了本次连接的各种信息，只要不是false就代表数据库连接成功。

####  操作数据库

- 语法：

```php
mysqli_query(连接通道，SQL语句);
```

##### 1 查询数据

- 例：

```php
$result =  mysqli_query($link,"select * from user");
```

>说明：
>
>​	这句话执行完后会得到一个结果，结果包含了查询得到的数据，我们用一个变量    `$result`  接收
>
>但是，这个返回值我们不能直接拿来用，还需要用一个  `解析函数`  来把数据解析出来

- 用法：

```php
mysqli_fetch_all(查询结果,MYSQLI_ASSOC);
```

- 例：

```php
$users = mysqli_fetch_all($result,MYSQLI_ASSOC);
```

说明：

- 参数1：我们传之前用`mysqli_query`函数查询到的结果
- 参数2：固定写  `MYSQLI_ASSOC`   ，如果记不住，就写 `1`。

>  函数执行后，会把结果转成一个关联型数组。这样，我们要的数据就比较明确了。
>
>  注：参数2如果不传  `MYSQLI_ASSOC`，得到的会是一个普通数组，那样我们取数据时只能根据下标来取。



##### 2 增、删、改数据

> 增、删、改数据，也是用  `mysqli_query`  这个函数操作。只不过把SQL语句换成对应的语句

- 增加：

```php
$rows = mysqli_query($link,'insert into user(name,age,desc) values("新人",16,"新增加的一条数据")');
```

- 删除：

```php
$rows = mysqli_query($link,'delete from user where id=2');
```

- 修改：

```php
$rows = mysqli_query($link,'update user set name="修改",age=18,desc="我被改了" where id=2');
```

> 因为增、删、改不是为了获取结果，所以此时  `mysqli_query`  的返回值不再会是一堆数据，而是获得受影响的行数，我们根据受影响的行数是否大于0，就可以知道是否操作成功

- 用法：

```php
if($rows > 0){
  echo "登录成功!";
}
```

#### 5 关闭数据库连接

>  无论你是做增删查改中的哪一种，请记得最后一定要关闭数据库连接！

- 用法：

```php
mysqli_close($link);
```

>  注意：请记得一定要关闭数据库连接，否则会占用服务器资源。


- 增删改
```
//1.连接数据库
$link = mysqli_connect('数据库服务器地址','数据库登录账号','数据库登录密码','要操作的数据库');
//2.执行sql语句
$sql = "";  //增删改.
$res = mysqli_query($link,$sql); //返回的是否成功!
//3. 返回受影响的行数.
$rows = mysqli_affected_rows($link); //受影响的行数
//4.关闭数据库
mysqli_close($link);
```
- 查询
```
//1.连接数据库
$link = mysqli_connect('数据库服务器地址','数据库登录账号','数据库登录密码','要操作的数据库');
//2.执行sql语句
$sql = "" ; //查
$res =  mysqli_query($link, $sql); //返回的结果不是我们想要的.
//3.处理返回的结果.
$arr =  mysqli_fetch_all($res,1);  //返回的结果是一个二维的关系型数组
//4.关闭数据库
mysqli_close($link);
```
#####Mysql排序
asc 升序排列
desc 降序排列
![](https://upload-images.jianshu.io/upload_images/9249356-a01bbe2c8fb14d14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
//增
insert into user(name,age,desc) values('andy',20,'打酱油的');
//删
delete from user where id = 2;
//查
select * from user where id < 10;
//改
update user set username = '$username',description = '$userDesc'where Id =$id 
```

![](https://upload-images.jianshu.io/upload_images/9249356-2d678d5cf1970e72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

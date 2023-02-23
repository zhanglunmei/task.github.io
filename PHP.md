## 1、跳转语句

### 	1.1、break：终端循环

```php
<?php
    for ($i = 1;$i<=10;$i++) {
        echo "第{$i}次循环";
        if ($i == 5) {
            break; //中断循环
        }
        echo '<br/>';
    }
//结果
第1次循环
第2次循环
第3次循环
第4次循环
第5次循环
```

### 	1.2、continue：终端当前循环，继续下一个循环

```php
 for ($i = 1;$i<= 10;$i++) {
        if ($i == 5) {
            continue; //中断本次循环，进入下一次循环
        }
        echo "第{$i}次循环".'<br/>';
    }
//结果
第1次循环
第2次循环
第3次循环
第4次循环
第6次循环
第7次循环
第8次循环
第9次循环
第10次循环
```

###  		1.3、中断多重循环

```php
    for ($i =1;$i<10;$i++) {
        for ($j = 1; $j<= $i;$j++) {
            echo $j;
            if ($j == 5) {
                //除了第一个循环可以不写后面的数值,如果第二个或者第三个必须写对应的循环数
                break 2; //中断第二个循环 
            }
        }
        echo '<br>';
    }
//结果
1
12
123
1234
12345
```

## 2、替代语法

​	php中除了do-while以外,其他的语法结果都有替代语法

​	规则:左大括号变冒号,右大括号变endXXX

### 		2.1.、if的替代语法

```php
if():

endif;
```

### 		2.2、if else的替代语法

```php
if():

elseif():

elseif():

endif;
```

### 		2.3、switch的替代语法

```php
switch():

endswitch;
```

### 		2.4、for的替代语法

```php
for():

endfor;
```

### 		2.5、while的替代语法

```php
while():

endwhile;
```

### 		2.6、foreach的替代语法

```php
foreach():

endforeach;
```

## 3、函数

​	1.函数就是一段代码块

​	2.函数可以实现模块化编程

### 		3. 1、函数定义

```php
//定义函数
function 函数名 (形参){
    //函数体
}
//调用函数 函数名不区分大小写
函数名();

```

##### 		小结:

​		1.变量名区分大小写

​		2.关键字、函数名不区分大小写

### 		3.2、可变函数

​	将函数名称存储到变量中

```php
 // 可变函数
    function showChinese()
    {
        echo '中文<br/>';
    }
    function showEnglish()
    {
        echo 'english<br/>';
    }
    //测试
    $fun = rand(1, 10)%2?'showChinese':'showEnglish'; //可变变量
    $fun();
```

### 		3.3、匿名函数

​	匿名函数就是没有名字的函数

```php
 // 匿名函数
    $func = function () {
        echo '<hr/>'.'你好！';
    };
    $func();
```

### 		3.4、参数传递

​	函数的参数有形式参数和实际参数

​	形式参数是定义函数的时候使用的参数，只起到形式的作用，没有具体的值

​	实际参数是调用函数的时候的参数

```php
 //参数传递
    function fun3($num1, $num2)
    {
        echo $num1 + $num2;
    }
    // 调用参数传递值
    fun3(15, 20);
```

​	默认情况下，函数的传递是值传递	

```php
	$num2 = 10;
    // 值传递
    function fun5($args)
    {
        $args = 100;
    }
    fun5($num2);
    echo $num2;
```

### 		3.5、地址传递

​	地址传递只能放变量

```php
 	$num = 10;
    // 地址传递
    function fun4(&$args)
    {
        $args = 100;
    }
    fun4($num);
    echo $num;

```

##### 	小结：

​	1.函数的参数默认是值传递

​	2.如果要传递地址，在参数面前加上&

​	3.如果是地址传递，不能直接写值

```php
  function fun4(&$args)
    {
        $args = 100;
    }
    fun4(10); //Fatal error: Only variables can be passed by reference (只有变量才能传递引用)
```

### 	3.6、参数默认值

#### 			3.6.1、在定义函数的时候给形参赋值，就是参数的默认值

```php
 	//参数的默认值
	function fun6($name, $add='地址不详')
    {
        echo '姓名:'.$name,'<br/>';
        echo '地址:'.$add,'<hr/>';
    }

    fun6('tom', '北京');
    fun6('breey');

	//运行结果
    10姓名:tom
    地址:北京
    姓名:breey
    地址:地址不详	
```

#### 			3.6.2、默认值必须是值,不能用变量代替

```php
  $str = '地址不详';
    // 参数默认值
    function fun6($name, $add=$str) //Constant expression contains invalid operations 
    {
        echo '姓名:'.$name,'<br/>';
        echo '地址:'.$add,'<hr/>';
    }
```

#### 			3.6.3、默认值可以使用常量

```php
	define('ADD', '地址不详');
    // 参数默认值
    function fun6($name, $add=ADD)
    {
        echo '姓名:'.$name,'<br/>';
        echo '地址:'.$add,'<hr/>';
    }
    fun6('breey');
```

#### 			3.6.4、没有默认值的写在前面，有默认值的写在后面

```php
 function fun7($name, $age = '未知', $add = '地址不详')
    {
        echo '姓名:'.$name,'<br/>';
        echo '年龄:'.$age,'<br/>';
        echo '地址:'.$add,'<hr/>';
    }
    fun7('tony');
//结果
姓名:tony
年龄:未知
地址:地址不详
```

#### 		3.6.5、参数个数不匹配

```php
function fun($num1,$num2){
	echo $num1,'<br/>';
    echo $num2,'<br/>';
}
fun(10); //实参少于形参(报错)
fun(10,20,30);//实参多于形参，只有前面对应的值
```

#### 		3.6.6、获取所有传递参数

```php
function fun(){
	$args = func_get_args();//获取参数数组
}
fun(10);
fun(10,20);
fun(10,20,30);
```

### 	3.7、参数个数约束

#### 		3.7.1、定义变长参数

```php
  // ...$hobby包含了除了前面参数以外的所有参数hobby可以根据需要命名
    function fun8($name, $age, ...$hobby)
    {
        echo '姓名:'.$name,'<br/>';
        echo '年龄:'.$age,'<br>';
        print_r($hobby);
        echo '<hr/>';
    }

    fun8('tom', 22);
    fun8('berry', 25, '打游戏', '睡觉', '吃饭');
	//结果
	姓名:tom
    年龄:22
    Array ( )
     
    姓名:berry
    年龄:25
    Array ( [0] => 打游戏 [1] => 睡觉 [2] => 吃饭 )	
```

​	多学一招：

```php
 	function fun9(...$args)
    {
        print_r($args);
        echo '<hr/>';
    }

    $arr = [10,20,30];
    echo '<pre>';
    fun9(...$arr); //将数组中的参数展开
```

#### 		3.7.2、类型约束

​	在形参面前加上一个变量类型

```php
  function fun10(string $naem, int $age)
    {
        echo '姓名:'.$naem,'<br/>';
        echo '年龄:'.$age,'<hr/>';
    }
    fun10('tom', 20);
//约束name是string类型 age是int类型
```

​	3、返回值约束

```php
 // 返回值约束
    function fun(int $num1, int $num2):int
    {
        return $num1+$num2;
    }		
```

可以约束string、int、float、bool、数组

```php
//约束返回类型是数组
function fun():array{
    
}
//约束return后面不能有返回值 
function fun():void{ //void是空的意思
    return;
}
```

### 3.8.return

#### 	3.8.1、终止脚本执行

```php
echo 'aaa<br/>';
return; 		//终止脚本执行
echo 'aaa<br/>';//不执行
```

​	提醒：return只能中断当前页面,	如果有包含文件，只能中断包含文件

##### 	例题：

​	12-函数.php

```php
echo 'aaaaa<br/>';
require './13-test.php';	//包含文件
echo 'aaaaa<br/>';
```

​	13-test.php

```php
<?php
echo '121111111<hr/>';
return;
echo '222222222<hr/>';
```

​	运行结果

```php
aaaaa
121111111aaaaa
aaaaa
```

​	如果要完全终止脚本执行,使用exit()或者die()

#### 	3.8.2、返回页面结果

​	13-test.php

```php
<?php
return array('name'=>'ls','age'=>'15','sex'=>'男');
```

​	12-函数.php

```php
$stu = require './13-test.php';
print_r($stu); //[name] => ls   [age] => 15   [sex] => 男
```

#### 	3.8.3、函数的返回和终止

​	3.8.3.1、终止函数运行

```php
function fun (){
    echo 'aaa';
    return;		//终止函数运行
    echo 'bbb';	
}
fun();	////aaa
```

3.8.3.2、返回值

```php
function fun(){
    return 10;	//返回值
}
fun(); //10
```

### 3.9、练习

#### 	1、求数组的和、平均值

```php
<?php
// 1.求数组的和、平均值
$num = [1,20,53,44,79,85,30,7];
$sum = 0;
for ($i = 0;$i<count($num); $i++) {
    $sum+= $num[$i];
}
echo '和是:'.$sum,'<br/>';
echo '平均值是:'.$sum/count($num),'<hr/>';
```

#### 	2、数组反转

```php
// 2.数组翻转
$stu = ['tom','berry','ketty','rose','jake'];
for ($i=0,$j=count($stu)-1;$i<$j;$i++,$j--) {
    [$stu[$i],$stu[$j]] = [$stu[$j],$stu[$i]];
}
print_r($stu);
echo '<hr/>';
```

#### 	3、便利二维数组

```php
// 3.便利二维数组
$stu2 = [
    [1,2,3,4,5],
    [10,11,12,13,14,15]
];
for ($i=0;$i<count($stu2);$i++) {
    for ($j = 0;$j<count($stu2[$i]);$j++) {
        echo $stu2[$i][$j],'&nbsp;';
    }
    echo '<hr/>';
}
```

#### 	4、循环输出1-100，其中3的倍数输出A，5的倍数输出B，15输出C

```php
// 4.循环输出1-100，其中3的倍数输出A，5的倍数输出B，15输出C
for ($i= 1;$i<=100;$i++) {
    if ($i %3 == 0) {
        echo 'A';
    } elseif ($i % 5 == 0) {
        echo 'B';
    } elseif ($i % 15 == 0) {
        echo 'C';
    } else {
        echo $i;
    }
    echo '&nbsp';
}
echo '<hr/>';
```

##  4、包含文件

### 	4.1、包含文件的方式

​	1、require:包含多次

​	2、include：包含多次

​	3、require_once：包含一次

​	4.、nclude_once：包含一次

#### 	4.1、小结

​	4.1.1、require遇到错误抛出error类别的错误，停止执行

​	4.1.2、include遇到错误抛出warning类型的错误,继续执行

​	4.1.3、require_once、include_once只能包含一次

​	4.1.4、HTML类型的包含页面中存在php代码，如果包含到PHP中是可以执行的

​	4.1.5、包含文件相当于把包含文件的代码拷贝到主文件中执行，魔术常量除外，魔术常量获取的是所在文件的信息

### 	4.2.包含文件的路径

```php
./	当前目录
../	上一级目录
```

​	区分如下包含的区别

```php
require './head.html'; //在当前目录下查找
require 'head.html'; 	//受include_path配置影响
```

​	include_path的使用场景:

​	如果包含文件的目录结构比较复杂,比如:在c:\aa\bb\cc\dd中有多个文件需要包含,可以包含路径设置为include_path，这样包含就只要写文件名就可以了

```php
set_include_path('c://aa/bb/cc/dd'); //设置include_path
require 'head1.html'; //受include_path影响
```

​	include_path可以设置多个，路径之间用分号隔开

```php
set_include_path('c://aa/bb/cc/dd';d://aa/bb/cc/dd);
```

## 5、错误处理

### 	5.1、错误的级别

​		1、notice：提示

​		2、warning：警告

​		3、error：致命错误

​	notice和warning报错后继续执行，error报错后停止执行

### 	5.2、错误的提示方法

​		方法一：显示在浏览器上

​		方法二：记录在日志中

### 	5.3、与错误处理有关的配置

```php
1、error_reporting = E_ALL:报告所有的错误
2、display_errors = On :将错误显示在浏览器上
3、log_erros= On:将错误记录在日志中
4、error_log = '地址':错误的报错地址
```

## 6、文件编程

### 	6.1文件夹操作

#### 	6.1、创建文件夹[mkdir(路径，权限，是否递归创建)]

```php
make	//创建
direction	//目录
```

##### 	6.1.1、实例:

```php
// 1、创建文件夹
mkdir('./aa');      //当前目录创建文件夹
mkdir('./aa/bb');   //在aa目录下创建bb文件夹(aa目录必须存在)
mkdir('./aa/bb/cc/dd', 0777, true); //递归创建
```

##### 	6.1.2、小结:  

​	6.1.2.1、0777表示文件夹的权限

​	6.1.2.2、true表示递归创建，默认是false

#### 	6.2、删除文件夹[rmdir]

```php
remove:移除
rmdir('./aa/bb/cc/dd');//删除文件夹
```

##### 	6.2.1、提醒：

```php
1、删除的文件夹必须是空的	

2、PHP基于安全考虑，没有提供递归删除
```

#### 	6.3、重命名文件夹【rename(旧名字,新名字)】

```php
rename('./aa/bb/cc', './aa/bb/uu'); //将cc改为uu
```

#### 	6.4是否是文件夹[is_dir()]

```php
echo is_dir('./aa')?'是文件夹':'不是文件夹';
```

#### 	6.5打开文件夹、读取文件夹、关闭文件夹

```php
$folder = opendir('./');  //打开目录

while ($f = readdir($folder)) {  //读取文件夹
    echo $f,'<br/>';
}
echo $f,'<hr/>';
closedir($folder); //关闭文件夹
```

##### 	6.5.1、小结	

```php
1、opendir()返回资源类型
2、每个文件夹中都有.和..
3、iconv()用来做字符编码转换
```

### 	6.2文件操作

#### 		6.2.1将字符串写入文件

```php
<?php
$str = 'aa1232';
file_put_contents('./test.txt', $str);
```

##### 		6.2.1.1小结	

```
1、所有的“写”操作都是清空重写
2、在文本中换行是\r\n
    \r：回车
    \n：换行
3、\r\n是特殊字符，必须写在双引号中
```

#### 		6.2.2将整个文件读取一个字符串

```php
//方法一
$str = file_get_contents('./test.txt'); //将整个文件读取一个字符串
echo $str;
//方法二
readfile('./text.txt');//读取输出文件内容

//注意：echo file_get_content() === readfile();
```

#### 		6.2.3打开文件 并操作

```php
fopen(地址，模式)  //打开文件
模式：
r:读 read
w:写 write
a:追加 addend
```

##### 			6.2.3.1、例题

```php
// 1. 打开文件
$fp = fopen('./test.txt', 'w'); //打开文件返回文件指针(文件地址)
// var_dump($fp); //resource(3) of type (stream)
fputs($fp, '12345677777'); //写一行
fclose($fp);    //关闭文件


// 2.打开文件读取
$fp =  fopen('test.txt', 'r');  //打开文件读取
while ($line = fgets($fp)) {
    echo $line,'<br/>';
}

// 打开文件追加
$fp = fopen('test.txt', 'a'); //打开文件追加
fputs($fp, '123456');
```

##### 			6.2.3.2、小结		

```php
1、打开文件(fopen)返回文件指针(文件指针就是文件地址),资源类型
2、打开文件写，追加操作，如果文件不存在，就创建新的文件
3、打开文件读操作，如果文件不纯在就报错
4、fputs()写一行,fgets()读一行,fclose()关闭文件
```

#### 		6.2.4是否是文件【is_file()】

```php
echo is_file('./test.txt')?'是文件':'不是文件';
```

#### 		6.2.5判断文件或文件夹是否存在[file_exists()]

```php
echo file_exists('./test.txt')?'文件存在':'文件不存在';
```

#### 		6.2.6删除文件[unlink]

```php
$path = './test.txt';
if (file_exists($path)) {  //文件存在
    if (is_dir($path)) {   //如果是文件夹用rmdir()删除
        rmdir($path);
    } elseif (is_file($path)) { //如果是文件使用unlink()删除
        unlink($path);
    }
} else {
    echo '文件或文件夹不存在';
}
```

#### 		6.2.7二进制文件读取[fread(文件地址,文件大小)]

​			文件的存储有两种：字符流和二进制流

​			二进制流的读取按文件大小来读的

```php
//方式一
$path ='./face.jpeg';
$fp = fopen($path, 'r');
header('content-type:image/jpeg');//告知浏览器下面的代码通过JPG图片方式解析
echo fread($fp, filesize($path)); //二进制读取
//方式二
header('content-type:image/jpeg');
echo file_get_contents('./face.jpeg');

```

##### 	6.2.7.1、小结

```php
1、文本流有明确的结束符，二进制流没有明确的结束符，通过文件大小判断文件是否读取完毕
2、file_get_content()既可以读取文本流，也可以读取二进制流
```

## 7、表单提交数据的两种方式

### 	7.1、两种方式

​		7.1.1、get

​		7.1.2、post

```html
<form method = "get" action = ""></form>
<form method = "post" action = ""></form>
```

### 	7.2、区别

​		7.2.1外观上看

​			get提交在地址栏上可以看到参数

​			post提交在地址栏上看不到参数

​		7.2.2、安全性

​			get不安全

​			post安全

​		7.2.3、提交原理

​			get参数是一个一个的提交

​			post是提交将所有参数作为一个整体一起提交

​		7.2.4、提交数据大小

​			get提交一般不超过255个字节

​			post提交的大小取决于服务器

```php
//在php.ini中，可以配置post的提交大小
post_max_size = 100M（默认数据）
```

​		7.2.5灵活性

​			get很灵活，只要有页面跳转就可以传递参数

​			post不灵活，post提交需要有表单的参与

```php+HTML
1、html跳转
	<a href="index.php?name=tom&age=20">跳转</a>
2、JS跳转
<script>
        // 属性跳转
	location.href = 'index.php?name=tom&age=20';
        // 方法跳转
	location.assign('index.php?name=tom&age=20');
        
	location.replace('index.php?name=tom&age=20');
</script>
3、PHP跳转
<?php
	header('location:index.php?name=tom&age=25');
?>
```

​		7.2.6小结

​		

|              | GET                                             | POST                                                         |
| ------------ | ----------------------------------------------- | ------------------------------------------------------------ |
| 外观上       | 在地址上看得到传递的参数和值                    | 在地址上看不得到传递的参数和值                               |
| 提交数据大小 | 提交少量数据，不同浏览器大小不同IE是255个字符   | 提交大了数据，可以通过更改php.ini配置文件来设置post提交数据大小 |
| 安全性       | 低                                              | 高                                                           |
| 提交原理     | 提交的数据和数据之间是独立的关系                | 将提交的数据变成XML格式提交                                  |
| 灵活性       | 很灵活，只要有页面跳转就可以传递使用get传递数据 | 不灵活                                                       |



## 8、服务器接受数据的三种方式

​	通过名字获取对于的值

```
$_POST:数组类型，保存的是POST提交的值
$_GET:数组类型，保存的是GET提交的值
$_REQUEST:既能获取GET提交的值也能获取POST提交的值
```

​	例题:

​	html页面

```HTML
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <form action="./19-test.php" method="get">
            语文: <input type="text" name="ch"> <br> <br>
            数学: <input type="text" name="math" > <br> <br>
            <input type="submit" value="提交" name="buttom"> <br> <br>
        </form>
        <!-- a链接跳转提交 -->
        <a href="./19-test.php?ch=85&math=75">a链接跳转提交</a> <br><br>
        <!-- js跳转提交 -->
        <input type="button" value="js跳转提交" onclick="location.href = './19-test.php?ch=45&math=84'" >
    </body>
</html>
```

​	PHP页面

```php
<?php
// post数组不为空
if (!empty($_POST)) {
    echo '这是POST提交<br/> <br/>';
    echo '语文:'. $_POST['ch'],'<br/> <br/>';
    echo '数学:'. $_POST['math'],'<br> <br/>';
}
echo '<hr>';
// 获取GET提交的数据
if (!empty($_GET)) {
    echo '这是GET提交<br/> <br/>';
    echo '语文:'. $_GET['ch'],'<br/> <br/>';
    echo '数学:'. $_GET['math'],'<br/> <br/>';
}
echo '<hr/>';
// 既能获取GET提交又能获取POST提交的数据
echo $_REQUEST['ch'],'<br/> <br/>';
echo $_REQUEST['math'],'<br/> <br/>';

```

​	问题

​	在一个请求中，既有get又有post，get和post传递的名字是一样的，这时候通过$_REQUEST获取的数据是什么?

​	答：取决与配置文件

```php
request_order = "GP" //先获取GET的值，在获取POST的值
```

​	例题

```php+HTML
 	<?php
        if (!empty($_POST)) {
            echo '姓名:'. $_REQUEST['username'],'<br/><br/>';
        }
    ?>
    <form action="?username=22" method="post">
        姓名: <input type="text" name="username" > <br><br>
        <input type="submit" value="提交" name="button">
    </form>
	//分析：先获取GET的username，在获取POST的username，那么后面的将前面的值覆盖
```

​	小结：

```php
	1.在开发的时候，如果明确是post提交就使用$_POST获取，如果明确是get提交就用$_GET获取

​	2.request获取效率低，尽可能不要使用，除非提交的类型不确定的情况下才使用
```



## 9、参数传递

### 	9.1、复选框值的传递

​			复选框的命名要注意带[]，name=‘bobby[]’;

```php+HTML
<?php
	if (isset($_POST['button'])) {
		print_r($_POST['hobby']);
	}
?>

<form action="" method="post">
	爱好: 
	<input type="checkbox" name="hobby[]" value="爬山">爬山
	<input type="checkbox" name="hobby[]" value="抽烟">抽烟
	<input type="checkbox" name="hobby[]" value="喝酒">喝酒
	<input type="checkbox" name="hobby[]" value="烫头">烫头
	<input type="submit" value="提交" name="button">
</form>
```

​	小结:	

```php
1、表单提交到本页面需要判断一下是否有POST提交
2、数组的提交表单元素的名字必须带怕[]
```

### 	9.2、例题

```php+HTML
<?php
        if (isset($_POST['button'])) {
            echo '姓名:'.$_POST['username'],'<br>';
            echo '密码:'. $_POST['pwd'],'<br>';
            echo '性别:' . $_POST['sex'],'<br>';
            echo '爱好:',isset($_POST['hobby'])?implode(',', $_POST['hobby']):'没有爱好','<br/>';
            echo '籍贯:' . $_POST['jiguan'],'<br/>';
            echo '留言:'. $_POST['words'],'<hr>';
        }
    ?>

     <form action="" method="post">
        姓名： <input type="text" name="username" > <br>
        密码: <input type="password" name="pwd" > <br>
        性别: <input type="radio" name="sex"  value="1" checked>男
              <input type="radio" name="sex" value="0"> 女 <br>
        爱好: 
        <input type="checkbox" name="hobby[]" value="爬山">爬山
        <input type="checkbox" name="hobby[]" value="抽烟">抽烟
        <input type="checkbox" name="hobby[]" value="喝酒">喝酒
        <input type="checkbox" name="hobby[]" value="烫头">烫头 <br>
        籍贯:
        <select name="jiguan" id="">
            <option value="021">上海</option>
            <option value="010">北京</option>
        </select> <br>
        留言:
        <textarea name="words" id="" cols="30" rows="5"></textarea> <br>
        
        <input type="submit" value="提交" name="button">

    </form>
    
    //运行结果
    //姓名:阿斯达
    //密码:asd
    //性别:1
    //爱好:爬山,抽烟
    //籍贯:010
    //留言:阿斯达
```

## 10、文件上传

​	开发中需要上传图片、音乐、视频等等，这种上传传递是二进制数据

### 	10.1 客户端上传文件

​		文件域

```html
 <input type="file" name="image" id="">
```

​		表单的enctype属性

​				默认情况下，表单传递的是字符流，不能传递二进制流，通过设置表单的enctype属性传递复合数据。

​		enctype属性的值有：

​			1.application/x-www-from-urlencoded;【默认】，表示传递的是带格式的文本数据。

​			2.multipart/from-data：复合表单的数据(字符串 文件)，文件上传必须设置此值

​			3.text/plain：用于项服务器传递无格式的文本数据，主要用于电子邮件

​		单词

```php
multipart：复合
form-data:表单数组
```

### 	10.2 服务器接受文件

​		超全局变量 $_FILES 是一个二维数组，用来保存客户端上传到服务器的文件信息。二维数组的行是文件域的名称，列有5个。

​		1、`$_FILES[]['name']`:上传的文件名
​		2、`$_FILES[]['type']`:上传的类型，这个类型是MIME类型
​		3、`$_FILES[]['size']`:文件大小，以字节为单位
​		4、`$_FILES[]['tmp_name']`:文件上传时的临时文件
​		5、`$_FILES`[]['error']:错误信息(值有0,1,2,3,4,6,7)0表示正确

```php
Array
(
    [face] => Array
        (
            [name] => background.jpg //上传的文件名
            [type] => image/jpeg	//上传的类型
            [tmp_name] => C:\Windows\php6BF6.tmp //临时文件
            [error] => 0			//错误信息
            [size] => 8177			//文件大小
        )

)
```

​		`$_FILES[]['error']详解`

| 值   | 错误描述                                                     |
| ---- | ------------------------------------------------------------ |
| 0    | 正确                                                         |
| 1    | 文件大小超过了php.ini中允许的最大值       upload_max_filesize=100M |
| 2    | 文件大小超过了表单允许的最大值                               |
| 3    | 只有部分文件上传                                             |
| 4    | 没有文件上传                                                 |
| 6    | 找不到临时文件                                               |
| 7    | 文件写入失败                                                 |

```php+HTML
<input type="hidden" name="MAX_FILE_SIZE" value="100">
```

​		注意:

​			MAX_FILE_SIZE必须在文件域的上面

   		 只要掌握错误号：0和4

### 	10.3 将上传文件移动到指定位置

​	函数：

```php
move_uploaded_file(临时地址，目标地址)
```

​	代码:

```php+HTML
 <?php
        if (!empty($_POST)) {
            if ($_FILES['face']['error'] == 0) { //上传正确
                //文件上传
                move_uploaded_file($_FILES['face']['tmp_name'], './'.$_FILES['face']['name']);
            } else {
                echo '上传有误'.$_FILES['face']['error'];
            }
        }
    ?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form>
```

​	小结：

​			上传的同名文件要给覆盖

### 	10.4 与文件上传有关的配置

```php
post_max_size = 8M:表单中允许的最大值
upload_max_filesize = 2M:允许上传的文件大小
upload_tmp_dir = F:\php\www:指定临时文件的地址
file_upload = On：是否允许多文件上传
max_file+uploads = 20 :允许同时上传多少个(20)文件 
```



## 11、优化文件上传

### 	11.1 更改文件名	

​			方法一：通过时间戳做文件名

```php+HTML
<?php
        if (!empty($_POST)) {
            if ($_FILES['face']['error'] == 0) {
                $name = strchr($_FILES['face']['name'], '.'); //从最后一个点开始截取，一直截取到最后
                move_uploaded_file($_FILES['face']['tmp_name'], './'.time().rand(100, 999).$name);
            } else {
                echo '上传有误'.$_FILES['face']['error'];
            }
        }
?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
```

​			方法二：通过uniqid()实现

```php+HTML
 <?php
        if (!empty($_POST)) {
            if ($_FILES['face']['error'] == 0) {
                // 通过uniqid()生成一个唯一ID
                move_uploaded_file($_FILES['face']['tmp_name'], './'.uniqid().$name); //生成唯一ID
                move_uploaded_file($_FILES['face']['tmp_name'], './'.uniqid('img_').$name); //生成带有前缀的唯一ID
                move_uploaded_file($_FILES['face']['tmp_name'], './'.uniqid('img_', true).$name);  //生成带有前缀的唯一ID+随机数
            } else {
                echo '上传有误'.$_FILES['face']['error'];
            }
        }
?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
```

### 	11.2 验证文件格式

​		方法一：判断文件的拓展名(不能失败文件伪装)

​		操作思路:将文件的后缀和允许的后缀对比

```php+HTML
<body>
    <?php
        if (!empty($_POST)) {
            $allow = ['.jpg','.png','.gif']; //允许的扩展名
            $ext = strchr($_FILES['face']['name'], '.');  //上传的扩展名
            if (in_array($ext, $allow)) {  //通过in_array查找$allow数组中是否包含$ext
                echo '允许上传';
            } else {
                echo '文件不合法';
            }
        }
    ?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
</body>

```

​		注意:比较扩展名不能防止文件伪装

​		方法二：通过`$_FILES[]['type']`类型(不能识别文件伪装)

```php+HTML
<body>
    <?php
        if (!empty($_POST)) {
            $allow = ['image/jpeg','image/png','image/gif']; //允许的类别
            $ext = $_FILES['face']['type'];  //上传文件的类型
            if (in_array($ext, $allow)) {
                echo '允许上传';
            } else {
                echo '文件不合法';
            }
        }
    ?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
</body>

```

​		注意：比较`$_FILES[]['type']`类型不能防止文件伪装

​		方法三:php_fileinfo扩展(可以防止文件伪装)

​			在php.ini中开启fileinfo扩展

```php
extension=fileinfo
```

​		注意：开启fileinfo扩展以后，就可以使用finfo_*的函数了

```php+HTML
<body>
    <?php
        if (!empty($_POST)) {
            // $allow = ['image/jpeg','image/png','image/gif']; //允许的类别
            // $ext = $_FILES['face']['type'];  //上传文件的类型
            // if (in_array($ext, $allow)) {
            //     echo '允许上传';
            // } else {
            //     echo '文件不合法';
            // }

            // fileinfo
            
            // 允许的mime类型
            $allow = ['image/jpeg','image/png','image/gif'];
            // 第一步:创建finfo资源
            $info = finfo_open(FILEINFO_MIME_TYPE);
            // var_dump($info);//resource(2) of type (file_info)
            // 第二步：将finfo资源和文件做比较
            // 获取文件的mime类型
            $mime = finfo_file($info, $_FILES['face']['tmp_name']);
            // 第三部：比较是否合法
            if (in_array($mime, $allow)) {
                echo '合法文件';
            } else {
                echo '文件不合法';
            }
        }
    ?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
</body>
```

​		小结：

​			1、可以验证拓展名(不可以防止文件伪装)

​			2、通过`$_FILES[][type]`验证(不可以防止文件伪装)

​			3、通过file_info拓展(可以防止文件伪装)

### 	11.3 优化文件上传例题

​		步骤

​		第一步：验证是否有误

​		第二步：验证格式

​		第三步：验证大小

​		第四步：验证是否是http上传

​		第五步：上传实现

​		代码：

```php+HTML
<body>
    <?php
        function check($file)
        {
            // 第一步验证是否有误
            if ($file['error'] != 0) {
                switch ($file['error']) {
                    case 1:
                        echo '文件大小超过了php.ini中允许的最大值'.ini_get('update_max_filesize');
                        return false;
                    case 2:
                        echo '文件大小超过表单允许上传的最大值';
                        return false;
                    case 3:
                        echo '只有部分上传';
                        return false;
                    case 4:
                        echo '没有上传文件';
                        return false;
                    case 6:
                        echo '找不到临时文件';
                        return false;
                    case 7:
                        echo '文件写入失败';
                        return false;
                    default:
                        echo '未知错误';
                        return false;
                 }
            }
            // 2、验证格式
            $info = finfo_open(FILEINFO_MIME_TYPE);
            $mime = finfo_file($info, $file['tmp_name']);
            $allow = ['image/jpeg','image/png','image/gif'];
            if (!in_array($mime, $allow)) {
                echo '只能上传'.implode(',', $allow).'格式';
                return false;
            }
            // 3、验证大小
            $size = 999999999;
            if ($file['size'] > $size) {
                echo '文件大小不能超过'.number_format($size/1024, 1).'K';
                return false;
            }
            // 4、验证是否是http上传
            if (!is_uploaded_file($file['tmp_name'])) {
                echo '文件不是HTTP POST上传的<br/>';
                return false;
            }

            return true;
        }

        if (!empty($_POST)) {
            if (check($_FILES['face'])) {
                // 文件上传
                $foldername = date('Y-m-d'); //文件夹的名称
                $folderpath = "./uploads/{$foldername}";   // 文件夹路径
                // 判断文件是否存在
                if (!is_dir($folderpath)) {
                    // 创建文件夹
                    mkdir($folderpath);
                }
                $filename = uniqid('img_', true).strrchr($_FILES['face']['name'], '.'); //文件名称
                $filepath = "$folderpath/$filename";
                if (move_uploaded_file($_FILES['face']['tmp_name'], $filepath)) {
                    echo "文件上传成功,路径是{$foldername}/{$filename}";
                } else {
                    echo '文件上传失败<br/>';
                }
            }
        }
    ?>
    <form action="" method="POST" enctype="multipart/form-data">
        <input type="file" name="face"> <br>
        <input type="submit" value="上传" name="btn">
    </form> 
</body>
```

​	小结：

​		3、将时间戳转换格式

```php
    echo date('Y-m-d H:i:s', time()),'<hr/>'; //将时间戳转换成年-月-日 小时：分钟：秒
    echo date('Y-m-d H:i:s'); //将当前的时间转成对于的格式
```

​		2、设置时区(php.ini)

```php
date.timezone=Asia/Shanghai 或者 date.timezone=PRC(People's Republic of China 中华人民共和国)
```

​		3、php的执行可以不需要Apache的参与

## 12、面向对象的介绍

### 	12.1介绍

​		面向对象是一个编程思想。编程思想有面向过程和面向对象

​		面向过程：编程思路集中在过程上‘

​		面向对象：编程思路集中在参与的对象

### 	12.2 面向对象的好处

​		1.多人合作方便’

​		2.减少代码冗余，灵活性高

​		3.代码的可重复性发挥到极致

​		4.可拓展性强

## 13 类和对象

​	1、对象是具体存在的事物，对象是由属性(变量)和方法(函数)组成的



​	2、类是具有相同属性和行为的一组对象的集合



​	结论：在开发的时候，先写类，通过类创建对象，然后调用对象的属性和方法实现功能。类--对象--调用成员

## 14 在PHP中实现类和对象

### 	14.1 创建类

​		语法：

```php
class 类名{
    //属性
    //方法
    //常量
}
//类是由属性、方法、常量组成的，也可以说类成员有：属性、方法、常量
```

​		类名的命名规则：	

```php
//1、以字母、下划线开头、后面跟字母、数字、下划线
//2、不能同PHP关键字做类名
//3、类名不区分大小写(变量名区分，关键字，类名不区分大小写)
//4、类名用帕斯卡命名法(大驼峰 单词的首字母大写)
class Student{
    
}
```

### 	14.2 对象实例化

​		通过new关键字实例化对象

```php
<?php
// 定义类
class Student
{
}
// 实例化对象
$stu1 = new Student();
$stu2 = new Student; //小括号可以省略

var_dump($stu1, $stu2); //object(Student)#1 (0) { } object(Student)#2 (0) { }
```

### 	14.3 对象的比较

​		**注意：对象的传递是地址传递**

​		相等：结构和保存的值一样就相等

​		全等：指向同一个对象才是全等

```php
<?php
// 定义类
class Student
{
}
// 实例化对象
$stu1 = new Student();
$stu2 = new Student; //小括号可以省略
$stu3 = $stu2; // 对象传递的是地址
var_dump($stu1, $stu2, $stu3); //object(Student)#1 (0) { } object(Student)#2 (0) { } object(Student)#2 (0) { }
// 对象比较
var_dump($stu1 == $stu2);   //bool(true),比较对象的结构
echo '<hr>';
var_dump($stu1 === $stu2);  //bool(false) $stu1和$stu2是否是同一个对象
echo '<hr>';
var_dump($stu2 === $stu3);  //bool(true) $stu2和$stu3是同一个对象
```

## 15 属性

```php
//属性本质就是变量
//通过 ->调用对象的成员	对象名->属性名 对象名->方法名
<?php
// 定义类
class Student
{
    public $name;               //属性
    public $add = '地址不详';
}
// 实例化对象
$stu = new Student;
// print_r($stu);   //Student Object ( [name] => [add] => 地址不详 )

// 操作属性
// 1、给属性赋值
$stu->name = '张三';
$stu->add = '北京';
// 2、获取属性值
echo '姓名:' . $stu->name, '<br/>';     //姓名:张三
echo '地址:' . $stu->add, '<br/>';      //地址:北京
//3、添加属性
$stu->age = 20;
print_r($stu);      //Student Object ( [name] => 张三 [add] => 北京 [age] => 20 ) 
echo '<br/>';
// 4、删除属性
unset($stu->add);
print_r($stu);      //Student Object ( [name] => 张三 [age] => 20 )
```

## 16 方法

​	方法本质就是函数

```php
<?php
class Student
{
    // 定义方法
    public function show()
    {
        echo '这是show方法<hr/>';
    }
    // public 可以省略，如果省略，默认就是public
    // 属性前面的public不能省略
    function test()
    {
        echo '这是test方法<hr/>';
    }
}
$stu = new Student;
$stu->show();
$stu->test();

```

## 17 访问修饰符

​	用来控制成员的访问权限

​	

|       修饰符        |           描述           |
| :-----------------: | :----------------------: |
|   public(公有的)    | 在类的内部和外部都能访问 |
|   private(私有的)   |    只能在类的内部访问    |
| protected(受保护的) |    在整个继承链的访问    |

​	一般来说，属性都用私用，通过公有方法对私有属性进行赋值和取值。来保证数据的合法性

```php
//$this 表示当前调用当前方法的对象
<?php
// 访问修饰符
class Student
{
    private $name;  //私有属性
    private $sex;   //私有属性
    // 通过公有方法对私有属性进行辅助
    public function setInfo($name, $sex)
    {
        if ($sex != '男' && $sex != '女') {
            echo '性别必须为男或女';
            exit;
        }
        $this->name = $name;   //$this表示当前对象
        $this->sex = $sex;
    }
    // 显示信息
    public function getInfo()
    {
        echo '姓名:' . $this->name, '<br/>';
        echo '性别:' . $this->sex, '<br/>';
    }
}
// 实例化
$stu = new Student;
$stu->setInfo('张三', '男');
$stu->getInfo();
echo '<hr/>';
$stu2 = new Student;
$stu2->setInfo('李四', '女');
$stu2->getInfo();

//运行结果
姓名:张三
性别:男
------------
姓名:李四
性别:女
```

## 18 封装

​	封装就是有选择性的提供数据

​	通过访问修饰符来实现封装

## 19 构造方法

### 	19.1 介绍

​		构造方法也叫构造函数，当实例化对象的时候自动执行

​		语法：

```php
function __construct(){

}
//前面是两个下划线
```

​		例题:

```php
<?php
class Student
{
    public function __construct()
    {
        echo '这是构造方法';
    }
}
$stu = new Student;     //这是构造方法
new Student;     //这是构造方法
```

​		**注意：在其他语言类，与类名同名的函数就是构造函数，在PHP中不允许这种写法**

```php
<?php
class Student
{
    // 和类同名的方法是构造方法，在PHP中不建议使用
    public function Student()
    {
        echo '这是构造方法';
    }
}
/*
Deprecated: Methods with the same name as their class will not be constructors in a future version of PHP; Student has a deprecated constructor in D:\phpstudy_pro\WWW\PHP\33-构造方法.php on line 2
*/
```

### 	19.2 构造函数的作用：初始化成员变量

```php
<?php
class Student
{
    private $name;
    private $sex;
	//初始化成员变量
    public function __construct($name, $sex)
    {
        $this->name = $name;
        $this->sex = $sex;
    }
    // 显示信息
    public function show()
    {
        echo '姓名：' . $this->name, '<br/>';
        echo '性别：' . $this->sex, '<br/>';
    }
}
//实例化
$stu = new Student('zs', '男');
$stu->show();
/*运行结果
姓名：zs
性别：男*/
```

**注意：构造函数可以带参数，但不能有return。**

## 20 析构方法

### 	20.1 介绍

​		当对象销毁的时候自动调用

​		语法：

```php
function __destruct(){
    
}
```

​		**析构函数不可以带参数**

​		例题:

```php
<?php
class Student5
{
    private $name;
    // 构造方法
    public function __construct($name)
    {
        $this->name = $name;
        echo "{$name}创建了", '<br/>';
    }
    // 析构方法
    public function __destruct()
    {
        echo "{$this->name}销毁了", '<br/>';
    }
}

$stu = new Student5('zs');
$stu2 = new Student5('ls');
$stu3 = new Student5('zl');
echo '<hr>';
/*
运行结果
zs创建了
ls创建了
zl创建了
----------
zl销毁了
ls销毁了
zs销毁了
*/
```

### 	20.2 计算机的内存管理

​		计算机内存管理方法：先进先出，先进后出

​		先进先出的内存管理方式一般用在业务逻辑中，比如秒杀，购票等等

​		先进后出是计算机的默认内存管理方式

## 21 继承

### 		21.1 介绍

​		1.继承使得代码具有层次

​		2.子类继承了父类的属性和方法，实现了代码的可重用性

​		3.使用extends关键字实现继承

​		4.父类和子类是相对的

​		语法：

```php
class 子类 extends 父类{

}
```

​		例题:

```php
<?php
// 父类
class Person
{
    public function show()
    {
        echo '这是人类<br>';
    }
}
// 子类继承父类
class Student6 extends Person
{
}
// 测试
$stu = new Student6;
$stu->show();	//这是人类
```

​		执行过程：

​		第一步：在Student类中查找show()，如果找到就用，找不到就到父类中查找

​		第二步：在Person类中查询show()

### 		21.2 子类中调用父类成员

```php
<?php
// 父类
class Person
{
    public function show()
    {
        echo '这是人类<br>';
    }
}
// 子类继承父类
class Student6 extends Person
{
    public function test()
    {
        // 方法一
        $person = new Person;
        $person->show();        //这是人类

        // // 方法二
        $this->show();       //这是人类
    }
}
// 测试
$stu = new Student6;
$stu->test();
```

​		小结：

​		1、方法一：通过实例化父类调用父类成员

​		2、方法二：通过$this关键字调用父类成员

### 		21.3 protected

​		protected:受保护的，在整个继承链上使用

​		例题:

```php
//例题一
class A
{ 
    protected $num = 10;  //在整个继承链上访问
}
class B extends A
{
    public function getNum()
    {
        echo $this->num;
    }
}
// 测试
$obj = new B;   //整个继承链上有A和B
$obj->getNum();

//例题二
class A
{
    public function getNum()
    {
        echo $this->num;
    }
}
class B extends A
{
    protected $num = 10;
}
// 测试
$obj = new B;		//整个继承链上有A和B
$obj->getNum();

//例题三
class A
{
    public function getNum()
    {
        echo $this->num;
    }
}
class B extends A
{
    protected $num = 10;
}
// 测试
$obj = new A; //整个继承链上
$obj->getNum(); //Notice：Undefined property：A::$num

```

### 		21.4 继承中的构造函数

​		规则：

```
1、如果子类有构造函数就调用子类的，如果子类没有就调用父类的构造函数

2、子类的构造函数调用后，默认不在调用父类的构造函数
```

​		通过类名调用父类的构造函数

```php
类目::__construct()
```

​		例题:

```php
<?php
class Person2
{
    //父类的构造函数
    public function __construct()
    {
        echo '这是父类<br/>';
    }
}
class Student7 extends Person2
{
    //子类的构造函数
    public function __construct()
    {
        Person2::__construct();     //通过父类的名字调用父类的构造函数
        parent::__construct();      //parent表示父类的名字
        echo '这是子类<br/>';
    }
}
// 测试
new Student7();
```

​		**parent关键字表示父类的名字，可以降低程序的耦合性**

​		例题：给父类传递参数

```php
<?php
class Person2
{
    protected $name;
    protected $sex;
	//父类的构造函数
    public function __construct($name, $sex)
    {
        $this->name = $name;
        $this->sex = $sex;
    }
}
class Student7 extends Person2
{
    private $score;
    //子类的构造函数
    public function __construct($name, $sex, $score)
    {
        parent::__construct($name, $sex);       //调用父类构造函数并传递参数
        $this->score = $score;
    }
    //显示信息
    public function getInfo()
    {
        echo "姓名:{$this->name}<br/>";
        echo "性别:{$this->sex}<br/>";
        echo "成绩:{$this->score}";
    }
}
// 测试
$stu = new Student7('zs', '男', 84);
$stu->getInfo();

/*结果
姓名:zs
性别:男
成绩:84
*/
```

### 		21.5 $this详解

​		$this表示当前对象的引用，也就是说$this保存的当前对象的地址

```php
<?php
class C
{
    public function __construct()
    {
        var_dump($this);
    }
}
class D extends C
{
}
new C();        //object(C)#1 (0) { }
echo '<br/>';
new D();        //object(D)#1 (0) { }

```

### 		21.6 多重继承

​		PHP不允许多重继承，因为多重继承容易产生二义性

​		如何实现C继承A和B，使用继承链

![image-20220610113703691](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610113703691.png)

## 22 多态

​	多态：多种形态

​	多态分为两种，方法重写和方法重载

### 	22.1 方法重写

​		子类重写了父类同名的方法

```php
<?php
// 父类
class Person3
{
    public function show()
    {
        echo '父类<br/>';
    }
}
// 子类
class Student8 extends Person3
{
    // 子类重写了父类的同名方法
    public function  ()
    {
        echo '子类<br/>';
    }
}
// 测试
$stu = new Student8;
$stu->show();
```

​		注意事项:

```
1.子类方法必须和父类的方法同名

2.参数个数要一致

3.子类修饰的不能比父类更加严格
```

![image-20220610140643461](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610140643461.png)

![image-20220610140804850](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610140804850.png)

### 	22.2 方法重载

​		在同一个类中，有多个同名的函数，通过参数的不同来区分不同的方法，称为重载

![image-20220610141115493](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610141115493.png)

​		**PHP不支持方法重载，但是可以通过其他方法来模拟方法重载**

## 23 面向对象的三大特性

​	1.封装

​	2.继承

​	3.多态

## 24 私有属性继承和重写

​	私有属性可以继承但不能重写

```php
<?php
class A
{
    private $name = 'PHP';
    public function showA()
    {
        // var_dump($this); //object(B)#1 (2) { ["name":"B":private]=> string(4) "Java" ["name":"A":private]=> string(3) "PHP" } 
        echo $this->name, '<br>';       //PHP
    }
}
class B extends A
{
    private $name = 'Java';
    public function showB()
    {
        // var_dump($this);    //object(B)#1 (2) { ["name":"B":private]=> string(4) "Java" ["name":"A":private]=> string(3) "PHP" } 
        echo $this->name, '<br>';       //Java
    }
}
$obj = new B();
$obj->showA();
$obj->showB();
/*分析:
showA()和showB()中的$this都表示B的对象，B继承了A的私有属性，所以B中有两个$name
在showA()中只能访问A中的$name，不能访问B中的$name;
在showB()中只能访问B中的$name,不能访问A中的$name
*/
```

​	例题

```php
//例题一
class A{
    protected $name = 'tom';
    public function showA(){
        echo $this->name,'<br>';
    }
}
class B extends A{
    public $naem = 'berry';
    public function showB(){
        echo $this->name,'<br>';
    }
}
//测试
$obj = new B();
$obj->showA();	//berry
$obj->showB(); 	//berry
/*
分析：B中将A的$name重写，所以$obj中只有一个$name,($name='berry'),不管$this在那个方法中访问，就只能访问这个$naem
*/
//例题二
class A{
    private $name = 'tom';
    public function showA(){
        exho $this->name,'<br>';
    }
}
class B extends A{
    public $name = 'berry';
    public function showB(){
        exho $this->name,'<br>';
    }
}
//测试
$obj = new B();
$obj->showA();	//tom
$obj->showB();	//berry
/*
分析：
$obj中有两个$name，一个是私有的，一个是公有的
在showA()中既能访问私有的$name,也能访问公有的$name,但是私有的比公有的权限高，所以输出tom
在showB()中不能访问私有的$name,只能访问公有的$naem，所以输出berry
*/
```

## 25 方法修饰符

​	方法修饰符有：static、final、abstract

### 	25.1 static【静态的】

​		1.static修饰的属性叫静态属性、static修饰的方法叫静态方法

​		2.静态成员加载类的时候分配空间，程序执行完毕后销毁

​		3.静态成员在内存中就一份

​		4.调用语法 类名：：属性   类名：：方法名()

```php
<?php
class Person
{
    public static $add = 'beijing';
    static public function show()	//修饰符之间没有顺序
    {
        echo '这是一个静态方法<br>';
    }
}
echo Person::$add, '<br>';  //beijing
Person::show();             //这是一个静态方法
```

​		统计在线人数

```php
<?php
class Student8
{
    private static $num = 0;    //静态变量，在内存中就一份
    public function __construct()
    {
        self::$num++;  //self 表示当前类的名字
    }
    public function show()
    {
        echo '总人数是:' . self::$num, '<br>';
    }
    public function __destruct()
    {
        self::$num--;
    }
}

$stu = new Student8;
$stu2 = new Student8;
$stu3 = new Student8;
$stu4 = new Student8;
$stu5 = new Student8;
$stu4->show();  //总人数是:5
unset($stu5);
$stu4->show();  //总人数是:4
```

​		**self 表示当前类的名字，使用self降低耦合性**

​		静态成员也可以被继承

```php
<?php
class Person3
{
    public static $add = '中国';
    public static function show()
    {
        echo '这是人类<br>';
    }
}
// 继承
class Student9 extends Person3
{
}
// 测试
echo student9::$add, '<br>'; //中国		通过子类名称访问父类的静态成员
Student9::show();			//这是人类

```

​		静态延时绑定

​		static表示对象所属的类

```php
<?php
class Person4
{
    public static $type = '人类';
    public function show()
    {
        var_dump($this);        //object(Student10)#1 (0) { } 
        echo static::$type;     //学生   延时绑定
        echo self::$type;       //人类
    }
}
class Student10 extends Person4
{
    public static $type = '学生';
    public function show2()
    {
        var_dump($this);        //object(Student10)#1 (0) { } 
        echo static::$type;     //学生
        echo self::$type;       //学生
    }
}
$obj = new Student10;
$obj->show();
$obj->show2();

```

​		小结：

```
1、static在内存中就一份，在类加载的时候分配空间
2、如果有多个修饰符，修饰符之间没有顺序
3、self 表示当前类的名字
4、static表示当前对象所属的类
5、static有两个作用，第一表示静态的，第二表示类名
```

### 	25.2 final【最终的】

​		final修饰的方法不能被从写

​		final修饰的类不能被继承

![image-20220610163929718](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610163929718.png)

![image-20220610163958899](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220610163958899.png)

​		作用：

​		1、如果一个类确定不被继承，一个方法不会被重写，用final修饰可以提高效率

​		2、如果一个方法不允许被其他类重写，可以用final修饰

### 	25.3 abstract【抽象的】

​	1.abstract修饰的方法是抽象方法，修饰的类是抽象类

​	2.只有方法的声明没有方法的实现称为抽象方法

​	3.一个类中只要有一个方法是抽象方法，这个类必须是抽象类

​	4.抽象类的特点是不能被实例化

​	5.子类继承了抽象类，就必须重新实现父类所有的抽象方法，否则不允许实例化

​	6.类中没有抽象的方法也可以声明成抽象类，用来组织类的实例化

​	例题

```php
<?php
//抽象类
abstract class Person5
{
    public abstract function setInfo(); //抽象方法
    public function getInfo()
    {
        echo '获取信息<br>';
    }
}
//继承
class Student12 extends Person5
{
    //重写父类的抽象方法
    public function setInfo()
    {
        echo '重新实现父类的抽象方法<br>';
    }
}
//测试
$stu = new Student12;
$stu->setInfo();        //重新实现父类的抽象方法
$stu->getInfo();        //获取信息

```

​	抽象类的作用：

​	1 定义命名规范

![image-20220611080317208](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220611080317208.png)

​	2、阻止实例化，如果一个类中所有方法都是静态方法，这时候没有必要去实例化，可任意通过abstract来阻止实例化



## 26 类常量

​	类常量是const常量

```php
<?php
class Student13
{
    // public const ADD = '地址不详';       //7.1版本后才支持访问修饰符
    const ADD = '地址不详';
}
echo Student13::ADD; 
```

​	问： define和const常量的区别？

​	答： const常量可以做类成员，define常量不可以做类成员

​	问： 常量和静态属性的区别

​	答： 相同点：都在加载时分配空间

​	 	    不同点：常量的值不可以更改，静态属性可以更改

## 27 接口（interface）

### 		27.1 接口

​		1.如果一个类中所有的方法都是抽象方法，那么这个抽象类可以声明成接口

​		2.接口是一个特殊的抽象类，接口中只能有抽象方法和常量

​		3.接口中的抽象方法只能是public，可以省略，默认也public

​		4.通过implement关键字来实现接口

​		5.不能使用abstract和final来修饰接口中的抽象方法

```php
<?php
// 声明接口
interface IPerson
{
    const ADD = '中国';
    function fun1();
    function fun2();
}
// 实现接口
class Student14 implements IPerson
{
    public function fun1()
    {
    }
    public function fun2()
    {
    }
}
// 访问接口中的常量
echo IPerson::ADD;
```

### 		27.2 接口的多重实现

​		类不允许多重继承，但是接口允许多重实现

```php
// 接口多重实现

interface Iperson
{
    function fun1();
}

interface Iperson2
{
    function fun2();
}
// 接口运行多重实现
class Student14 implements Iperson, Iperson2
{
    public function fun1()
    {
    }
    public function fun2()
    {
    }
}
```

​		**在接口的多重实现中，如果有重名的方法，只要实现一次即可**

​		**类可以继承的同时实现接口**

```php
class Student extends Person implements Iperson,Iperson2{
   
}
```

## 28 匿名类

​	**PHP7.0以上支持**

```php
<?php

$stu = new class
{
    public $name = 'tom';
    public function __construct()
    {
        echo '构造函数<br>';
    }
};
echo $stu->name;
/*运行结果：
构造函数
tom
*/
```

​	**如果类只被实例化一次就可以使用匿名类**

​	**好处：实例化完毕后就回收了类的空间**

## 29 方法绑定

​	**PHP7.0以上支持**

​	将方法绑定到对象上，并调用

​	语法：

```php
闭包->call(对象)：将闭包绑定到对象上，并调用
```

​	在php中匿名函数称为闭包

​	例题：

```php
<?php
$lang = 'en';
//类
class Student15
{
}
// 匿名函数
if ($lang == 'ch') {
    $fun = function () {
        echo '我是一名学生';
    };
} else {
    $fun = function () {
        echo 'i am astudent';
    };
}
// 绑定
$stu = new Student15;
$fun->call($stu);       //i am astudent

```



## 30 异常处理

​	集中处理在代码块中发生的异常

​	在代码块中发生了异常直接抛出，代码块中不处理异常，将异常集中起来一起处理

### 		30.1 使用的关键字

```php
try：检查代码块
catch：捕获异常
throw：抛出异常
finally：无论有无异常都会执行，可以省略
Exception:异常类
```

​		语法结构：

```php
try:{
    //检测代码
}catch(Exception $ex){
    //捕获异常
}
finally{
    //不论是否有异常，都要执行，finally可以省略
}
```

​		例题：

```php+HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <?php
    if (isset($_POST['button'])) {
        try {
            $age = $_POST['age'];
            if ($age == '') {
                throw new Exception('年龄不能为空', 10001);             //抛出异常
            }
            if (!is_numeric($age)) {
                throw new Exception('年龄必须是数字', 10002);           //抛出异常
            }
            if (!($age >= 10 && $age <= 30)) {
                throw new Exception('年龄必须在10~30之间', 10003);      //抛出异常
            }
            echo '年龄在正常范围之内';
        } catch (Exception $ex) {       //捕获异常
            echo '错误信息:' . $ex->getMessage(), '<br>';
            echo '错误码:' . $ex->getCode(), '<br>';
            echo '文件地址:' . $ex->getFile(), '<br>';
            echo '错误行号:' . $ex->getLine(), '<br>';
        }
    }
    ?>
    <form action="" method="POST">
        年龄: <input type="text" name="age" id=""><br>
        <input type="submit" value="提交" name="button">
    </form>
</body>

</html>
```

​		**抛出异常后，try块终止运行，执行权限交给catch块**

### 		30.2 自定义异常

​		场景：如果实现异常分类处理？比如异常有三个级别对应三种处理方式

​		自定义三种异常即可

​		所有异常类的父类是Exception，Exception中的方法不允许重写

```php+HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <?php
    // 自定义空异常类
    class MyNullException extends Exception
    {
    }
    // 自定义类型异常类
    class MyTypeException extends Exception
    {
    }
    // 自定义范围异常类
    class MyRangeException extends Exception
    {
    }
    // 逻辑代码
    if (isset($_POST['button'])) {
        try {
            $name = $_POST['name'];
            $age = $_POST['age'];
            if ($name == '') {
                throw new MyNullException('姓名不能为空', 10001);
            }
            if ($age == '') {
                throw new MyNullException('年龄不能为空', 20001);
            } elseif (!is_numeric($age)) {
                throw new MyTypeException('年龄不是数字', 20002);
            } elseif ($age < 10 || $age > 30) {
                throw new MyRangeException('超出年龄范围10~30', 20003);
            }
        } catch (MyNullException $ex) {
            echo $ex->getMessage();
            echo '错误记录保存在日志中';
        } catch (MyTypeException $ex) {
            echo $ex->getMessage();
            echo '发送电子邮件';
        } catch (MyRangeException $ex) {
            echo $ex->getMessage();
            echo '给管理员打电话';
        }
    }
    ?>
    <form action="" method="POST">
        姓名：<input type="text" name="name"> <br>
        年龄: <input type="text" name="age"><br>
        <input type="submit" value="提交" name="button">
    </form>
</body>

</html>
```

## 31 自动加载类

​	在项目开发中，因为一个文件只能写一个类，并且在执行过程中会有很多的类参与，如果一个一个加载很麻烦，所有，就需要一个机制实现在PHP执行过程中自动加载需要的类

### 			31.1 书写类的规则

​		1.一个文件只能放一个类(必须)

​		2.文件名和类名同名(必须)

​		3.类文件以.class.php结尾

### 			31.2 手动加载类

​		1、创建`Goods1.class.php`页面

```php
<?php
abstract class Goods1
{
    protected $name;
    public final function setName($naem)
    {
        $this->name = $naem;
    }
    public abstract function getName();
}
```

​		2、创建`Book.class.php`页面

```php
<?php
class Book extends Goods1
{
    public function getName()
    {
        echo "《{$this->name}》<br>";
    }
}
```

​		3、创建`Phoen.class.php`页面

```php
<?php
class Phone extends Goods1
{
    public function getName()
    {
        echo $this->name;
    }
}
```

​		4、在PHP页面加载类文件

```php
<?php
require './54-53/Goods1.class.php';		//手动加载类文件
require './54-53/Book.class.php';		//手动加载类文件
require './54-53/Phone.class.php';		//手动加载类文件
// 测试
$book = new Book;
$book->setName('面向对象编程');
$phone = new Phone;
$phone->setName('HAWEI MATE 40 PRO');
$book->getName();
$phone->getName();
//运行结果
//《面向对象编程》
//HAWEI MATE 40 PRO
```

### 			31.3 自动加载类 方法一 : __autoload()函数

​		当缺少类的时候自动调用`__autoload()`函数，并且将缺少的类名作为参数传递给`__autoload()`

```php
<?php
/*
* 自动加载类
* @param $class_name string 缺少的类名
*/
function __autoload($class_name)
{
    require "./54-53/{$class_name}.class.php";
}
// 测试
$book = new Book;
$book->setName('面向对象编程');
$phone = new Phone;
$phone->setName('HAWEI MATE 40 PRO');
$book->getName();
$phone->getName(); 
```

​		**__autoload()函数在PHP7.2以后就不在支持了**

### 			31.4 自动加载类 方法二：spl_autoload_register()

​		注册__autoload()函数

```php
<?php
//方法一
/* 
// 加载类函数
function loadClas($class_name)
{
    require "./54-53/{$class_name}.class.php";
}
// 注册加载函数
spl_autoload_register('loadClas');
*/

// 方法二
spl_autoload_register(function ($class_name) {
    require "./54-53/{$class_name}.class.php";
});
// 测试
$book = new Book;
$book->setName('面向对象编程');
$phone = new Phone;
$phone->setName('HUAWEI MATE40 PRO');
$book->getName();
$phone->getName();

```

​		1、spl_autoload_register()可以注册多个自动加载函数

```php
<?php
function load1($class)
{
    require "./54-53/{$class}.class.php";
}
function load2($class)
{
    require "./54-53/{$class}.class.php";
}
function load3($class)
{
    require "./54-53/{$class}.class.php";
}
spl_autoload_register('load1');
spl_autoload_register('load2');
spl_autoload_register('load3');

```

​		2、PHP5.1以后就开始支持此函数

### 			31.5 类文件存储不规则的加载方法

​		将类文件和文件名地址做一个映射，组成一个关联数组

```php
 $map=array(
     	//类名  =》 文件地址
    	'Goods' => './aa/Goods.class.php',
        'Book'  => './bb/Book.class.php',
        'Phone' => './cc/phone.class.php'
    );
```

​		代码：

```php
<?php
spl_autoload_register(function($class_name){
    //类名和文件地址映射成一个关联数组
    $map=array(
    	'Goods' => './aa/Goods.class.php',
        'Book'  => './bb/Book.class.php',
        'Phone' => './cc/phone.class.php'
    );
    //在映射数组中查找是否包含
    if(isset($map[$class_name])){
        require $amp[$class_name];
    }
});
//测试
$book = new Book;
$book ->setName('面向对象编程');
$phone = new Phone;
$phone ->setName('HUAWEI MATE 40 PRO');
$book -> getName();
$phone -> getName();
```

​		**在项目中，绝大部分都是规则存储的，不规则的比较少**

## 32 clone和_clone()

​	创建对象的方式有哪些？

```
方式一：实例化
方式二：克隆
```

​	例题

```php
<?php
class Student15
{
    public function __clone()
    {
        echo '正在克隆对象<br>';
    }
}

$stu1 = new Student15;
$stu2 = clone $stu1;
var_dump($stu1, $stu2);     //object(Student15)#1 (0) { } <br> object(Student15)#2 (0) { }
```

​	**clone创建对象的方法之一**

​	**当执行clone指令的时候，会自动的调用__clone()方法**

## 33 设计模式

### 33.1 单例模式

​	一个类只能有一个对象

​	应用场景：多次请求数据库只需要一个连接对象

​	实现：三私一公

```
1、私有的静态属性用来保存对象的单例
2、私有的构造方法用来阻止在类的外部实例化
3、私有的__clone用来阻止在类的外部克隆(clone)对象
4、公有的静态方法用来获取对象的单例
```

​	代码：

```php
<?php
// 三私一公
class DB
{
    // 静态的属性用来保存对象的单例
    private static $instance;
    // 私有的构造方法阻止在类的外部实例化
    private function __construct()
    {
    }
    // 私有的__clone()阻止在类的外部克隆(clone)对象
    private function __clone()
    {
    }
    public static function getInstance()
    {
        // 保存的值不属于DB类的类型就实例化
        if (!self::$instance instanceof self) {
            self::$instance = new self;
        }
        return self::$instance;
    }
}
// 测试
$db1 = Db::getInstance();
$db2 = Db::getInstance();
var_dump($db1, $db2);	//object(DB)#1 (0) { } object(DB)#1 (0) { }
```

### 			33.2 工厂模式

​	 特点：传递不同的参数获取不同的对象

```php
<?php
class ProductsA
{
}
class ProductsB
{
}
class ProductsFactory
{
    public function create($num)
    {
        switch ($num) {
            case 1:
                return new ProductsA;
            case 2:
                return new ProductsB;
            default:
                return null;
        }
    }
}
$factory = new ProductsFactory;
$obj1 = $factory->create(1);
$obj2 = $factory->create(2);
var_dump($obj1, $obj2);     //object(ProductsA)#2 (0) { } object(ProductsB)#3 (0) { }

```

### 			33.3 策略模式

​	特点：传递不同的参数调用不同的方法

```php
<?php
class Walk
{
    public function way()
    {
        echo '步行<br>';
    }
}
class Bus
{
    public function way()
    {
        echo '公交<br>';
    }
}
// 策略模式
class Student16
{
    public function play($obj)
    {
        $obj->way();
    }
}
// 测试
$stu1 = new Student16;
$stu1->play(new Walk());	//步行
$stu2 = new Student16;
$stu2->play(new Bus());		//公交
```



## 34 序列化与反序列化

​	在PHP中，数组和对象无法保存，如果需要保存就要将数组或对象转换成一个序列

​	序列化：将数组或对象转成一个序列(serialize)

​	反序列化:将序列化的字符串转换成数组或对象(unserialize)

### 			34.1 数组的序列化与反序列化

```php
<?php
//数组的序列化
/*
$stu = ['tom', 'berry', 'ketty'];
$str = serialize($stu);         //序列化
file_put_contents('./54-53/stu.txt', $str);

*/

//数组的反序列化
$str = file_get_contents('./54-53/stu.txt');
$stu =  unserialize($str);      //反序列化
print_r($stu);      //Array ( [0] => tom [1] => berry [2] => ketty )

```

### 			34.2 对象的序列化与反序列化

​	**注意：对象的反序列化需要有类的参与，如果没有类的在反序列化的时候无法确定类**

​	![image-20220612100306258](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220612100306258.png)

​	代码

```php
<?php
class Student17
{
    public $name;
    protected $sex;
    private $add;
    public function __construct($name, $sex, $add)
    {
        $this->name = $name;
        $this->sex = $sex;
        $this->add = $add;
    }
}
/* 序列化
$stu = new Student17('zs', '男', '背景');
// 序列化 
echo $str = serialize($stu);        //O:9:"Student17":3:{s:4:"name";s:2:"zs";s:6:"*sex";s:3:"男";s:14:"Student17add";s:6:"背景";}
file_put_contents('./54-53/stu.txt', $str);

*/

// 反序列化 类的反序列化必须有类的参与
$str = file_get_contents('./54-53/stu.txt');
$stu = unserialize($str);
echo '<pre>';
var_dump($stu);

//运行结果
/*
object(Student17)#1 (3) {
  ["name"]=>
  string(2) "zs"
  ["sex":protected]=>
  string(3) "男"
  ["add":"Student17":private]=>
  string(6) "背景"
}
*/
```

## 35 魔术方法

​	已经学习的魔术方法

```php
__construct()
__destruct()
__clone()
```

### 			35.1 __tostring()\_\_invoke()

​	`__tostring()`:将对象当成字符串使用的时候自动调用

​	`__invoke()`:将对象当成函数使用的时候自动调用

```php
<?php
class Student18
{
    // 把对象当成字符串使用的时候自动执行
    public function __toString()
    {
        return '这是一个对象，不是字符串<br>';
    }
    // 把对象当成函数使用的时候自动执行
    public function __invoke()
    {
        echo '这是一个对象，不是方法(函数)';
    }
}
$stu = new Student18;
echo $stu;      //当成字符串使用
$stu();         //当成函数使用

```

### 			35.2 __set()\_\_get()\_\_isset()\_\_unset()

```php
__set($name,$value):给无法访问的属性赋值的时候自动执行
__get($name):获取无法访问的属性的时候自动执行
__iset($name):判断无法访问的属性是否存在，自动执行
__unset($name):销毁无法访问的属性的时候自动执行
```

​	例题：

```php
<?php
class Student18
{
    private $name;
    private $sex;
    private $age;
    // 给无法访问的属性赋值的时候自动执行
    public function __set($name, $value)
    {
        $this->$name = $value;
    }
    // 获取无法访问的属性值的时候自动调用
    public function __get($name)
    {
        return $this->$name;
    }
    // 判断无法访问的属性是否存在的时候自动调用
    public function __isset($name)
    {
        return isset($this->$name);
    }
    // 销毁无法访问的属性的时候自动执行
    public function __unset($name)
    {
        unset($this->$name);
    }
}
// 测试
$stu = new Student18;
$stu->name = 'tom';
$stu->sex = '男';
$stu->age = 20;
// echo $stu->name;
// var_dump(isset($stu->name));
unset($stu->age);
print_r($stu);
```

​	应用：设置读写属性

```php
<?php
class Student18
{
    private $name;
    private $add = '中国';
    private $age;
    // 给无法访问的属性赋值的时候自动执行
    public function __set($name, $value)
    {
        if (in_array($name, array('name', 'age')))
            $this->$name = $value;
        else
            echo "{$name}是只读属性<br>";
    }
    // 获取无法访问的属性值的时候自动调用
    public function __get($name)
    {
        if (in_array($name, array('name', 'add')))
            return $this->$name;
        else
            echo "{$name}是只写属性<br>";
    }
    /* 
    // 判断无法访问的属性是否存在的时候自动调用
    public function __isset($name)
    {
        return isset($this->$name);
    }
    // 销毁无法访问的属性的时候自动执行
    public function __unset($name)
    {
        unset($this->$name);
    }
    */
}
// 测试
$stu = new Student18;
$stu->name = 'tom';
// $stu->sex = '男';
$stu->age = 20;

echo '姓名:' . $stu->name, '<br>';
echo '地址:' . $stu->add, '<br>';

```

### 			35.3 __call()\_\_callstatic()

```php
__call($name, $arguments):调用无法访问的方法时自动执行
__callstatic():调用无法访问的静态方法时自动执行
```

​	例题:

```php
<?php
class Student19
{
    /*
    *作用：调用无法访问的方法时自动执行
    *@param $name string  方法名
    *@param $arguments array 参数数组
    */
    public function __call($name, $arguments)
    {
        echo "{$name}方法不存在<br>";
    }
    // 调用无法访问的静态方法时自动执行
    public static function __callStatic($name, $arguments)
    {
        echo "{$name}静态方法不存在<br>";
    }
}

// 测试
$stu = new Student19;
$stu->show(10,20);

Student19::show();

```

### 			35.4 __sleep()\_\_wakeup()

```
__sleep()：当序列化的时候自动执行
__wakeup():当反序列化的时候自动执行
```

​	例题：

```php
<?php
class Student20
{
    private $name;
    private $sex;
    private $add = '中国';

    public function __construct($name, $sex)
    {
        $this->name = $name;
        $this->sex = $sex;
    }
    /*
    *当序列化的时候自动调用
    *@return attay 序列化的字段名 
    */
    public function __sleep()
    {
        return array('name', 'sex');
    }
    //反序列化的时候自动调用
    public function __wakeup()
    {
        $this->type = '学生';
    }
}
$stu = new Student20('tom', '女');
$str = serialize($stu);     //序列化
$stu = unserialize($str);   //反序列化
print_r($stu);

```

## 36 模拟方法重载

​	通过魔术方法模拟方法重载

```php
<?php
class Math
{
    public function __call($name, $arguments)
    {
        $sum = 0;
        foreach ($arguments as $value) {
            $sum += $value;
        }
        echo implode(',', $arguments) . '的和是：' . $sum, '<br>';
    }
}
// 测试
$stu = new Math;
$stu->call(10, 20);
$stu->call(10, 20, 30);
$stu->call(10, 20, 30, 40);

```

## 37 遍历对象

​	**通过foreach遍历对象**

```php
<?php
class Student21
{
    public $name = 'tom';
    protected $sex = '男';
    private $age = 22;
    public function show()
    {
        foreach ($this as $k => $v) {
            echo "{$k}-{$v}<br>";
        }
    }
}

$stu = new Student21;
foreach ($stu as $k => $v) {
    echo "{$k}-{$v}<br>";
}
echo '<hr>';
$stu->show();

```

​	name-tom

------

​	name-tom
​	sex-男
​	age-22

​	**结论：遍历到当前位置所能访问到的属性**

## 38 封装MySQL的单例

### 38.1 分析

​	1、实现单例

​	2、连接数据库

​	3、对数据库进行操作

### 38.2 步骤

​	第一步：实现单例

​	第二步：初始化参数

​	第三步：连接数据库

​	第四步：操作数据

​		1、执行数据操作语句(增、删、改)

​		2、执行数据查询语句

​			返回二维数组

​			返回一维数组

​			返回一行一列

### 38.3代码实现

​	第一步：实现单例

```php
<?php
class MySQLDB
{
    private static $instance;
    private function __construct()
    {
    }

    private function __clone()
    {
    }
    public static function getInstance()
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self();
        }
        return self::$instance;
    }
}
// 测试
$db = MySQLDB::getInstance();
var_dump($db);

```

​	**A instanceof B，表示A是否是B的类型，返回bool值**

​	第二步：初始化参数

```php
<?php
class MySQLDB
{
    private $host;      //主机地址
    private $port;      //端口号
    private $user;      //用户名
    private $password;  //密码
    private $dbname;    //数据库名称
    private $charset;   //字符集
    private $link;      //连接对象
    private static $instance;
    private function __construct($param)
    {
        $this->initParam($param);
        $this->initConnect();
    }
    private function __clone()
    {
    }
    // 获取单例
    public static function getInstance($param = array())
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self($param);
        }
        return self::$instance;
    }
    // 初始化参数
    private function initParam($param)
    {
        $this->host = $param['host'] ?? '127.0.0.1';
        $this->port = $param['port'] ?? '3306';
        $this->user = $param['user'] ?? 'root';
        $this->password = $param['pwd'] ?? 'root';
        $this->dbname = $param['dbname'] ?? '';
        $this->charset = $param['charset'] ?? 'utf8';
    }
}
// 测试
// 配置参数
$param = array(
    'host' => '127.0.0.1',
    'user' => 'root',
    'pwd' => 'zhang0613',
    'port' => '3306',
    'dbname' => 'data'
);
// 获取单例
$db = MySQLDB::getInstance($param);
var_dump($db);

```

​	第三步：连接数据库

```php
<?php
class MySQLDB
{
    private $host;      //主机地址
    private $port;      //端口号
    private $user;      //用户名
    private $password;  //密码
    private $dbname;    //数据库名称
    private $charset;   //字符集
    private $link;      //连接对象
    private static $instance;
    private function __construct($param)
    {
        $this->initParam($param);
        $this->initConnect();
    }
    private function __clone()
    {
    }
    // 获取单例
    public static function getInstance($param = array())
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self($param);
        }
        return self::$instance;
    }
    // 初始化参数
    private function initParam($param)
    {
        $this->host = $param['host'] ?? '127.0.0.1';
        $this->port = $param['port'] ?? '3306';
        $this->user = $param['user'] ?? 'root';
        $this->password = $param['pwd'] ?? 'root';
        $this->dbname = $param['dbname'] ?? '';
        $this->charset = $param['charset'] ?? 'utf8';
    }
    // 连接数据库
    private function initConnect()
    {
        $this->link = @mysqli_connect($this->host, $this->user, $this->password, $this->dbname, $this->port);
        if (mysqli_connect_errno()) {
            echo '数据库连接失败<br>';
            echo '错误信息：' . mysqli_connect_error(), '<br>';
            echo '错误码:' . mysqli_connect_errno(), '<br>';
            exit;
        }
        mysqli_set_charset($this->link, $this->charset);
    }
}
// 测试
// 配置参数
$param = array(
    'host' => '127.0.0.1',
    'user' => 'root',
    'pwd' => 'zhang0613',
    'port' => '3306',
    'dbname' => 'data'
);
// 获取单例
$db = MySQLDB::getInstance($param);
var_dump($db);
```

​	第四步:执行操作功能

​		1、执行数据操作语句(增、删、改)

```php
<?php
class MySQLDB
{
    private $host;      //主机地址
    private $port;      //端口号
    private $user;      //用户名
    private $password;  //密码
    private $dbname;    //数据库名称
    private $charset;   //字符集
    private $link;      //连接对象
    private static $instance;
    private function __construct($param)
    {
        $this->initParam($param);
        $this->initConnect();
    }
    private function __clone()
    {
    }
    // 获取单例
    public static function getInstance($param = array())
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self($param);
        }
        return self::$instance;
    }
    // 初始化参数
    private function initParam($param)
    {
        $this->host = $param['host'] ?? '127.0.0.1';
        $this->port = $param['port'] ?? '3306';
        $this->user = $param['user'] ?? 'root';
        $this->password = $param['pwd'] ?? 'root';
        $this->dbname = $param['dbname'] ?? '';
        $this->charset = $param['charset'] ?? 'utf8';
    }
    // 连接数据库
    private function initConnect()
    {
        $this->link = @mysqli_connect($this->host, $this->user, $this->password, $this->dbname, $this->port);
        if (mysqli_connect_errno()) {
            echo '数据库连接失败<br>';
            echo '错误信息：' . mysqli_connect_error(), '<br>';
            echo '错误码:' . mysqli_connect_errno(), '<br>';
            exit;
        }
        mysqli_set_charset($this->link, $this->charset);
    }
    // 执行数据操作语句（增删改）
    private function execute($sql)
    {
        if (!$rs = mysqli_query($this->link, $sql)) {
            echo 'SQL语句执行失败<br>';
            echo '错误信息:' . mysqli_error($this->link), '<br>';
            echo '错误码:' . mysqli_errno($this->link), '<br>';
            echo '错误的SQL语句:' . $sql, '<br>';
            exit;
        }
        return $rs;
    }
    /*
    * 执行增删改
    *@return bool 成功返回true，失败返回false
    */
    public function exec($sql)
    {
        $key = substr($sql, 0, 6);
        if (in_array($key, array('insert', 'delete', 'update'))) {
            return $this->execute($sql);
        } else {
            echo '非法访问<br>';
            exit;
        }
    }
    // 获取自动增长的编号
    public function getLastInsertId()
    {
        return mysqli_insert_id($this->link);
    }
    // 获取匹配类型
    private function getType($type)
    {
        switch ($type) {
            case 'num':
                return MYSQLI_NUM;
                break;
            case 'both':
                return MYSQLI_BOTH;
                break;
            default:
                return MYSQLI_ASSOC;
                break;
        }
    }
}
// 测试
// 配置参数
$param = array(
    'host' => '127.0.0.1',
    'user' => 'root',
    'pwd' => 'zhang0613',
    'port' => '3306',
    'dbname' => 'data'
);
// 获取单例
$db = MySQLDB::getInstance($param);
// 更新
// $db->exec("update news set title='青草' where id =2 ");
/*插入
if ($db->exec("insert into news values(null,'aa','bb',unix_timestamp())")) {
    echo '编号是:' . $db->getLastInsertId();
}
*/

echo '<pre>';
var_dump($list);

```

​		2、执行数据查询语句

```php
<?php
class MySQLDB
{
    private $host;      //主机地址
    private $port;      //端口号
    private $user;      //用户名
    private $password;  //密码
    private $dbname;    //数据库名称
    private $charset;   //字符集
    private $link;      //连接对象
    private static $instance;
    private function __construct($param)
    {
        $this->initParam($param);
        $this->initConnect();
    }
    private function __clone()
    {
    }
    // 获取单例
    public static function getInstance($param = array())
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self($param);
        }
        return self::$instance;
    }
    // 初始化参数
    private function initParam($param)
    {
        $this->host = $param['host'] ?? '127.0.0.1';
        $this->port = $param['port'] ?? '3306';
        $this->user = $param['user'] ?? 'root';
        $this->password = $param['pwd'] ?? 'root';
        $this->dbname = $param['dbname'] ?? '';
        $this->charset = $param['charset'] ?? 'utf8';
    }
    // 连接数据库
    private function initConnect()
    {
        $this->link = @mysqli_connect($this->host, $this->user, $this->password, $this->dbname, $this->port);
        if (mysqli_connect_errno()) {
            echo '数据库连接失败<br>';
            echo '错误信息：' . mysqli_connect_error(), '<br>';
            echo '错误码:' . mysqli_connect_errno(), '<br>';
            exit;
        }
        mysqli_set_charset($this->link, $this->charset);
    }
    // 执行数据操作语句（增删改）
    private function execute($sql)
    {
        if (!$rs = mysqli_query($this->link, $sql)) {
            echo 'SQL语句执行失败<br>';
            echo '错误信息:' . mysqli_error($this->link), '<br>';
            echo '错误码:' . mysqli_errno($this->link), '<br>';
            echo '错误的SQL语句:' . $sql, '<br>';
            exit;
        }
        return $rs;
    }
    /*
    * 执行增删改
    *@return bool 成功返回true，失败返回false
    */
    public function exec($sql)
    {
        $key = substr($sql, 0, 6);
        if (in_array($key, array('insert', 'delete', 'update'))) {
            return $this->execute($sql);
        } else {
            echo '非法访问<br>';
            exit;
        }
    }
    // 获取自动增长的编号
    public function getLastInsertId()
    {
        return mysqli_insert_id($this->link);
    }
    // 查询语句
    private function query($sql)
    {
        if (substr($sql, 0, 6) == 'select' || substr($sql, 0, 4) == 'show' || substr($sql, 0, 4) == 'desc') {
            return $this->execute($sql);
        } else {
            echo '非法访问<br>';
            exit;
        }
    }
    /*
    *执行查询语句返回二维数组
    *@$sql string 查询语句
    *@$type string assoc|num|both 
     */
    public function fetchAll($sql, $type = 'assoc')
    {
        $rs =  $this->query($sql);
        $type = $this->getType($type);
        return mysqli_fetch_all($rs, $type);
    }
    // 获取匹配类型
    private function getType($type)
    {
        switch ($type) {
            case 'num':
                return MYSQLI_NUM;
                break;
            case 'both':
                return MYSQLI_BOTH;
                break;
            default:
                return MYSQLI_ASSOC;
                break;
        }
    }
    // 匹配一维数组
    public function fetchRow($sql, $type = 'assoc')
    {
        $list = $this->fetchAll($sql, $type);
        if (!empty($list))
            return $list[0];
        return array();
    }
    // 匹配一行一列
    public function fetchColumn($sql)
    {
        $list = $this->fetchRow($sql, 'num');
        if (!empty($list))
            return $list[0];
        return null;
    }
}
// 测试
// 配置参数
$param = array(
    'host' => '127.0.0.1',
    'user' => 'root',
    'pwd' => 'zhang0613',
    'port' => '3306',
    'dbname' => 'data'
);
// 获取单例
$db = MySQLDB::getInstance($param);
// 更新
// $db->exec("update news set title='青草' where id =2 ");
/*插入
if ($db->exec("insert into news values(null,'aa','bb',unix_timestamp())")) {
    echo '编号是:' . $db->getLastInsertId();
}
*/
// 查询
// 二维数组
// $list = $db->fetchAll('select*from news', 'assoc');
// 一维数组
// $list = $db->fetchRow('select * from news where id =1 ', 'aa');
// 一行一列
$list = $db->fetchColumn('select count(*) from news');

echo '<pre>';
var_dump($list);

```

## 39 命名空间

### 	39.1 介绍

​	在一个大的项目中，可能会遇到同名的类、函数、常量，为了区分这些元素，我们可以将这些元素分布存放到不同的命名空间中

​	1、命名空间就是包，用来存放项目中的类、函数、常量

​	2、通过namespace关键字来声明命名空间

### 	39.2 声明命名空间

```php
<?php

namespace china;    //定义命名空间
function getInfo()
{
    echo 'I am a China<br>';
}
getInfo();  //I am a China

namespace USA;      //定义命名空间
function getInfo()
{
    echo 'I am a America<br>';
}

// 调用
getInfo();  //I am a America

\china\getInfo();   //I am a China
\USA\getInfo();     //I am a America

```

​	**\表示公共空间**

### 	39.3 多级命名空间

​	命名空间的名字是可以多级的(子级命名空间)。

```php
<?php

namespace China\Beijing\shunyi;
class Student
{
}

namespace USA\Washington;
class Student
{
}

$stu1 = new Student;    //相对路径
$stu2 = new \China\Beijing\shunyi\Student;  //绝对路径
var_dump($stu1, $stu2);
//USA\Washington\Student)#1 (0) { }
// object(China\Beijing\shunyi\Student)#2 (0) { }
```

​	**如果将相对路径转成绝对路径:**

```
公共空间+命名空间+空间元素
公共空间			命名空间				空间元素
	\		China\Shanghai\PuDong\		Student::$type
```

### 	39.4 访问命名空间

​	1、非限定名称访问

​	2、完全限定名称访问

​	3、限定名称访问

```php
<?php

namespace China\Beijing\Shunyi;

function getInfo()
{
    echo '顺义<br>';
}


namespace China\Beijing;

function getInfo()
{
    echo '北京<br>';
}
//访问空间元素的三种方式
getInfo();                      //非限定名称访问        北京...
\china\Beijing\getInfo();       //完全限定名称访问      北京...
Shunyi\getInfo();               //限定名称访问          顺义...
```

### 	39.5 命名空间引入

​	完全限定名称访问元素路径太长，可以将其他空间引入到当前空间来

​	通过use引入命名空间

```php
<?php

namespace China\BeiJing\shunyi;

function getInfo()
{
    echo '李白<br>';
}

namespace USA;

function getInfo()
{
    echo 'Lincoln<br>';
}
// 引入命名空间
use China\BeiJing\shunyi;
// 测试
getInfo();          //Lincoln
shunyi\getInfo();   //李白
/*
*分析：
*第一步：通过当前空间拼接成绝对路径：\USA\shunyi\getInfo(),这个地址没有应对的空间元素
*第二部：通过引入的空间拼接绝对路径：\China\BeiJing\shunyi+shunyi\getInfo(),shunyi是公共部分，只需要取一个，最后拼接的地址是：*\China\BeiJing\sunyi\getInfo(),这个地址可以找到对应的元素
*/
```

​	引入命名空间的拼接规则

```php
公共空间+引入空间+(去除公共部分，公共部分只能有一级)空间元素

比如：
```

### 	39.6 引入空间元素

​	引入类：use

​	引入函数：use function	[PHP7.0以后版本支持]

​	引入常量：use const		[PHP7.0以后版本支持]

```php
<?php

namespace China\BeiJing\Shunyi;

class Student
{
}
function getInfo()
{
    echo '李白';
}
const TYPE = '学生';

namespace China\ShangHai\Pudong;
//引入类
use China\BeiJing\shunyi\Student;
// 引入方法
use function China\BeiJing\Shunyi\getInfo;
// 引入常量
use const China\BeiJing\Shunyi\TYPE;
// 测试
$stu = new Student;
var_dump($stu);
echo '<hr>';
getInfo();
echo '<hr>';
echo TYPE;
```

### 	39.7 给类、函数取别名

 	如果引入的类和函数与当前的类和函数名称相同，需要给引入的类和函数取别名

​	通过as取别名

```php
<?php

namespace China\beiJing\Shunyi;

class Student
{
}
function getInfo()
{
    echo '李白';
}
const TYPE = '工人';

namespace China\ShangHao\Pudong;

class Student
{
}
function getInfo()
{
    echo '张三';
}
const TYPE = '学生';
// 引入类
use China\BeiJing\Shunyi\Student as BeiJingStudent;
// 引入函数
use function China\BeiJing\Shunyi\getInfo as BeiJingGetInfo;
// 引入常量
use const China\BeiJing\Shunyi\TYPE as BeiJingTYPE;

// 测试
$stu = new Student;         //object(China\ShangHao\Pudong\Student)#1 (0) { }
var_dump($stu);
echo '<hr>';
$stu = new BeiJingStudent;  //object(China\beiJing\Shunyi\Student)#2 (0) { }
var_dump($stu);
echo '<hr>';
getInfo();                  //张三
echo '<hr>';
BeiJingGetInfo();           //李白
echo '<hr>';
echo  BeiJingTYPE;          //工人
echo '<hr>';
echo TYPE;                  //学生
```

### 	39.8 公共命名空间

​	如果一个页面没有namespace声明空间，这个页面的元素在公共空间下

​	公共空间用`\`表示

```php
<?php
function getInfo()
{
    echo '李白';
}

\getInfo();
```

### 	39.9 命名空间注意事项

​	1、命名空间只能存放类，函数，const常量

​	2、第一个namespace前面不能有任何的代码，空白字符，header()也不行

​	3、包含文件不影响当前的命名空间

## 40 trait(原型)

​	trait为了减少单继承语言的限制，可以在不同的层次结构内独立的类中复用类的方法集

```php
<?php
// 原型
trait A
{
    public function getInfo()
    {
        echo 'trait原型';
    }
}
// 使用原型
class Student2
{
    use A;  //代码复用
}
// 测试
$stu = new Student2;
$stu->getInfo();
```

​	引入多个trait

```php
<?php
// 原型
trait A
{
    public function getInfo1()
    {
        echo 'trait原型A';
    }
}
trait B
{
    public function getInfo2()
    {
        echo 'trait原型B';
    }
}
// 使用原型
class Student2
{
    use A, B;  //代码复用  引入A、B trait
}
// 测试
$stu = new Student2;
$stu->getInfo1();       //trait原型A
$stu->getInfo2();       //trait原型B
```

​	trait和继承结合

```php
<?php
trait A
{
    public function getInfo()
    {
        echo '这是trait<br>';
    }
}
class Person
{
    public function getInfo()
    {
        echo '这是Person类<br>';
    }
}
// 继承同时代码复用
class Student2 extends Person
{
    use A;      //继承链getInfo，又被A中的getInfo覆盖
}
// 测试
$stu = new Student2;
$stu->getInfo();        //这是trait

```

​	解决同名冲突

```php
<?php
// 原型
trait A
{
    public function getInfo()
    {
        echo 'trait原型A';
    }
}
trait B
{
    public function getInfo()
    {
        echo 'trait原型B';
    }
}
// 使用原型
class Student2
{
    use A, B {       //引入A和B的trait，同时解决同名冲突
        // 方法一：方法替换
        // A::getInfo insteadof B;        //将A中的getInfo替换掉B中的getInfo
        // B::getInfo insteadof A;        //将B中的getInfo替换掉A中的getInfo
        // 方法二：改名
        A::getInfo insteadof B;
        B::getInfo as getInfo2;           //将B中的getInfo改名为getInfo2
    }
}
// 测试
$stu = new Student2;
$stu->getInfo();        //trait原型A
echo '<hr>';
$stu->getInfo2();       //trait原型B
/*
*同名冲突的解决方法有两个：
*第一：方法替换
*第二：改名
*/
```

​	trait更改权限

```php
<?php
trait A
{
    private function show()
    {
        echo '测试';
    }
}
class Student3
{
    use A {
        // show as public;         //将show方法的权限设置为public
        show as public show2;      //将show方法的权限设置为public，并改名为show2
    }
}

//测试
$stu = new Student3;
// $stu->show();
$stu->show2();
```

## 41 迭代器

### 41.1 遍历数组

​	手动遍历数组

​	步骤：

​	1、复位指针

​	2、检查指针合法性

​	3、获取当前值

​	4、获取当前键

​	5、指针下移

​	实现：

```php
<?php
$stu = ['tom', 'berry', 'ketty', 'rose'];

reset($stu);        //复位指针
while (key($stu) !== null) {    //键合法
    echo key($stu) . '-' . current($stu), '<br>';   //获取键值，键合法
    next($stu);     //指针下移
}
/*
*0-tom
*1-berry
*2-ketty
*3-rose
*/
```

### 41.2 迭代器

​	迭代器是PHP内置的接口

![image-20220613163630523](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220613163630523.png)

​	场景：遍历对象，获取的是对象中属性保存的数组

```php
<?php
class MyClass implements Iterator
{
    // $list属性用来保存学生数组
    private $list = array();
    // 添加学生
    public function addstu($name)
    {
        $this->list[] = $name;
    }
    // 实现接口中的复位方法
    public function rewind(): void
    {
        reset($this->list);
    }
    // 验证当前指针是否合法
    public function valid(): bool
    {
        return key($this->list) !== null;
    }
    public function current()
    {
        return current($this->list);
    }
    // 获取键
    public function key()
    {
        return key($this->list);
    }

    // 获取值

    // 指针下移
    public function next(): void
    {
        next($this->list);
    }
}
// 创建班级
$class = new MyClass;
// 添加学生
$class->addstu('tom');
$class->addstu('berry');
$class->addstu('ketty');
// 遍历班级
foreach ($class as $key => $value) {
    echo "{$key}-{$value}<br>";
}
/*
*0-tom
*1-berry
*2-ketty
*/
```

## 42 分页

### 42.1 分析

```
-- 1、获取当前页码的数据
页码			数据
1				select * from products linmit 0,10
2				select * from products linmit 10,10
3				select * from products linmit 20,10
结论:
$pageno:页码
$startno:起始位置
$pagesize=10;页面大小
公式“$startno=($pageno-1)*$pagesize;
-- 2、如何获取页码
用户点击页面低端页码，传递当前的页面
--3、如何获取总页码
记录数		页数		计算
60			6		60/10=6
51			6		ceil(51/6)=6

结论：
$rowcount:记录总行数
$pagecount:总页数
公式$pagecount = ceil($rowcount/$pagesize)

-- 4、如何获取总记录数
select count(*) from products;
```

### 42.2 步骤

​	第一步：获取总记录数

​	第二步：求出总页数

​	第三步：循环显示页码

​	第四步：通过当前页面求出起始位置

​	第五步：获取当前页面数据，并遍历显示

42.3 代码实现

```php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <?php
    // 连接数据库
    class MySQLDB
    {
        private $host;      //主机地址
        private $user;      //用户
        private $password;  //密码
        private $dbname;    //数据库名称
        private $port;      //端口号
        private $charset;   //字符集
        private $link;      //连接对象
        private static $instance;
        // 私有的构造函数，阻止外部创建对象
        private function __construct($param)
        {
            $this->initParam($param);
            $this->initConnent();
        }
        // 私有的克隆，阻止外部克隆对象
        private function __clone()
        {
        }
        // 连接数据库
        private function initConnent()
        {
            $this->link = mysqli_connect($this->host, $this->user, $this->password, $this->dbname, $this->port);
            if (mysqli_connect_errno()) {
                echo '数据库连接失败';
                echo '错误信息:' . mysqli_connect_error(), '<br>';
                echo '错误码：' . mysqli_connect_errno();
                exit;
            }
            mysqli_set_charset($this->link, $this->charset);
        }
        // 初始化参数
        private function initParam($param)
        {
            $this->host = $param['host'] ?? '127.0.0.1';
            $this->user = $param['user'] ?? '';
            $this->password = $param['password'] ?? '';
            $this->dbname = $param['dbname'] ?? '';
            $this->port = $param['port'] ?? '3306';
            $this->charset = $param['charset'] ?? 'utf8';
        }
        // 获取单例
        public static function getInstance($param = array())
        {
            if (!self::$instance instanceof self) {
                self::$instance = new self($param);
            }
            return self::$instance;
        }
        // 增 删 改
        private function execute($sql)
        {
            if (!$rs = mysqli_query($this->link, $sql)) {
                echo 'SQL语句执行失败<br>';
                echo '错误信息:' . mysqli_error($this->link), '<br>';
                echo '错误语句:' . $sql, '<br>';
                echo '错误码:' . mysqli_errno($this->link), '<br>';
                exit;
            }
            return $rs;
        }
        // 增 删 改 使用
        public function exec($sql)
        {
            $key = substr($sql, 0, 6);
            if (in_array($key, array('insert', 'update', 'detele'))) {
                return $res = $this->execute($sql);
            } else {
                echo '数据不合法<br>';
                exit;
            }
        }
        // 查询
        private function query($sql)
        {
            if (substr($sql, 0, 6) == 'select' || substr($sql, 0, 4) == 'show' || substr($sql, 0, 4) == 'desc') {
                return $this->execute($sql);
            } else {
                echo '非法访问<br>';
                exit;
            }
        }
        // 获取二维数组
        public function fetchAll($sql, $type = 'assoc')
        {
            $rs = $this->query($sql);
            $type = $this->getType($type);
            return mysqli_fetch_all($rs, $type);
        }
        // 获取一维数组
        public function fetchRow($sql, $type = 'assoc')
        {
            $list = $this->fetchAll($sql, $type);
            if (!empty($list))
                return $list[0];
            return array();
        }
        // 获取一行一列
        public function fetchColumn($sql)
        {
            $list = $this->fetchRow($sql, 'num');
            if (!empty($list))
                return $list[0];
            return null;
        }
        // 
        private function getType($type)
        {
            switch ($type) {
                case 'num':
                    return MYSQLI_NUM;
                    break;
                case 'both':
                    return MYSQLI_BOTH;
                    break;
                default:
                    return MYSQLI_ASSOC;
                    break;
            }
        }
    }

    $param = array(
        'host' => '127.0.0.1',
        'user' => 'root',
        'password' => 'zhang0613',
        'dbname' => 'data',
        'port' => '3306',
        'charset' => 'utf8'
    );
    $db = MySQLDB::getInstance($param);



    $pagesize = 10;  //页面大小
    //​	第一步：获取总记录数
    $rowscount = $db->fetchColumn('select count(*) from news');
    //第二步：求出总页数
    $pagecount = ceil($rowscount / $pagesize);
    //第四步：通过当前页面求出起始位置
    $pageno = $_GET['pageno'] ?? 1;
    $pageno = $pageno < 1 ? 1 : $pageno;
    $pageno = $pageno > $pagecount ? $pagecount : $pageno;
    $startno = ($pageno - 1) * $pagesize;
    //第五步：获取当前页面数据，并遍历显示
    $sql = "select * from news where id>=(select id from news limit $startno,1) limit $pagesize";
    $rs = $db->fetchAll($sql);
    ?>
    <table>
        <tr>
            <th>序号</th>
            <th>标题</th>
            <th>内容</th>
            <th>时间</th>
        </tr>
        <?php foreach ($rs as $rows) : ?>
            <tr>
                <td><?= $rows['id'] ?></td>
                <td><?= $rows['title'] ?></td>
                <td><?= $rows['content'] ?></td>
                <td><?= $rows['createtime'] ?></td>
            </tr>
        <?php endforeach; ?>
    </table>
    [<a href="?pageno=1">首页</a>]
    [<a href="?pageno=<?= $pageno - 1 ?>">上一页</a>]
    <!--  第三步：循环显示页码 -->
    <?php for ($i = 1; $i <= $pagecount; $i++) : ?>
        <a href="?pageno=<?= $i ?>"><?= $i ?></a>
    <?php endfor; ?>
    [<a href="?pageno=<?= $pageno + 1 ?>">下一页</a>]
    [<a href="?pageno=<?= $pagecount ?>">末页</a>]
</body>

</html>
```

### 42.4 分页优化

​	在上面的分页代码中，虽然SQL语句比较经典，但是每次都要获取不需要的数据，浪费资源

```php
select * from news where id>=(select id from news limit $startno,1) limit $pagesize
```

## 43 PDO介绍

### 43.1 连接数据库方式



### 43.2 PDO介绍



### 43.3 开启PDO拓展

​	开启PDO连接MySQL扩展

```php
extension=php_pdo_mysql.dll
```

## 44 PDO核心类

​	1、PDO类：表示PHP和数据库之间的一个连接

​	2、PDOStatement类

​		第一：表示执行数据查询语句(select ,show)后的相关结果集

​		第二：预处理对象

​	3、PDOException类：表示PDO的异常

![image-20220615080434046](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615080434046.png)



## 45 实例化PDO对象

​	语法

```php
__construct($dsn,用户名,密码)
```

### 45.1 DSN

​	DSN:data source name,数据源名称，包含的是连接数据库的信息，格式如下：

```php
$dsn=数据库类型：host=主机地址;port=端口号;dbname=数据库名称;charset=字符集
```

​	数据库类型：

```
MySQL数据库	=>	mysql;
oracle数据库   =>  oci;
SQL Server    =>  sqlsrv;
```



### 45.2 实例化PDO

​	实例化PDO的过程就是连接数据库的过程

```php
<?php
$dsn = 'mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8';
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);     //object(PDO)#1 (0) { }
```

### 45.3 注意事项	

​	1、如果连接的是本地数据库，host可以省略

```php
<?php
$dsn = 'mysql:port=3306;dbname=data;charset=utf8';
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);     //object(PDO)#1 (0) { }
```

​	2、如果使用的端口是3306端口，port也可以省略

```php
<?php
$dsn = 'mysql:dbname=data;charset=utf8';
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);     //object(PDO)#1 (0) { }
```

​	3、charset也可以省略，如果省略，使用的是默认字符编码

```php
<?php
$dsn = 'mysql:dbname=data';
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);     //object(PDO)#1 (0) { }

```

​	4、dbname也可以省略，如果省略就没有选择数据库

```php
<?php
$dsn = 'mysql:';
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);     //object(PDO)#1 (0) { }
```

​	5、host、port、dbnmae、charset不区分大小写，没有先后顺序

​	6、驱动名称不能省略，冒号不能省略(因为冒号是驱动名组成的部分)，数据库驱动只能小写

## 46 使用PDO

### 46.1 执行数据库操作语句

​	方法：$pdo->exec($sql),执行数据增、删、改语句，执行成功返回受影响的记录行数，如果SQL语句错误返回false

```php
<?php
// 实例化
$dsn = 'mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8';
$pdo = new PDO($dsn, 'root', 'zhang0613');
// 执行数据操作语句
// 执行增加
/*
if ($pdo->exec("insert into news values(null,'dd','dddddddd',unix_timestamp())")) {
    echo '编号:' . $pdo->lastInsertId();
}
*/
// 执行修改
// echo $pdo->exec("update news set title ='啥都能' where id in(9,18)");
// 执行删除
echo $pdo->exec("delete from news where id=20");
```



### 46.2 执行数据库查询语句

​	方法：$pdo->query($sql),返回的是PDOStatement对象

```php
<?php
$dsn = "mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8";
$pdo = new PDO($dsn, 'root', 'zhang0613');

// 执行数据查询语句
$stmt = $pdo->query("select * from news");
// var_dump($rs);      //object(PDOStatement)#2
// 获取数据
// 获取二维数组
// $rs = $stmt->fetchAll();    //默认返回关联和索引数组
// $rs = $stmt->fetchAll(PDO::FETCH_BOTH);    //返回关联和索引数组
// $rs = $stmt->fetchAll(PDO::FETCH_NUM);    //返回索引数组
// $rs = $stmt->fetchAll(PDO::FETCH_ASSOC);    //返回关联数组
// $rs = $stmt->fetchAll(PDO::FETCH_OBJ);    //返回对象数组

// 获取一维数组,匹配完成后指针下移一条
// $rs = $stmt->fetch();   //关联和索引数组
// $rs = $stmt->fetch(PDO::FETCH_NUM);   //索引数组
// $rs = $stmt->fetch(PDO::FETCH_ASSOC);   //关联数组
// 通过while循环获取所有数据
// while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
//     $rs[] = $row;
// }

// 匹配列：匹配当前的行的低n列，列的编号从0开始，匹配完毕后指针下移一条
// echo $stmt->fetchColumn();  //获取当前行的第0列
// $stmt->fetchColumn();  //获取当前行的第0列
// $stmt->fetchColumn();  //获取当前行的第0列
// echo $stmt->fetchColumn(1);  //获取当前行的第1列


// 总行数，总列数
// echo '总行数' . $stmt->rowCount();
// echo '<br>';
// echo '总列数' . $stmt->columnCount();


// 便利PDOStatement对象,(PDOStatement对象是有迭代器)
foreach ($stmt as $row) {
    echo $row['title'], '<br>';
}

```

​	**stdClass类是所有PHP类的父类**

### 46.3 PDO操作事务

​	事务：是一个整体，要么一起执行，要么一起回滚

​	事务的特性：原子性，一致性，隔离性，永久性

​	需要将多个SQL语句作为一个整体执行，就需要使用到事务

​	语法

```php
start transaction 或 begin  开启事务
commit	提交事务
rollback	回滚事务
```

​	例题

​	创建测试数据

```mysql
create table bank(
	cardid char(4) primary key comment'卡号',
    balance decimal(10,2) not null comment'余额'
 )engine = innodb charset=utf8 comment='银行卡号表';

insert into bank values('1001',1000),('1002',741),('1003',247);
```

​	PDO操作事务

```php+HTML
<body>
    <?php
    if (!empty($_POST)) {
        $dsn = "mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8";
        $pdo = new PDO($dsn, 'root', 'zhang0613');
        $out = $_POST['card_out'];      //转出卡号
        $in = $_POST['card_in'];        //转入卡号
        $money = $_POST['money'];       //余额
        $pdo->beginTransaction();       //开启事务
        // 转账
        $flag1 = $pdo->exec("update bank set balance = balance - $money where cardid='$out'");
        $flag2 = $pdo->exec("update bank set balance= balance + $money where cardid='$in'");
        $stmt = $pdo->query("select balance from bank where cardid = '$out'");
        // 查看转出的账号是否小于0
        $flag3 = $stmt->fetchColumn() >= 0 ? 1 : 0;
        if ($flag1 && $flag2 && $flag3) {
            $pdo->commit();             //提交事务
            echo '转账成功';
        } else {
            $pdo->rollBack();           //回滚事务           
            echo '转账失败';
        }
    }

    ?>
    <form action="" method="POST">
        转出卡号： <input type="text" name="card_out" id=""> <br>
        转入卡号： <input type="text" name="card_in" id=""> <br>
        金额： <input type="text" name="money" id=""> <br>
        <input type="submit" value="提交">
    </form>
</body>
```



### 46.4 PDO操作预处理

​	**MySQL中预处理**

​	预处理好处：编译一次多次执行，用来解决一条SQL语句多次执行的问题，提高了执行效率

​	预处理语句：

```mysql
prepare 预处理名称 from 'sql语句'
```

​	执行预处理

```mysql
execute 预处理名字 [using 变量]
```

**PDO中的预处理--位置占位符**

```php
<?php
$dsn = "mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8";
$pdo = new PDO($dsn, 'root', 'zhang0613');
var_dump($pdo);
// 创建预处理对象
$stmt = $pdo->prepare("insert into bank values (?,?)");  //?是占位符

$cards = [
    ['1004', 500],
    ['1005', 400]
];

foreach ($cards as $card) {
    /*方法一
    绑定参数，并执行预处理 
    $stmt->bindParam(1, $card[0]); //占位符的位置 从一开始
    $stmt->bindParam(2, $card[1]);
    $stmt->execute();               //执行预处理
    */

    // 方法二
    /* 
    $stmt->bindValue(1, $card[0]);
    $stmt->bindValue(2, $card[1]);
    $stmt->execute();
    */

    // 方法三：如果占位符的顺序和数组的顺序相同
    $stmt->execute($card);
}
```

**PDO中的预处理--参数占位符**

```php
<?php
$dsn = "mysql:host=127.0.0.1;port=3306;dbname=data;charset=utf8";
$pdo = new PDO($dsn, 'root', 'zhang0613');
// 参数占位符前面必须加上：
$stmt = $pdo->prepare("insert into bank values(:p1,:p2)");  //:p1,:p2是参数占位符

$cords = [
    ['p1' => '1010', 'p2' => '8415'],
    ['p1' => '1011', 'p2' => '4145']
];

foreach ($cords as $cord) {
    // 方法一
    // $stmt->bindParam(':p1', $cord['p1']);
    // $stmt->bindParam(':p2', $cord['p2']);
    // $stmt->execute();
    // 方法二
    // $stmt->bindValue(':p1', $cord['p1']);
    // $stmt->bindValue(':p2', $cord['p2']);
    // $stmt->execute();
    // 方法三：如果数组的下标和参数名一直的时候就可以直接传递关联数组
    $stmt->execute($cord);
}
```

​	**小结：**

​	1、？是位置占位符

​	2、参数占位符以冒号开头

​	3、$stmt->bindParam()和$stmt->bindValue()区别

![image-20220615124449595](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615124449595.png)

​	4、预处理的好处

```
a 提高执行效率
b 提高安全性
```



## 47 PDO异常处理

```php
<?php
try {
    $dsn = 'mysql:dbname=data;charser=utf8';
    $pdo = new PDO($dsn, 'root', 'zhang0613');
    // 这是PDO错误模式属性，PDO自动抛出异常
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    $pdo->query("select * from newss ");
} catch (PDOException $ex) {
    echo '错误信息：' . $ex->getMessage(), '<br>';
    echo '错误文件:' . $ex->getFile(), '<br>';
    echo '错误行号:' . $ex->getLine();
}
```

​	**小结**

​	1、PDOException是PDO的异常类

​	2、实例化PDO会自动抛出异常

​	3、其他操作不会抛出异常，需要设置PDO的异常模式

​	4、PDO异常模式

```php
PDO::ERRMODE_NOEN
PDO::ERRMODE_EXCEPTION		抛出异常
PDO::ERRMODE_SILENT			中断
PDO::ERRMODE_WARNING		警告
```



## 48 单例模式封装MyPDO类

### 48.1 步骤

​	1、单例模式

​	2、初始化参数

​	3、连接数据库

​	4、执行增 删 改

​	5、执行查询

​		a 返回二维数组

​		b 返回一维数组

​		c 返回一行一列

### 48.2 代码实现

​	第一部分：实现单例、初始化参数、连接数据库

​	第二部分：实现 执行查询

```php
<?php
class MyPDO
{
    private $type;      //数据库类别
    private $host;      //主键地址
    private $port;      //端口号
    private $dbname;    //数据库名
    private $charset;   //字符集
    private $user;      //用户名
    private $password;  //密码
    private $pdo;       //保存PDO的对象

    private static $instance;
    private function __construct($param)
    {
        $this->initParam($param);
        $this->initPDO();
        $this->initException();
    }
    private function __clone()
    {
    }
    public static function getInstance($param = array())
    {
        if (!self::$instance instanceof self) {
            self::$instance = new self($param);
        }
        return self::$instance;
    }

    // 初始化参数
    private function initParam($param)
    {
        $this->type = $param['type'] ?? 'mysql';
        $this->host = $param['host'] ?? '127.0.0.1';
        $this->port = $param['port'] ?? '3306';
        $this->dbname = $param['dbname'] ?? '';
        $this->charset = $param['charset'] ?? 'utf8';
        $this->user = $param['user'] ?? 'root';
        $this->password = $param['password'] ?? 'root';
    }
    // 初始化PDO
    private function initPDO()
    {
        try {
            $dsn = "{$this->type}:host={$this->host};port={$this->port};dbname={$this->dbname};charset={$this->charset}";
            $this->pdo = new PDO($dsn, $this->user, $this->password);
        } catch (PDOException $ex) {
            $this->showException($ex, '');
            exit;
        }
    }

    // 显示异常
    private function showException($ex, $sql)
    {
        if (!empty($sql)) {
            echo 'SQL语句执行失败<br>';
            echo '错误的SQL语句：' . $sql, '<br>';
        }
        echo '错误编号：' . $ex->getCode(), '<br>';
        echo '错误信息：' . $ex->getMessage(), '<br>';
        echo '错误行号：' . $ex->getLine(), '<br>';
        echo '错误文件：' . $ex->getFile();
    }

    // 设置异常模式
    private function initException()
    {
        $this->pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    }

    // 执行曾 删 改
    public function exec($sql)
    {
        try {
            return $this->pdo->exec($sql);
        } catch (PDOException $ex) {
            $this->showException($ex, $sql);
            exit;
        }
    }
    // 获取自动增长的编号
    public function lastInsertId()
    {
        return $this->pdo->lastInsertId();
    }
    // 判断匹配的类型
    private function fetchType($type)
    {
        switch ($type) {
            case 'num':
                return PDO::FETCH_NUM;
            case 'both':
                return PDO::FETCH_BOTH;
            case 'obj':
                return PDO::FETCH_OBJ;
            default:
                return PDO::FETCH_ASSOC;
        }
    }
    //获取所有数据,返回二维数组
    public function fetchAll($sql, $type)
    {
        try {
            $stmt = $this->pdo->query($sql);        //获取PDOStatement对象
            $type  = $this->fetchType($type);       //获取匹配方式
            return $stmt->fetchAll($type);
        } catch (PDOException $ex) {
            $this->showException($ex, $sql);
            exit;
        }
    }
    // 获取一维数组
    public function fetchRow($sql, $type = 'assoc')
    {
        try {
            $stmt = $this->pdo->query($sql);
            $type = $this->fetchType($type);
            return  $stmt->fetch($type);
        } catch (PDOException $ex) {
            $this->showException($ex, $sql);
            exit;
        }
    }
    // 返回一行一列
    public function fetchColumn($sql)
    {
        try {
            $stmt = $this->pdo->query($sql);
            return $stmt->fetchColumn();
        } catch (PDOException $ex) {
            $this->showException($ex, $sql);
            exit;
        }
    }
}

// 测试
$param = array(
    'host' => '127.0.0.1',
    'port' => '3306',
    'dbname' => 'data',
    'charset' => 'utf8',
    'user' => 'root',
    'password' => 'zhang0613'
);
$mypdo = MyPDO::getInstance($param);
// var_dump($mypdo);
/*
if ($mypdo->exec("insert into news values (null,'111','1234568213DFS71245',unix_timestamp())")) {
    echo '自动增长的编号是' . $mypdo->lastInsertId();
}
*/
$list = $mypdo->fetchColumn("select * from news");
echo '<pre>';
var_dump($list);
```

## 49 MVC介绍

​	1、MVC是一个思想编程，是一种设计模式

​	2、思想：将一个功能分解成3个部分，M V C

​	Model(模型)：出来与数据有关的逻辑

​	View(试图)：显示页面

​	Controller(控制器)：处理业务逻辑

## 50 MVC演化

### 50.1显示商品

```php+HTML
<?php
spl_autoload_register(function ($class_name) {
    require "./90-{$class_name}.class.php";
});

$param = array(
    'type'  =>  'mysql',
    'host'  =>  '127.0.0.1',
    'port'  =>  '3306',
    'dbname'   =>  'data',
    'charset'  =>  'utf8',
    'user'  =>  'root',
    'pwd'   =>  'zhang0613'
);
$mypdo = MyPDO::getInstance($param);
$list = $mypdo->fetchAll("select * from products", 'assoc');
?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <table border="1px" width=1200px align="center" bordercolor='#000'>
        <tr>
            <th>商品序号</th>
            <th>商品名称</th>
            <th>商品规格</th>
            <th>商品单位</th>
            <th>产地</th>
            <th>零售价</th>
            <th>备注</th>
            <th>正常零售价</th>
            <th>同类超市特价</th>
            <th>删除</th>
        </tr>
        <?php foreach ($list as $rows) : ?>
            <tr>
                <td><?= $rows['proID'] ?></td>
                <td><?= $rows['proname'] ?></td>
                <td><?= $rows['proguige'] ?></td>
                <td><?= $rows['procompany'] ?></td>
                <td><?= $rows['proplaceoforigin'] ?></td>
                <td><?= $rows['proprice'] ?></td>
                <td><?= $rows['procomment'] ?></td>
                <td><?= $rows['pronormalprice'] ?></td>
                <td><?= $rows['prospecialoffer'] ?></td>
                <td><a href="">删除</a></td>
            </tr>
        <?php endforeach ?>
    </table>
</body>

</html>
```

### 50.2演化一：分离视图

​	1、创建html页面(视图页面)，将显示部分的代码拷贝到视图页面上

```php+html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <table border="1px" width=1200px align="center" bordercolor='#000'>
        <tr>
            <th>商品序号</th>
            <th>商品名称</th>
            <th>商品规格</th>
            <th>商品单位</th>
            <th>产地</th>
            <th>零售价</th>
            <th>备注</th>
            <th>正常零售价</th>
            <th>同类超市特价</th>
            <th>删除</th>
        </tr>
        <?php foreach ($list as $rows) : ?>
        <tr>
            <td> <?= $rows['proID'] ?> </td>
            <td> <?= $rows['proname'] ?> </td>
            <td> <?= $rows['proguige'] ?> </td>
            <td> <?= $rows['procompany'] ?> </td>
            <td> <?= $rows['proplaceoforigin'] ?> </td>
            <td> <?= $rows['proprice'] ?> </td>
            <td> <?= $rows['procomment'] ?> </td>
            <td> <?= $rows['pronormalprice'] ?> </td>
            <td> <?= $rows['prospecialoffer'] ?> </td>
            <td><a href="">删除</a></td>
        </tr>
        <?php endforeach ?>
    </table>
</body>

</html>
```

​	2、在php页面上加载视图

```php
<?php
spl_autoload_register(function ($class_name) {
    require "./90-{$class_name}.class.php";
});

$param = array(
    'type'  =>  'mysql',
    'host'  =>  '127.0.0.1',
    'port'  =>  '3306',
    'dbname'   =>  'data',
    'charset'  =>  'utf8',
    'user'  =>  'root',
    'pwd'   =>  'zhang0613'
);
$mypdo = MyPDO::getInstance($param);
$list = $mypdo->fetchAll("select * from products", 'assoc');
//加载视图
require './92-演化一：分离视图.html';
```



### 50.3演化二：分离模型

​	模型的规则：

​	1、一个表对应一个模型，表名和模型名一致(必须)

​	2、模型一Model结尾(可选)

​	代码实现

​	1、创建XXXModel.class.php页面

```php
<?php
class ProductsModel
{
    public function getList()
    {
        $param = array(
            'type'  =>  'mysql',
            'host'  =>  '127.0.0.1',
            'port'  =>  '3306',
            'dbname'   =>  'data',
            'charset'  =>  'utf8',
            'user'  =>  'root',
            'pwd'   =>  'zhang0613'
        );
        $mypdo = MyPDO::getInstance($param);
        return  $mypdo->fetchAll("select * from products", 'assoc');
    }
}

```

​	2、在主php页面调用模型的getList()

```php
<?php
spl_autoload_register(function ($class_name) {
    require "./90-{$class_name}.class.php";
});
// 实例化模型
$model = new ProductsModel();
$list = $model->getList();
// 加载视图
require './90-演化一：分离视图.html';

```



### 50.4演化三：分离基础模型

​	连接数据库的代码每个模型都要使用，所有我们需要将连接数据库的代码封装到基础模型类中

![image-20220615164831861](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615164831861.png)

​	第一步：创建Model.class.php页面（基础模型）

```php
<?php
class Model
{
    protected $mypdo;
    public function __construct()
    {
        $this->initMyPDO();
    }
    private function initMyPDO()
    {
        $param = array(
            'type'  =>  'mysql',
            'host'  =>  '127.0.0.1',
            'port'  =>  '3306',
            'dbname'   =>  'data',
            'charset'  =>  'utf8',
            'user'  =>  'root',
            'pwd'   =>  'zhang0613'
        );
        $this->mypdo = MyPDO::getInstance($param);
    }
}
```

第二步：ProductsModel类继承基础模型

```php
<?php
// ProductsModel模型用来操作Products表
class ProductsModel extends Model
{
    // 获取Products表的数据
    public function getList()
    {
        // 获取商品数据
        return  $this->mypdo->fetchAll("select * from products", 'assoc');
    }
}
```

### 50.5演化四：分离控制器

​	控制器放在index.php页面中是不合理的，因为项目中的控制器会很多，而index.php只有一个。所以需要将控制器分离开来

​	控制器的规则：

​	1、一个模块对应一个控制器（必须）

​	2、控制器以Controller结尾（可选）

​	3、控制器中的方法以Action结尾（可选），目的是防止方法名是PHP的关键字

​	创建ProductsController.class.php

```php
<?php
 //商品模块
class ProductsController
{
    // 获取商品列表
    public function listAction()
    {
        // 实例化模型
        $model = new ProductsModel();
        $list = $model->getList();
        // 加载视图
        require './90-演化一：分离视图.html';
    }
 
}
```

​	主php页面

```php
<?php
spl_autoload_register(function ($class_name) {
    require "./90-{$class_name}.class.php";
});
// 确定路由
$c = $_GET['c'] ?? 'Products';
$a = $_GET['a'] ?? 'list';
$c = ucfirst(strtolower($c));       //首字母大小
$a = ucfirst(strtolower($a));       //首字母大小
$controller_name = $c . 'Controller'; //拼接控制器类名
$action_name = $a . 'Action';       //拼接方法名
// 请求分发
$obj = new $controller_name();
$obj->$action_name();

```

![image-20220615170913947](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615170913947.png)

![image-20220615170857804](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615170857804.png)

![image-20220615174415597](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615174415597.png)

## 51 删除商品

​	入口(html)

```php+HTML
<td><a href="90-MVC演化-显示商品.php?c=products&a=del&peroid=<?= $rows['proID'] ?>"onclick="return confirm('是否删除此元素')">删除</a></td>
```

​	控制器(ProductsController)

```php
<?php
class ProductsController
{
    ...
	//删除商品
    public function delAction()
    {
        $id = (int)$_GET['peroid'];  //如果参数明确是整数，要强制转成整形
        $model = new ProductsModel();
        if ($model->del($id)) {
            header('location:90-MVC演化-显示商品.php?c=Products&a=list');
        } else {
            echo '删除失败';
            exit;
        }
    }
}
```

​	模型(ProductsModel)

```php
<?php
// ProductsModel模型用来操作Products表
class ProductsModel extends Model
{
   ...
    // 删除数据
    public function del($proid)
    {
        return $this->mypdo->exec("delete from products where proid=$proid");
    }
}
```

## 52 框架目录

### 52.1 创建目录结构

![image-20220615192743731](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220615192743731.png)

### 52.2 文件分类存放	

​	将文件存放到不同的目录以后，由于类文件地址发生了改变，所以无法完成自动加载类

​	由于每次都请求入口文件，所以入口文件表示所在的目录

## 53 添加命名空间

​	通过文件地址目录做命名空间，这样获取了命名空间就能知道文件存放的地址

​	Model.class.php

```php
namespace Core;
class Model{
    ...
}
```

​	MyPDO.class.php

```php
namespace Core;
class MyPDO{
    ...
}
```

​	ProductsModel.class.php

```php
namespace Model;
class ProductsModel{
    ...
}
```

​	ProductsController.class.php

```php
namespace Controller\Admin;
class ProductsController{
    ...
}
```

## 54 框架类实现

### 54.1 定义路径常量

​	由于文件路径使用频率很高，而且路径比较长，所以将固定不变的路径定义成路径常量

​	知识点

```
1、getwcd():入口文件的绝对路径
2、windows下默认的目录分隔符是'\',Linux下默认的目录分隔符是'/'。DIRECTORY_SEPARATOR常量根据不同的操作系统返回不同的目录分隔符。
```

​	代码实现

​	在Core文件夹下创建Framework.class.php

```php
<?php
class Framework
{
    // 定义路径常量
    public static function initConst()
    {
        define('DS', DIRECTORY_SEPARATOR);          //定义目录分隔符
        define('ROOT_PATH', getcwd() . DS);        //入口文件所在目录
        define('APP_PATH', ROOT_PATH . 'Application' . DS);   //application 目录
        define('CONFIG_PATH', APP_PATH . 'Config' . DS);
        define('CONTROLLER_PATH', APP_PATH . 'Controller' . DS);
        define('MODEL_PATH', APP_PATH . 'Model' . DS);
        define('VIEW_PATH', APP_PATH . 'View' . DS);
        define('FRAMEWORK_PATH', ROOT_PATH . 'Framework' . DS);
        define('CORE_PATH', FRAMEWORK_PATH . 'Core' . DS);
        define('LIB_PATH', FRAMEWORK_PATH . 'Lib' . DS);
        define('TRAITS_PATH', ROOT_PATH . 'Traits' . DS);
    }
}
```

### 54.2 引入配置文件

​	1、在config目录下创建congif.php

```php
<?php
return array(
    // 数据库配置
    'database' => [],
    //应用程序配置
    'app'      => [
        'dp'    =>  'Admin',
        'dc'    =>  'Products',
        'da'    =>  'list'
    ],
);
```

​	2、在类框架中引入配置文件

```php
private static function initConfig()
{
	$GLOBALS['config'] = require CONFIG_PATH . 'config.php';
}
```

### 54.3 确定路由

​	p:[platform] 平台

​	c:[coontroller] 控制器

​	a:[action] 方法

![image-20220616162248635](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220616162248635.png)

```php
private static function initRoutes()
    {
        $p = $_GET['p'] ?? $GLOBALS['config']['app']['dp'];
        $c = $_GET['c'] ?? $GLOBALS['config']['app']['dc'];
        $a = $_GET['a'] ?? $GLOBALS['config']['app']['da'];
        $p = ucfirst(strtolower($p));
        $c = ucfirst(strtolower($c));
        $a = strtolower($a);
        define('PLATFROM_NAME', $p);    //平台
        define('CONTROLLER_NAME', $c);  //控制器
        define('ACTION_NAME', $a);      //方法
        define('__URL__', CONTROLLER_PATH . $p . DS);
        define('__VIEW__', VIEW_PATH . $p . DS);
    }
```

### 54.4 自动加载类

```php
  private static function initAutoLoad()
    {
        spl_autoload_register(function ($class_name) {
            $namespace = dirname($class_name);
            $class_name = basename($class_name);
            if (in_array($namespace, array('Core', 'Lib'))) {
                $path = FRAMEWORK_PATH . $namespace . DS . $class_name . '.class.php';
            } elseif ($namespace  == 'Model') {
                $path = MODEL_PATH . $class_name . '.class.php';
            } elseif ($namespace == 'Traits') {
                $path = TRAITS_PATH . $class_name . '.class.php';
            } else {
                $path = CONTROLLER_PATH . PLATFROM_NAME . DS . $class_name . '.class.php';
            }
            if (file_exists($path) && is_file($path)) {
                require $path;
            }
        });
    }
```

### 54.5 请求分发

```php
  private static function initDispatch()
    {
        $controller_name = '\Controller\\' . PLATFROM_NAME . '\\' . CONTROLLER_NAME . 'Controller';
        $action_name = ACTION_NAME . 'Action';
        $obj = new $controller_name;
        $obj->$action_name();
    }
```

### 54.6 封装run()方法

```php
   public static function run()
    {
        self::initConst();
        self::initConfig();
        self::initRoutes();
        self::initAutoLoad();
        self::initDispatch();
    }
```

### 54.7 在入口中调用run()方法

```php
<?php
require './Framework/Core/Framework.class.php';
Framework::run();
```

## 55 运行项目

​	更改配置

​	1、连接数据库的参数从配置文件获取

```php
<?php

namespace Core;

class Model
{
    protected $mypdo;

    ...
    private function initMyPDO()
    {
        $this->mypdo = MyPDO::getInstancel($GLOBALS['config']['database']);
    }
}

```

​	2、更改ProductsControleller控制器

```php
<?php

namespace Controller\Admin;

class ProductsController
{
    public function listAction()
    {
        $model = new \Model\ProductsModel;
        $list = $model->getList();
        require __VIEW__ . 'products_list.html';
    }
    public function delAction()
    {
        ...
        $model = new \Model\ProductsModel;
        ...
    }
}
```

​	3、更改ProductsModel类

```php
<?php
namespace Model;
class ProductsModel extends \Core\Model
{
    ...
}
```

​	4、更改MyPDO类

```php
<?php

namespace Core;

class MyPDO
{
   ...
    private function initParam()
    {
        $this->type = $GLOBALS['config']['database']['type'];
        $this->host = $GLOBALS['config']['database']['host'];
        $this->port = $GLOBALS['config']['database']['port'];
        $this->dbname = $GLOBALS['config']['database']['dbname'];;
        $this->charset = $GLOBALS['config']['database']['charset'];
        $this->user = $GLOBALS['config']['database']['user'];
        $this->pwd = $GLOBALS['config']['database']['pwd'];
    }
    private function initPDO()
    {
        $dsn = "{$this->type}:host={$this->host};port={$this->port};dbname={$this->dbname};charset={$this->charset}";
        $this->pdo = new \PDO($dsn, $this->user, $this->pwd);
    }
    private function initException()
    {
        $this->pdo->setAttribute(\PDO::ATTR_ERRMODE, \PDO::ERRMODE_EXCEPTION);
    }
  	...
    public function exec($sql)
    {
        try {
            ...
        } catch (\PDOException $ex) {
            ...
        }
    }
    private function getType($type)
    {
        switch ($type) {
            case 'num':
                return \PDO::FETCH_NUM;
            case 'obj':
                return \PDO::FETCH_OBJ;
            case 'both':
                return \PDO::FETCH_BOTH;
            default:
                return \PDO::FETCH_ASSOC;
        }
    }
    public function fetchAll($sql, $type)
    {
        try {
           ...
        } catch (\PDOException $ex) {
          ...
        }
    }
    public function fectRows($sql, $type)
    {
        try {
            ...
        } catch (\PDOException $ex) {
           ...
        }
    }
    public function fetchClount($sql)
    {
        try {
            ...
        } catch (\PDOException $ex) {
        	...
        }
    }
}

```

## 56 Traits代码复用

​	有的控制器操作完毕后要跳转，有的不需要，

​	解决：将跳转的方法封装到traits中

​	代码实现：

![image-20220617080444842](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220617080444842.png)

​	2、在Traits目录中创建Jump.class.php

```php+HTML
<?php

namespace Traits;

trait Jump
{
    //成功的方法
    public function success($url, $info, $time)
    {
        $this->redirect($url, $info, $time, 'success');
    }
    //失败的方法
    public function error($url, $info, $time)
    {
        $this->redirect($url, $info, $time, 'error');
    }
     /*
    *作用：跳转的方法
    *@param $url string 跳转的地址
    *@param $info string 显示信息
    *@param $time int 停留时间
    *@param $flag string 显示模式 success|error 
    */
    private function redirect($url, $info, $time, $flag)
    {
        if ($info == '') {
            header("location:{$url}");
        } else {
            echo <<<str
            <!DOCTYPE html>
            <html lang="en">
            
            <head>
                <meta charset="UTF-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Document</title>
                <style>
            
                </style>
            </head>
            
            <body>
                <img src="../Public/images/{$flag}.png" alt="">
                <div>{$info}</div>
                <div><span id="success">$time</span>秒后跳转</div>
            
                <script>
                    var time = $time;
                    setInterval(function () {
                        document.querySelector('#success').innerHTML = --time;
                        if (time == 0) {
                            location.href = 'index.php?'
                        }
                    }, 1000);
                </script>
            </body>
            
            </html>
            str;
        }
    }
}

```

​	在ProductsController控制器中使用原型

```php
<?php

namespace Controller\Admin;

class ProductsController
{
    use \Traits\Jump;
    ...
```

## 57 删除功能

​	入口

```php+HTML
<a href="index.php?c=products&a=del&proid=<?= $rows['proID'] ?>"
                    onclick="return confirm('是否删除此商品')">删除</a>
```

控制器(ProductsController)

```php
 public function delAction()
    {
        $id = (int) $_GET['proid'];
        $model = new \Model\ProductsModel;
        if ($model->delItm($id)) {
            $this->success('location:index.php?c=Products&a=list&p=Admin', '删除成功', 3);
        } else {
            $this->error('location:index.php?c=Products&a=list&p=Admin', '删除失败', 3);
        }
    }
```

模型、视图

```
无改变
```


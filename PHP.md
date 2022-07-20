# PHP



```
apt install php7.4-cli

apt install php
apt install libapache2-mod-php
apt install php7.0-mysql
apt install phpmyadmin

服务操作
service apache2 restart
service mysql restart
service php7.0-fpm restart

apache2.conf
末尾添加
include /etc/phpmyadmin/apache.conf

AddType applicatin/x-httpd-php .php .html .htm

AddDefaultCharset UTF-8

访问 http://localhost/phpmyadmin/

php
php -v

```

```
<?php
/**
 * Created by IntelliJ IDEA.
 * User: Developer
 * Date: 2020/12/28
 * Time: 0:38
 */

//include "yes.ican/YicDataType.php";

//phpinfo();
//echo  "Yes I Can";
//print("Yes I Can");

//function () {
//    $a = function () {
//        echo 'aaaa <br>';
//    };
//    return call_user_func($a);
//}

logMap(array(
    "12"    =>  "asdf",
    "123"   =>  "",
    "234"   =>  "",
));
logMap("asdfasdf");

function logMap($object) {
    $object = json_encode($object);
    $pos1 = strpos($object,"{") === false;
    $pos2 = strpos($object,"}") === false;
    $pos3 = strpos($object,"[") === false;
    $pos4 = strpos($object,"]") === false;


    if((!$pos1 && !$pos2) || (!$pos3 && !$pos4)) {
        printJson($object);
    } else {
        println($object);
    }
}

function printJson($json) {
    $tabNum = 0;
    $startIndex = 0;
    $endIndex = 0;
    $strNum = 0;
    $length = strlen($json);
    for($i=0; $i< $length; $i++) {
        $c = $json[$i];
        if($c == '"' && $json[$i-1] != '\\') {
            $strNum ^= 1;
        }
        if($strNum != 0) {
            continue;
        }
        switch ($c) {
            case '[':
            case '{':
                $oldTabNum = $tabNum;
                if($length > ($i + 1) && $json[$i + 1] == '}' && $c == '{') {
                    $i++;
                    if($length > ($i + 1) && $json[$i + 1] == ',') {
                        $i++;
                    }
                } else if($length > ($i + 1) && $json[$i + 1] == ']' && $c == '[') {
                    $i++;
                    if($length > ($i + 1) && $json[$i + 1] == ',') {
                        $i++;
                    }
                } else {
                    $tabNum++;
                }
                $endIndex = $i + 1;
                outString($json, $oldTabNum, $startIndex, $endIndex);
    //						$tabNum++;
                $startIndex = $endIndex;
                break;
            case '}':
            case ']':
                if($json[$i - 1] != '}' && $json[$i - 1] != ']') {
                    $endIndex = $i;
                    outString($json, $tabNum, $startIndex, $endIndex);
                    $startIndex = $endIndex;
                }
                if($length > ($i + 1) && $json[$i + 1] == ',') {
                    $i++;
                }
                $endIndex = $i + 1;
                $tabNum--;
                outString($json, $tabNum, $startIndex, $endIndex);
                $startIndex = $endIndex;
                break;
            case ',':
                $endIndex = $i + 1;
                outString($json, $tabNum, $startIndex, $endIndex);
                $startIndex = $endIndex;
                break;
        }
    }
}

function outString($json, $tabNum, $startIndex, $endIndex) {
    $stringBuilder = "";
    for ($i=0; $i< $tabNum; $i++) {
        $stringBuilder .= "\t";
    }

    println($stringBuilder.trim(substr($json, $startIndex, ($endIndex - $startIndex))));
}

function println($object) {
    print("$object\n");
}



```

```
echo ("<script type=\"text/javascript\">");
echo ("function fresh_page()");
echo ("{");
echo ("window.location.reload();");
echo ("}");
echo ("setTimeout('fresh_page()',1000);");
echo ("</script>");

session_start();
$num = $_SESSION['hhh'];
$_SESSION['hhh'] = $_SESSION['hhh']+1;

echo $num.'<br/>';

$con = mysqli_connect("localhost:3306","root","");
if (!$con)
{
    die('Could not connect: ' . mysql_error());
}

mysqli_select_db($con,"newsdb");

$result = mysqli_query($con,"SELECT author,author_avatar FROM author limit 10 OFFSET ".($num*10));

while($row = mysqli_fetch_row($result))
{
    echo "<a href=".$row[1].">".$row[0]."</a>";
    echo "<br />";
}

mysqli_close($con);

echo basename('asdf/asdf.txt');

$json = array('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
$jsonString = json_encode($json);
var_dump(json_decode($jsonString, false));

$day = cal_days_in_month(CAL_GREGORIAN, 10, 2005);
echo $day;

$file = fopen("Roach_PHP.php", "r");
//while(!feof($file))
//{
////    echo fgets($file)."";
////    echo fgetc($file);
//}
fclose($file);
```



## 注释

```
// 单行注释
/* */ 多行注释
```

## 变量定义

```
$<name> = <value>;

字符串
$string= <<<EOF
    "abc"$string
    "123"
EOF;

// 结束需要独立一行且前后不能空格
```

## 数据类型

```
"" '' # 字符串
100 # 整型
100.0 # 浮点型

var_dump

define("CONSTDEF", "mydreem",false);
echo CONSTDEF;
```

## 运算符

```
算术运算符 + - * / % ++ --
逻辑运算符 and or xor && || !
关系运算符 条件 ? :
比较运算符 > >= < <= == != <> === !==
赋值运算符 = += -= *= /= %= .=
并置运算符 连接字符串 .
数组运算符 + == != <> === !==
```

## 流程控制

```
分支流程
if # if elseif else
switch # switch case default
循环流程
for # for
foreach # foreach as
while # while
do while # do while
跳转流程

if($intValue==12)
    {
    }
    else if($intValue)
    {
    }
    else
    {
    }

    switch ($intValue)
    {
        case 12:
            break;
        case 10:
            break;
        default:
    }
```

## 数组

```
$array = array("string1","string2","string3");
var_dump($array);
print_r($array);
echo $array[0];
echo count($array);

for($x=0;$x<count($array);$x++){
    echo $array[$x]."\n";
}
$array=array("key1"=>"string1","key2"=>"string2","key3"=>"string3");
foreach ($array as $x=>$value){
    echo $x."=".$value."\n";
}

    sort($array);
    rsort($array);
```

## 函数

```
function

function functionDef(){
//    $int = 12;
    global $int;
    echoln($int);
    echoln($GLOBALS['string']);

    static $x=0;
    echo $x;
    $x++;
    echo $x;
    echo PHP_EOL;
}

phpinfo
```

## 类

```
class ClassDef
{
    var $varDef;

    public function __construct($varDef="red")
    {
        $this->varDef = $varDef;
    }

    function funDef(){
        return $this;
    }
}
```

## 接口

```

```

## 超级全局变量

```

```

```

```



## 数据库

```

```

# 字符串函数

```
    strlen($string);
    strpos($string,$string);
```

```

```



```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```


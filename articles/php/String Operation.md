# 字符串操作

## 1. 字符串的格式化
### 1.1 字符串的整理：
#### rtrim(),chop()是此函数的别名，可以理解为小名。
 + 除字符串右端的空白字符或其他预定义字符
 + chop(string,charlist)
   - string：必需。规定要检查的字符串。
   - charlist:可选。规定从字符串中删除哪些字符。<br/>
            如果 charlist 参数为空，则移除以下字符：<br/>
            "\0" - NULL<br/>
            "\t" - 制表符<br/>
            "\n" - 换行<br/>
            "\x0B" - 垂直制表符<br/>
            "\r" - 回车<br/>
            " " - 空格
            
+ 函数示例：
 
 ```
function funcChop() {
    $str = "Hello YLD!";
	echo $str . "<br>";
	echo chop($str,"YLD!"). "<br>";
	echo rtrim($str,"YLD!")."<br>";//chop()是此函数的别名，可以理解为小名。
}
 ```
 
+ 输出：
 
 ```
Hello YLD!
Hello
Hello
 ```
            
#### ltrim()
+ 删除字符串开头空格或者预定的其它字符
+ ltrim(string,charlist)
 - string,必需。规定要转换的字符串。
 - charlist,可选。规定从字符串中删除哪些字符。<br/>
            如果未设置该参数，则全部删除以下字符<br/>
            "\0" - ASCII 0, NULL<br/>
            "\t" - ASCII 9, 制表符<br/>
            "\n" - ASCII 10, 新行<br/>
            "\x0B" - ASCII 11, 垂直制表符<br/>
            "\r" - ASCII 13, 回车<br/>
            " " - ASCII 32, 空格<br/>
            
+ 函数示例：

```
function funcLtrim() {
    $str = "~Hello small yellow luo";
	echo $str."<br>";
	echo ltrim($str,"~Hello")."<br>";
	echo ltrim($str,"~he")."<br>";//区分大小写的；字符串必须连贯
	echo ltrim($str,"ll")."<br>";//必须从左侧第一个字符开始；
}
```

+ 输出：

```
~Hello small yellow luo
small yellow luo
Hello small yellow luo
~Hello small yellow luo
```


#### trim()
+ 此函数返回字符串 str 去除首尾空白字符后的结果。
+ ltrim(string,charlist)
 - string,必需。规定要转换的字符串。
 - charlist,可选。规定从字符串中删除哪些字符。<br/>
            如果未设置该参数，则全部删除以下字符<br/>
            "\0" - ASCII 0, NULL<br/>
            "\t" - ASCII 9, 制表符<br/>
            "\n" - ASCII 10, 新行<br/>
            "\x0B" - ASCII 11, 垂直制表符<br/>
            "\r" - ASCII 13, 回车<br/>
            " " - ASCII 32, 空格<br/>
            
+ 函数示例：
 
 ```
function funcTrim() {
	$question = " \0 what's up? \r";
	$answer = " no";
	var_dump($question.$answer);
	var_dump(trim($question).trim($answer));
}
 ```
 
+ 输出：
 ```
string(18) " what's up? no" 
string(12) "what's up?no"  //注意字符串的个数变化
 ```
 
### 1.2 格式化字符串以便输出
#### 1.2.1 nl2br()
+ 在字符串所有新行之前插入 HTML 换行标记.
+ 在字符串 string 所有新行之前插入`<br />` 或 `<br>`，并返回。
+ string nl2br ( string $string [, bool $is_xhtml = true ] )
 - string,输入字符串
 - is_xhtml,是否使用 XHTML 兼容换行符
 
+ 函数示例：
 
 ```
function funcNl2br() {
	echo nl2br("luo is \n ugly \r\n");
	$string = "Small\r\nYellow\n\rLuo\nis\rstupid";
	echo nl2br($string,false);//注意输出换行
}
 ```
 
+ 输出：
 ```
luo is 
ugly 
Small
Yellow
Luo
is
stupid
 ```

#### 1.2.2 为打印输出而格式化
#### printf()
+ 输出格式化字符串
+ `printf ( string $format [, mixed $args [, mixed $... ]] )`
+ 函数示例：
```
function funcPrintf() {
	//与java中格式化输出一样
	printf('I need to pay $%.02lf',1.3568);
	echo "<br>";
	$goodevil = array('good', 'evil');
	//巧用printf
	printf_array('There is a difference between %s and %s', $goodevil);

}
function printf_array($format, $arr)
{
	//回调printf函数
	return call_user_func_array('printf', array_merge((array)$format, $arr));
}
```

+ 输出：

```
I need to pay $1.36
There is a difference between good and evil
 ```

#### sprintf()
+ sprintf() 函数把格式化的字符串写入变量中。
+ sprintf(format,arg1,arg2,arg++)
 - format,必需。规定字符串以及如何格式化其中的变量。可能的格式值：<br/>
                %% - 返回一个百分号 % <br/>
                %b - 二进制数  <br/>
                %c - ASCII 值对应的字符 <br/>
                %d - 包含正负号的十进制数（负数、0、正数）<br/>
                %e - 使用小写的科学计数法（例如 1.2e+2） <br/>
                %E - 使用大写的科学计数法（例如 1.2E+2） <br/>
                %u - 不包含正负号的十进制数（大于等于 0） <br/>
                %f - 浮点数（本地设置）<br/>
                %F - 浮点数（非本地设置）<br/>
                %g - 较短的 %e 和 %f  <br/>
                %G - 较短的 %E 和 %f  <br/>
                %o - 八进制数  <br/>
                %s - 字符串   <br/>
                %x - 十六进制数（小写字母） <br/>
                %X - 十六进制数（大写字母   <br/>
 - arg1,必需。规定插到 format 字符串中第一个 % 符号处的参数。
 - arg2,可选。规定插到 format 字符串中第二个 % 符号处的参数。
 - arg++,可选。规定插到 format 字符串中第三、四等 % 符号处的参数。
 
+ 函数示例：

```
function funcSprintf() {
	$number  = 2;
	$location = "HangZhou";
	//与printf相比，只有格式化的功能，没有打印的功能
	$text = sprintf("I have %u friends in %s",$number,$location);
	echo $text;
}
```

+ 输出：

```
I have 2 friends in HangZhou
```
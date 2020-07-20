# ■ 教学目标!!!

能够理解异步请求概念&好处

能够独立发送异步请求

能够独立实现异步请求案例



明确：后期实战工作1/3工作量就是今天知识点



# ■ HTTP协议（理解重要）

## 应用

![1592359627461](images/1592359627461.png) 

## 明确需求 

- 明确：在生活中，我们经常通过浏览器输入网址打开一个网站，例如打开淘宝，天猫，京东等
- 思考：网页显示的内容数据哪里来的？
- 回答：

> 用户角度 - 输入网址回车可以看到网页内容
>
> 开发角度 - 输入网址 - 通过DNS文件找到服务器IP -> 然后发送请求 -> ... -> 最终返回html浏览器解析
>
> 脚下留心：解析的过程中发现img、js、css继续发送请求解析

![1568782521808](images/1568782521808.png) 

![1568782743163](images/1568782743163.png) 

- 思考：请求可以随意发吗，还是有规则的？
- 回答： 不可以，所有请求都必须HTTP规则（举例生活中的斑马线和红绿灯



## 概念

- 概念

> ```
> HTTP是一种【超文本传输协议】（HyperText Transfer Protocol)，
> 它是互联网上应用最为广泛的一种网络协议。
> ```

- 说明

> ```
> 协议：是指计算机通信网络中两台计算机之间进行通信所必须共同遵守的规定或规则。
> 协议概括：计算机和计算机 通信  必须遵循的规则 （举例：接打电话
> 
> 超文本传输协议（HTTP）：是一种通信协议，它允许将超文本标记语言（HTML）文档从Web服务器传送到客户端的浏览器。
> 
> 
> 普通文本：字符、汉字等 s r c a  $ -
> 超文本：也可以输入字符、汉字等，但是字符的组合变成了图片、音频等。
> 	  如：<img src='' />
> ```

- 概括：HTTP协议，就是一个规则，遵循这个规则可以实现计算机之间相互通信，传递超文本数据

- 其他

```
http	简单的传输数据    80
https   加密传输数据     443    后期三阶段讲到微信小程序会强调 因为必须用
```



## 作用

HTTP协议

规定了客户端 和 服务端 通信方式（客户端如何传递数据给服务端，服务端如何返回数据给客户端）



场景：淘宝、京东、微信APP等等



## 通过谷歌开发工具查看HTTP协议规!!!

每次通信：有请求（request）有响应（response）

请求中包含：请求行、请求头、请求体（传递的参数   

响应中包含：响应行、响应头、响应体（响应的数据response  一般看preview

![1568789586371](images/1568789586371.png) 



## 小总结!!!

- 单词：request请求、response响应

- 什么是http：就是互联网通信规则

作用：客户端如何传递数据，服务端如何响应数据

请求：请求行（请求方式/请求状态/请求地址）、请求头、请求体（请求参数

响应：响应行（请求方式/请求状态/请求地址）、响应头、响应体（返回的数据一般看preview



- 面试题：谈谈对HTTP协议的理解

回答：

```
首先概念  HTTP是超文本传输协议
接着作用  主要规定计算机之间如何相互通信
```

追问：HTTP协议你都知道哪些

回答：请求/响应行、请求/响应头、请求/响应体





# ■ AJAX简介

## 明确需求

在工作中，我们经常要检测用户或邮箱等是否存在，搜索下拉提示等。

明确：仅通过之前学习知识点肯定不够。

![1568783242097](images/1568783242097.png) 



![1568783250334](images/1568783250334.png) 

思考：如何解决呢？

回答：通过ajax技术



## 是什么

Ajax是“Asynchronous JavaScript and XML”的简写（Ajax 中文名 异步请求）

异步请求（ajax）：允许`客户端`和`服务端` `无刷新通信`的技术。



思考：无刷新通信技术的好处

回答：局部刷新、减少请求、减轻服务器压力





## 能干吗/应用场景

异步分页

异步检测邮箱是否存在（举例126、163邮箱）

![1568783644277](images/1568783644277.png) 

异步检测用户是否存在。

等



注：后期做项目用来异步获取项目数据



## 去哪下

不用下，直接下JS代码即可





## 其他（特点、好处）

特点：不用刷新页面

好处：减轻服务器压力，用户体验度更好



## 小总结

ajax异步请求是什么：允许  客户端  和  服务端  无刷新通信的 技术

能干吗：检测用户是否存在、检测邮箱是否存在、搜索等等

去哪下：不用下 直接下js代码

特点：无刷新

好处：减轻服务器压力，提高用户体验度



# ■AJAX使用（重点）

## 语法

注：语法不推荐记，因为工作不用 ，工作都是别人封装好的，但步骤最好记一下（相对重要

````javascript
// 步骤1：创建ajax对象：
const xhr =  new XMLHttpRequest();

// 步骤2：时时监听ajax状态   5个状态
xhr.onreadystatechange = fn

// 步骤3：创建HTTP请求头
xhr.open（请求类型POST/GET，请求地址URL，[默认异步true或者同步false]）

// 注：POST请求必须设置请求编码，不然后端无法解析获取数据 (切记切记别乱放 注意位置)
xhr.setRequestHeader( "content-type", "applicativon/x-www-form-urlencoded" );

// 步骤4：发送请求
xhr.send（POST请求则为POST请求数据没有数据就不写/GET请求则null）

function fn() {
	//只要ajax状态改变就打印
	if (xhr.readyState == 4 && xhr.status == 200)  {
		alert(xhr.responseText);
	}
}
````

<https://www.w3cschool.cn/ajax/ajax-xmlhttprequest-onreadystatechange.html> 

脚下留心

```
1. 必须走http协议，也就是通过浏览器访问 
2. get请求参数   直接请求地址后面加 文件名及后缀?键1=值1&....&键n=值n
3. post请求参数  send(键1=值1&....&键n=值n)
```





## 练习

需求1：自己定义一个接口返回任意数据，接口是json文件

```
{
    "meta": {
        "msg": "操作成功",
        "status": 200
    },
    "data": null
}
```

需求2：页面搞一个按钮，点击之后发送请求

```
<meta charset="UTF-8">

<button id="getBtn">点击发送get异步请求</button>
<button id="postBtn">点击发送post异步请求</button>

<script>
// 1. 获取
let postBtnObj = document.querySelector('#postBtn')
// 2. 绑定点击事件
postBtnObj.addEventListener('click', function() {
    // 3. 发送异步请求

    // 1. 创建ajax对象
    const xhr = new XMLHttpRequest
    // 2. 监听状态
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log('post请求也收到数据啦~.~', xhr.responseText)
        }
    }
    // 3. 通过open设置请求地址、请求参数
    xhr.open('post', './api.json')
    
    // 注：POST请求必须设置请求编码，不然后端无法解析获取数据 (切记切记别乱放 注意位置)
    xhr.setRequestHeader( "content-type", "application/x-www-form-urlencoded" );

    // 4. 发送请求  键1=值1&....&键n=值n
    xhr.send('name=随便写&pwd=123456')
})
</script>

<script>
// 1. 获取
let getBtnObj = document.querySelector('#getBtn')
// 2. 绑定点击事件
getBtnObj.addEventListener("click", function() {
    // 发送异步请求（请求地址写相对路径 ./../

    // 1. 创建ajax对象
    const xhr = new XMLHttpRequest
    // 2. 监听状态
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log('收到数据', xhr.responseText)
        }
    }
    // 3. 设置请求方式、请求地址  open
    // get请求参数   直接请求地址后面加 文件名及后缀?键1=值1&....&键n=值n
    // xhr.open('get', 'http://qf2.com/day2/api.json')
    // xhr.open('get', './api.json')
    xhr.open('get', './api.json?name=随便写&pwd=123456')
    // 4. 发送请求  send
    xhr.send(null)
})
</script>
```



 



# ■AJAX同步与异步(主要理解异步同步区别)

## 概念

同步和异步概念：

同步: 指的就是事情要一件一件做。等做完前一件才能做后一件任务

异步: 不受当前任务的影响，两件事情同时进行，做一件事情时，不影响另一件事情的进行。

编程中：异步程序代码执行时不会阻塞其它程序代码执行,从而提升整体执行效率。

![1568785050328](images/1568785050328.png) 

## 练习

同步：必须每一步走完了 才会继续向下

异步：同时走  不等

```js
<script>
console.log(111)

// 1. 创建xhr对象
const xhr = new XMLHttpRequest

// 2. 监听请求状态
xhr.onreadystatechange = fn

// 3. 设置请求方式、请求地址
xhr.open('get', './test.json', true) // 默认异步
//xhr.open('get', './test.json', false) // 同步代码

// 注：POST请求必须设置请求编码，不然后端无法解析获取数据
// xhr.setRequestHeader( "content-type", "application/x-www-form-urlencoded" );

// 4. 发送请求
xhr.send(null)

function fn()
{
    if (xhr.readyState == 4 && xhr.status == 200) {
        // console.log(xhr.responseText)  返回对象格式的字符串
        console.log(222)
        console.log(JSON.parse(xhr.responseText))
    }
}

console.log(333)
</script>
```

> // 同步：代码必须按顺序执行，等每一行执行完毕了 再回继续向下走  123
> // 异步：触发代码运行，但不等待   132





# ■AJAX案例（推荐多多练习）

## 准备接口

### 说明

1 - 大家不用写，但是最好每一行都看懂   实在不行必须能用

2-使用接口时记得修改数据库名和账号密码





### 表数据

```
CREATE TABLE `stu` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `uname` varchar(255) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `sex` varchar(255) DEFAULT NULL,
  `created_at` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=MyISAM CHARSET=utf8;

INSERT INTO `stu` VALUES ('1', '千锋刘德华', '19', '男', '2017-03-15');
INSERT INTO `stu` VALUES ('2', 'webopenfather2', '18', '男', '2017-03-15');
INSERT INTO `stu` VALUES ('3', 'data13', '20', '男', '2017-03-15');
INSERT INTO `stu` VALUES ('4', 'data14', '20', '女', '2017-03-15');
INSERT INTO `stu` VALUES ('5', 'data15', '20', '女', '2017-03-15');
INSERT INTO `stu` VALUES ('6', '千锋webopenfather6', '20', '男', '2017-03-15');
INSERT INTO `stu` VALUES ('7', '你好刘德华我在你心里7', '20', '男', '2017-03-15');
INSERT INTO `stu` VALUES ('8', '南京千锋8', '20', '男', '2017-03-15');
```



###checkUser.php

```
<?php
// GET传值都是   文件名.php?键=值&....&键n=值n

// 1.获取用户名
$uname = @$_GET['uname']; // 错误抑制

// 验证写后端所有接受的数据都得过滤
if (!$uname) {
    $tips = [
        "meta" => [
            "msg" => "参数有误",
            "status" => 400
        ],
        "data" => null
    ];
    echo json_encode($tips);
    die;//终止后面代码执行 
}

// 2.检测用户是否存在
$pdo = new PDO('mysql:dbname=web', 'root', 'admin888');
//JS 反引号 ${变量名}   PHP  双引号 {变量名}
//脚下留心：name对应的值必须写引号  where name = '张三'
//脚下留心：pdoStatement打印没意义  你看不懂  固定语法 接着通过fetch取数据
$pdoStatement = $pdo->query("select * from stu where uname = '{$uname}';");
$data = $pdoStatement->fetch(PDO::FETCH_ASSOC);
// 找不到 bool(false)
// 找到了 Array ( [id] => 8 [uname] => 野猪佩奇 [age] => 19 )
// var_dump($data);
// print_r($data);
// die;//终止后面代码执行，相当于循环中的break  函数中的return

if ($data) {
// 已注册
    $tips = [
        "meta" => [
            "msg" => "用户已经注册",
            "status" => 403
        ],
        "data" => null
    ];
} else {
// 未注册
    $tips = [
        "meta" => [
            "msg" => "用户未注册",
            "status" => 200
        ],
        "data" => null
    ];
} 

// 3.响应消息
// 直接echo字符串也可以，不利于后期优化
// 而且工作中都是返回json数据 所以采用
// echo '用户已经注册';
// echo '用户未注册';
echo json_encode($tips);
```

使用：

```
./checkUser.php?uname=用户名
```



### search.php

```
<?php
// 1.获取数据
$search = @$_GET['search'];

if (!$search) {
    $arr = [
        "meta" => [
            "msg" => "参数有误",
            "status" => 400
        ],
        "data" => null
    ];
    
    echo json_encode($arr);

    die; //PHP语法终止后面代码执行
}

// 2.操作数据库 查询数据
$pdo = new PDO('mysql:dbname=web', 'root', 'admin888');
$pdoStatement = $pdo->query("select * from stu where uname like '%{$search}%';");
$datas = $pdoStatement->fetchAll(PDO::FETCH_ASSOC);

// 3.响应给请求着
$arr = [
    "meta" => [
        "msg" => "操作成功",
        "status" => 200
    ],
    "data" => $datas
];
echo json_encode($arr);
```



select * from stu wehre uname = "张三"

select * from stu where uname like '%fa%'    含fa

select * from stu where uname like 'fa%'      开头fa

select * from stu where uname like '%fa'      fa结尾



like 就是模糊查询

where 字段名  like '%%'





- 使用接口

```
http://qf2.com/day2/search.php?search=要搜索的内容
```







### page.php

![1568860897196](images/1568860897196.png) 

```
<?php

// 步骤1：定义接口page.php（参数当前页  返回对应页数据）

// 1. 接受当前页参数 pageno
$pageno = @$_GET['pageno'];

if ($pageno < 1) {
    $arr = [
        "meta" => [
            "msg" => "参数有瑕疵",
            "status" => 400
        ],
        "data" => null
    ];
    
    echo json_encode($arr);
    die;
}

// 2. 写sql查询数据
// select * from 表名  order by id asc  limit 起始位置,页面显示条数
// 查询指定表数据，按照id升序（1,2,3...） 然后返回指定条数
// 起始位置 = （当前页 - 1） * 每页显示条数
$pagesize = 2;
$start = ($pageno - 1) * $pagesize;
$pdo = new PDO('mysql:dbname=web', 'root', 'admin888');
$pdoStatement = $pdo->query("select * from stu  order by id asc  limit {$start},{$pagesize}");
$datas = $pdoStatement->fetchAll(PDO::FETCH_ASSOC);
// 3. 响应返回

$arr = [
    "meta" => [
        "msg" => "操作成功",
        "status" => 200
    ],
    "data" => $datas
];

echo json_encode($arr);
```



- 使用接口

```
http://qf2.com/day2/page.php?pageno=第几页
```





## 检测用户名是否存在

![1568783242097](images/1568783242097.png) 

步骤1：创建checkUser.html文件（切记后期必须走80端口访问）

步骤2：先写静态效果（框框 & 框框后面的提示信息）

步骤3：写ajax代码，请求接口

步骤4：根据响应结果写逻辑判断

```
<meta charset="utf-8" />
<input type="text" >
<span>
    <!-- <font color="red">错误信息</font>
    <font color="green">√</font> -->
</span>

<script>
// 当input框失去焦点 -> 发送异步请求
document.querySelector('input').addEventListener('blur', function() {

    // 0. 获取数据
    let uname = this.value

    // 1. 创建xhr对象
    const xhr = new XMLHttpRequest

    // 2. 监听状态
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200)
        {
            // 服务器响应的数据 result
            let res = JSON.parse(xhr.responseText)
            // {"meta":{"msg":"提示信息","status":200},"data":null}

            // 判断
            if (res.meta.status == 200)
            {
                document.querySelector('span').innerHTML = '<font color="green">√</font>'
            } else {
                document.querySelector('span').innerHTML = `<font color="red">X ${res.meta.msg}</font>`
            }
        }
    }

    // 3. 设置请求方式、请求地址
    xhr.open('get', `./checkUser.php?uname=${uname}`)

    // 4. 发送请求
    xhr.send(null)
})
</script>
```







## 搜索下拉提示

![1568783250334](images/1568783250334.png) 

步骤1：显示静态效果

步骤2：获取input框标签对象，绑定键盘松开事件

步骤3：在事件处理函数中发送异步获取数据 并 展示

```html
<meta charset="utf-8">
<input type="text">
<ul> 
    <li>001</li>
    <li>002</li>
    <li>003</li>
</ul>
<script>
// 发现：搜索 中国  没按一下都会发送请求  性能等问题
// 解决：延迟发送请求（节流和防抖）

// 1. 获取input标签对象， 设置事件
// document.querySelector('input').addEventListener('keyup', function() {
//    // 1.获取数据
//    let search = this.value
//    // 2. 发送异步请求
//    const xhr = new XMLHttpRequest
//    xhr.onreadystatechange = function() {
//        if (xhr.readyState == 4 && xhr.status == 200)
//        {
//            let res = JSON.parse(xhr.responseText)
//            console.log(res)
//        }
//    } 
//    xhr.open('get', `./search.php?search=${search}`)
//    xhr.send(null)
// })

let t
document.querySelector('input').addEventListener('keyup', function() {
   
   clearTimeout(t)

   t = setTimeout(() => {

       // 发送异步请求前 先展示loading图
        document.querySelector('ul').innerHTML = '<img src="./loading.jpg" />'
        
        // 1.获取数据
        let search = this.value
        console.log(search)
        // 2. 发送异步请求
        const xhr = new XMLHttpRequest
        xhr.onreadystatechange = function() {
            if (xhr.readyState == 4 && xhr.status == 200)
            {
                let res = JSON.parse(xhr.responseText)
                // console.log(res)

                // 遍历拼接数据
                let html = ``
                res.data.forEach((item, index) => {
                    html += `<li>${item.id} -- ${item.uname}</li>`
                })
                document.querySelector('ul').innerHTML = html
            }
        } 
        xhr.open('get', `./search.php?search=${search}`)
        xhr.send(null)
   }, 1000)
})
</script>
```



## 加载更多

![1568850988532](images/1568850988532.png) 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * { padding:0px; margin:0px; }
        .wrapper { width:100%; }
        .wrapper ul li { width:100%; line-height: 40px; border-bottom: solid 1px #ccc }
        .wrapper div.more { width:100%; line-height: 40px; background: #f2f2f2; border-bottom: solid 1px #ccc; font-size: 20px; text-align: center;cursor: pointer}
    </style>
</head>
<body>
    <div class="wrapper">
        <ul class="content">
            <li>习近平：推进国家治理体系和能力现代化</li>
            <li>习近平对这个问题连说“重话”</li>
            <li>国家主席习近平任免驻外大使</li>
            <li>重启磋商四大看点  确保主题教育取得实效</li>
            <li>这些文物背后的故事令人落泪 经历艰辛 走向胜利</li>
            <li>张錩：活态传承，表现当代的中国  泥美人活力与魅力</li>
            <li>中美贸易谈判下周重启 中方要求美取消全部加征关税</li>
            <li>北上广深平均工资大PK：北京领跑，广深首超10万元</li>
            <li>农业农村部：国家正积极推进非洲猪瘟疫苗研发</li>
            <li>刚刚！福建向全球自我介绍！</li>
            <li>7日17时21分小暑:热浪滚滚"三伏"启 防暑降温纳清凉</li>
            <li>租房便宜了 房租连续两季度下降！你的租金减少没？</li>
        </ul>
        <div class="more">查看更多</div>
    </div>
    <script>
    </script>
</body>
</html>
```

发送请求的情况：点击发送请求追加数据。

```html
1. 获取查看更多标签对象 -> 发送异步请求
2. 根据返回的数据 追加到页面



<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>Document</title>
<style>
    * { padding:0px; margin:0px; }
    .wrapper { width:100%; }
    .wrapper ul li { width:100%; line-height: 40px; border-bottom: solid 1px #ccc }
    .wrapper div.more { width:100%; line-height: 40px; background: #f2f2f2; border-bottom: solid 1px #ccc; font-size: 20px; text-align: center;cursor: pointer}
</style>
</head>
<body>
<div class="wrapper">
    <ul class="content">
        <li>习近平：推进国家治理体系和能力现代化</li>
        <li>习近平对这个问题连说“重话”</li>
        <li>国家主席习近平任免驻外大使</li>
        <li>重启磋商四大看点  确保主题教育取得实效</li>
        <li>这些文物背后的故事令人落泪 经历艰辛 走向胜利</li>
        <li>张錩：活态传承，表现当代的中国  泥美人活力与魅力</li>
        <li>中美贸易谈判下周重启 中方要求美取消全部加征关税</li>
        <li>北上广深平均工资大PK：北京领跑，广深首超10万元</li>
        <li>农业农村部：国家正积极推进非洲猪瘟疫苗研发</li>
        <li>刚刚！福建向全球自我介绍！</li>
        <li>7日17时21分小暑:热浪滚滚"三伏"启 防暑降温纳清凉</li>
        <li>租房便宜了 房租连续两季度下降！你的租金减少没？</li>
    </ul>
    <div class="more">查看更多</div>
</div>
<script>
let pageno = 0

//1.获取more标签对象
document.querySelector('.more').addEventListener('click', function() {

    pageno++
    
    this.innerText = '加载中...'
    
    const xhr = new XMLHttpRequest
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200)
        {
            // result 结果
            let res = JSON.parse(xhr.responseText)
            // res {meta, data}   

            // 遍历展示数据
            res.data.forEach((item, index) => {

                let liObj = document.createElement('li')
                liObj.innerText = item.uname
                
                document.querySelector('.content').appendChild(liObj)
            })

            document.querySelector('.more').innerText = '查看更多'
        }
    }
    xhr.open('get', `./page.php?pageno=${pageno}`)
    xhr.send(null)
})
</script>
</body>
</html>
```


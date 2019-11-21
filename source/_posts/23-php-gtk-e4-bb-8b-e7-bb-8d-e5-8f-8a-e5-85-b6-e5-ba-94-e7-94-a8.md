---
title: PHP-GTK 介绍及其应用
url: 23.html
id: 23
categories:
  - 'NULL'
  - 技术杂文
date: 2008-12-19 09:41:00
tags:
---

1\. PHP-GTK介绍

1.1 PHP-GTK  
PHP-GTK是PHP的延伸模组，它可以让程式设计师写出在客户端执行的、且独立的GUI的程式。这个模组不允许在浏览器上显视GTK+的程式，它一开始就是开发来写独立的GUI程式的。

1.2 GTK  
GTK原本是为GIMP，一个GUI的影像处理软体而开发的。GTK+是GIMP的套装工具。GTK+从这里开始发展，直到现在已经成为Gnome的中心(Gnome是一个桌面环境)。後来GTK+也已经被推广到BeOS和Win32，使得它成为PHP延伸模组的最佳选择，维持PHP可以跨平台并可以用PHP为Linux,BeOS,Windows等平台开发视窗介面的程式。

2\. PHP-GTK概念

2.1 前言  
接下来就要教各位一点点比较观念性的东西罗┅因为这章的概念都是非常重要的，所以就算不懂，也还是要慢慢的看懂它，不然┅以後就┅。还有，接下来的内容不建议没有程式设计经验的读者阅读，因为有很多的观念很容易会搞不清楚。还有，接下来该用英文的部分我都会用英文，这样大家在看国外文件的时候才不会不知所措，加油吧!!如果对本章有任何不懂之处，请自行查阅  
PHP-GTK Manual：[http://gtk.php.net/manual/en/](http://gtk.php.net/manual/en/)

2.2 Widget(s)  
Widget是一个GUI程式中基本的functions和forms。最常用的几个Widget是：label、button、window、frame和text  
box。所有的widget都是来自於一个抽象的基本class─GtkWidget。每个widget都是一个class

一个Widget一生大概都有五个时期：  
1\. 建立(Creation)：宣告一个物件(declaring an object)  
2\. 放置(Placement)：将它加入一个容器中(adding it to a container)  
3\. 信号连接(Signal Connection)：接收信号以及进行动作(the action it will perform)  
4\. 显示(Display)：它是否是可见的(whether it is viewable or not)  
5\. 删除(Destruction)：关闭程式(closing of a program)

2.3 Container(s)  
Container是一个可以包含其他widget的widget。大部分的widget都是container，例如：GtkWindow、GtkTable和GtkBox。除了这点之外，container跟其他的widget没两样，也可以被放到其他container去。而所有的container都是来自於一个class─GtkContainer，本身来自於GtkWidget的class。所以container也是widget的一种。

2.4 Signal(s)  
当程式设计师在程式中做了一个动作时，程式需要有一个动作来回应使用者的动作。Signals使程式可以知道使用者做了动作并可以触发适合的回应。

例如，当使用者按了一个可以开新视窗的按钮(GtkButton)，程式认出这个请求，於是就开了一个新的视窗。这件事可以经由signal来做到。当按钮按下去之後，会使widget发出一个signal，接着再由该signal触发callbacks，产生一个新的视窗(GtkWindow)。

2.5 Callback(s)  
Callback就是当signal送出之後，被signal唤起的function。Callback会执行function传回一个值或是做一个动作。Callback就是signal的handler  
funciton。它可以是该signal的预设handler或着是程式设计师定义的function。要建立一个callback，就必须把function  
connect 到 signal。

2.6 Signal Inheritance(继承)  
和methods一样，signals可以被物件继承。一个widget可以送出任何它的parent widget可以送出的还有它自己特有的signal。

2.7 Connecting Signals  
你必须为PHP-GTK指定一个callback  
function当signal送出时来对signal做回应。把一个signal连接到一个function可以用connect()  
这个object 方法达成。

如下：

<?php  
//建立一个GtkWindow  
$window = &new GtkWindow();  
//将"destroy" signal用connect() 方法连接到shutdown函式  
$window->connect("destroy", "shutdown");  
//建立一个GtkButton，按钮文字为"按我"  
$button = &new GtkButton("按我");  
$button->connect("clicked", "you_clicked");  
//把GtkButton放到是container的GtkWindow中  
$window->add($button);  
//显示$window以及它的所有child widget  
$window->show_all();  
//进入程式主回圈(即程式启动之意)  
gtk::main();  
?>

  
执行它的话，就会出现一个视窗，里面有一个写着"按我"的按钮，按下按钮程式就会执行you_clicked函式。在这个程式中，$window物件的"destroy"  
signal是在使用者按下视窗右上角的"X"时会送出的；而$button物件的"clicked"  
signal是在使用者按下该按钮的时候会送出的。最後那一行的gtk::main()  
是一定要执行的，这样才能告诉电脑要开始执行程式，既然有开始执行，那就一定有停止吧? 没错，用gtk::main_quit()  
就可以停止程式了。

看完了以上的范例，有些读者可能会有疑问「如果我想执行送出signal的widget之外的widget的method怎么办?」，这时候，就要用另一个method了  
a connect_object()，它可以跨物件呼叫方法或是传递其他物件做为function的叁数。跨物件呼叫方法如下：

$window->connect\_object("destroy", array("gtk","main\_quit"))

  
如此，在$window物件的"destroy" signal送出的时候就会唤起gtk::main_quit()这个方法，程式就会终指执行。

在介绍连接方法的最後，再提一下connect() 和 connect_object() 的自订增加要传给callback function的叁数的办法。见例子：  
<?php  
$parameter="新超人";  
$button1 = &new GtkButton("测试");  
//将"clicked" signal连接到who\_are\_you函式，附加叁数$parameter  
$button1->connect("clicked","who\_are\_you",$parameter);  
$button2 = &new GtkButton("测试二");  
//将"clicked" signal连接到kill\_the\_button1函式，附加叁数$button1  
$button2->connect\_object("clicked","kill\_the_button1",$button1);

function who\_are\_you($widget,$parameter){  
echo $parameter;  
}

function kill\_the\_button($button){  
$button->destroy();  
}  
?>

  
注意那两个function，who\_are\_you有两个叁数对吧? 第一个是做什么用的呢?为什么它会自动出现??  
因为，每个signal的callback function都会因为signal的不同而加上一些内定一定会传入callback  
function的叁数，而基本上所有的signal都至少会传给callback  
function一个叁数a产生该signal的物件。所以who\_are\_you的第一个叁数就是$button1，而第二个就是$parameter，也就是新超人。那kill\_the\_button函式就不一样罗~  
因为connect_object()函式会呼略原本signal的callback  
function的预设叁数，所以kill\_the\_button就只有附加在connect\_object最後的$button1叁数了，如此，kill\_the_button就可以呼叫$button1的方法或是取得它的属性，这里呼叫了$button1的destroy方法，於是$button1就会被消灭。

2.8 Event(s)  
Event是signal的一种，但是它的用途还有功能都非常强大。就signal来说，signal这种东西都是内建在widget上的，所以，例如GtkWindow没有"clicked"signal，那么在不用event  
signal的情况下，GtkWindow是决对不可能送出clicked之类的signal的。那如果用了event signal呢?  
Event signal是可以允许被加到任何的widget上的，所以就算这个widget本来没有发出"clicked"signal的功能，你也可以用add_events()  
来为它加上按了它之後event signal会做什么样的反应。而event  
signal中包含的资讯比较多，比如说当你在使用"key-press-event"这个event  
signal的时候，同时也会记录到你按下的是什么按键，於是通常event signal的callback  
function格式内定会有两个叁数，第一个依然是送出signal的widget，而第二个就是$event，这个$event是一个class，里面的属性和方法会因为送过来的event  
signal种类而不同。就"key-press-event"传回的$event  
class来说，里面有一个属性是keyval，内容就是使用者按的是哪一个键。这些对於一个程式设计师来说常常是很有用的资讯。所以event的重要性是不可忽视的，就算刚开始会有点不懂，也要慢慢的融入才行。这一节也非常重要。

3\. 安装PHP-GTK

3.1 在Windows系统下安装  
首先要从[http://gtk.php.net/download.php](http://gtk.php.net/download.php)下载...HP-GTK的windows binary档案(本文撰写时为0.5.1版)。

接着来看看PHP-GTK 0.5.1 binary档的内容：  
\\php4 → php 和 php-gtk binary 档案  
\\winnt → 预设的php.ini档案  
\\winnt\\system32 → gtk binaries used by extension  
\\test → 几个测试用的档案  
\\README.txt → 安装说明档

开始安装：  
1\. 复制 \\php4 的内容到你的php安装目录下(例C:\\php)。  
2\. 复制 \\winnt 的内容到你的winnt资料夹。在Windows  
NT或Windows2000上是C:\\winnt，在Window95、98、xp上是C:\\windows。如果该资料夹里已经有  
php.ini，那就不用做这个动作。  
3\. 复制 \\winnt\\system32 的内容到你的winnt\\system32资料夹。在Windows  
NT或Windows2000上是C:\\winnt\\system32，在Window95、98、xp上是C:\\windows\\system32。  
4\. 复制 \\test 的内容到你想要执行你的script的地方(此步骤非必要)。

如何执行PHP-GTK程式：  
PHP-GTK程式可以在「开始」-「执行」下输入指令(或是建立捷径)来启动，如：C:\\php\\php -q  
c:\\php\\test\\gtk.php ## 表示不送印出 HTTP Header，但一直使用这个视窗，直到关闭程式。  
C:\\php\\php -q -c php.ini c:\\gtk.php ## 同上，但执行指定的php.ini设定。  
C:\\php\\php C:\\php\\test\\gtk.php ## 表示会送印出 HTTP Header，但一直使  
用这个视窗，直到关闭程序  
C:\\php\\php_win C:\\php\\test\\gtk.php ## 表示不使用视窗，执行後独立一个执行程式，他是使用 php  
-q模式，但是只要output出任何字元，例如错误讯息，就会停止执行。

3.2 在UNIX系统下安装  
Debian的使用者可以在 [http://www.debian.org](http://www.debian.org) 下载PHP-GTK的binary档。系统需求须已安装下列package：

PHP 4.1.0 或之後的版本，必须是编为CGI binary(command-line) 版本，包含所有的header  
files和devlement scripts。

PHP-GTK支援GTK+ v1.2而需要安装1.2.6以上版本的GTK+。GTK+  
v2.0还未被支援，必须等到它开发完成并且普及了之後才会被支援。你可以从下面的网址取得GTK+  
v1.2.X的最新版本：[ftp://ftp.gtk.org/pub/gtk/v1.2/](ftp://ftp.gtk.org/pub/gtk/v1.2/)

在将取得的档案解压缩或是由CVS中check out出来之後，切换到该目录下，开始进行安装(打指令罗~)：

取得CVS版本，执行  
cvs -d server:cvsread@cvs.php.net:/repository co php-gtk  
或下载最新版本  
[http://gtk.php.net/download.php](http://gtk.php.net/download.php)

1\. ./buildconf  
2\. ./configure (想要加装extensions的话请输任./configure --help看说明)  
3\. make(如果看到"Could not write┅"，只是代表该GTK+ object还没被支援，不算是什么错误讯息)  
4\. make install

执行看看test/资料夹中的范例scripts来测试，特别是gtk.php，这些都是展示如何使用的好例子。

4\. 第一支程式

4.1 前言  
本章会教导各位一些常用的GtkClass(widget)，还有运用这些来做出你的第一支PHP-GTK程式，如果概念那章不是很熟的话，这章可以给你一个练习的机会喔!  
如果对本章的内容有不懂或是想要深入了解其他的widget，可以到[http://gtk.php.net/manual/en/](http://gtk.php.net/manual/en/)  
看手册，手册里面有不少范例程式。

4.2 会用到的widgets  
在开始写程式之前，先来对等一下会用到的widget class们做一个overview。

GtkWindow()  
GtkWindow()建立一个视窗，里面有很多方法可以使用，如：set\_title,set\_name,  
connect,set\_border\_width等┅。

GtkFrame()  
GtkFrame()纯粹建立一个好Border，你可以设定它的label name,alignment,  
shadow(用英文，读Manual的时候会比较方便)。

GtkVBox()  
GtkVBox()建立一个直立的container来放入widgets。

GtkLabel()  
GtkLabel()可以建立一个label，内容文字可以建立时设定也可以建立後用方法来设定，如果没有设定内容文字，将会建立一个空的label(这是废话吗┅?)。

GtkHSeparator()  
GtkHseparator()建立一个水平线。

GtkEntry()  
GtkEntry()建立一个textbox供使用者输入资讯。

GtkHButtonBox()  
GtkHButtonBox()建立一个以水平方式排列Button的container。

GktBtton()  
GtkButton()或许可以说是GUI程式中最常用的widget了，它建立一个可以让使用者按的按钮。

4.3 开始

If(!class_exist("gtk"))  
{  
dl("php\_gtk.".(strstr(PHP\_OS,"WIN") ? "dll" : "so"));  
}

  
这段程式码会判断PHP-GTK延伸模组是否已启动，如果没有，它就会读取适当的档案。在上面的范例中，是靠判断执行的作业系统是Windows还是其它来判断要载入[php\_gtk.dll还是php\_gtk.so](http://php_gtk.xn--dllphp_gtk-j07uf299a.so)。

  
Function delete_event()  
{  
return false;  
}

  
这里建立了一个名为delete_event的function，这个function是等会儿delete-event  
signal发出时的callback function。内容传回false会告诉PHP-GTK用预设的signal  
handler来处理，而预设的handler会关闭视窗(同时会呼叫该视窗的destroy()  
函式)，在这里，它会关闭程式(因为这个范例程式只有一个主视窗，一旦关闭就会关闭程式)。

Function destroy()  
{  
Gtk::main_quit();  
}

  
这里建立了一个函式，destroy()。在这个程式中，这个函式是很重要的，因为我们在关闭程式的时候会连接到它。之前说过，Gtk::main\_quit()会关闭程式，如果我们在这个程式中没有定义这个function或是这个function里面没有Gtk::main\_quit()这行，那么这个程式就不会关闭了。以上一段程式码说明里提到的delete-event来说，return  
false之後预设会执行关闭视窗的动作，还会呼叫destroy()函式，如果这里没有定义或是没有Gtk::main_quit()这段的话，主视窗的确会关闭，可是程式并不会结束，因为主程式回圈aGtk::main()还在跑。

<?php  
$window = &new GtkWindow();  
//设定名字以辨别各个视窗  
$window->set_name('main window');  
//设定视窗的标题  
$window->set_title('对PHP-GTK的介绍');  
//设定视窗的大小  
$window->set_usize(160, 120);  
//呼叫destroy()函式来结束程式  
$window->connect('destroy', 'destroy');  
//呼叫delete_event()函式来关闭视窗  
$window->connect('delete-event', 'delete_event');  
//设定视窗的边框宽度  
$window->set\_border\_width(10);  
//设定视窗的位置  
$window->set\_position(GTK\_WIN\_POS\_CENTER);  
//显示视窗和所有child widget (不显示就看不到)  
//最後这两行一定要放在程式码的最後，否则什么都看不到  
$window->show_all();  
Gtk::main();  
?>

  
执行程式可以看到如下的图：

//建立一个GtkFrame  
$frame = &new GtkFrame('经过简易修改的程式');  
//把GtkFrame放到GtkWindow里  
$window->add($frame);  
//最下面两行不要动

  
结果如下图：

下面这段建立一个GtkVBox作为container，并把GtkEntry、GtkHSeperator、GtkLabel和GtkButtonBox都pack进去，所谓pack，是GtkBox底下的container们特别加入的放入widget的方法，就类似於add()，而pack用的方法一般是pack\_start()和pack\_end()，比add()好的地方是可以控制将widget增加进去之後widget的位置(不过只要是container就会有add()方法)，欲查询详细资料请至  
[http://gtk.php.net/manual/en](http://gtk.php.net/manual/en)。

  
//建立一个GtkVBox，为常用的container  
$box1 = &new GtkVBox();  
//把GtkVBox放到GtkFrame里面  
$frame->add($box1);  
//建立一个GtkLabel并将它pack到GtkVBox里  
$label = &new GtkLabel();  
$box1->pack_start($label);  
//建立一个GtkHSeparator并将它pack到GtkVBox里  
$separator = &new GtkHSeparator();  
$box1->pack_start($separator);  
//建立一个GtkEntry并将它pack到GtkVBox里  
$entry = &new GtkEntry();  
$box1->pack_start($entry);  
//建立一个GtkButtonBox并将它add到GtkVBox里  
//因为GtkButtonBox也是一个无形的container，位置不重要，所以用add()  
$box2 = &new GtkHButtonBox();  
$box1->add($box2);

执行如下图：

最後这段程式码会建立两个GtkButton并pack到GtkButtonBox里去，还有为两个按钮加上连接，使它们起作用，并建立一个函式，只要按下GtkButton就会将GtkLabel的内容换成GtkEntry中的文字。

$button = &new GtkButton('显示输入的字');  
//连接"clicked" signal到set_name()函式，附加$label和$entry两个widget  
$button->connect\_object('clicked','set\_name',$label,$entry);  
$box2->pack_start($button);  
$button = &new GtkButton('离开程式');  
//连接"clicked" signal到destroy()函式，将会关闭程式  
$button->connect('clicked','destroy');  
$box2->pack_start($button);

function set_name($label,$entry)  
{  
//用GtkEntry的get_text()方法从取得文字方块内容  
$gettext=$entry->get_text();  
//用GtkLabel的set_text()方法设定新的文字  
$label->set_text($gettext);  
}  
//最後再提一下那两行┅.  
$window->show_all();  
Gtk::main();

  
?到??，整?程式就算是完成了，?看看?行的?果吧~

  
5\. 其它

5.1 进一步学习  
如果在结束了上面的课程之后你还想要更了解PHP-GTK，或是对于本文的内容有任何  
不明白的地方，这里提供你几个地方可以查询资料：

PHP-GTK官方网站(En)： [http://gtk.php.net](http://gtk.php.net)  
GTK官方网站(En)： [http://www.gtk.org](http://www.gtk.org)  
PHP-GTK官方网站上的Manual(En)： [http://gtk.php.net/manual/en](http://gtk.php.net/manual/en)  
TIM官方网站(zh-Tw)： [http://tim.jerry.com.tw](http://tim.jerry.com.tw)

5.2 另一个范例  
这里有一个笔者写的猜数字游戏，算是比较进阶的范例，可以抓回去研究看看。  
[http://pc035860.infor.org/download/GuessNumber.zip](http://pc035860.infor.org/download/GuessNumber.zip)

5.3 参考数据  
本文主要是参考PHP-GTK官方Manual和Zend网站上的Tutorial而编撰成的：  
[http://gtk.php.net/manual/en](http://gtk.php.net/manual/en)  
[http://www.zend.com/zend/tut/tutorial-silva.php](http://www.zend.com/zend/tut/tutorial-silva.php)  
5.4 关于作者  
无敌铁金刚(自称)，目前(2002/08/18)是台北市立建国中学一升二年级的学生，在  
学校参加了信息社，这篇文章就是放在社刊上的。

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-4495803211150079018?l=www.humen1.net)
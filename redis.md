# Linux  



目录结构  
![](http://oxfjt5cth.bkt.clouddn.com/redis-1.png)  

- 目录的操作命令（增删改查）

cd usr切换到该目录下usr目录  
cd ../切换到上一层目录  
cd /切换到系统根目录  
cd ~切换到用户主目录  
cd -切换到上一个所在目录  

(1)增加目录操作  
命令：mkdir 目录名称  

(2)查看目录  
命令：ls [-al] 父目录  
a表示显示所有包括隐藏  
l表示显示详细信息  
注意：ls -l 可以缩写成ll  

(3)寻找目录  
命令：find 目录 参数  
示例：find /root -name ‘test*’  

(4)修改目录的名称  
命令：mv 目录名称 新目录名称  
示例：test目录下有一个oldTest目录，使用mv oldTest newTest命令修改  

(5)移动目录的位置---剪切  
命令：mv 目录名称 目录的新位置  
示例：在test下将newTest目录剪切到 /usr下面，使用mv newTest /usr  

(6)拷贝目录  
命令：cp -r 目录名称 目录拷贝的目标位置 -----r代表递归拷贝(拷文件夹要拷下面的文件)
示例：将/usr下的newTest拷贝到根目录下的test中，使用cp -r /usr/newTest /test  

(7)删除目录  
命令：rm [-rf] 目录(f表示强制不会询问是否删除子文件)  
示例：删除/test下的newTest而不需要询问强制删除，在/test下使用rm -rf newTest  


- 文件的操作命令（增删改查）  

(1)文件的创建（增）  
命令：touch 文件名称  

(2)文件的查看（查）  
命令：cat/more/less/tail 文件  

示例：使用cat查看/etc/sudo.conf文件，只能显示最后一屏内容  

示例：使用more查看/etc/sudo.conf文件  
可以显示百分比，回车可以向下一行，空格可以向下一页，q可以退出查看  

示例：使用less查看/etc/sudo.conf文件  
可以使用键盘上的PgUp和PgDn向上和向下翻页，q结束查看  

示例：使用tail -10 查看/etc/sudo.conf文件的后10行，Ctrl+C结束  


注意：命令 tail -f 文件可以对某个文件进行动态监控，例如tomcat的日志文件  
会随着程序的运行，日志会变化，可以使用tail -f catalina-2016-11-11.log监控文件的变化  


(3)修改文件的内容（改）  
命令：vim 文件  
示例：编辑/test下的aaa.txt文件，使用vim aaa.txt  
但此时并不能编辑，因为此时处于命令模式，点击键盘i/a/o进入编辑模式，可以编辑文件  
编辑完成后，按下Esc，退回命令模式  
此时文件虽然已经编辑完成，但是没有保存，需输入冒号：进入底行模式  
在底行模式下输入wq代表写入内容并退出，即保存；输入q!代表强制退出不保存。  


(4)删除文件（删）  
同目录删除：熟记 rm -rf 文件 即可  

- 压缩文件的操作命令  

(1)打包并压缩文件  
Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。  
而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。  
命令：tar -zcvf 打包压缩后的文件名 要打包压缩的文件  
其中：
  z：调用gzip压缩命令进行压缩  
  c：打包文件  
  v：显示运行过程  
  f：指定文件名  
示例：打包并压缩/test下的所有文件 压缩后的压缩包指定名称为xxx.tar.gz  
tar -zcvf xxx.tar.gz aaa.txt bbb.txt ccc.txt  
或：tar -zcvf xxx.tar.gz /test/*  

(2)解压压缩包（重点）  
命令：tar [-xvf] 压缩文件  
其中：x：代表解压  
示例：将/test下的xxx.tar.gz解压到当前目录下  
tar -xvf xxx.tar.gz  

示例：将/test下的xxx.tar.gz解压到根目录/usr下  
tar -xvf xxx.tar.gz -C /usr------C代表指定解压的位置  

- 其他命令  
(1)显示当前所在位置  
pwd  

(2)搜索命令  
命令：grep 要搜索的字符串 要搜索的文件  
示例：搜索/usr/sudu.conf文件中包含字符串to的行  
grep to sudo.conf  
示例：搜索/usr/sudu.conf文件中包含字符串to的行 to要高亮显示  
grep to sudo.conf --color

(3)管道命令  
命令：|   将前一个命令的输出作为本次目录的输入  
示例：查看当前系统中所有的进程中包括system字符串的进程  
ps -ef | grep system  

(4)查看进程  
命令：ps -ef  
示例：查看当前系统中运行的进程  

(5)杀死进程  
命令：kill -9 进程的pid  

(6)网络通信命令  
查看当前系统的网卡信息：ifconfig  
查看与某台机器的连接情况：ping  
查看当前系统的端口使用：netstat -an  


- Linux的权限命令  
权限是Linux中的重要概念，每个文件/目录等都具有权限  
通过ls -l命令我们可以	查看某个目录下的文件或目录的权限  
示例：在随意某个目录下ls -l  

文件的类型：  
d：代表目录  
-：代表文件  
l：代表链接（可以认为是window中的快捷方式）  
后面的9位分为3组，每3位置一组，分别代表属主的权限，与当前用户同组的，用户的权限，其他用户的权限  
r：代表权限是可读，r也可以用数字4表示  
w：代表权限是可写，w也可以用数字2表示  
x：代表权限是可执行，x也可以用数字1表示  

修改文件/目录的权限的命令：chmod  
示例：修改/test下的aaa.txt的权限为属主有全部权限，属主所在的组有读写权限，  
其他用户只有读的权限  
chmod u=rwx,g=rw,o=r aaa.txt  
上述示例还可以使用数字表示：  
chmod 764 aaa.txt  

查看网卡配置，使用vim命令配置  
cat /etc/sysconfig/network-scripts/ifcfg-eth0  


- 安装mysql  

1）查看CentOS自带的mysql  
输入 rpm -qa | grep mysql  

2）将自带的mysql卸载  
rpm -e --nodeps mysql-libs-5.1.66-2.el6_3.i686  

3）上传Mysql到linux  

4）安装mysql的依赖（选做）  
yum -y install libaio.so.1 libgcc_s.so.1 libstdc++.so.6  
yum  update libstdc++-4.4.7-4.el6.x86_64  

5）解压Mysql到/usr/local/下的mysql目录(mysql目录需要手动创建)内  
cd /usr/local   
mkdir mysql  
tar -xvf MySQL-5.6.22-1.el6.i686.rpm-bundle.tar -C /usr/local/mysql  


6）在/usr/local/mysql下安装mysql  
安装服务器端：rpm -ivh MySQL-server-5.6.22-1.el6.i686.rpm  
安装客户端：rpm -ivh MySQL-client-5.6.22-1.el6.i686.rpm  

7）启动mysql(这种每次都要手动启动)  
service mysql start  

8）将mysql加到系统服务中并设置开机启动  
加入到系统服务：chkconfig --add mysql  
自动启动：chkconfig mysql on  

9）登录mysql  
mysql安装好后会生成一个临时随机密码，存储位置在/root/.mysql_secret  
msyql –u root -p命令登入mysql  

10）修改mysql的密码  
set password = password('root');  

11）开启mysql的远程登录  
默认情况下mysql为安全起见，不支持远程登录mysql，所以需要设置开启	远程登录mysql的权限  
登录mysql后输入如下命令：  

```
grant all privileges on *.* to 'root' @'%' identified by 'root';
flush privileges;
```

12）开放Linux的对外访问的端口3306  
/sbin/iptables -I INPUT -p tcp --dport 3306 -j ACCEPT  
/etc/rc.d/init.d/iptables save ---将修改永久保存到防火墙中  

- Tomcat安装  
步骤：  
1）上传Tomcat到linux上  
2）解压Tomcat到/usr/local下  
3）开放Linux的对外访问的端口8080  
/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT  
/etc/rc.d/init.d/iptables save  
4）启动关闭Tomcat  
进入tomcat的bin下启动：./startup.sh  
进入tomcat的bin下关闭：./shutdown.sh  

# vim命令  

- 命令历史  
以:和/开头的命令都有历史纪录，可以首先键入:或/然后按上下箭头来选择某个历史命令。  

- 启动vim  
在命令行窗口中输入以下命令即可  
vim 直接启动vim  
vim filename 打开vim并创建名为filename的文件  

- 文件命令  
打开单个文件  
vim file  
同时打开多个文件  
vim file1 file2 file3 ...  
在vim窗口中打开一个新文件  
:open file  
在新窗口中打开文件  
:split file  
切换到下一个文件  
:bn  
切换到上一个文件  
:bp  
查看当前打开的文件列表，当前正在编辑的文件会用[]括起来。  
:args  
打开远程文件，比如ftp或者share folder  
:e ftp://192.168.10.76/abc.txt  
:e \\qadrive\test\1.txt  

- vim的模式  
正常模式（按Esc或Ctrl+[进入） 左下角显示文件名或为空  
插入模式（按i键进入） 左下角显示--INSERT--  
可视模式（不知道如何进入） 左下角显示--VISUAL--  

- 导航命令  
% 括号匹配  

- 插入命令  
i 在当前位置生前插入  
I 在当前行首插入  
a 在当前位置后插入  
A 在当前行尾插入  
o 在当前行之后插入一行  
O 在当前行之前插入一行  

- 查找命令  
/text　　查找text，按n健查找下一个，按N健查找前一个。  
?text　　查找text，反向查找，按n健查找下一个，按N健查找前一个。  
vim中有一些特殊字符在查找时需要转义　　.*[]^%/?~$  
:set ignorecase　　忽略大小写的查找  
:set noignorecase　　不忽略大小写的查找  
查找很长的词，如果一个词很长，键入麻烦，可以将光标移动到该词上  
按*或#键即可以该单词进行搜索，相当于/搜索。而#命令相当于?搜索。  
:set hlsearch　　高亮搜索结果，所有结果都高亮显示，而不是只显示一个匹配。  
:set nohlsearch　　关闭高亮搜索显示  
:nohlsearch　　关闭当前的高亮显示，如果再次搜索或者按下n或N键，则会再次高亮。  
:set incsearch　　逐步搜索模式，对当前键入的字符进行搜索而不必等待键入完成。  
:set wrapscan　　重新搜索，在搜索到文件头或尾时，返回继续搜索，默认开启。  

- 替换命令  
ra 将当前字符替换为a，当期字符即光标所在字符。  
s/old/new/ 用old替换new，替换当前行的第一个匹配  
s/old/new/g 用old替换new，替换当前行的所有匹配  
%s/old/new/ 用old替换new，替换所有行的第一个匹配  
%s/old/new/g 用old替换new，替换整个文件的所有匹配  
:10,20 s/^/    /g 在第10行知第20行每行前面加四个空格，用于缩进。  
ddp 交换光标所在行和其下紧邻的一行。  

- 移动命令  
h 左移一个字符  
l 右移一个字符，这个命令很少用，一般用w代替。  
k 上移一个字符  
j 下移一个字符  
以上四个命令可以配合数字使用，比如20j就是向下移动20行，  
5h就是向左移动5个字符，在Vim中，很多命令都可以配合数字使用，  
比如删除10个字符10x，在当前位置后插入3个！，3a！<Esc>，这里的Esc是必须的，否则命令不生效。  
w 向前移动一个单词（光标停在单词首部），如果已到行尾，则转至下一行行首。此命令快，可以代替l命令。  
b 向后移动一个单词 2b 向后移动2个单词  
e，同w，只不过是光标停在单词尾部  
ge，同b，光标停在单词尾部。  
^ 移动到本行第一个非空白字符上。  
0（数字0）移动到本行第一个字符上，  
<HOME> 移动到本行第一个字符。同0健。  
$ 移动到行尾 3$ 移动到下面3行的行尾  
gg 移动到文件头。 = [[  
G（shift + g） 移动到文件尾。 = ]]  
f（find）命令也可以用于移动，fx将找到光标后第一个为x的字符，3fd将找到第三个为d的字符。  
F 同f，反向查找。  
跳到指定行，冒号+行号，回车，比如跳到240行就是 :240回车。另一个方法是行号+G，比如230G跳到230行。  
Ctrl + e 向下滚动一行  
Ctrl + y 向上滚动一行  
Ctrl + d 向下滚动半屏  
Ctrl + u 向上滚动半屏  
Ctrl + f 向下滚动一屏  
Ctrl + b 向上滚动一屏  

- 撤销和重做  
u 撤销（Undo）  
U 撤销对整行的操作  
Ctrl + r 重做（Redo），即撤销的撤销。  

- 删除命令  
x 删除当前字符  
3x 删除当前光标开始向后三个字符  
X 删除当前字符的前一个字符。X=dh  
dl 删除当前字符， dl=x  
dh 删除前一个字符  
dd 删除当前行  
dj 删除上一行  
dk 删除下一行  
10d 删除当前行开始的10行。  
D 删除当前字符至行尾。D=d$  
d$ 删除当前字符之后的所有字符（本行）  
kdgg 删除当前行之前所有行（不包括当前行）  
jdG（jd shift + g）   删除当前行之后所有行（不包括当前行）   
:1,10d 删除1-10行  
:11,$d 删除11行及以后所有的行  
:1,$d 删除所有行  
J(shift + j)　　删除两行之间的空行，实际上是合并两行。  

- 拷贝和粘贴  
yy 拷贝当前行   
nyy 拷贝当前后开始的n行，比如2yy拷贝当前行及其下一行。  
p  在当前光标后粘贴,如果之前使用了yy命令来复制一行，那么就在当前行的下一行粘贴。  
shift+p 在当前行前粘贴  
:1,10 co 20 将1-10行插入到第20行之后。  
:1,$ co $ 将整个文件复制一份并添加到文件尾部。  
正常模式下按v（逐字）或V（逐行）进入可视模式，然后用jklh命令移动即可选择某些行或字符，再按y即可复制  
ddp交换当前行和其下一行  
xp交换当前字符和其后一个字符  

- 剪切命令  
正常模式下按v（逐字）或V（逐行）进入可视模式，然后用jklh命令移动即可选择某些行或字符，再按d即可剪切  
ndd 剪切当前行之后的n行。利用p命令可以对剪切的内容进行粘贴  
:1,10d 将1-10行剪切。利用p命令可将剪切后的内容进行粘贴。  
:1, 10 m 20 将第1-10行移动到第20行之后。  

- 退出命令  
:wq 保存并退出  
ZZ 保存并退出  
:q! 强制退出并忽略所有更改  
:e! 放弃所有修改，并打开原来文件。  

- 窗口命令  
:split或new 打开一个新窗口，光标停在顶层的窗口上  
:split file或:new file 用新窗口打开文件  
split打开的窗口都是横向的，使用vsplit可以纵向打开窗口。  
Ctrl+ww 移动到下一个窗口  
Ctrl+wj 移动到下方的窗口  
Ctrl+wk 移动到上方的窗口  
关闭窗口  
:close 最后一个窗口不能使用此命令，可以防止意外退出vim。  
:q 如果是最后一个被关闭的窗口，那么将退出vim。  
ZZ 保存并退出。  
关闭所有窗口，只保留当前窗口  
:only  
录制宏  
按q键加任意字母开始录制，再按q键结束录制（这意味着vim中的宏不可嵌套），  
使用的时候@加宏名，比如qa。。。q录制名为a的宏，@a使用这个宏。  

- 执行shell命令  
:!command
:!ls 列出当前目录下文件  
:!perl -c script.pl 检查perl脚本语法，可以不用退出vim，非常方便。  
:!perl script.pl 执行perl脚本，可以不用退出vim，非常方便。  
:suspend或Ctrl - Z 挂起vim，回到shell，按fg可以返回vim。  

- 注释命令  
perl程序中#开始的行为注释，所以要注释某些行，只需在行首加入#  
3,5 s/^/#/g 注释第3-5行  
3,5 s/^#//g 解除3-5行的注释  
1,$ s/^/#/g 注释整个文档。  
:%s/^/#/g 注释整个文档，此法更快。  

- 帮助命令  
:help or F1 显示整个帮助  
:help xxx 显示xxx的帮助，比如 :help i, :help CTRL-[（即Ctrl+[的帮助）。  
:help 'number' Vim选项的帮助用单引号括起  
:help <Esc> 特殊键的帮助用<>扩起  
:help -t Vim启动参数的帮助用-  
：help i_<Esc> 插入模式下Esc的帮助，某个模式下的帮助用模式 主题的模式  
帮助文件中位于||之间的内容是超链接，可以用Ctrl+]进入链接，Ctrl+o（Ctrl + t）返回  



# redis  

- redis的应用场景  
缓存（数据查询、短连接、新闻内容、商品内容等等）（最多使用）  
分布式集群架构中的session分离。  
聊天室的在线好友列表。  
任务队列。（秒杀、抢购、12306等等）  
应用排行榜。  
网站访问统计。  
数据过期处理（可以精确到毫秒）  


- redis在Linux上的安装  
1）安装redis编译的c环境，yum install gcc-c++  
2）将redis-2.6.16.tar.gz上传到Linux系统中  
3）解压到/usr/local下  tar -xvf redis-2.6.16.tar.gz -C /usr/local  
4）进入redis-2.6.16目录 使用make命令编译redis  
5）在redis-2.6.16目录中 使用make PREFIX=/usr/local/redis install命令安装redis到/usr/local/redis中  
6）拷贝redis-2.6.16中的redis.conf到安装目录redis中  
7）启动redis 在bin下执行命令redis-server redis.conf  
8）如需远程连接redis，需配置redis端口6379在linux防火墙中开发  
/sbin/iptables -I INPUT -p tcp --dport 6379 -j ACCEPT  
/etc/rc.d/init.d/iptables save  

- 前后端启动  
前端启动的关闭：  
	强制关闭：Ctrl+c  
	正常关闭：[root@itheima bin]# ./redis-cli shutdown  
前端启动的问题：  
	一旦客户端关闭，则redis服务也停掉。  


- 后端启动的配置和关闭    
第一步：需要将redis解压之后的源码包中的redis.conf文件拷贝到bin目录下  
[root@itheima bin]# cp /root/redis-3.0.0/redis.conf ./  
第二步：修改redis.conf文件，将daemonize改为yes  
先要使用vim redis.conf  
第三步：使用命令后端启动redis  
[root@itheima bin]# ./redis-server redis.conf  
第四步：查看是否启动成功  

关闭后端启动的方式：    
强制关闭：[root@itheima bin]# kill -9 5071  
正常关闭：[root@itheima bin]# ./redis-cli shutdown  

在项目中，建议使用正常关闭。  
因为redis作为缓存来使用的话，将数据存储到内存中，如果使用正常关闭，则会将内存数据持久化到本地之后，再关闭。  
如果是强制关闭，则不会进行持久化操作，可能会造成部分数据的丢失。  




- jedis  

导包  
jedis-2.7.0.jar  
commons-pool2-2.3.jar  


- 连接池的使用  

```java
package com.ithiema.jedis;

import org.junit.Test;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig;

public class JedisTest {

	//通过java程序访问redis数据库

	@Test
	//获得单一的jedis对象操作数据库
	public void test1(){
		
		//1、获得连接对象
		Jedis jedis = new Jedis("192.168.213.128", 6379);
		
		//2、获得数据
		String username = jedis.get("username");
		System.out.println(username);
		
		//3、存储
		jedis.set("addr", "北京");
		System.out.println(jedis.get("addr"));

		
	}
	
	
	//通过jedis的pool获得jedis连接对象
	@Test
	public void test2(){
		//0、创建池子的配置对象
		JedisPoolConfig poolConfig = new JedisPoolConfig();
		poolConfig.setMaxIdle(30);//最大闲置个数
		poolConfig.setMinIdle(10);//最小闲置个数
		poolConfig.setMaxTotal(50);//最大连接数
		
		//1、创建一个redis的连接池
		JedisPool pool = new JedisPool(poolConfig, "192.168.186.131", 6379);
		
		//2、从池子中获取redis的连接资源
		Jedis jedis = pool.getResource();
		
		//3、操作数据库
		jedis.set("xxx","yyyy");
		System.out.println(jedis.get("xxx"));
		
		//4、关闭资源
		jedis.close();
		pool.close();
		
	}
}
```

工具类和配置文件  

```java
package com.ithiema.jedis;

import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig;

public class JedisPoolUtils {
	
	private static JedisPool pool = null;
	
	static{
		
		//加载配置文件
		InputStream in = JedisPoolUtils.class.getClassLoader().getResourceAsStream("redis.properties");
		Properties pro = new Properties();
		try {
			pro.load(in);
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		//获得池子对象
		JedisPoolConfig poolConfig = new JedisPoolConfig();
		poolConfig.setMaxIdle(Integer.parseInt(pro.get("redis.maxIdle").toString()));//最大闲置个数
		poolConfig.setMinIdle(Integer.parseInt(pro.get("redis.minIdle").toString()));//最小闲置个数
		poolConfig.setMaxTotal(Integer.parseInt(pro.get("redis.maxTotal").toString()));//最大连接数
		pool = new JedisPool(poolConfig,pro.getProperty("redis.url") , Integer.parseInt(pro.get("redis.port").toString()));
	}

	//获得jedis资源的方法
	public static Jedis getJedis(){
		return pool.getResource();
	}
	
	public static void main(String[] args) {
		Jedis jedis = getJedis();
		System.out.println(jedis.get("xxx"));
	}
	
}

```



- 图形界面管理工具  

不指定默认存到第0号数据库  
![](http://oxfjt5cth.bkt.clouddn.com/redis-2.png)  

选择数据库的方式：  
使用select 加上数据库的下标 就可以选择指定的数据库来使用，下标从0开始  
select 15  


String数据类型..................................................................................  
- 
赋值  
语法：SET key value  
set test 123  
OK  

取值  
语法：GET key  
get test  
"123“

取值并赋值  
语法：GETSET key value  
getset s2 222  
"111"  
get s2  
"222"  


设置/获取多个键值  
语法：  
MSET key value [key value …]  
MGET key [key …]  
mset k1 v1 k2 v2 k3 v3  
OK  
get k1  
"v1"  
mget k1 k3  
1) "v1"  
2) "v3"  

删除  
语法：DEL key  
del test  
(integer) 1  

数值增减
递增数字 
当存储的字符串是整数时，Redis提供了一个实用的命令INCR，其作用是让当前键值递增，并返回递增后的值。  

语法：INCR key  
incr num  
(integer) 1  
incr num  
(integer) 2  
incr num  
(integer) 3  

增加指定的整数  
语法：INCRBY key increment  
incrby num 2  
(integer) 5  
incrby num 2  
(integer) 7  
incrby num 2  
(integer) 9  

递减数值  
语法：DECR key  
decr num  
(integer) 9  
decr num  
(integer) 8  

减少指定的整数  
语法：DECRBY key decrement  
decr num  
(integer) 6  
decr num  
(integer) 5  
decrby num 3  
(integer) 2  
decrby num 3  
(integer) -1  

向尾部追加值  
APPEND的作用是向键值的末尾追加value。如果键不存在则将该键的值设置为value，  
即相当于 SET keyvalue。返回值是追加后字符串的总长度。   
语法：APPEND key value  
set str hello  
OK  
append str " world!"  
(integer) 12  
get str  
"hello world!"  


获取字符串长度  
STRLEN命令返回键值的长度，如果键不存在则返回0。  
语法：STRLEN key  
strlen str 
(integer) 0  
set str hello  
OK  
strlen str  
(integer) 5  


应用-----自增主键
商品编号、订单号采用string的递增数字特性生成。  
定义商品编号key：items:id  
INCR items:id  
(integer) 2  
INCR items:id  
(integer) 3  

Hash散列类型..................................................................................  
- 
类似于对象，key是对象名  
redis hash介绍  
hash叫散列类型，它提供了字段和字段值的映射。字段值只能是字符串类型，不支持散列类型、集合类型等其它类型。 

![](http://oxfjt5cth.bkt.clouddn.com/redis-3.png)  
 

命令  
赋值  
HSET命令不区分插入和更新操作，当执行插入操作时HSET命令返回1，当执行更新操作时返回0。  
一次只能设置一个字段值  
语法：HSET key field value	
hset user username zhangsan  
(integer) 1  

一次可以设置多个字段值  
语法：HMSET key field value [field value ...]  
hmset user age 20 username lisi  
OK  

当字段不存在时赋值，类似HSET，区别在于如果字段存在，该命令不执行任何操作  
语法：HSETNX key field value  
hsetnx user age 30	如果user中没有age字段则设置age值为30，否则不做任何操作  
(integer) 0  

取值  
一次只能获取一个字段值  
语法：HGET key field  
hget user username  
"zhangsan“  

一次可以获取多个字段值  
语法：HMGET key field [field ...]  
hmget user age username  
1) "20"  
2) "lisi"  

获取所有字段值  
语法：HGETALL key  
hgetall user  
1) "age"  
2) "20"  
3) "username"  
4) "lisi"  


删除字段  
可以删除一个或多个字段，返回值是被删除的字段个数  
语法：HDEL key field [field ...]  
hdel user age  
(integer) 1  
hdel user age name  
(integer) 0  
hdel user age username  
(integer) 1  


增加数字   
语法：HINCRBY key field increment  
hincrby user age 2	将用户的年龄加2  
(integer) 22  
hget user age		获取用户的年龄  
"22“  


其它命令(自学)   
判断字段是否存在  
语法：HEXISTS key field  
hexists user age	查看user中是否有age字段  
(integer) 1  
hexists user name	查看user中是否有name字段  
(integer) 0  



只获取字段名或字段值  
语法：  
HKEYS key  
HVALS key  
hmset user age 20 name lisi  
OK  
hkeys user  
1) "age"  
2) "name"  
hvals user  
1) "20"  
2) "lisi"  


获取字段数量  
语法：HLEN key  
hlen user  
(integer) 2  


list数据类型 ..................................................................................
-

Arraylist和linkedlist的区别  
Arraylist是使用数组来存储数据，特点：查询快、增删慢  
Linkedlist是使用双向链表存储数据，特点：增删快、查询慢，但是查询链表两端的数据也很快。  

Redis的list是采用来链表来存储的，所以对于redis的list数据类型的操作，是操作list的两端数据来操作的。  


命令  
向列表两端增加元素  
向列表左边增加元素  
语法：LPUSH key value [value ...]  
lpush list:1 1 2 3  
(integer) 3  

向列表右边增加元素  
语法：RPUSH key value [value ...]  
rpush list:1 4 5 6  
(integer) 3  

查看列表  
LRANGE命令是列表类型最常用的命令之一，获取列表中的某一片段，  
将返回start、stop之间的所有元素（包含两端的元素），索引从0开始。  
索引可以是负数，如：“-1”代表最后边的一个元素。  
语法：LRANGE key start stop  
lrange list:1 0 2(list:1是指该链表名称)  
1) "2"  
2) "1"  
3) "4"  
lrange list1 0 -1会输出所有  

从列表两端弹出元素  
LPOP命令从列表左边弹出一个元素，会分两步完成：  
第一步是将列表左边的元素从列表中移除  
第二步是返回被移除的元素值。  
语法：  
LPOP key  
RPOP key  
lpop list:1  
"3"  
rpop list:1  
"6"  

获取列表中元素的个数  
语法：LLEN key  
llen list:1  
(integer) 2  

其它命令(自学)  
删除列表中指定的值  
LREM命令会删除列表中前count个值为value的元素，返回实际删除的元素个数。  
根据count值的不同，该命令的执行方式会有所不同：   
当count>0时， LREM会从列表左边开始删除。   
当count<0时， LREM会从列表后边开始删除。   
当count=0时， LREM删除所有值为value的元素。   
语法：LREM key count value  

获得/设置指定索引的元素值   
获得指定索引的元素值  
语法：LINDEX key index  
lindex l:list 2  
"1"  

设置指定索引的元素值  
语法：LSET key index value  
lset l:list 2 2  
OK  
lrange l:list 0 -1  
1) "6"  
2) "5"  
3) "2"  
4) "2"  

只保留列表指定片段  
指定范围和LRANGE一致  
语法：LTRIM key start stop  
lrange l:list 0 -1  
1) "6"  
2) "5"  
3) "0"  
4) "2"  
ltrim l:list 0 2  
OK  
lrange l:list 0 -1  
1) "6"  
2) "5"  
3) "0"  


向列表中插入元素 
该命令首先会在列表中从左到右查找值为pivot的元素，  
然后根据第二个参数是BEFORE还是AFTER来决定将value插入到该元素的前面还是后面。   
语法：LINSERT key BEFORE|AFTER pivot value  
lrange list 0 -1  
1) "3"  
2) "2"  
3) "1"  
linsert list after 3 4  
(integer) 4  
lrange list 0 -1  
1) "3"  
2) "4"  
3) "2"  
4) "1"  

将元素从一个列表转移到另一个列表中  
语法：RPOPLPUSH source destination  
rpoplpush list newlist   
"1"  
lrange newlist 0 -1  
1) "1"  
lrange list 0 -1  
1) "3"  
2) "4"  
3) "2"  

应用  
商品评论列表  
思路：  
在Redis中创建商品评论列表  
用户发布商品评论，将评论信息转成json存储到list中。  
用户在页面查询评论列表，从redis中取出json数据展示到页面。  

定义商品评论列表key：  
商品编号为1001的商品评论key【items: comment:1001】  
LPUSH items:comment:1001 '{"id":1,"name":"商品不错，很好！！","date":1430295077289}'  


set数据类型 ..................................................................................
-

Set集合类型  
集合类型：无序、不可重复  
列表类型：有序、可重复  

命令  
增加/删除元素  
语法：SADD key member [member ...]  
sadd set a b c  
(integer) 3  
sadd set a  
(integer) 0  
语法：SREM key member [member ...]  
srem set c d  
(integer) 1  


获得集合中的所有元素   
语法：SMEMBERS key  
smembers set  
1) "b"  
2) "a”  

判断元素是否在集合中  
语法：SISMEMBER key member  
sismember set a  
(integer) 1  
sismember set h  
(integer) 0  

运算命令  
集合的差集运算 A-B  
属于A并且不属于B的元素构成的集合。  
语法：SDIFF key [key ...]  
sadd setA 1 2 3  
(integer) 3  
sadd setB 2 3 4  
(integer) 3  
sdiff setA setB   
1) "1"  
sdiff setB setA  
1) "4"  

集合的交集运算 A ∩ B  
属于A且属于B的元素构成的集合。   
语法：SINTER key [key ...]  
sinter setA setB  
1) "2"  
2) "3"  

集合的并集运算 A ∪ B  
属于A或者属于B的元素构成的集合  
 

语法：SUNION key [key ...]  
sunion setA setB  
1) "1"  
2) "2"  
3) "3"  
4) "4"  

其它命令(自学)  
获得集合中元素的个数   
语法：SCARD key  
smembers setA   
1) "1"  
2) "2"  
3) "3"   
scard setA  
(integer) 3  

从集合中弹出一个元素  
注意：由于集合是无序的，所有SPOP命令会从集合中随机选择一个元素弹出  
语法：SPOP key  
spop setA  
"1“  

sortedset数据类型 ..................................................................................
-


Sortedset是有序集合，可排序的，但是唯一。  

Sortedset和set的不同之处，是会给set中的元素添加一个分数，然后通过这个分数进行排序。  

命令  
增加元素  
向有序集合中加入一个元素和该元素的分数，  
如果该元素已经存在则会用新的分数替换原有的分数。  
返回值是新加入到集合中的元素个数，不包含之前已经存在的元素。  
语法：ZADD key score member [score member ...]  
zadd scoreboard 80 zhangsan 89 lisi 94 wangwu  
(integer) 3  
zadd scoreboard 97 lisi  
(integer) 0  

获取元素的分数  
语法：ZSCORE key member  
zscore scoreboard lisi  
"97"  

删除元素  
移除有序集key中的一个或多个成员，不存在的成员将被忽略。  
当key存在但不是有序集类型时，返回一个错误。  
语法：ZREM key member [member ...]  
zrem scoreboard lisi  
(integer) 1  


获得排名在某个范围的元素列表  
获得排名在某个范围的元素列表  
按照元素分数从小到大的顺序返回索引从start到stop之间的所有元素（包含两端的元素） 

语法：ZRANGE key start stop [WITHSCORES]	  
zrange scoreboard 0 2  
1) "zhangsan"  
2) "wangwu"  
3) "lisi"  

按照元素分数从大到小的顺序返回索引从start到stop之间的所有元素（包含两端的元素）  
语法：ZREVRANGE key start stop [WITHSCORES]  
zrevrange scoreboard 0 2  
1) " lisi "  
2) "wangwu"  
3) " zhangsan"  

如果需要获得元素的分数的可以在命令尾部加上WITHSCORES参数  
zrange scoreboard 0 1 WITHSCORES  
1) "zhangsan"   
2) "80"  
3) "wangwu"  
4) "94"  

获取元素的排名  
从小到大  
语法：ZRANK key member  
ZRANK scoreboard lisi  
(integer) 0  

从大到小  
语法：ZREVRANK key member  
ZREVRANK scoreboard zhangsan   
(integer) 1  

其它命令(自学)  
获得指定分数范围的元素  
语法：`ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count] `   
ZRANGEBYSCORE scoreboard 90 97 WITHSCORES  
1) "wangwu"  
2) "94"  
3) "lisi"   
4) "97"  
ZRANGEBYSCORE scoreboard 70 100 limit 1 2  
1) "wangwu"  
2) "lisi"  

增加某个元素的分数  
返回值是更改后的分数  
语法：ZINCRBY  key increment member  
ZINCRBY scoreboard 4 lisi  
"101“  


获得集合中元素的数量  
语法：ZCARD key  
ZCARD scoreboard  
(integer) 3  

获得指定分数范围内的元素个数  
语法：ZCOUNT key min max  
ZCOUNT scoreboard 80 90  
(integer) 1  

按照排名范围删除元素  
语法：ZREMRANGEBYRANK key start stop  
ZREMRANGEBYRANK scoreboard 0 1  
(integer) 2  
ZRANGE scoreboard 0 -1  
1) "lisi"  
按照分数范围删除元素  
语法：ZREMRANGEBYSCORE key min max  
zadd scoreboard 84 zhangsan	 
(integer) 1  
ZREMRANGEBYSCORE scoreboard 80 100 
(integer) 1  

应用  
商品销售排行榜  
需求：根据商品销售量对商品进行排行显示  
思路：定义商品销售排行榜（sorted set集合），Key为items:sellsort，分数为商品销售量。  
写入商品销售量：  
商品编号1001的销量是9，商品编号1002的销量是10  
ZADD items:sellsort 9 1001 10 1002  
商品编号1001的销量加1  
ZINCRBY items:sellsort 1 1001  
商品销量前10名：  
ZRANGE items:sellsort 0 9 withscores  

keys命令 ..................................................................................
-

keys  
返回满足给定pattern 的所有key  
keys mylist*  
1) "mylist"   
2) "mylist5"  
3) "mylist6"  
4) "mylist7"  
5) "mylist8"  


exists   
确认一个key 是否存在  
示例：从结果来看，数据库中不存在HongWan 这个key，但是age 这个key 是存在的  
exists HongWan  
(integer) 0  
exists age  
(integer) 1  


del  
删除一个key  
del age  
(integer) 1  
exists age  
(integer) 0  

rename  
重命名key  
示例：age 成功的被我们改名为age_new 了  
keys *  
1) "age"  
rename age age_new  
OK  
keys *  
1) "age_new"  


type  
返回值的类型  
示例：这个方法可以非常简单的判断出值的类型  
type addr  
string  
type myzset2  
zset  
type mylist  
list  


设置key的生存时间  
Redis在实际使用过程中更多的用作缓存，    
然而缓存的数据一般都是需要设置生存时间的，即：到期后数据销毁。   

EXPIRE key seconds			设置key的生存时间（单位：秒）key在多少秒后会自动删除  
TTL key 					查看key生于的生存时间  
PERSIST key				    清除生存时间  
PEXPIRE key milliseconds	生存时间设置单位为：毫秒  


例子：  
set test 1		设置test的值为1  
OK   
get test		获取test的值  
"1"  
EXPIRE test 5	设置test的生存时间为5秒  
(integer) 1
TTL test		查看test的生于生成时间还有1秒删除  
(integer) 1  
TTL test  
(integer) -2  
get test		获取test的值，已经删除  
(nil)  

Redis持久化方案..................................................................................
-


Rdb方式  
Redis默认的方式，redis通过快照来将数据持久化到磁盘中。  

设置持久化快照的条件  
在redis.conf中修改持久化快照的条件，如下：  
![](http://oxfjt5cth.bkt.clouddn.com/redis-4.png)  

持久化文件存储的目录  
在redis.conf中可以指定持久化文件存储的目录  
![](http://oxfjt5cth.bkt.clouddn.com/redis-5.png)  

Rdb问题  
一旦redis非法关闭，那么会丢失最后一次持久化之后的数据。  
如果数据不重要，则不必要关心。  
如果数据不能允许丢失，那么要使用aof方式。  

Aof方式  
Redis默认是不使用该方式持久化的。Aof方式的持久化，是操作一次redis数据库，则将操作的记录存储到aof持久化文件中。  

第一步：开启aof方式的持久化方案  
将redis.conf中的appendonly改为yes，即开启aof方式的持久化方案。  
![](http://oxfjt5cth.bkt.clouddn.com/redis-6.png)  
 
Aof文件存储的目录和rdb方式的一样。  

Aof文件存储的名称  
![](http://oxfjt5cth.bkt.clouddn.com/redis-7.png)  

结论  
在使用aof和rdb方式时，如果redis重启，则数据从aof文件加载。  

Redis的主从复制..................................................................................
- 

从机配置，主机无需配置  

第一步：复制出一个从机  
[root@itheima redis19]# cp bin/ bin2 –r  
第二步：修改从机的redis.conf  
语法：Slaveof masterip masterport  
slaveof 192.168.213.128 6379  
 

第三步：修改从机的port地址为6380  
在redis.conf中修改  
 

第四步：清除从机中的持久化文件  
[root@itheima bin2]# rm -rf appendonly.aof dump.rdb  

第五步：启动从机  
[root@itheima bin2]# ./redis-server redis.conf  

第六步：启动6380的客户端  
[root@itheima bin2]# ./redis-cli -p 6380  


注意：  
	主机一旦发生增删改操作，那么从机会将数据同步到从机中  
	从机不能执行写操作  
127.0.0.1:6380> set s2 222  
(error) READONLY You can't write against a read only slave.  



Redis的集群搭建..................................................................................
- 
架构细节:  
(1)所有的redis节点彼此互联(PING-PONG机制),内部使用二进制协议优化传输速度和带宽.  
(2)节点的fail是通过集群中超过半数的节点检测失效时才生效.  
(3)客户端与redis节点直连,不需要中间proxy层.客户端不需要连接集群所有节点,连接集群中任何一个可用节点即可  
(4)redis-cluster把所有的物理节点映射到[0-16383]slot上,cluster 负责维护node<->slot<->value  


Redis 集群中内置了 16384 个哈希槽，当需要在Redis集群中放置一个key-value时，  
redis先对key使用crc16算法算出一个结果然后把结果对 16384 求余数，这样每个key  
都会对应一个编号在 0-16383 之间的哈希槽，redis 会根据节点数量大致均等的将哈希  
槽映射到不同的节点  


(1)集群中所有master参与投票,如果半数以上master节点与其中一个master节点通信超过  
(cluster-node-timeout),认为该master节点挂掉.  
(2):什么时候整个集群不可用(cluster_state:fail)?   
如果集群任意master挂掉,且当前master没有slave，则集群进入fail状态。也可以理解成  
集群的[0-16383]slot映射不完全时进入fail状态。  
如果集群超过半数以上master挂掉，无论是否有slave，集群进入fail状态。  

搭建流程  

搭建集群最少也得需要3台主机，如果每台主机再配置一台从机的话，则最少需要6台机器。  
端口设计如下：7001-7006  

第一步：复制出一个7001机器  
[root@itheima redis19]# cp bin ./redis-cluster/7001 –r  
第二步：如果存在持久化文件，则删除  
[root@itheima 7001]# rm -rf appendonly.aof dump.rdb  
第三步：设置集群参数  
把conf中cluster-enable 改为yes  
第四步：修改端口  
修改conf中端口为7001  
第五步：复制出7002-7006机器  
cp 7001/ 7002 -r  
cp 7001/ 7003 -r  
cp 7001/ 7004 -r  
cp 7001/ 7005 -r  
cp 7001/ 7006 –r  
第六步：修改7002-7006机器的端口  
第七步：启动7001-7006这六台机器，start-all.sh  

```
cd 7001
./redis-server redis.conf
cd ..
cd 7002
./redis-server redis.conf
cd ..
cd 7003
./redis-server redis.conf
cd ..
cd 7004
./redis-server redis.conf
cd ..
cd 7005
./redis-server redis.conf
cd ..
cd 7006
./redis-server redis.conf
cd ..
```

第八步：修改start-all.sh文件的权限  
chmod u+x start-all.sh  
./start-all.sh  

第九步：创建集群  

```
./redis-trib.rb create --replicas 1 192.168.213.128:7001 192.168.213.128:7002 192.168.213.128:7003 192.168.213.128:7004 192.168.213.128:7005  192.168.213.128:7006
```


- 连接集群  

./redis-cli -h 192.168.242.137 -p 7001 -c  
-c：指定是集群连接  
查看集群信息  
cluster info  
查看集群节点  
cluster nodes  

```java
	public void jedisCluster() {
		// 创建jedisCluster
		Set<HostAndPort> nodes = new HashSet<>();
		nodes.add(new HostAndPort("192.168.242.137", 7001));
		nodes.add(new HostAndPort("192.168.242.137", 7002));
		nodes.add(new HostAndPort("192.168.242.137", 7003));
		nodes.add(new HostAndPort("192.168.242.137", 7004));
		nodes.add(new HostAndPort("192.168.242.137", 7005));
		nodes.add(new HostAndPort("192.168.242.137", 7006));
		nodes.add(new HostAndPort("192.168.242.137", 7007));

		JedisCluster cluster = new JedisCluster(nodes);

		cluster.set("s4", "444");

		String result = cluster.get("s4");
		System.out.println(result);

		cluster.close();
	}
```


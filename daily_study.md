## 2017-07-24

awk命令：
awk -F "\t" '{print $1}' wenda_1_1.gbk | head
iconv命令：
iconv -f utf-8 -t gb18030 wenda_1_1.utf8 > wenda_1_1.gbk
sort命令：
sort -k1,1n sim.txt.seg 

## 2017-07-24

### 1.hydoop学习：mapper/reducer

  streaming架构

#### url编码

query = urllib.unquote(query) 
query = query.decode("gbk", "ignore")

## 2017-07-27

dos2unix test_20170728_1.txt  // 将windows系统下的txt文本中的换行符转换成unix系统中的换行符
nohup ./chatbot_test.py test_20170728_1.txt output_20170728.txt wechat > log & // nohup 后台运行进程
ps aux  // 进程控制和显示
kill 。。。 // 杀死相关进程
grep 命令  // 可依据正则表达式显示相关文件

##2017-07-31
debug: baike_percent.py脚本，import chatdet时，本地运行可行，上传hadoop出错，原因是集群里没有chatdet包

reducer的原理：

print xx,xx输出时，是用空格分开的

## 2017-08-02

awk函数进阶，过滤
grep函数进阶
比较命令vimdiff, svn log
最终整理的排序结果中前一段有很多数字，需要进行过滤

## 2017-08-03

paste 粘贴两个文件（同行）
wc 查看文件字节数、行数

##2017-08-04
python中多断式的用法
dict([itm.split('="') if len(itm.split('="    ')) == 2 
else (itm, '') for itm in rank_str.replace('<rank ',     '')
.replace('"></rank>', '').split('" ')])

shell脚本中定义字符串
STR1 = "abc"(错误写法)

STR1="abc"(正确写法)
不能有空格

if \[\$STR1=\$STR2](错误写法)

if \[ \$STR1 = $STR2 ](正确写法)

awk命令 length($1)可直接获取字符串的长度

## 2017-08-07

1.grep命令 grep 'xx\|xx\|xx' 不能少了转义符，不然不能多个义项进行选择
2.python 中的in, 单个项在词典和列表是否存在可以直接用in，单个字母在字符串中的判断也可以使用，一串字符是否在另一串
  字符中使用findt

3. 中文字符用in判断时出现bug：Non-ASCII character '\xe5' in file
  解决方法在行首添加#coding=utf-8后，可以使用中文字符编码用in

## 2017-08-10

Ctrl+w 切换窗口(vim）

## 2017-08-16

pdb.set_trace()  // 单步调试
awk -F '\t' '{print $2}' bank_result.txt  | sort | uniq > bank-urls& 
uniq -c testfile // 删除出现重复的行数

## 2017-08-21

cd - // 返回上一个（非上一级）目录
AttributeError: 'Worksheet' object has no attribute 'nrows' // xlrd有该属性，xlwt没有，需要自己计算行数
搜狗放炮哥是谁 在本地测试和集群测试的结果不一致 // get_yaoting的参数query需要作为
import os // os包，用于管理本地文件及路径
os.path.abspath(__file) // 当前文件的绝对路径
os.path.dirname(abspath) // 指定绝对路径的目录地址
os.path.join(dir, '../../lib') // 根据dir和str连接得到新的地址
import sys // sys包，管理系统文件
sys.path.append(dir) // 在程序链接库中增加dir指定的库
sys.argv	// 传入参数
import xlrd
import xlwt	// 分别用于管理xls文件的读和写的工具包
wb = xlrd.open_workbook(infilename) // 打开xls文件
for sheet in wb.sheets():	// wb.sheets()为表格文件的每一个工作单
xls = xlwt.Workbook() // 打开一个用于写入的表格
table = xls.add_sheet(sheet.name) // sheet.name为sheet的名字，add_sheet在表格中加入一个工作单
table.write(index, 0, query.decode('utf-8')) // 在一个sheet中[index, 0]位置写入str
****** 代码路径：http://svn.sogou-inc.com/svn/websearch4/web/dialogue/chatbot
svn checkout|co svn全路径 本地全路径（默认当前目录） 
svn add *.php ＜－ 添加当前目录下所有的php文件
svn commit -m “添加我的测试用全部php文件“ *.php

## 2017-08-17
??? Ques: 搜狗汪仔客户端和本地测试不一致，如下列问题：

1. 鲁豫那么瘦是为什么
2. 冯小刚的第一部影片是哪部
3. 刘德华是四大天王之一么
4. 为何说莫高窟是丝绸之路上的艺术殿堂
5. 金庸写过哪些长篇武侠小说
6. 搜狗放炮哥是谁
。。。
经过多次尝试发现，当web search返回的结果为空时，即使yaoting的结果是对的，也不会返回yaoting结果。
应该是汪仔在结果判断中出现的问题。

命令学习：
svn update 更新当前目录下所有文件到最新版本
svn up 文件名  //只更新当前文件到最新版本
svn update -r 版本号 文件名 //将文件更新到指定版本

svn　delete　svn://路径(目录或文件的全路径) -m “删除备注信息文本”
推荐如下操作：
svn　delete　文件名 
svn　ci　-m　“删除备注信息文本”//进行备注说明

svn　lock　-m　“加锁备注信息文本“　[--force]　文件名 // 对文件进行上锁
svn　unlock　文件名 // 解锁

## 2017-08-17
svn命令学习
svn　diff　文件名 
svn　diff　-r　修正版本号m:修正版本号n　文件名 // 比较两个文件的差异
svn diff -r 200:201 test.php //示例

svn st // 显示目录下的文件和子目录状态

svn log 文件名 // 显示这个文件的所有修改记录，及其版本号变化

## 2017-08-18
svn命令学习
svn list svn://localhost/test  // 查看版本目录下的全部文件和子目录列表

svn mkdir -m "Making a new dir." svn://localhost/test/newdir
该命令用完后需要用 svn update 不然在该目录下提交文件会提示“提交失败”

svn　revert　[--recursive]　文件名 // 丢弃对一个文件的修改，加上参数后为对目录的操作

## 2017-09-04

lsof -i:9200 // 查看端口号

## 2017-09-07

tar -zcvf 压缩后文件名 要压缩的文件或者目录
tar -zxvf 待解压文件 -C 要解压到的目录
xlwt的超链接读写操作:
sheet.write(
​    0, 0,
​    Formula('HYPERLINK("http://www.python.org";"Python")'),
​    style)

## 2017-09-08

lambda关键字：sorted(list, key = lambda student: (-x[1], x[0]))
map(f, list) // map函数
zip() //zip函数 
注意深度学习的交叉验证训练

## 2017-09-09

每天一个linux命令：
chattr +a|i 文件名称
lsattr 文件目录 

## 2017-09-15

libboost安装问题：
在运行skill-platform中的platform_server.py时，一直提示：
找不到libboost_python3.so.1.64.0，因此，从源代码编译boost_python。
1.下载boost_1_64_0.tar.gz
2.解压文件
3.进入boost_1_64_0
4.终端输入:./configure --with-python=python3 // 之前这一步没加，要用python3编译
5.修改./tools/build/src/tools/python.jam,547行，includes ?= $(prefix)/include/python$(version)m ;
（注意加上m）
6.运行./b2 --with-python 
7.运行./b2 install //这一步是将库加入/usr/local目录，很关键
以上，完成libboost_python3.so.1.64.0的编译

##2017-09-15

vim命令：
f命令用于行内快速查找，fx定位于本行本字符后的x字符上，
t命令同上
*命令，全文搜索当前词

shell脚本:
for f in $(ls | grep tupu) 
do 
  ...
done
// shell 脚本与shell命令结合，for循环

--------？-------
web search问题：海贼王的作者是谁
回答出现了符号：》《尾田荣一郎...

##2017-09-15

linux去重：
sort -u 文件名 > 新文件名 // 注意导向符不可缺，否则不对原文件进行操作

##2017-09-26

awk命令学习：
NR:当前行数
NF:当前列数
for循环，if与c++类似，不需要指定变量类型，如: awk -F '·' '{ print $0; for (i = 1; i <= NF; i++) 
​    print $i}' OFS="\n" $before_file > $after_name
$0指整行；
OFS指定输出的分隔符

##2017-09-28

linux c++下编码的转换：
从utf-8转换到gbk：

1. locale -a 查看所有机器支持的编码，这里需要用到zh_CN.utf8和zh_CN.gbk，
保证这两个编码在输出列表中；
2. include <locale>包；
3. 具体代码的关键步骤：
   // 从utf8转换为gbk
   setlocale(LC_ALL, "zh_CN.utf8"); // 将机器编码转换为zh_CN.utf8、
   int medlen = mbstowcs(NULL, src, 0); // 测试unicode长度
   wchar_t* medStr = (wchar_t*)calloc(sizeof(wchar_t), medlen）; // 分配wchar_t字符
   mbstowcs(medStr, src, strlen(src));  // 将src转换为unicode
   // 再重复一次，从unicode转换为gbk
   setlocale(LC_ALL, "zh_CN.gbk"); // 将机器编码转换为zh_CN.gbk
   int deslen = wcstombs(NULL, medStr, 0); // 测试gbk长度
   char* gbkstr = new char[gbklen + 1];
   wcstombs(medStr, src, strlen(src));  // 将src转换为unicode

**********************************************************************
**********************2017-09-29**************************************
**********************************************************************
c++编译错误：
collect2: error: ld returned 1 exit status // 由于存在命名冲突造成的，
​                                           //我这边是因为冲突的libboost_regex定义（53和60的冲突）
git fsck --lost-found // very good 

**********************************************************************
**********************2017-11-03**************************************
**********************************************************************
在计算机中计算n*(n+1)*(n-1)*(2*m-n)/12 mod （10e9 + 7)的值。其中n,m取值在int的正整数范围内。
这看起来简单，但在c中最长整数表示为8个字节的限制下，需要考虑很多问题。利用同余的性质是关键。
由于一开始不太熟悉，走了不少弯路。正确的做法是：先计算前边的所有乘积的模，根据最后结果，累
加10e9+7得到可以被12整除的最小整数，之后除以12就可以了。

**********************************************************************
**********************2017-11-24**************************************
**********************************************************************
cat /etc/redhat-release 查看cent OS版本号
curl -XPOST 'localhost:9200/twitter/tweet?routing=kimchy&pretty' -H 'Content-Type: application/json' -d'
{
​    "user" : "kimchy",
​    "postDate" : "2009-11-15T14:12:12",
​    "message" : "trying out Elasticsearch"
}
'

**********************************************************************
**********************2017-12-11**************************************
**********************************************************************
python中的枚举类型：
1.先定义枚举函数：
def enum(**enums):
  return type('Enum', (), enums)

2.使用枚举函数定义枚举：
  A = enum(B=1, C=2)

3.调用枚举
  print A.B

**********************************************************************
**********************2017-12-15**************************************
**********************************************************************
lsb_release -a (适用于所有的linux，包括Redhat、SuSE、Debian等发行版，但是在debian下要安装lsb)

**********************************************************************
**********************2017-12-27**************************************
**********************************************************************
A,Shell支持作用控制，有以下命令：
1. command& 让进程在后台运行
2. jobs 查看后台运行的进程
3. fg %n 让后台运行的进程n到前台来
4. bg %n 让进程n到后台去；   
   PS:"n"为jobs查看到的进程编号.
   
**********************************************************************
**********************2018-02-11**************************************
**********************************************************************
python reduce
在python中，有很多为了处理列表和字典的便捷接口，比如说zip、map、lambda，
今天学到了一个reduce函数，它对列表的每个元素进行判断，进行函数操作后生成
新的列表，我用它来对元素是字典的列表进行去重。set方法没办法对字典元素列表
进行去重，这是因为字典属于不可哈希类。因此通过reduce方法解决。

**********************************************************************
**********************2018-02-24**************************************
**********************************************************************
tensorflow中图Graph和会话Session的概念
按照我的理解，Graph保存一个变量和结构，可以说是一个静止概念，就像神经网络
的图形一样，由点和流程线构成；
Session是一个运行概念，它将Graph中的变量输出成对应的形式。
Graph中可以有多个Session，而Session中也可以有多个Graph。

**********************************************************************
**********************2018-02-28**************************************
**********************************************************************
linux grep命令不匹配：
1. grep -v "xxx"  用-v命令表示不匹配某个字段
2. grep "[^xxx]"  用正则表达式表示不匹配某个字段

**********************************************************************
**********************2018-03-05**************************************
**********************************************************************
Tensorflow容易犯的错误：
全连接层最后一层容易加了某个非线性函数后，再用softmax；实际上最后直接
wx+b然后softmax就可以了，多加了会影响结果，在此谨记，以免再犯同样的错误。

**********************************************************************
**********************2018-03-05**************************************
**********************************************************************
locust测试网站抗压能力的工具，locust网站地址：https://locust.io/

**********************************************************************
**********************2018-03-20**************************************
**********************************************************************
tensorflow中的数组操作：
1. tf.scatter_nd_update()
example:
###
    ref = tf.Variable([1, 2, 3, 4, 5, 6, 7, 8])
    indices = tf.constant([[4], [3], [1] ,[7]])
    updates = tf.constant([9, 10, 11, 12])
    update = tf.scatter_nd_update(ref, indices, updates)
    with tf.Session() as sess:
      print sess.run(update)
###
2. tf.gather_nd()
example:
###
    indices = [[1], [0]]
    params = [['a', 'b'], ['c', 'd']]
    output = [['c', 'd'], ['a', 'b']]
###
    indices = [[1]]
    params = [[['a0', 'b0'], ['c0', 'd0']],
              [['a1', 'b1'], ['c1', 'd1']]]
    output = [[['a1', 'b1'], ['c1', 'd1']]]
    
    indices = [[0, 1], [1, 0]]
    params = [[['a0', 'b0'], ['c0', 'd0']],
              [['a1', 'b1'], ['c1', 'd1']]]
    output = [['c0', 'd0'], ['a1', 'b1']]
    
    indices = [[0, 0, 1], [1, 0, 1]]
    params = [[['a0', 'b0'], ['c0', 'd0']],
              [['a1', 'b1'], ['c1', 'd1']]]
    output = ['b0', 'b1']
###
3. tf.squeeze()
function: Removes dimensions of size 1 from the shape of a tensor.
example: 
###
    # 't' is a tensor of shape [1, 2, 1, 3, 1, 1]
    tf.shape(tf.squeeze(t))  # [2, 3]
###
    # 't' is a tensor of shape [1, 2, 1, 3, 1, 1]
    tf.shape(tf.squeeze(t, [2, 4]))  # [1, 2, 3, 1]
###

**********************************************************************
**********************2018-03-21**************************************
**********************************************************************
今天在用git push到远程服务器时遇到代理无法访问的问题，在105.106这台机器
上，当时以为git访问远程服务必须使用正确的代理（毕竟我是用公司的服务器跑的
）。今天找到了解决方法，一条命令：
git config --global --unset http.proxy
取消git的代理设置即可，看来想太多有时并不是好事啊。

**********************************************************************
**********************2018-03-23**************************************
**********************************************************************
解决同一台机器上提交多个git服务器的方法：（以自已的例子为例）
在~/.ssh目录下已经有公用的id_rsa，连接到公司的git服务器上。以下建立自己
的id_rsa
1. 生成新的id_rsa，取名xxx_id_rsa（名称随意，有区别就行）：
cd ~/.ssh
ssh-keygen -t rsa -C "gejx2010@gmail.com"
2. 添加私钥
ssh-agent -s
ssh-add ~/.ssh/gejx_id_rsa(若执行出错则执行"ssh-agent bash"后再执行本句，我的情况就是这样通过的）。
3. 将私钥添加到自己的git账户上，即添加ssh key粘贴gejx_id_rsa.pub的内容。
4. 配置config
cd ~/.ssh
touch config
config的内容如下：

'''
# self(gejx2010@gmail.com)
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/gejx_id_rsa
User gejx
'''

5. 测试：
ssh -T git@github.com 
如果显示：
Hi gejx2010! You've successfully authenticated, but GitHub does not provide shell access.
则为成功。此时可以使用git push|pull 等命令连接自己的git账户。

**********************************************************************
**********************2018-03-28**************************************
**********************************************************************
tensorflow 拆分tensor的方法：
1. tf.split()
	# 'value' is a tensor with shape [5, 30]
	# Split 'value' into 3 tensors with sizes [4, 15, 11] along dimension 1
	split0, split1, split2 = tf.split(value, [4, 15, 11], 1)
	tf.shape(split0)  # [5, 4]
	tf.shape(split1)  # [5, 15]
	tf.shape(split2)  # [5, 11]
	# Split 'value' into 3 tensors along dimension 1
	split0, split1, split2 = tf.split(value, num_or_size_splits=3, axis=1)
	tf.shape(split0)  # [5, 10]
2. tf.dynamic_partition()
    # Scalar partitions.
    partitions = 1
    num_partitions = 2
    data = [10, 20]
    outputs[0] = []  # Empty with shape [0, 2]
    outputs[1] = [[10, 20]]

    # Vector partitions.
    partitions = [0, 0, 1, 1, 0]
    num_partitions = 2
    data = [10, 20, 30, 40, 50]
    outputs[0] = [10, 20, 50]
    outputs[1] = [30, 40]
	
**********************************************************************
**********************2018-04-23**************************************
**********************************************************************
在skill_platform代码中，import acmotion时遇到以下问题：
Eroor: ImportError: libboost_python27.so.1.67.0: cannot open shared object
 file: No such file or directory
解决步骤：
1. 使用命令：
locate libboost_python27.so
显示如下：
/search/odin/spgoal/lib_sp/boost_1_67_0/bin.v2/libs/python/build/gcc-4.8.5/release/threading-multi/libboost_python27.so.1.67.0
/search/odin/spgoal/lib_sp/boost_1_67_0/stage/lib/libboost_python27.so
/search/odin/spgoal/lib_sp/boost_1_67_0/stage/lib/libboost_python27.so.1.67.0
/usr/lib/libboost_python27.so
/usr/lib/libboost_python27.so.1.67.0
该结果显示文件存在，说明相关路径没有添加到系统路径中。（若没有显示结果，则说明boost未编译安装成功，需要重新编译生成该文件）
2. 使用如下命令编辑系统路径:
vim ~/.bashrc
添加以下行：
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib"
3. 重新编译c++代码生成acmotion及acmotion.so，问题解决。

**********************************************************************
**********************2018-04-23**************************************
**********************************************************************
scp文件传输时，遇到乱码问题，原文件使用utf-8编译，copy后变成乱码.
该问题和linux系统语言设置有关。原机器上，locale的设置为en_US.UTF-8,
而新机器上为en_US。使用以下命令后解决问题：
export LC_ALL=en_US.UTF-8

**********************************************************************
**********************2018-04-24**************************************
**********************************************************************
很厉害的一个命令：
os.system("rm -rf " + dir_name)
利用os.system()接口直接调用命令行命令。

**********************************************************************
**********************2018-04-26**************************************
**********************************************************************
linux查看nvidia显卡：
lspci | grep -i nvidia  
查看显卡信息：
lspci -v -s 00:0f.0  

**********************************************************************
**********************2018-04-26**************************************
**********************************************************************
boost.python安装：
1）下载boost(网址https://www.boost.org/，我的是boost_1_67_0.tar.gz)
wget https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.gz
2） 安装：
tar -zxvf boost_1_67_0.tar.gz
cd boost_1_67_0
./bootstrap.sh --with-python=PYTHON --prefix=/search/odin/spgoal/lib/boost \
  --with-libraries=system,thread,python
./b2 install
./b2 cxxflags=-fPIC cflags=-fPIC --c++11
echo "LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/search/odin/spgoal/lib/boost/lib" >> ~/.bashrc
source ~/.bashrc

## 2018-05-02

### 配置nvidia驱动：

#### Part I

##### 确保nouveau被禁用

```
 lsmod | grep nouveau
```

若以上命令输出信息，则表示nouveau没有被禁用。
在centos系统中在**/etc/modprobe.d/blacklist-nouveau.conf**（没有则创建）文件中输入:

```shell
blacklist nouveau
options nouveau modeset=0
```

重新生成kernel initramtf:

```
$ sudo dracut --force
```

#### Part II.

##### python-pip 安装并更新到最新目录

```
yum install python-pip
pip install --upgrade pip
```

##### boost.python安装（参见daily)

#### Part III. (安装GPU驱动)

#####1. 安装gcc工具

```
yum install gcc*
```

#####2. 安装dkms

```
wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -ivh epel-release-latest-7.noarch.rpm
yum install --enablerepo=epel dkms
```

#####3. 安装kernel 开发包等

```
yum install kernel*
```

#####4. 安装cuda

```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run
```

(此处根据对应机型以及tensorflow对应版本寻找合适版本安装，例如，我想安装tensorflow1.8.0，在https://www.tensorflow.org/install/install_sources#common_installation_problems

网站上发现需要cuda9.0以及cudnn7，因此需要cuda9.0，9.1或者其他版本不适用)

```
sh cuda_9.0.176_384.81_linux-run --silent --driver --toolkit --toolkitpath=/tmp/ --samples --samplespath=/tmp/ --verbose
```

(路径可修改，此处安装可能会有丢失包，看打印信息，比如我安装时有libX11.so,libXi.so等未安装，则使用yum install libX11命令安装上，余者类推)

#####5. 编辑环境变量

在~/.bashrc中添加以下几行。

```
CUDA_HOME=/usr
PATH=PATH:CUDA_HOME/bin
LD_LIBRARY_PATH=LD_LIBRARY_PATH:CUDA_HOME/lib64:CUDA_HOME/extras/CUPTI/lib64
```

使环境变量生效：

```
 source ~/.bashrc
```

#####6. 挂载驱动

```
modprobe nvidia
```

(到此CUDA安装成功)

#### Part IV. 安装cuDNN

官网地址：https://developer.nvidia.com/cudnn
按照指示下载软件，我下载的是：cudnn-9.0-linux-x64-v7
安装：

```
tar -xzvf cudnn-9.0-linux-x64-v7
sudo cp cuda/include/cudnn.h /tmp/include
sudo cp cuda/lib64/libcudnn* /tmp/lib64
sudo chmod a+r /tmp/include/cudnn.h /tmp/lib64/libcudnn*

```

#### Part V. 安装Tensorflow

```
pip install tensorflow-gpu==1.8.0
```

(为了使服务器上的tensorflow版本同步，不加版本号默认为最新)

#### Part VI. 测试

```
 python
 >>> import tensorflow as tf 
 >>> hello = tf.constant('Hello, TensorFlow!')
 >>> sess = tf.Session()
 >>> print(sess.run(hello))
 Hello, TensorFlow!
```

如果此处不成功，提示：ImportError: libcublas.so.9.0: cannot open shared object file: No such file or directory,则添加以下指令：则添加以下指令：

```
echo "/tmp/lib64" >> /etc/ld.so.conf.d/cuda.conf
ldconfig
```

其中"/tmp/lib64"为安装路径，若安装路径不同则更换之；

若通过以上测试，说明安装tensorflow成功。

## 2018-05-03

文件去重等相关操作：
1. 取出两个文件的并集(重复的行只保留一份)
$ cat file1 file2 | sort | uniq > file3
2. 取出两个文件的交集(只留下同时存在于两个文件中的文件)
$ cat file1 file2 | sort | uniq -d > file3
3. 删除交集，留下其他的行
$ cat file1 file2 | sort | uniq -u > file3
4. 合并两个文件
4.1 一个文件在上，一个文件在下
$ cat file1 file2 > file3
4.2 一个文件在左，一个文件在右
$ paste file1 file2 > file3
5. 一个文件去掉重复的行
$ sort file | uniq
注意：重复的多行记为一行，也就是说这些重复的行还在，只是全部省略为一行！
$ sort file | uniq –u
上面的命令可以把重复的行全部去掉，也就是文件中的非重复行！

##2018-05-26

java.net.UnknownHostException: xxx: 未知的名称或服务
这是由于本地域名localhost未解析造成的。我出该问题的机器是nmyjs_105_106,
将它映射到127.0.0.1上即可，即在/etc/hosts添加一行：
127.0.0.1 nmyjs_105_106 localhost

##2018-06-05

```
pip --default-timeout=100 （设置延迟时间） -i https://pypi.tuna.tsinghua.edu.cn/simple (设置源）--ignore-installed ipython (忽略包针）
cat /usr/local/cuda/version.txt
```

## 2018-06-13

cuda 版本 
cat /usr/local/cuda/version.txt

cudnn 版本 
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2

##2018-07-02

安装Expect:
1. 下载最新版本的Tcl和Expect
已下载位置：(root@10.141.105.106:/search/odin/gejx2010/software/soft_expect)
2. 解压安装包
unzip tcl868-src.zip
tar -zxvf expect5.45.3.tar.gz
3. 安装TCL
  3.1 进入解压目录tcl8.6.8/unix，然后依次执行以下命令：
	sed -i "s/relid'/relid/" configure
	./configure --prefix=/expect
	make
	make install
	mkdir -p /tools/lib
	cp tclConfig.sh /tools/lib/
  3.2 将/tools/bin目录export到环境变量，在~/.bashrc中编辑：
	export tclpath=/tools/bin
	source ~/.bashrc
4. 安装Expect
  4.1 进入解压目录expect5.45.3，执行：
    ./configure --prefix=/tools --with-tcl=/tools/lib --with-x=no
	如果最后一行提示：
	configure: error: Can't find Tcl private headers
	则需要添加一个头文件目录参数：即执行：
	./configure --prefix=/tools --with-tcl=/tools/lib --with-x=no --with-tclinclude=../tcl8.4.11/generic
	然后：
	make
	make install
	编译完成后会生在/tools/bin内生成expect命令(我的是在解压目录中生成的，将它拷贝到了/tools/bin中仍然能用）
    执行/tools/bin/expect出现expect1.1>提示符说明expect安装成功. 
5. 创建符号链接
    ln -s /tools/bin/expect /usr/bin/expect 
	
##2018-07-03

一、命令行解析工具：
import argparse
parser.add_argument('--batch_size', default=100, type=int, help='batch size')

二、pip的相关命令参数对python同样适用，或者说是从python衍生出去的
python test.py --default-timeout=100 -i https://pypi.tuna.tsinghua.edu.cn/simple
在研究tf-hub时发现的，由于经常出现超时，以及下载速度过慢，所以尝试使用了pip控制超时的参数，可以通过。

##2018-07-13

注重异步程序的编写：

```python
from tornado.httpclient import AsyncHTTPClient
import asyncio
import json
import urllib

async def check_music(query):
    client = AsyncHTTPClient()
    resp = await client.fetch("http://10.141.105.106:5858/response?query=%s" % urllib.parse.quote_plus(query))
    maybe_music = json.loads(resp.body.decode("utf-8"))[0] == 1
    if maybe_music:
        r = await search_qq_music(query)
        if r is not None:
            return True, {"music_result": r}
    return False, None
	
async def main():
    r = await check_music("周杰伦的青花瓷")
	print ("r:", r)

if name == "main":
    loop = asyncio.get_event_loop()
	loop.run_until_complete(main())

```

可以学习的地方：
1. async 定义异步函数；
2. 使用await导出异步函数的结果；
3. 使用event loop运行异步函数；
4. 使用AsyncHTTPClient()引入异步请求Client，使用fetch方法获得请求结果；
5. 使用urllib.parse.quote_plus转义query函数；

##2018-07-13

字符串拼接方法：
a = "".join("bcd")

##2018-08-08

git针对不同项目设置不同的用户名（不需要修改全局设置）:
1. 进入git项目文件夹根目录，配置文件在.git/config中，使用如下命令可以修改
  用户名和邮箱：

  ```sh
  git config user.name "gejunxiang"
  git config user.email "gejunxiang@sogou-inc.com"
  ```

  如果有必要，使用如下命令取消全局设置：

  ```sh
  git config --global --unset user.name
  git config --global --unset user.email
  ```

2. ~/.ssh/config配置，参见(2018-03-23的日志），设置针对本项目的内容，例如我的：

  ```sh
  #self(gejunxiang@sogou-inc.com)
  Host intent
  HostName git.sogou-inc.com
  PreferredAuthentications publickey
  IdentityFile /root/.ssh/gejx_sogou_id_rsa
  User gejunxiang
  ```
3. 在本地git项目的config中，将url中的hostname url改成~/.ssh/config中使用的host，我的情况是：
  原来：

  ```
  [remote "origin"]
    url = git@git.sogou-inc.com:gejunxiang/IntentJustify.git
    fetch = +refs/heads/:refs/remotes/origin/
  ```

  修改后：

  ```
  [remote "origin"]
    url = git@intent:gejunxiang/IntentJustify.git
    fetch = +refs/heads/:refs/remotes/origin/
  ```

  只有这样，git才能正确使用配置的内容。 

## 2018-08-27

1.这会为你保留本地文件，但会在其他人拉下时删除它。

git rm --cached <file-name>或git rm -r --cached <folder-name>

2.这是为了优化，就像一个包含大量文件的文件夹，例如可能永远不会改变的SDK。 它告诉git每次更改时都不再检查那个大文件夹，因为它没有任何更改。

git update-index --assume-unchanged <path-name>

3. 这是告诉git你想要你自己的独立版本的文件或文件夹。 例如，您不想覆盖（或删除）生产/登台配置文件。

git update-index --skip-worktree <path-name>

##2018-08-30

一、 今天遇到python3中的编码问题，具体是这样的：
​    从xiaowei请求时，拿到的response基本是utf-8编码的，但有个别会报UnicodeDecodeError；细查后发现
​    这些response中有不合法编码（unicode的编码），导致上述错误。在查询API后发现以下解决方法：
​	response.body().decode("utf-8", errors="replace")
​	errors对应不同的处理方法，replace是针对出现unicode编码时的替换；ignore是忽略；
​	
二、对于git的一个困扰是：一旦在某一次向仓库中提交一个大文件后，即便后来将其删除或者加入ignore，文件仍然会保留在历史
记录中(.git)。如果这些文件曾被提交到服务器，会造成远程库新建时把这些记录也一并抓取，造成抓取缓慢。

搜索过程中学到了以下有意思的指令，记录一下：

链接1:（https://segmentfault.com/q/1010000002564327）
1. 新建一个可以作为根的分支：
	git checkout --orphan new_start
	然后使用：
	git branch -D master
	可以完全丢弃之前的历史记录。
	不过令人失望的是，该方法的操作记录仍然会记录在.git中，大文件记录无法抹去。
2. git rebase命令，该命令并没有使用，虽然有趣，因为估计效果和1的作用差不多；
-----------------------------------------------------------------------------------------
链接2：https://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E7%BB%B4%E6%8A%A4%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D
这部分内容主要学习了git gc以及相关命令，包括：
1. git count-objects -v 查询使用空间
2. git verify-pack -v .git/objects/pack/pack*.idx | sort -k3nr | tail -3 查看objects的大小及记录
3. git rev-list --objects --all | grep 7a9eb2fb 查看objects的名称（看到这我心想，要是早点知道这条命令多好，之前
有过一次类似的情况，但我是把objects一条条恢复的，因为不知道文件的名字）
4. git log --pretty=oneline --branches -- git.tbz2 找出与文件相关的记录
5. git filter-branch --index-filter 'git rm -rf --cached --ignore-unmatch shorten_tupu' -- 6df7640^..
   rm -Rf .git/refs/original
   rm -Rf .git/logs
   git gc

------------------------------------------------------------------------------------------
链接3：https://stackoverflow.com/questions/1029969/why-is-my-git-repository-so-big/1036595#1036595
1. git gc --prune=now --aggressive
   git repack
-------------------------------------------------------------------------------------------
上述三个方法都有尝试，均未成功。最终解决问题的方案为（基本是在链接2的基础上）：

```
git filter-branch --index-filter 'git rm -rf --cached --ignore-unmatch "shorten_tupu tree_tupu"' --prune-empty -- --all
rm -rf .git/refs/original
rm -rf .git/logs
git gc
git prune --expire now (这行是完全删除，谨慎；上一步已经可以保证大文件不再传播）
git push origin master --force --all
```

##2018-09-03

?*? 对NLP的一些感悟：
做过了文本分类、翻译和预测等的模型后，神经网络确实在很大程度上提高了人的
效率和机器对语言、图形、图像的理解；但仍感觉无法接触到语言和图像的真谛，
且因为训练过程的纯抽象性和数字化，人无法理解机器是如何表示自己的理解的，
而机器也仍然无法按照人的思维逻辑去具体化、抽象化一个问题。
在我看来，语言，应当是一个整体，是一个作为整体的大数据库和搜索库，不能单靠
抽出来的几万条句子拿来训练就奢望机器懂得该类语言所有的规则，单纯建立在部分
文本和翻译上的神经网络模型都缺乏准确性；基于整体的语言理解才能最终让机器懂
得人的语言。

##2018-09-04

一、今天使用std map时，传入map<char*, int>类型，结果遇到以下两个问题：
1）使用char* start读取值，传入时因为没有更新指针，导致几次插入后map中始终
   只有一个元素；应当每次插入时start需要new一下；
2）使用char* 作为key，结果在find时比较的是char*也就是字符串地址而非内容，
   应当改为string输入，切记切记！

##2018-09-07

一、vim中显示实时更新的文件：
Esc + : + e

二、sed命令
sed "2,$d" file



##2018-09-12

一、python查看第三方库版本号：
   我们可以利用  pip list 和 pip freeze命令查看所有安装包的版本号

二、shuf 命令
  shuf -i 1-10 -n5 #从1-10中随机取5个数

三、seq命令
  seq 16 #生成从1-16的数
  seq 2 3 20 #以2起始，3为间隔生成[2,20]间的数
  seq -s" " -f"str%03g" 9 11 #-s指定分隔符，-f指定输出样式, -w指定同宽

##2018-09-13

python为结构或者方法增加in关键字：
一、为结构实现in关键字有两种协议A和B，在两种方法同时存在的情况下优先使用A。

  1. 协议A: __iter__ + next

    ```python
    class A:
    	def iter(self):
    		self.limit = 4 
    		self.times = 0 
    		self.init = 1 
    		return self
    		
    	def next(self):
            if self.times >= self.limit:
                raise StopIteration()
            else:
                x = self.init
                self.times += 1
                self.init += 1
                return x
                
    print 'A>>>>>>'
    for x in A():
    	print x
    ```

  2. 协议B：__getitem__ + __len__

    ```python
    class B:
        def __init__(self):
            self._list = [5, 6, 7, 8]
    
        def __getitem__(self, slice):
            return self._list[slice]
    
        def __len__(self):
            return len(self._list)
            
    print 'B>>>>>>'
    for x in B():
    
    print x
    ```


二、为方法实现in只需要加上yield关键字即可。

```python
def C():
    for x in range(9, 13):
        yield x

print 'C>>>>>>'
for x in C():
    print x
```



##2018-09-19

一、git取消每次输入密码：
  git config --global credential.helper store（只需要输入一次）
二、yes命令
  对每个选项输入yes

##2018-09-25

一、字符串编码新解(python2)
  在python2下，确实有很多字符串编码方式令人困惑，比如以下规律：
  1)任何字符串拼接，只要其中一个出现unicode，结果必为unicode；如：
​     #coding=utf-8
​     "abc" + u"def" = u"abcdef"
​	 u"def" + "abc" = u"defabc"
​	 "abc" + "def" = "abcdef"
  2)os.path.join()同理，只要参数中出现一个unicode编码，则结果为unicode；
  这个bug导致acmotion load_struct时出错。

##2018-09-26

一、lsof -i :80 (查看端口号为80的进程)
二、xargs (将输出重定向为输入参数)

##2018-09-27

一、C++ STL排序算法:
  sort：快排+内插排序，不同于普通快排，有很好的平均性能，可以保证算法为
  nlogn且系数很小；
  stable_sort: 归并排序，保持稳定性；
  partial_sort: 堆排序，对[start, end]的元素取[start, mid]的前mid-start+1个
  nth_element: 取数组中的第n个；

##2018-09-29

一、Kickstart Sums of Sums问题总结：
  （感慨：花了近三天的时间搞定这个问题，虽然算法一开始就想到了，但实现算法
  的过程却异常曲折，出了无数的bug，查阅了很多C/C++算法。有一段时间没写C代码
  了，因此需要重新总结自己入过的坑，记在这里供自己参考和提高。）
  一）先说下我对这个问题第一次分析的主要过程和key point：
  1）问题是计算连续子序列和排序后的新数列的连续子序列和，最长序列长度是200000，
  看到这个数字，首先需要反应过来的是，算法绝对不能是个平方以上的算法，否则必定
  超时，所幸这个反应我还是有的；
  2）在纸上稍微画一下或者想一下就知道，连续数列和会组成一个三角形状的金字塔，其
  每条斜线都是偏序的，这应该是一个很直观且容易想到的东西；
  3）问题是求解整个金字塔中第li个到第ri个数区间中所有数的和；所以第一次做这题时，
  会绕以下弯：
​    3.1）能不能做简单转换，让所有金字塔天然形成所有数排好序的序列；
​    3.2）第n个数映射到金字塔中的某个数是不是有规律，即存在n=f(i,j)，i,j是三角形坐标；
​    3.3）会不会存在s=f(li,ri)的简单关系，或者动态规划可以解决；
  4）由于之前看过这题，知道以上思路行不通，很快便get到这个问题需要以下两步：
​    4.1）在偏序序列中确定li和ri的位置以及对应的数值；
​	4.2）快速计算li到ri间所有数的和；
  5）想到第4步时，再稍微分析一下就会get到快速计算的key point所在：
​    5.1）金字塔中的所有数，给定位置i,j后，可以在O(1)时间计算其值。将所有的数与第一斜
​	行（从左下第一个数到右上最大的数）比较，会发现其映射关系(暂不考虑边界)：
​	        a(i, j) = a(0, i+j) - a(0, i - 1)
​	这说明，在读入数据的过程中，我们只需要计算第一斜行的值即可知道任意位置的值；
​	5.2）接下来很自然的会考虑，能不能也在O(1)的时间内计算同一个斜行上的连续序列的和呢？
​	答案是肯定的，因为同样可以将其映射到第一斜行上（暂不考虑边界）：
​	    s((i, j1) ~ (i, jn)) = s((0, i+j1) ~ (0, i+jn)) - (jn - j1) * a(0, i - 1)
​	这说明我们中需要在读入数据时再计算第一斜行从起始开始的连续和的和，再加上5.1）的连续和，
​	我们可以在O(1)时间得到某一斜行上的连续和，那么即便是累加n行，复杂度也仅是O(n)，完全可以
​	接受。
  6）有了5的分析，很自然地会想到这种思路下问题的关键是：
​    6.1）确定第li个数的大小、位置及在每一斜行上的边界（value(li) <|<= a(i, bi)；同样的方法
​	确定ri；
​	6.2）5）中的方法计算两个边界内的数的和；
​	很显然问题的关键在6.1；
  7）由于每个斜行序列是偏序的，很自然会想到二分查找，但怎么查找？由于所有问题都从第一斜行开始，
  于是我想到如果能知道第一斜行中每个数在整个序列中排第几，那么使用二分查找可以快速定位问题区间；
  这种想是自然的，可惜也存在了一个算法误区，这个误区在debug个过程中会提到，在此引以为戒；
  8）所谓定位区间，就是在相邻的第一斜行上的两个数，定位这两个数在全序列中的边界，由两个边界组成
  的定位区域；分析复杂度会发现，由于每个区间偏序，而每个值由5）中的分析可以在O(1)时间确定，使用
  二分查找确定每个数的全序列边界就是一个nlogn的算法，没有n^2，因此可以接受；
  9）接下来自然是在定位区间中找到排行第li的那个数及其位置，很自然地，这是一个n个不等长有序数列查找
  第k大的问题，在这里进入第二个误区。开始做的时候，第一想法是归并，于是。。。我以为递归的归并可以在
  O(n)的时间内解决这个问题。。。解决方法在debug列，这里仅记录第一次的分析过程。
  10）当找到第li个数和位置后，无非是重复8)的步骤，再花nlogn的时间定位第li个数的边界；然后第ri个数也
  用相同的方法；
  11）最后再使用5）中的方法在O(n)时间内计算li到ri形成的区间内所有数的和；
  12）这样得到了一个解决方法，假设上述每一步都如分析那样，最长的耗时也不过是nlogn，那么问题就可以得到
  解决了；（实际上解决过程差不多，不过中间的某些步分析并不正确，因为我掉进坑里了）；
  二）然后是记忆中有印象的debug过程：
  1）首先是C代码和python的区别，句尾和括号问题，记住：
​    1.1）写代码时每一行想想要不要加分号；
​	1.2）控制流的判断句式想想要不要加括号、大括号；
​	1.3）每一个变量需要声明和初始化，并注意初始化的类型到底是什么；
​	1.4）开指针时要注意需不需要开辟空间；另外，注意传值和传引用。指针慎重。
  2）二分查找时遇到的一些问题。没有写递归，用迭代实现二分查找，出现以下问题：
​    2.1）没有注意起始和终止的区间；我的习惯是在[start,end）左闭右开区间进行
​	二分，因此，当改动左边界时，应置start = mid + 1；否则二分查找会无限循环，
​	会犯这个错我还是太弱了。
​	2.2）注意二分查找的终止条件，while (start < end) 一般来说已经足够；不要加
​	等号；
​	2.3）注意二分查找结束时的情况；当命中某个数时，即start < end时，二分查找返回
​	的id对应的值等于该数；否则，返回id对应值必大于该数或者id==end，因为在过程中
​	始终有value(id) < value(end)（假设value(end)初始时无穷大)；而结束时start==mid
​	==end；因此，如果要查找不大于命中数的秩，当没有直接命中时应减去1，即二分查找
​	注意边界条件；
  3）边界条件非常重要。如果边界条件都不对，整个循环从一开始就已经错了；
​    3.1）在二分查找时，当查找不大于命中数的第一个数时，一开始没有考虑返回-1的情况；
​	3.2）当二分查找返回end - 1时，处理也和一般的处理不一致；
​	3.3）在本题中，暂时不需要处理返回end的情况，因为这不可能，但以后遇到这类问题时
​	还是要多考虑一重；
​	3.4）在考虑定位区间时，一开始考虑的非常混乱，一会左开右闭，一会左闭右开，一会
​	又左闭右闭，导致边界始终定位不清析，增加了很多debug的负担。相同序列的大小关系倒
​	是一开始就定义好的，但在处理这些边界时还是花了不少时间。以后在处理这类问题时需要
​	在一开始就定好区间的标准，出现新的边界问题上再在原来的基础上定新的标准，而不是回头
​	修改原来的标准，否则问题会绕来绕去，始终定不清楚；在定位区间的边界、计算和的边界，
​	计算和加上右边界的第一个点这个问题上都花费了不少时间；需要不断训练减少这块的失误；
  4）merge_array问题。
​    4.1）我清楚地记得归并排序的归并过程，有序数组A和有序数组B归并成新的有序数组只需
​	要线性的时间和空间，于是天真的我以为n个有序数组A1,A2,...,An归并成新的有序数组用
​	递归的归并也只需要O(n)时间；于是我两两归并，将归并好的新数组与下一个归并。。。这
​	样做的实际复杂度是n*A1+(n-1)*A2+···+An，亦即平方算法。
​	4.2）在一开始，我还用vector处理空间问题，实际上非常浪费时间，不断的开辟和清理空间
​	需要花费额外的时间。
​	4.3）后来改成固定的空间200000（本题最大输入量）+1，然后发现上限有可能比这个大，充裕
​	计算应该还需要乘以200；
​	4.4）这个过程中重写了归并的过程，需要注意边界条件和里边的四个循环的条件；如果是要求
​	稳定一定要注意方向，是否需要加等号；
​	4.5）make_pair的使用，make_pair产生的判别对可以直接push进vector，也可以直接赋值，还
​	可以直接进行比较，使用less<pair<int, int> >()函数，相当好用；
  5）当意识到merge_array的算法复杂度不对时，首先想到用快排解决，然后又进入了好多坑：
​    5.1）其实这一次写快排我写的还是挺正确的，需要注意的是排序的不是int，而是pair，注意
​	初始赋值和最终的值要返还给结束时秩所对应的值时就行；
​	5.2）上面其实并非我遇到的坑，坑的地方在于：我默认相同的数，右边斜行的数大于左边，因此
​	返回的第k大数跟其位置也是息息相关的；因为一开始使用归并，数列的稳定性可以保持，所以返回
​	的第k大数是正确的，改为快排后，第k大数实际上不对的，因为快排会改变序列的稳定性！！！！
​	因为没想到这一点，我debug了很久，虽然很快定位到快排出错，但并没有考虑到是稳定性的问题，
​	一直以为是自己好久没写C++代码了，连快排都不会写了，于是我看了n*n遍快排，还是没能看出快排
​	到底哪里写错了（哎，根本不是快排写错了好嘛，是快排本身就不能用在这好嘛！）。真的花了好多
​	时间在这个地方debug；后来发现是稳定性的问题是这样子的，在网上查找sort函数的说明，发现了
​	昨天记的nth_element的stl函数，替换掉快排的那一行代码后，结果在小数据集上又重归正确了；这样
​	一分析，结合归并时结果也是正确的情况，我才一下子意识到稳定性的问题。
​	在此形成意识，排序时对稳定性要形成意识，一个问题需不需要保持其稳定性，这是很重要的思考点，
​	切记切记！
​	5.3）然后就是nth_element函数了，新学到的，以及less<pair <int, int> >()这个函数，以及pair可以
​	直接比较这些新知识点；
  6）还是边界问题，重新说下计算连续和时的几个边界：
​    6.1）考虑右边界小于左边界的问题，这种情况其实不存在，但为了鲁棒和习惯还是加上了；
​	6.2）一开始没考虑到要加上右边界的那个值，所以没考虑确定第ri个数所在位置的问题，后来加上了；
​	6.3）考虑left和right和0的问题；
​	6.4）考虑是否第一斜行(rank == 0)的问题；
​	6.5）考虑加上第ri个数的问题；
​	6.6）考虑相对于第一斜行的数值偏移问题；
  7）debug到这个地步时，小测试样本(small.in)已经能输出正确的结果，测试通过，而且发现时间也挺快的；
  于是我以为算法就是nlogn没问题了，然后发现跑大样本需要几个小时，但此时我还是没考虑到是复杂度出错
  的问题，以为算法仍然是nlogn。这个时候报了个段错误(segment fault)，然后发现是merge_array的地方，
  总的数组空间不够，需要再乘上200这个最大上限；于是又改了后run，又要花几个小时；
  8）段错误还有可能出现的地方除了数组越界外，就是函数递归层数过深，此时一定是递归写错导致深度一直
  不降，就像处理二分查找和其他类型时start要加上1定为新的边界一样；
  9）时间意识相当重要，和7）一样的反思。
  当上边这些错都解决后，试了很多遍算法竟然还是小时量级的，我这时才意识到一定有某个地方复杂度计算
  不对。但想了很久都没找到问题所在，于是我用最笨的方法把每一步所花的时间打印出来，最后才发现竟然在
  自己最不注意的地方，initialize的时候就已经是n^2的复杂度。就像第一部分写自己的解题思路所提及的一样，
  我想在第一步先建立第一斜行每一个数在全序列中排第几，这样的话，每一个定位区间就可以在logn内时间确定
  自己在第一斜行上的位置，可这样的代价是，在第一步initialize时，对第一斜行的n个数中的每一个数，我都
  需要花费nlogn的时间定位，所以一开始的复杂度就已经是n^2logn了，很尴尬，真得很尴尬。就在这么一个不起眼
  的地方，把好多个小时都浪费了。
  仔细想想，这一步根本没必要，虽然我没办法在logn时间找到第li个数在第一斜行上的位置，但我可以花费logn的
  时间计算定位，也就是说用两层二分查找，实际复杂度为nlognlogn，但这远比n^2快，也是我找到的解决方法。纠正
  了这点之后，程序的运行时间大概在20s以内，虽然不是最快，但已经是可以接受的了。
  假如我一开始对每一步都认真分析，假如我有更强的时间意识，假如我对自己写的代码有更高的全局和大局意识，
  我就不需要花费大把的时间去等结果，也不会把这个问题拖到三天才能解决，真是给我好好的上了一课了，引以为戒
  引以为戒！
  10）long long问题要谨记。
  当完成到这一步时，跑大测试样本时以为会安全通过，结果还是出错了，又进到了一个新坑里了，这个时候的坑点在于
  无法调试。因为结果咋一看都是正常的，18多万的数据那一个测试样本，每一个输出数据又都是long long级别的没有错，
  这个时候真得有点无助，因为我没办法拿到标准答案来比较，更没法通过调试方法告诉我哪一步出错了。
  没办法，我只有从大测试样本入手，打印一些基本信息，因为小样本测试通过，那么bug的来源应该是在大样本上出的，
  看了几行终于发现有点问题，因为有A:[l1,r1]和B:[l2,r2]满足l1<l2<r2<l1,也就是说A区间完全包含B区间的情况但结果却
  反了过来，A对应的输出结果反而大于B，这终于让我找到了调试的方向。
  于是乎我把li、ri对应的数和位置都打印出来，同时看数据和代码，一开始以为是查找位置时出错，因为原来是n^2logn算法
  时，有计算第一行的ini_rank数组储存每一行的排序，后来去掉initialize时，在查找第一斜行用二分查找时会给ini_rank赋值，
  我以为是在出结果时忘了给ini_rank赋值，结果在出口处赋值后错误依然存在。
  于是仔细分析数值和位置貌似都符合规律，然后转到计算和的这块地方，我意识到可能是long long的问题了。我发现在使用第一
  部分5）中的计算公式，减去偏移的时候是long long - int * int，确实存在问题，于是把这部分计算公式后边改为long long，
  于是另一个奇怪的现象出现了：大样本的测试结果居然全部都是负数！
  百思不得其解，没办法，我只好打印更多信息，才发现问题出现在计算第一斜行和的和(sum of sum array)的地方，大数的和居然
  为负，最终找到问题的来源，居然是在我一开始计算时，用int累加来得到long long，最终导致计算sum of sum出错，出现负数的
  情况。
  在此再次提醒自己，要更加注意long long的情况了，
  10.1）包括定义一个变量和函数是否用long long；
  10.2）注意long long和int混合的运算公式是否正确；
  10.3）上边出现的错误，由int累加计算得到long long的一般都是错的，特别注意；
  三）以上这些都完成后，终于全部跑通，结果通过，瞬间感觉全身舒畅，这个过程虽然曲折，但总结后相信我会学到不少东西，最后
  再把重要的几点总结一下：
  1）C++和python区别的地方，终极境界要练到一次代码就能保证不出声明、定义、格式错误；
  2）边界问题要考虑清楚，递归和迭代都是，而且定义好一个边界后就沿着这个边界往后思考问题，不要反复在这个边界进行修改，
  导致解决思路进行不下去；
  3）仔细分析每一步所需要的算法时间和空间复杂度，不要想当然的以为O(n)，结果却是个O(n^2)；时间观念、算法复杂度分析都
  要进一步提高；
  4）熟练掌握一些常用算法的编写，做到不出错，并清楚这些算法的边界和使用范围、限制，比如快排就是不稳定算法，当需要稳定
  性时绝不能使用等等；二分查找出来的边界需不需要再加减1等等；
  5）long long问题要重视，每一次数据的定义都尽量分析是否存在错误。

##2018-09-30

一、C++ STL函数学习：
  1）lower_bound返回第一个不小于比较数的数，该数可能等于比较数；
  2）upper_bound返回第一个大于比较数的数，不可能等于比较数；
  3）binary_search，二分查找，但只返回True或者False;
二、Google测试小技巧：数据处理时将数据按照[1,n]考虑，秩为0时赋为0或者其他值，往往可以起到减轻边界处理负担的作用。
三、EvenDidigs刷题教训：
  3.1）边界问题没考虑清楚，出现9的时候向上会进1仍然是奇数，因此出现9只能向下取；
  3.2）代码确实按思路写了，但跑出来的结果始终不能通过；这时候我陷入了一个思维深渊，无从入手，不断地试数字也不知道
  哪错了；花费了不少时间才发现，我记录最高位奇数位数值last_bit没做对，导致结果在2098类似的数时输出依然是2，坑啊，
  类似的错误确实很难调试。如果出现类似问题，以后要多加debug信息了。保持思路清晰必须很重要啊。

## 2018-10-08

一、linux增加用户名，指定目录，设定密码：
  useradd|adduser -d /search/odin/open open
  passwd open

##2018-10-08

处理边界问题有没有比较通用的模式？减少边界问题的处理和定义；目前还没找到比较有效的思考方法，总是在定义边界时花费
太多时间思考。

##2018-10-12

一、linux命令:
  1) cat t | colrm 4 6 删除文件t中第4列到第六列的字符
  2) comm -123 file1 file2 比较文件差异，第三列放两个文件共同数据；
  3) split & csplit (后者支持更加复杂的模式)
​    3.1) split [-3|-l 3](分隔文件每个多少行) [-b 8|-C 8](分隔文件每个多少字节) file prefix
​	3.2) csplit -f prefix -n3(数字部分指定位数) -b "%02d.log"(指定后缀格式) [-s|-q](静默模式) -k(异常也输出) -z(删除
​	空文件) file pattern
​	pattern范例:
​	i) csplit file 100 (在第100行分割一次)
​	ii) csplit file 11 22 44 100 (在指定行数各进行一次分割)
​	iii) csplit file 100 {*} (每隔100行分割一次)
​	iv) csplit file /Part / {*} (每遇到Part分割一次)

二、判断最长回文字符串有O(n)的方法，记住这个方法；

##2018-10-16

一、Kickstart/NoNine问题总结：
  这是一首总体来说比较简单的题，然而对我来说还是有不少坑踩进去了。
  1）思路：很简单，统计包含9的数字和统计9的倍数，再减去二者的交集即可。
  这很容易想到，但实际实现时，二者的交集如何计算？是这道题的keypoint；
  2）开始时是直接计算[L, R]区间，给出结果；二者的交集需要知道被9整除的
  数的特性，像3一样，能被9整除的数其和一定能被9整除，这是个充要条件；稍微
  总结下发现了这个特点；
  3）但光这点不够，统计交集不可能将包含9的数全都判断一遍是否和能被9整除；
  时间复杂度不允许，需要进一步的统计；于是我发现，如果依次考虑Pattern：
​          [bef]9[0-8]+
  bef表示所有可允许的前缀，9表示当前判断的位置填9，[0-8]+表示在此位之后所有
  的数字填0-8之间的数字，如此，因为0-8包含mod 9后的所有数，当最后一位之前的
  所有数确定之后，最后一位只有一种可能能够满足被9整除，而依次按位数判断，则
  可以计算出所有包含9的数以及被9整除的数（到最后一位之前）。
  4）这个时候来到这个问题最关键的地方，如果到了最后一位呢，亦即最后一位是9，
  而它的后边已经没有[0-8]这个选项了。在这里想了很久，因为一直没发现前缀的规律，
  其实前缀就是[L / 10, R / 10 - 1]中能被9整除的所有数；
  5）发现上边这点是因为我把问题分成统计[0, R], [0, L]时发现的，有时候思绪就会
  像这样短路，明明不难的一道题，因为绕进一个死胡同，以为4）无法统计，结果绕了
  一道圈最后又回来了。以后面对类似的问题，需要思维是递进式的，这有助于保持思路
  清晰。另外，像这种L和R的左右区间问题，第一时间想想能不能[0, R], [0, L]解决也
  是一种好方法。
  6）后期遇到几个小细节注意一下：
6.1）pow(9, 18)函数出界，以后long long时慎用，可以自己写get_pow函数替代求和；
6.2）long long时还要注意；

6.3）c++转换字符串时要注意在最后加上休止符'\0'。

##2018-10-16

一、kickstart/ScrambleWords总结：
​    这是一道想了很久的问题，断断续续想了一周，始终在考虑能不能在线性或者
​	nlogn的时间内解决。今天看了下网上解决人的做法，才发现自己或许进了一个
​	误区。
​	下载了三个人的解决方案，他们的算法大同小异，都是用我一开始就能想到的
​	M*N的平方算法逻辑，加上现成的数据结构完成任务。初步估计了下，他们的
​	算法复杂度应该是M*sqrt(N)，至少第一个人的应该是这样，运算次数在3亿次以
​	上。第一个人的方案运行时间总共是10多分钟。
​	这时我才意识到，因为是应试的角度，即使一个算法没有达到复杂度上的最优，
​	但只要能在考试时间内跑出来并给出结果，就可以了。虽然心里有点小失落，想
​	了许久的题没有找到nlogn以内的算法，但也无疑让我学到了这点应试小技巧。
​	总结一些他们算法给我的启发：
​	1）Mister的做法很简单也很有启发性: Hash编码+遍历搜索，算法主要难点在于
​	一定要保证Hash编码的唯一性和正确性，即对应字符串生成的Hash编码也必须是一
​	样的(对应是指按题目要求，两端一样，中间的字母组合必须一致但顺序可以乱），
​	不同字符串HashCode一定不一致。为保证这点，他使用了64位随机数产生库：
​	                     mt19937_64 rng(24);
​	这是C++11可以用的随机数<random>库中的函数，产生一个64位的随机大数。对头和
​	尾以及每一个字母(a-z)产生一个对应的随机码，计算hashcode时对字符串连加就可
​	以了。搜索的时候按字符串长度搜索，将相同长度的字符串组织成一个vector，对
​	字符串长度-待匹配字符串长度、字符串长度-当前长度的所有字符串进行一次遍历。
​	2）jocobitpl的思路与前者几乎是一致的，他生成的唯一编码是用模余方法实现的：
​	Base是1299827ll，模数是1000000007ll。他将数据组织成multimap的方式，即允许
​	键值key重复，与Mister其实差不多，只是可以在查到之后方便地删除这个key。search
​	的时候仍然是遍历。
​	3）wcwswswws的做法也差不多，他的唯一标识码是最自然的思路，直接用首末以及中间
​	的数组唯一代表这个序列，数据是用三个逐层嵌套的vector，最里层一个unordered_map
​	实现的。
​	4）总结来说，这三个人的做法并没有从算法层面带来什么启发，但他们组织和使用的数据
​	结构值得我学习，他们都使用了c++11中的标准函数，我之前用的少。比如:
​	4.1) mt19934_64随机数生成库；
​	4.2）auto关键字替代复杂的iterator的书写；
​	4.3）for (string s : words[len]) 让我第一次感觉c++有点python的意思了；
​	4.4) 各种集成好的高级数据库的使用:unordered_set/map,multimap等等。
​	

##2018-10-23

一、tornado.options.parse_command_line()函数会默认为我们配置标准logging
​    模块，即默认开启了日志功能，并向标准输出（屏幕）打印日志信息。如果
​	想关闭tornado默认的日志功能，代码中该句之前添加：
​	options.logging = None
​	options.parse_command_line()
​	

##2018-10-24

一、linux命令ab测试服务器性能
  ab -c 5 -n 5 http://10.141.105.106:8787/?query=xxx(-c指定并发数，-n指定用户数)

##2018-10-25

一、安装python3.x(python3.6为例)的简单方法(yum直接安装):

```
  yum -y install https://centos7.iuscommunity.org/ius-release.rpm; 
  yum -y install python36u python36u-devel
  wget https://bootstrap.pypa.io/get-pip.py
  python3.6 get-pip.py(或者yum install python36u-pip -y)
```


二、rpm打包方法学习：

```
宏列表：
	%{sysconfdir}        /etc
	%{prefix}            /usr
	%{exec_prefix}       %{prefix}
	%{bindir}            %{exec_prefix}/bin
	%{libdir}            %{exec_prefix}/%{lib}
	%{libexecdir}        %{exec_prefix}/libexec
	%{sbindir}           %{exec_prefix}/sbin
	%{sharedstatedir}    /var/lib
	%{datarootdir}       %{prefix}/share
	%{datadir}           %{datarootdir}
	%{includedir}        %{prefix}/include
	%{infodir}           /usr/share/info
	%{mandir}            /usr/share/man
	%{localstatedir}     /var
	%{initddir}          %{sysconfdir}/rc.d/init.d
	%{var}               /var
	%{tmppath}           %{var}/tmp
	%{usr}               /usr
	%{usrsrc}            %{usr}/src
	%{lib}               lib (lib64 on 64bit multilib systems)
	%{docdir}            %{datadir}/doc
	%{buildroot}          %{buildrootdir}/%{name}-%{version}-%{release}.%{arch}
	$RPM_BUILD_ROOT       %{buildroot}
  rpm build目录：
	!/rpmbuild				%topdir		顶层目录			
    ~/rpmbuild/SPECS		%specdir		Spec 文件目录		保存 RPM 包配置（.spec）文件
	~/rpmbuild/SOURCES		%sourcedir		源代码目录			保存源码包（如 .tar 包）和所有 patch 补丁
	~/rpmbuild/BUILD		%builddir		构建目录			源码包被解压至此，并在该目录的子目录完成编译
	~/rpmbuild/BUILDROOT	%buildrootdir	最终安装目录		保存 %install 阶段安装的文件
	~/rpmbuild/RPMS			%rpmdir		标准 RPM 包目录		生成/保存二进制 RPM 包
	~/rpmbuild/SRPMS		%srcrpmdir		源代码 RPM 包目录	生成/保存源码 RPM 包(SRPM)
  rpm 隐藏文件(~/.rpmmacros)，可以定义在当前工程下，可以定义系统变量，当前工程生效：
	%topdir       /home/ambari/rpm
	%_tmppath      /home/ambari/rpm/tmp
```



##2018-10-31

一、Centos搭建ftp服务器
​	yum install -y vsftpd 

二、docker修改默认配置路径： /etc/docker/daemon.json
​	docker文档及安装：https://docs.docker.com/install/linux/docker-ce/centos/#upgrade-docker-ce
​    docker卸载：

```
  sudo yum remove docker \
					docker-client \
					  docker-client-latest \
					  docker-common \
					  docker-latest \
					  docker-latest-logrotate \
					  docker-logrotate \
					  docker-selinux \
					  docker-engine-selinux \
					  docker-engine
```

​					  

##2018-11-01

### 一、docker安装nvidia-docker问题及为使用tensorflow-gpu for docker：

​	参照nvidia-docker的git文档使用下列脚本安装:

```sh
#If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU     #containers
docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo yum remove nvidia-docker

# Add the package repositories
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | \
  sudo tee /etc/yum.repos.d/nvidia-docker.repo

# Install nvidia-docker2 and reload the Docker daemon configuration
sudo yum install -y nvidia-docker2
sudo pkill -SIGHUP dockerd

# Test nvidia-smi with the latest official CUDA image
docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi	
```

遇到/etc/docker/daemon.json无法创建的问题，查找许久未发现原因，最后定位是docker版本太低导致的；
机器上装的是docker_18.06.0，重装docker_18.06.1，问题解决。
以下测试安装并验证nvidia-docker和nvidia/cuda：

```docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi```

二、requests问题：
​    requests包是很多其他包依赖的软件，使用pip uninstall requests并无法删除干净该包，因此也不能直接
​	使用pip install --upgrade requests的方法进行升级。需要从源码安装升级。
​	1）删除现有目录：rm -rf /usr/lib/python2.7/site-packages/requests
​	2) git clone git://github.com/kennethreitz/requests.git
​	3) cd requests && python setup.py install
​	在import requests时仍然遇到urllib3的import问题，使用：
​	pip install --upgrade urllib3
​	解决

## 2018-11-07

一、c++ 11新特性总结:
​    1）nullptr:	区别NULL和0出现。当需要使用 NULL 时候，养成直接使用 nullptr的习惯。   
​	2）auto关键字和decltype关键字，分别对变量和表达式自动进行类型推导；
​	3）for循环的简单化: for(auto &i: arr);
​	4) 初始化列表： vector<int> a = {1, 3, 5, 7, 9};
​	5) 模板增加： 
​	   5.1）vector<vector<int>>合法；
​	   5.2）默认模板template<typename T=int, typename U=int>
​	   5,3）模板别名：template<typename T>
​	                  using NewType = SuckType<int, T, 1>;	
​	6）类继承：
​	   struct B : A {
​	        using A::A;
​	   }
​	7) lambda表达式：

```		[capture[ , =, &]](params) opt[mutable] -> ret { body; }   ```

```c++
int a = 0;
auto f = [&a] { return a; }
# lambda与STL函数的结合使用：
int value = 3;
vector<int> v {1, 3, 5, 2, 6, 10};
int count = std::count_if(v.beigin(), v.end(), [value] { return x > value; });
```

还有generate, for_each;
​	8) 新增容器：
​	     array, forward_list, unordered系列，
​		 tuple：三个核心接口：make_tuple | get | tie;
​    9) 正则表达式：

```c++
std::regex base_regex("([a-z]+)\.txt");
std::smatch base_match;
for(const auto &fname: fnames) {
    if (std::regex_match(fname, base_match, base_regex)) {
        // sub_match 的第一个元素匹配整个字符串
        // sub_match 的第二个元素匹配了第一个括号表达式
        if (base_match.size() == 2) {
            std::string base = base_match[1].str();
            std::cout << "sub-match[0]: " << base_match[0].str() << std::endl;
            std::cout << fname << " sub-match[1]: " << base << std::endl;
        }
    }
}
```

## 2018-11-13

### 一. Kickstart教训：

​       刷CaveEscape方法时遇到的，使用深度优先加层级搜索解决了问题，但无论怎么提交都报错，完全不知道bug所在，折腾了一天后才知道，居然是提交了错误目录的文件！！！看来我还是不够细心严谨，有时候考虑问题真得从源头、从最高层考虑出错所在。谨记谨记！

​	

## 2018-11-16

### 一、python类重载运算符：

#### 1. get和set方法（property）：

```python
class Person(object):

    def __init__(self):
        self._age = None

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self,age):
        if isinstance(age,str):
            self._age = int(age)
        elif isinstance(age,int):
            self._age = age

    @age.deleter
    def age(self):
        del self._age

p = Person()
p.age = "18"
print p.age #18
del p.age
print p.age #报错,AttributeError: 'Person' object has no attribute '_age'
```

#### 2. 基本运算符重载：

| Method                                                | Overloads | Call for |
| ----------------------------------------------------- | --------- | -------- |
| \__init__                                             |           |          |
| \__del__                                              |           |          |
| \__add__/__sub__                                      |           |          |
| \__or__                                               |           |          |
| _repr__／__str__                                      |           |          |
| \__call__                                             |           |          |
| \__getattr__                                          |           |          |
| \__setattr__                                          |           |          |
| \__delattr__                                          |           |          |
| \__getattribute__                                     |           |          |
| \__getitem__                                          |           |          |
| \__setitem__                                          |           |          |
| \___lt\__, \__gt\__, \__le\__,\__ge\__,__eq__, __ne__ |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |
|                                                       |           |          |





## 2018-11-20

### 一、kickstart 2018 H summary:

#### 1. Big Button

##### 0) 问题描述：

考虑只有‘B'和'R’组成的字符串，给定其长度N，和M个字符串数组，每一个数组Mi表示该字符串不能以此串开头，示解所有可能性；

##### 1) 解题思路：

I. 一开始想的是给M个字符串数组按长度排序，使用map<int, string>的结构，按长度从小到大依次减去以其开关的可能性，码完代码加编译运行通过估计有30分钟；

II. 发现该方法不对，因为没有考虑到字符串间的包含关系，从而重复计算了某些已经删除的字符串；为此，想到需要靠树来建立包含关系，在std c++中查找有没有快速建树的方法，花了10多分钟；

III. 没有找到快速建树的方法；开始自己写树，建树，遍历树再输出；码完代码加编译通过花了近30分钟，最终耗时近70分钟；

##### 2) 遇到的坑：

I. 树要不要写解析方法，因为不想耗用内存，纠结了一段时间；

II. pow(a, N)的方法，又一次越界，之前总结过一次，但又忘了；需要自己写pow，2为底数的话用<<快速写出；

III. 在遍历树时，采用了先序遍历，定义了计算变量cnt，类型long long，初始化为0；定义节点访问函数为view(TREE*, int&, int)，依次表示当前节点， cnt的值，深度信息；结果一直编译出错；花了一段时间才发现cnt的定义类型不对，long long传给了int&；需要特别注意；

#### 2.  Mural：

##### 0) 问题描述：

![ks_mural](./photo/ks_mural.jpg)

##### 1) 分析思路：

1.1) 对着给出的样例分析了半天，首先以下这点很容易想到：最后选择的长度一定是$\lfloor(N+1)/2\rfloor$; 但从哪一点开始选是问题的关键，一开始我以为要从最大的数开始选，但很明显不科学；对最后一个例子分析良久才知道解题思路；因为最后一个例子一开始我没明白他是怎么保证这样的结果不会被洪水冲走，只要看明白了，题目就很简单了；

1.2) 将题目转化为：对长度为N的数组，寻找和最大的长度为$\lfloor(N+1)/2\rfloor$的连续子数组，且该子数组能够保证被选出；

1.3) 由此，问题的关键在于判断区间[L, R]的合理性；这是这首题最花时间的一部分了。因为不太熟练，花了不少时间在分析这步，估计有20分钟以上；一开始用极端分析法，从最左边一直选到最右边，但最后一个示例就否认了这种思路；最终想到用通用分析法，设$L <= k <= R$，表示从k开始选择该区间，再分析k需要满足的上下界，得到：

$$ max(R * 2 + 1 - N, L) <= k <= min(2 * L, R) $$

1.4) 完成代码编译及运行，总共花费时间约1小时；

##### 2）遇到的坑：

2.1) 小样例通过的很快，但大样例超时了还没跑出来。于是我以为自己又不注意写成了$O(n^2)$ 的算法，但怎么写怎么看代码都是线性的，我又纠结了；又花了不少时间想到，可能是因为我**打印了太多信息**导致的；我使用的是公司的服务器，每一步打印信息都需要从公司传到家里的电脑上，然后程序才能执行下一步；难怪在大样例时跑不出来，我真是被自己蠢到了。然后最悲剧的事情发生了，当我改完代码，去掉多余的打印信息重新跑出正确的结果后发现：<font	face="黑体" size=4 color=red>大样本只允许跑一次，必须在规定的时间内跑完，否则无效</font>;

结果，我只能悲剧的失去解决大样本的机会，引以为鉴！

#### 3. Let Me Count The Way

##### 0) 问题描述：

一首排列组合题目，计算所有可能数$S(N, M)$，N表示有N对夫妻，M表示其中有M对新婚夫妻，求解所有的排列数便利任何一对新婚夫妻不相邻；

##### 1) 分析思路：

花了近一天的时间思考这首题，看来需要重新复习一下组合数学里的知识了；

1.1) 开始想的是加1法，即已知$S(N, M)$，如何计算$S(N+1, M)$和$S(N+1, M+1)$;但仔细分析发现，需要考虑的情况有点多，比如$S(N, M) \rightarrow S(N+1, M)$，简单来看，在原来的基础上的$2 \times N + 1$个空隙中选择两个空隙插入即可；但仔细想想，插入一个元素后，原来该元素两端的元素（假设空隙在中间）是可以放一对夫妻的，这样就有缺漏的情况没有考虑，而这种情况会不断传递到底层，所以后来放弃了该思路；

1.2) 通用分析法，即直接排；考虑$S(N + M, M)$的情况，先把N对夫妻排好，剩下的一对一对插入排好的空隙中；在$M=1$时，很明显是对的，但当$1<M$时，会出现和1类似的缺漏情况，即：上一对新婚夫妻不一定要分开，可以由新插入的夫妻将其分开；这样一来，这种情况会一直传递到M结束；于是我又放弃了该思路；

1.3) 在1.1)和1.2）间来回绕，想寻找直接的递推或者通项公式，但总不得法。最终耐下性子按照1.2的思路一步步展开寻找规律，最终才发现这是容斥原理的应用问题，见下：

1.3.1) 先排好N对老夫妻，得到$(2N)!$；

1.3.2) 将一对对新婚夫妻依次插入空隙，得到$A_{2N + 2M}^{2M} * (2N)! = (2N+2M)!$;

1.3.3) 在上述情况中，多计算了有一对新婚夫妻相邻的情况，因此减去这种情况，即考虑有一对新婚夫妻相邻时的可能数；重复1.3.1)和1.3.2)的步骤，得到$C_{M}^{1} \cdot 2^1 \cdot (2N+2M-1)!$;

1.3.4) 依次类推，按照容斥原理，多减去的加上，多加上的减去，再总结规律，得到最终的计算公式：

$$S(N+M, M) = \sum_{i=0}^{M} (-1)^i \cdot (2N + 2M - i)! \cdot C_M^i \cdot 2^i$$

1.4) 得到计算公式后，需要计算的项也就清楚了，不过，阶乘和幂次模余好计算，但组合数的计算方法在预处理阶段怎么计算又成了问题的一个关键。在这个地方卡了很久，通过$C_{n+1}^{m+1} = C_n^m + C_n^{m+1}$计算，但需要时间太长；最后也意识到除法相当于是找逆的问题，如$kx \equiv 1(mod \, y)$的问题，但如何找出k，又想了很久，线性累加的话时间要求肯定是不允许的，半天多的时间卡在了这里；

1.5) 没办法，借鉴别人的做法最终解决了组合数模余的解决方法；总结在经验里；

##### 2）经验教训：

2.1) 1e9 + 7是个大素数；

2.2) 排列阶乘的预处理计算；

2.3) 组合数模余的计算方法，即求$N^k$模M的余数，使用二分算法：

1. 将k表示成二进制形式，即: $k=\overline{d_r \cdots d_2  d_1 d_0} = d_0 \cdot 2^0 + d_1 \cdot 2^1 + \cdots + d_r \cdot 2^r $;
2. 于是$N^k = N^{d_0 \cdot 2^0 } \cdot N^{d_1 \cdot 2^1 } \cdots N^{d_r \cdot 2^r}$
3. 递推计算每一项即可，复杂度为$O(log_2{k})$;

贴算法如下：

```c++
// M is a prime number
int count_combo(int n, int k, int M) {
    int res = 1;
    while (k) {
        if (k & 1) res = (long long) res * n % M;
        n = (long long)n * n % M;
        k >>= 1;
    }
    return res;
}
```

2.4) 最终计算时在大数时仍出错，经过一段时间检查我才发现，题目规定N <= 100000，但组合数需要计算到200000，如上边的分析所示；最终解决这首题；

#### 4. 总体感受

这次的题目总体来说难度不大，相比于前几轮而言（在规定时间内解决两个大问题，虽然第二个问题的大样本因为次数受限没有提交)，而且偏数学一些；特别是第三题，对组合数学及其计算有很高的要求；我需要重新复习一下组合数学的相关知识和应用。



## 2018-11-27

### 一、kickstart 2018 G Round

#### 1. Product Triplets

##### 0) 问题描述：

该题是找数组中所有满足(x, y, z)的三元组合，使得: $xy=z, 0<=x<y<z<N;$

##### 1) 总结：

该题较简单，简单Case直接用暴力算法$O(n^3)$也可以解出来；由三元和(**leetcode中的题**)的经验，在固定x及排除边缘情况后，(y, z)的组合数可以在$O(n^2)$的时间内给出；

在解决该题的过程中，边缘问题考虑的比较久，debug花了一些时间；另外，第一次做时，固定x及y后用二分查找查找z，因此算法复杂度为$O(n^2logN)$;

#### 2. Combining Class

##### 0) 问题描述：

该题可以简单理解成下列问题的求解：

给定一系列区间数组：[a1, b1], [a2, b2], ... , [an, bn]

求解Q组查询，每一个查询Qi表示查询上数区间数组集合中第Qi大的数；

##### 1) 解题思路：

由于有SumsOfSums的经验，很容易想到Small Case的解题思路。注意到Small Case中固定$Q=1$，即只有一次查询，那么使用SumsOfSums中的二分查找策略，算法复杂度仅为O(NlogN)，完全符合要求；

在此再次总结区间二分的代码：

```c++
/**
*** 查找分散区间中第k大的数；
*** 前提1: get_rank(), 确定某个数第几大由函数get_rank()给出，只需要遍历一遍数组即可
*** 在此不予列出
*** 前提2: min、max表示数组的临界点，很容易得到，这里直接使用
**/
int bin_search_area(int k) {
    int l = min, r = max, res = -1;
    while (l <= r) {
        int mid = (l + r) >> 1;
        if (get_rank(mid) < k) {
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return r + 1;
}
```

然而遗憾的是，上述思路并不能直接适用于Large Case，因为此时Q=100000，算法复杂度变成$O(Q*N*logN)$，变成了一个平方复杂度的算法，因此不能在规定时间内完成；

在这个地方考虑了很久，说白了就是一个预处理的过程，然而想到如何组织数据却没有想像中的那么容易。最后发现了计算规律，即分别统计端点出现次数和区间出现次数即可；在端点处预计算其rank值；

```
1. 首先用map将区间端点存入map中，并标记每个端点和其区间，亦即开个足够大的数组；
2. 遍历map，从最大的点开始，依次更新当前端点的rank，以及更新此前区间的出现次数；
3. 对于每次查询，使用二分查找确定端点，再加上区间出现次数得到k值；
```

上述方法的复杂度为O(NlogN + QlogN)；

##### 2) 经验教训：

从这道题中得到了又一个处理区间数组的经验，并且需要根据情况采用不同的策略。

#### 3. Cave Escape

##### 0）问题描述：

这是一道迷宫题，等效为图论；问题是给定起始点和终点，问最节省能量（出去时能量值最大）的方法，输出最大能量值；

##### 1) 解题思路：

小样本因为没有potion(可以增加能量值的点)，因此就是一个dijsktra算法，寻找最短路径出去即可；该题难在大样本的处理。大样本中不仅有trap(trap数量限制在15个以内)，还有potion。

###### 1.1) 暴力算法：

以动态规划的思路，最佳方法应该依次由其相邻节点的最佳方法给出；于是，每次遍历未访问节点中的一个即可；实现这个动态规划的方法并不困难；一开始就想到了这一点；然而很遗憾，这是个阶乘算法；因为记trap点的标记为1~15的话，1->2和2->1会是不同的路径，于是算法变成了$O(15!)$，显然无法接受；

于是问题的关键点在于，如何剪枝，如何使相同结果的路径不再重复搜索；

###### 1.2) 路径去重：

试了很多种方法。比如建立路径集合，由当前集合判断路径是否重复，重复后就不再继续往下搜索，然而由于我是全图遍历并标记遍历点，因而这种方法会排除一部分可能存在的路径。想加上这些搜索可能性却又无法避开阶乘；

后来尝试写了几层的递归，思路都有点忘了，由于逻辑过于复杂，始终没有调通，所以放弃了；

###### 1.3) bitmask技术

由于苦思无果，我看了kickstart官方给的解题思路，学到了bitmask这个处理技术；数据集不大，15个trap点，因此，所有可能组合的集合用bitmask技术可知为$2^{15+2}$种可能，这完全在可接受范围内；

另外一点，去重的问题关键在于判断什么是相同的路径，什么是不同的路径，由于我的思路始终不清楚，所以没有考虑清楚这点；官方给出的去重思路如下，一个bitmask路径，表示所有已访问过的trap集合，因此他们有以下确定的值：

```
1. 是否到达了目标点: reach_target[mask];
2. 未访问的trap点集: unvisited[mask];
3. 当前能量: leave_energy[mask];
```

如果当初我能如此清晰地分析出这些，想必也不会纠结这么多天了吧。这样的分析思路值得我认真学习。

###### 1.4) 又一个坑

当我按照上述思路实现代码后，发现代码竟然无法在规定时间内解决问题，反复确定算法没有写错后，又让我纠结究竟问题出在了哪里？

花费了一番功夫才注意到问题出在我写的dfs算法。每次扩展一个新节点时，我都要在该图重新访问一次可扩展的potion节点和normal节点，如此，算法变成了$O((N*M)^2*2^{C_T)})$; 因此新的坑出现了，我必须预处理这些节点，以便利扩展点时不需要再做全图dfs；

想了很久实现了以下思路：

```
1. 对区间范围进行编号，区间范围表示从一个普通点或者potion出发不跨过trap及obstacle所能达到的点的集合；那么对于每一个区间范围，预处理确定以下值：
  1.1 每个点对应的区间编号；
  1.2 每个区间范围周围的trap点集，使用bitmask技术压缩成int;
  1.3 每个区间范围能够获得的potion值；
2. 扩展当前集合时，选取unvisited[mask]中的一个点，那么：
  2.1 新的mask值容易计算；
  2.2 新的reach_target由预处理的reach_target和当前reach_target求或得到；
  2.3 新的unvisited可以用异或运算计算；
  2.4 新的leave_energy可以依次访问新的trap点周围四个点的区间范围，确定端点和去重后得到；
```

最终，实现了Large Case的求解。

###### 1.5) 经验教训：

```
1. 学习到了bitmask技术；
2. 学习到了去重的分析文法；
3. 养成看到限制12~30的数字想到阶乘不允许，n方算法允许的意识；
4. 考虑问题要全面，在实现large Case过程中，一开始没有注意到算法由于重复dfs超时，然后是计算leave_energy时，没有考虑插入初始点时的特殊情况，没有给初始点赋值正确的leave_energy，然后是计算potion时；没有考虑四个点的去重问题，以为用位判断足够了。
5. 使用位处理运算要注意：(a & b == c)这种写法有问题，应该写成((a & b) == c); 位运算优先级低；
```



## 2018-12-05

### 一、memset错误

使用c++的memset时经常会犯以下错误，在此记之：

1. 忘记包含头文件，#include<memset>;
2. memset使用sizeof时，如果sizeof的参数是用new开辟指针，则返回的是指针变量的长度8；如果传入的是数组，则会返回正确的大小；
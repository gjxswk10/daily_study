[TOC]

﻿## 2017-07-24

awk命令：

```sh
awk -F "\t" '{print $1}' wenda_1_1.gbk | head
```

iconv命令：

```sh
iconv -f utf-8 -t gb18030 wenda_1_1.utf8 > wenda_1_1.gbk
```

sort命令：

```sh
sort -k1,1n sim.txt.seg 
```



## 2017-07-24

### 1.hydoop学习：mapper/reducer

  streaming架构

### 2.url编码

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
### 1. python中多断式的用法

```python
dict([itm.split('="') if len(itm.split('="    ')) == 2 else (itm, '') for itm in rank_str.replace('<rank ',     '').replace('"></rank>', '').split('" ')])
```

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
5.修改./tools/build/src/tools/python.jam,547行，includes ?= $(prefix)/include/python​$(version)m ;
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

### 一、 linux c++下编码的转换：

从utf-8转换到gbk：

1. locale -a 查看所有机器支持的编码，这里需要用到zh_CN.utf8和zh_CN.gbk，
  保证这两个编码在输出列表中；

2. include <locale>包；

3. 具体代码的关键步骤：

   ```c
   // 从utf8转换为gbk
   setlocale(LC_ALL, "zh_CN.utf8"); // 将机器编码转换为zh_CN.utf8、
   int medlen = mbstowcs(NULL, src, 0); // 测试unicode长度
   wchar_t* medStr = (wchar_t)calloc(sizeof(wchar_t), medlen）; // 分配wchar_t字符
   mbstowcs(medStr, src, strlen(src));  // 将src转换为unicode
   // 再重复一次，从unicode转换为gbk
   setlocale(LC_ALL, "zh_CN.gbk"); // 将机器编码转换为zh_CN.gbk
   int deslen = wcstombs(NULL, medStr, 0); // 测试gbk长度
   char gbkstr = new char[gbklen + 1];
   wcstombs(medStr, src, strlen(src));  // 将src转换为unicode
   ```

## 2017-09-29

c++编译错误：
collect2: error: ld returned 1 exit status // 由于存在命名冲突造成的，
​                                           //我这边是因为冲突的libboost_regex定义（53和60的冲突）
git fsck --lost-found // very good 

## 2017-11-03

### 一、除法的模余计算

在计算机中计算$n*(n+1)*(n-1)*(2*m-n)/12  mod （10e9 + 7)$的值。其中n,m取值在int的正整数范围内。
这看起来简单，但在c中最长整数表示为8个字节的限制下，需要考虑很多问题。利用同余的性质是关键。
由于一开始不太熟悉，走了不少弯路。正确的做法是：先计算前边的所有乘积的模，根据最后结果，累
加10e9+7得到可以被12整除的最小整数，之后除以12就可以了。

(2018-12-28) 补充：现在知道了这道题的通用做法，即求12的逆余数，因为$10e9+7$是一个素数，即求$12^{10e9+5} mod (10e9+7)$的值，利用二分法可快速计算。 

## 2017-11-24

cat /etc/redhat-release 查看cent OS版本号
curl -XPOST 'localhost:9200/twitter/tweet?routing=kimchy&pretty' -H 'Content-Type: application/json' -d'
{
​    "user" : "kimchy",
​    "postDate" : "2009-11-15T14:12:12",
​    "message" : "trying out Elasticsearch"
}
'

## 2017-12-11

python中的枚举类型：
1.先定义枚举函数：
def enum(**enums):
  return type('Enum', (), enums)

2.使用枚举函数定义枚举：
  A = enum(B=1, C=2)

3.调用枚举
  print A.B

## 2017-12-15

lsb_release -a (适用于所有的linux，包括Redhat、SuSE、Debian等发行版，但是在debian下要安装lsb)

## 2017-12-27

A,Shell支持作用控制，有以下命令：
1. command& 让进程在后台运行
2. jobs 查看后台运行的进程
3. fg %n 让后台运行的进程n到前台来
4. bg %n 让进程n到后台去；   
   PS:"n"为jobs查看到的进程编号.
   
## 2018-02-11

python reduce
在python中，有很多为了处理列表和字典的便捷接口，比如说zip、map、lambda，
今天学到了一个reduce函数，它对列表的每个元素进行判断，进行函数操作后生成
新的列表，我用它来对元素是字典的列表进行去重。set方法没办法对字典元素列表
进行去重，这是因为字典属于不可哈希类。因此通过reduce方法解决。

```python
reduce(lambda x, y: x + y, [1,2,3,4,5], 0)
# 第一个参数是函数入口，对列表中的两个元素进行参数
# 第二个参数是需要处理的集合类型，列表、字典、元组皆可
# 第三个参数是默认值，他相当于被放在秩为-1的位置上，当列表为空时返回该值
# 在python3中，需要reduce时需要引入functools包
```

## 2018-02-24

tensorflow中图Graph和会话Session的概念
按照我的理解，Graph保存一个变量和结构，可以说是一个静止概念，就像神经网络
的图形一样，由点和流程线构成；
Session是一个运行概念，它将Graph中的变量输出成对应的形式。
Graph中可以有多个Session，而Session中也可以有多个Graph。

## 2018-02-28

linux grep命令不匹配：
1. grep -v "xxx"  用-v命令表示不匹配某个字段
2. grep "\[^xxx]"  用正则表达式表示不匹配某个字段

## 2018-03-05

Tensorflow容易犯的错误：
全连接层最后一层容易加了某个非线性函数后，再用softmax；实际上最后直接
wx+b然后softmax就可以了，多加了会影响结果，在此谨记，以免再犯同样的错误。

##2018-03-05

locust测试网站抗压能力的工具，locust网站地址：https://locust.io/

## 2018-03-20

tensorflow中的数组操作：
1. tf.scatter_nd_update()

  ```python
  #example
  ref = tf.Variable([1, 2, 3, 4, 5, 6, 7, 8])
  indices = tf.constant([[4], [3], [1] ,[7]])
  updates = tf.constant([9, 10, 11, 12])
  update = tf.scatter_nd_update(ref, indices, updates)
  with tf.Session() as sess:
    print sess.run(update)
  ```
2. tf.gather_nd()

  ```python
  # example
  indices = [[1], [0]]
  params = [['a', 'b'], ['c', 'd']]
  output = [['c', 'd'], ['a', 'b']]
  
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
  ```
3. tf.squeeze()
  function: Removes dimensions of size 1 from the shape of a tensor.

  ```python
  # example: 
  # 't' is a tensor of shape [1, 2, 1, 3, 1, 1]
  tf.shape(tf.squeeze(t))  # [2, 3]
  
  # 't' is a tensor of shape [1, 2, 1, 3, 1, 1]
  tf.shape(tf.squeeze(t, [2, 4]))  # [1, 2, 3, 1]
  ```
## 2018-03-21

今天在用git push到远程服务器时遇到代理无法访问的问题，在105.106这台机器
上，当时以为git访问远程服务必须使用正确的代理（毕竟我是用公司的服务器跑的
）。今天找到了解决方法，一条命令：
git config --global --unset http.proxy
取消git的代理设置即可，看来想太多有时并不是好事啊。

##2018-03-23

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

  ```
  # self(gejx2010@gmail.com)
  Host github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/gejx_id_rsa
  User gejx
  ```

5. 测试：
ssh -T git@github.com 
如果显示：
Hi gejx2010! You've successfully authenticated, but GitHub does not provide shell access.
则为成功。此时可以使用git push|pull 等命令连接自己的git账户。

## 2018-03-28

tensorflow 拆分tensor的方法：
1. tf.split()

  ```python
  # 'value' is a tensor with shape [5, 30], 
  # Split 'value' into 3 tensors with sizes 
  # [4, 15, 11] along dimension 1
  split0, split1, split2 = tf.split(value, [4, 15, 11], 1)
  tf.shape(split0)  # [5, 4]
  tf.shape(split1)  # [5, 15]
  tf.shape(split2)  # [5, 11]
  
  # Split 'value' into 3 tensors along dimension 1
  split0, split1, split2 = tf.split(value, num_or_size_splits=3, axis=1)
  tf.shape(split0)  # [5, 10]
  ```

2. tf.dynamic_partition()

    ```python
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
    ```
## 2018-04-23

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

##2018-04-23

scp文件传输时，遇到乱码问题，原文件使用utf-8编译，copy后变成乱码.
该问题和linux系统语言设置有关。原机器上，locale的设置为en_US.UTF-8,
而新机器上为en_US。使用以下命令后解决问题：
export LC_ALL=en_US.UTF-8

##2018-04-24

很厉害的一个命令：
os.system("rm -rf " + dir_name)
利用os.system()接口直接调用命令行命令。

##2018-04-26

linux查看nvidia显卡：
lspci | grep -i nvidia  
查看显卡信息：
lspci -v -s 00:0f.0  

## 2018-04-26

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

**cuda 版本 **

```shell
cat /usr/local/cuda/version.txt
```

**cudnn 版本 **

```sh
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```

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
二、对于git的一个困扰是：一旦在某一次向仓库中提交一个大文件后，即便后来将其删除或者加入ignore，文件仍然会保留在历史记录中(.git)。如果这些文件曾被提交到服务器，会造成远程库新建时把这些记录也一并抓取，造成抓取缓慢。

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
3. git rev-list --objects --all | grep 7a9eb2fb 查看objects的名称（看到这我心想，要是早点知道这条命令多好，之前有过一次类似的情况，但我是把objects一条条恢复的，因为不知道文件的名字）
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



## 2018-10-16

### 一、Kickstart/NoNine问题总结：

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

### 二、kickstart/ScrambleWords总结：

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

1.4) 得到计算公式后，需要计算的项也就清楚了，不过，阶乘和幂次模余好计算，但组合数的计算方法在预处理阶段怎么计算又成了问题的一个关键。在这个地方卡了很久，通过$C_{n+1}^{m+1} = C_n^m + C_n^{m+1}$计算，但需要时间太长；最后也意识到除法相当于是找逆的问题，如$kx \equiv 1(mod \, y)​$的问题，但如何找出k，又想了很久，线性累加的话时间要求肯定是不允许的，半天多的时间卡在了这里；

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

1. 忘记包含头文件，#include<cstring>;
2. memset使用sizeof时，如果sizeof的参数是用new开辟指针，则返回的是指针变量的长度8；如果传入的是数组，则会返回正确的大小；



## 2018-12-12

### 一、kickstart B 2018总结	

第一个问题No Nine已经在[2018-10-16](#2018-10-16)日志中给出，在此略去；

#### 1. Sherlock and the Bit Strings

##### 0) 问题描述

只有0和1组成的字符串，加上m个区间限制条件[l, r, k]表示第l个到第r个字符间恰好出现k个1，求所有满足限制条件的字符串中，字母序第P大的字符串是什么？题目中限制每个区间条件$r - l <= 15$；

##### 1) 解决思路

由于区间之间存在相互交错的情况，如果一个个讨论将会非常复杂，在这个地方纠结了一段时间；随后想到，将区间放在线段上讨论，讨论每一个最小区间，比如[2, 15]和[6, 20]，就分成[2,6], [7, 15], [16, 20]三个小区间；这样的话，需要计算每一个小区间的所有可能情况，最后再取出其中第P大；

照着上述思路尝试实现代码，由于逻辑过于复杂，而且没考虑清楚复杂度是什么，只好放弃了；

最后参照答案，得到如下算法：

```
定义f(n)为当前生成串，c(n)为当前生成串最后16位；r(n)为当前生成串的rank；
1. 递归计算r(n)；即尝试在下一位分别补0和补1，更新当前的c(n)及f(n);
2. 根据当前r(n)和P的大小比较决定加0还是加1；输出最终字符串；
```

想到这个算法后，实现起来并不复杂，难度在于动态规划的过程；

##### 2) 总结

- 看到15的限制需要想到bitmask技术；
- 类似的问题首先考虑动态规划，设计动态规划的状态及转移；



#### 2. King's Circle

##### 0) 问题描述

该问题可简化为，在二维平面上的n个点，求其中所有可方的三个点的组合数；可方是指，三个点可以用一个正文形依次穿过（正文形与x、y坐标轴平行)，三个点位于该正文形上（即位于顶点或者边上，但不包括正方形内部或外部）；

##### 1) 解题思路

拿到这到题，首先想的是可方的条件；很容易推算出，如果三个点出现以下情况：$A(x_1, y_1), B(x_2, y_2), C(x_3, y_3)$满足:

$$ x_1 < x_2 < x_3 且 y_1 < y_2 < y_3 $$ 或者 $$ x_1 < x_2 < x_3 且 y_3 < y_2 < y_1 $$

时，三个点一定不可方；那么问题就变成，所有三个点的组合减去所有不可方的组合，即得到问题的解；

想到这点很容易，难点在计算不可方的组合数；

一开始，注意到上述规律，采用如下动态规划转移方程计算：

$$ S(n + 1) = S(n) + F(n) $$

其中，先将n个点按照其坐标排序，得到一个从1到n的点序列数组；那么记到第n个节点之前的不可方可能数为$S(n)$,则$S(n+1)$可以迭代计算，而$F(n)$则表示包含当前点$C(x_c, y_c)$在内，在第n个点之前的所有$x_1 < x_2 < x_c, y_1 < y_2 < y_c$的两点组合（另一个方向上的用类似文法计算）；

然后F(n) 的计算似乎也可以迭代计算；这样一来，貌似找到了问题的求解方法；但仔细一想，才发现不对；出问题的关键点在于，如何计算小于给定点的已访问节点序列的个数，无论是一维还是二维的；

然后我就陷入了一个思维循环，始终想用动态规划解决这个问题，但在数组组织的结构中始终又得不到该问题的求解；耗费了大把的时间；

无果后，我参考了答案，才发现这个问题其实可以转化为线段树的问题；应该说，二者本质上是相同的，但我因为陷入的误区始终没有联系到这一点；

求解一个区间内已知点序列及其个数需要用线段树模型来解决，如果是二维或更高维的话，可以使用kd树或者range树算法解决；这道题里，只要用到一维的线段树就可以了；

另外一个误区是，我只想到了从三维降到二维再降到一维的动态规划算法，但实际上，如果我们从中间的点B开始考虑，那么所有的不可方点就可以表示成：

$$ Sum = \sum_{i = 0}^{n} ld(A_i) * ru(A_i) + rd(A_i) * lu(A_i) $$

其中$ld, rd, lu, ru$分别表示位于点$A_i$的左下方、右下方、左上方、右上方的所有的点个数，问题便可借助线段树迎刃而解；算法复杂度为$O(nlogn)​$; 

##### 2) 总结

- 学会归同思想，将看起来陌生的问题转化为已知的问题；
- 学会从中间考虑问题，降维或者升维的思想固然重要，当从中间向两边扩展的思想方法同样需要学习；
- 熟练掌握一些经典算法和模型的求解，比如这首题中的线段树；

在编程中，借鉴了Benq的代码，他用极少量的代码量就实现了计数，而并没有明显的建树过程，而仅是借助了树的结构；以下是关键代码：

```c++
ll cnt_rank(int k) {
  ll res = 0;
  for (; k > 0; k -= (k & -k)) res += cm[k];
  return res;
}

ll search(int l, int r) {
  return cnt_rank(r) - cnt_rank(l - 1); 
}

void update(int k) {
  for (; k < LARGE; k += (k & -k)) cm[k]++;
}
```

其中，search时根据线段树来考虑，[0, r]区间内的所有数就是输出从根到查找节点路径上向右转节点左边的所有数的和；即上述代码中实现的search和cnt_rank函数；而对于一个新节点，使用update更新计数，即更新到所有会向右转的节点的计数（计数加1）；非常简洁漂亮的借助线段树思想而不用线段树结构地实现了这个问题的求解；需要向他学习；

## 2018-12-14

### 一、C++错误记录：

#### 1. sort错误

sogou-coding项目的flash_sort子项目遇到如下错误：

```c++
sort(bks[i].begin(), bks[i].end(), cmp_cs);
```

其中，bks是vector<char\*>类型的array，每一个bks[i]对应一个vector<char\*>的容器；cmp_cs为进行两个char*类型比较的函数；

该函数在运行前414269个bks[i]时都没问题，在第414270个时遇到了如下所示错误：

![error_flash_sort](D:\gjx\daily_study\photo\error_flash_sort.jpg)

奇怪的是，使用如下代码访问bfk[414270]时：

```c++
for (auto& it: bfk[414270]) {
    prt(it);
}
```

结果是正常的（其中，prt为打印当前字符串到换行符为止的所有字符），并且没有出现上图中最后几行的奇怪字符；

更奇怪的是，当我使用稳定排序时，这个错误就消失了，即把代码改成：

```c++
stable_sort(bks[i].begin(), bks[i].end(), cmp_cs);
```

尚未定位原因，在此记录一下。



## 2018-12-27

### 一、Kickstart Round C 2018

#### 1. Planet Distance

##### 0) 问题描述

该问题是图算法问题。保证一个全连通图有且只有一个环路，求图上所有点到环的最短距离。

##### 1) 思路

分两步：首先是找环路。我用的方法是从任意一点做DFS，当记录路径中第一次找到路径中已有的点时，则该点作为起点，依次输出此后记录的节点即找到环；

以环节点为初始节点集，按照dijsktra算法的思路，依次扩展最短路径直到全图，输出即可。

##### 2） 总结

思路很简单，但实现算法的时候还是不太熟练，对图中的一些基本操作不够老练；

- 图的数据结构，一般用到两种，矩阵和邻接表，矩阵需要空间大，很多时候会超出题目限制，邻接表可以用vector<vector<T>>的形式实现，并不复杂；

- 图的遍历算法，DFS和BFS，我尚不能熟练地将两种算法倒背如流地写出来，总是临场发挥，按照题目的要求写出新的遍历模式，这其实也没什么，只不过实现的过程有点久，需要想些方法加快实现的过程；

- 容器的erase坑又进去了一遍，即如下形式的代码：

  ```
  for (auto& it: v) {
      v.erase(it);
  }
  ```

  在容器遍历时又同时对其元素进行修改，很容易出问题，切记不要再踩坑；

- 在实现第二步时，对于扩展的算法实现了很久。对环路初始点用set集合实现，这没什么疑问，但接下来需要考虑将剩下的与初始点距离为1的所有点全部加入set，然后再考虑与新加入的set距离为1的新的set，如此下去，但重复量有点大，因为每次都会在老节点上判断一次，然后两个set集合同时扩张；

  最后实现时是这样考虑的，已扩展set集和未扩展set集，每次遍历未扩展set集中的点，当发现有路径到已扩展set集时，则将其加入扩展集县城计算距离。



#### 2. Fairies and Witches

##### 0) 问题描述

用矩阵表示的图，图表示n个点相互的连接方式，矩阵元素A[i, j]表示第i个点和第j个点间有一条长度为A[i, j]的边。在这些图中选取一些边组成凸多边形。限制是，每选取一条边时，确定该边的两个点，与这两个点相连的所有边都会消失不可选取。求所有可选取的组合数。图不存在自环，图为无向图。

##### 1) 思路

开始时看到题目中15这个最大图限制时，马上想到了bitmask技术，想用bitmask中16位图每一位表示一种状态，最后证明我是想多了，这题不需要bitmask也无需bitmask，只要暴力时有序即可。

这样进行考虑，每次从未选取点中选取一个最小的点k，k之前的点已经被选过了，在点k相连的剩余边中遍历选取每一条边，以及考虑不选取点k的情况(这点很重要，因为点k也可以不选取，这样才能覆盖所有的可能性)；去掉选择的边对应的点，更新不可选取点和边情况。继续进行下去。

由于在每一轮选取k时，下一个点的选取是遍历的，因此选择的边不同也保证了遍历的是不同的可能性。此外，因为是按照从小到大选择的点k，因此任意一种可能性，仅会被遍历一次，保证了结果不会重复。

最后，选取出来的点是否可以组成凸多边形，这倒是不难想到，根据三角表不等式可以很容易扩展到凸多边形。至此，这道题算法是解决了，使用我想到的算法，复杂度应该是：

$ (n + 1) * (n - 1) * (n - 3) ···  * 2$

相当于$ \sqrt{16!} $， 其结果并不大，可以在规定时间内得到答案。

##### 2） 总结

代码实现起来比第一题简单，回溯就可以了，需要注意的就是，一定要考虑第i个点本身不选的情况，否则会遗漏可能性。

#### 3. Kickstart Alarm

##### 0）问题描述

这相当于是一道纯数学计算题，设计规定时间内的算法计算大数。题目可以翻译成这样。给定N个元素的数组a及数K，求下列式的值：

$$ E = \sum_{i = 1}^{K} \sum_{s \subset {1, 2, ... , n}} \sum_{j = s_1}^{s_n} (a_j * j ^ i) $$

上式中，s表示{1,2, ... , n}集合的一个非空连续子集合，即记录a中元素位置的集合。

##### 1) 思路

由于大数限制，直接计算数组a的所有连续子集合，暴力算法行不通，所以需要对计算形式进行转化。思路过程省略，最后得到计算形式如下：

$$ E = \sum_{i = 1}^{n} ( (N - i + 1) * a_i * \sum_{j = 1}^{k} \sum_{m = 1}^{i} m^j ) $$

到这一步，再利用等比数列求和及除法模余算法，即可计算出E。预存1~n除法模余大数(10e9+7)的值后，总的复杂度为$O(NlogK)$; 

##### 2) 总结

这道题想到之后就不难了，有以前计算除尘模余的经验，很快就能实现该算法。

* 模余的基本性质；
* 费马小定理；
* 二分法计幂次模余，参见[2018-11-20](#2018-11-20)；
* 等比数列求和；

以上这些知识要能熟练掌握。



## 2018-12-28

### 一、 Kickstart Round D 2018

#### 1. Candies

##### 0) 问题描述

最大连续和问题的加强版，给定N个数的数组${a_n}$，以及数D和O，要求：

* 连续子序列的和不能超过D；
* 连续子序列中奇数个数不能超过O；

求解满足限制条件的和最大的连续子序列；

##### 1) 解题思路

普通最大连续和算法我还是知道的，$O(n)$时间内可以得到答案。于是，对于这道题，我以为可以完全如法刨制。即用动态规划的思想。

先看我理解的普通最大连续和的算法。区间【1，N】的数组中，最大的连续和无非有以下两种情况：

* 以元素$a_N$结尾；
* 不以元素$a_N$结尾；

对于每二种情况，其值可以保存，并且不会需要在扩展到N+1时再判断；对于第一种情况，无非是：

* 加入元素$a_{N+1}$计算和；若和为负，说明此前的和可舍弃，重新从0开始计和。

然后是取两种情况中的较大者为【1，N + 1】中的最大和。

那么，对于这首题，我类推地想：

* 以元素$a_N$结尾的满足条件的最大和，扩展到N+1时，同样需要寻找以元素$a_{N+1}$的满足条件的最大和，方法是加上$a_{N+1}$，然后从上一个满足条件的区间（指以元素$a_N$结尾的最大和，记为[l, N]）向后递增（递增l直到N+1)，直到寻找到新的满足条件的最大和。

这即是针对第一种情形的在本题条件下的类推。

##### 2) 误区

1)中的算法思路上是没有问题的，使用上述算法后，小样本也成功通过。然而，在大样本上遭到了拒绝。仔细分析了一下，发现如下坑：

**大样本中存在负数，本来这也没什么，因为最大连续和的思想就是针对负数的，但因为加入了特定限制；导致连续和是负值也是应该保留的，区别于原算法和负舍弃；**

于是，对于元素$a_{N+1}$结尾的情形，在上一个满足条件的区间上递增就是不对的，因为还需要考虑向前的情况，因为当前若为负值且满足条件时，我还应当向[l, N]中l的反方向延伸数组，找到最大和，这便利算法变成了$O(N^2)$的算法，失去了递推性。即每增加一个元素，需要从该元素往前扩展寻找满足条件的最大和。

在此又遇到一个坑，重点记录一下。在意识到上述这点时，我曾天真地以为，只要在原区间向前再扩展到第一个不满足条件限制的时候退出就可以了，实际上上述这种情况会无限循环直到起始点。因为即便【ll, N] (ll < l, 为从l 向前扩展到第一个不满足条件限制的点)，区间不满足，也不能保证【ll - 1, N]一定不满足条件，因为存在负值。在这里，处理奇数限制和处理最大和限制的方法也不一样了。

原先就是太想将这两个限制统一起来，所以才会遇到这样的坑。陷入这个坑后，我又跳不出来了，觉得算法没问题，但结果就是不对。最后还是看答案才解决的。

##### 3） 总结

这道题基于最大连续和，但又存在不一样的地方。我需要意识到这个不同之处。最大连续和算法之所以适用，有以下条件：

* 求和没有上限，那么最后的结果一定为非负数，因为不选就已经是0了；这使得递推时无需考虑值为负的情况。也使得递推时无需考虑向前的情况。

而这道题递推性不成立，就在于限制了上限，这使得上一次保存的最大连续和区间不一定是因为和最大被保留了，而是因为和最接近上限才被保留了，此前可能存在和比他大但超过上限被删除的情形，如此，向后递推就不成立。并且，向前的情形会一直延续到起始点（另一个奇数限制导致此种情形会受限制，但极端来说确实会延伸到起点。

于是，最终算法需要设计成$O(NlogN)$才能完成大样本测试，最后实现时借鉴了参考的答案中的算法，预计算数组连续和（从起始元素开始累加至各元素形成的和数组），这样，连续区间可以由端点和相减得到，再借助set的数据结构，将连续和存入成排序数组，即可快速查到到当前点的最大连续和了。不再详述。

#### 2. Paragliding

(Add: Jan. 9th, 2019)

##### 0) 问题描述

简单说是平面区域覆盖问题。给定塔点$T(x, y)$，则认为其覆盖一个三角区间，区间端点依次为$L(x - y, 0)$, $T(x, y)$, $R(x + y, 0)$；处于此区间的点O，包含边界，则认为点O为T覆盖。

当平面上有多个塔点${T_n}$时，其覆盖区域会相互叠加成为新的覆盖区间，问：给定待查询点集${O_n}$中，有多少个节点为${T_n}$覆盖。

##### 1) 思路

一开始拿到这题时，我想到了线段树，因为每个塔点对应一个y=0上的区间；每个点集中的点x坐标可构建成一棵一维线段树。但后来仔细想想，无论是按搭点或是待查询点建，都无助于将算法复杂度降低到log。

于是，回到最容易想到的思路，人在做这道题时，可以直接将覆盖区域求出来，然后每个点在不在区域内也就一目了然了。这样做的复杂点在于，如何确定区域与新塔点的交点。最后的覆盖区域由一个有序的交点集构成。最终的结果也证明，这个思路是对的。

##### 2) 教训

很快按1)中的思路实现了代码，但调试过程并不顺利，遇到了一些坑。

* 一开始读入数据时没有按照题目要求，写错了一个字母；因为需要读入的变量较多，行之间是copy的所以导致了这个错误，以后要首先保证讲话数据正确；
* stl容器问题。又一次遇到了erase和insert导致iterator不正确的问题。当插入或删除一个元素时，有可能导致原先iterator指向的元素值发生改变，从而给程序带来bug。因此，在程序中使用iterator时，不要进行插入或者删除操作。这些操作应当在不使用iterator时批量进行，这样做同时也可以提高效率。
* 考虑问题不全面。在建区域图时，没有考虑清楚可以直接插入塔点的三个端点的情况。一开始我只判断了当塔点大于或者小于已有区域点的情况，没有考虑中间情况；花了很长时间才意识到这一点，然后，我直接使用大于塔点的区域中的第一个点和小于塔点的第一个点是否相邻来决定，然而这仍是不对的，最后改成两个点的y坐标为0，程序才最终通过。

实现过程中也自己总结了一些经验：

* 由于交点可能存在小数，但因为塔点都是整数，且线段间与x轴的夹角都是45度，因此交点的小数值仅有0.5一种可能。所以将交点值乘2表示，就可以不用考虑浮点数的问题了。
* 求解两个线段的交。涉及到一些简单的几何知识。

由于在debug时很无助，所以查看了答案中的做法，它并没有求交，而是使用了如下思路：

* 塔点按x座标排序；
* 计算没有覆盖塔点的情况。即$T_1$完全为$T_2$所覆盖，则$T_1$可以从集合中去除；
* 最后得到相互有交集，但无覆盖的塔点集；
* 查询时只要考虑与当前点最近的两个塔点的关系即可。

#### 3. Funniest Word Search

##### 0) 问题描述

给定矩阵$A[m][n]$，每个元素是一个大写字母，并给定一个单词集$W_p$， 每个元素为一个单词。考虑包含于区域[m1, n1, m2, n2]的包含于A的子矩阵。记

Y = 该区域的行和列中出现单词集中某单词的次数 * 该单词的长度；

L = (m2 - m1 + 1) + (n2 - n1 + 1); 

F = Y / L

单词逆序出现在行和列中也要计算一次次数。求对于所有区域的最大F值，及最大值出现的次数C，对应于最大值的最简分数$Y_0/L_0$；

##### 1) 思路

开始思考时，首先想到用动态规划算法解决。考虑的方向是实现$mn$级别的算法，因为暴力算法是$m^2n^2$，题目中的对应量为100，于是会出现亿级别的运算题，我以为这是不允许的（因此也导致我直接排除了暴力算法，实际上这道题完全可以使用暴力算法求解）。我之后使用减1法考虑相互间的关系。但开始时将行和列一起考虑，始终没有想到在大集合下一起解决的算法。想了大概三小时后仍然无果。于是借鉴答案的思路，方才豁然开朗，仅考虑行出现和列出现的话，动态规划的思路方才可行。

另外一个让我觉得这道题棘手的地方在于，缺少之前二维矩阵如何动态规划的经验。在学习到了题目的思路后，学到了这方面的常用思考方法。

##### 2) 总结

最后按照答案中的方法实现了算法，总的来说，是在暴力算法中加入动态规划以减少重复计算量。有以下几个点可以学习：

* 将查询单词组织成树，这是将程序从一个case耗时5秒提高到0.5秒的关键，虽然直接查也足够快；

* 在这里，由于单词可以逆序出现，使用一个小技巧，直接将单词的逆序也加入待查询字典中即可，这样考虑行或列包含时，仅需要考虑按顺序的情况；

* 仅考虑行包含情况时，有以下关系式：

  $$ S(i, j, k, m) = S(0, j, k, m) - S(0, j, i - 1, m)$$

  这给了我们两点提示：1. 减少存储和计算量，存储和计算量从亿级降到百万级；2. 仅计算从0开始的所有情况已然够；上述公式转换后也同样可以用于简化列包含的情况。

* 那么如何计算行或列包含下的$S(0,j,k,m)$呢？这个时候使用减1法考虑相互之间的联系。从$S(0,j,k,m)$到$S(0,j,k,m+1)$，我们需要计算所有新加入的第m+1列中的元素，而增加的则是所有以这些元素结束，长度不超过新区间长度的元素。这提示我们需要计算$L(i, j, k)$，表示以元素(i,j)结束，长度不超过k的单词长度和（按Y的计算方式）。

* 于是进行到$L(i,j,k)$的计算问题，这同样可以使用减1法递推:

  $$ L(i,j,k+1) = L(i,j,k) + W(i,j,k+1)$$

  上式中，W(i,j,k+1)表示，以(i,j)结束的，长度为k + 1的行字符串是否出现在字典中，若出现，则表示该单词的长度。这样，所有的子问题都可以计算了。

* 回到$S(0,j,k,m)$的计算，这个时候，直接加上所有新元素的L值，仍需要在每个循环内再加上k + 1次；但实际上从$S(0,j,k,m)$到$S(0,j,k,m+1)$值计算时，与$S(0,j,k+1,m)$到$S(0,j,k+1,m+1)$计算时，重复计算了一部分和，仅相差L(k+1,m+1,k-i+1)的部分。意识到这点，可以将$S(0,j,k,m)$的计算再降一维。

* 最后组合行序列与列序列的结果，即可知道区间S(i,j,k,m)的F值，暴力遍历每个可能即得答案；

从以上分析思路可以总结出以下几点：

* 当k <= 100时，$O(k^4)$算法可以在秒量级内计算得到；所以考虑问题时不要排斥暴力算法，从暴力算法开始思考，也是一种思路；

* 动态规划不一定适用于直接计算整个问题，但可以计算出其中某一部分。仅考虑行包含或列包含的情况，便很容易得到思路；

* 二维矩阵的一些计算方法。除了以上三维的行计算思路外，有时也可以降到二维的思路。即：

  $$ S(i,j,k,m) = S(0,0,k,m) - S(0,0,k,j-1) - S(0,0,i-1,m) + S(0,0,i-1,j-1)$$

  遗憾的是，这首题并不能使用，因为跨边的情况导致这样计算并不正确。但很多其他题目可以用到。

* 灵活使用动态规划简化计算过程，核心考虑问题便是减少重复计算，已经计算过的量如果后续要用，那就存起来。

最后再说一下debug中花费时间许久的一个bug。

* 计算F=Y/L时，需要更新到最大值。通常使用乘法代替除法进行比较既可以减少运算时间，也可以防止浮点数带来的不正确性，是经常用到的一个技巧。此题中，初始化$Y_0=0$，$L_0=1$; 对于每一个区域中Y和L，判断条件变为: $Y_0 * L < Y * L_0$; 这本身没有问题，但隐藏的bug是int到long long的越界。我又是栽在了long long的问题上，调试了几个小时没找到问题所在，反复检查算法的设计，最后才发现问题出现在这么一个不走眼的地方。越界的意识真的是时刻要注意啊，他会给你带来意想不到的隐藏bug。 

最后，新学到的stl函数：

* std::__gcd(a, b)这个函数用于计算最大公约数，之前我是自己写的算法；
* std::reverse()这个函数用于将字符串等容器类逆序。

## 2019-01-09

### 一、c+=程序加速小技巧

因为之前感觉自己写的程序和别人的程序在运行时间上总有几倍的差距，即便实现的是完全相同的算法。所以今天做了一下这方面的总结。

#### 1. 加减代乘，乘代除

意思就是，能用加减法代替不要用乘；能用乘法代替不用除法。

#### 2. 位移代替乘除法

据说c++在编译时已经对这块进行了优化，将乘法自动转化为位移运算。但还是提醒自己，写代码时尽量用位移运算代替乘除法；

#### 3. 前缀运算代替后缀运算

++i比i++快，尤其当i是一个结构体时；

#### 4. 利用缓存机制

cpu缓存：合理的利用cpu cache可以极大的提高代码的运行效率(例如：数组中以每列遍历和每行遍历的效率的不同)，当然多线程环境下也要考虑cpu cache带来的影响。

####5. move操作深拷贝

std::move操作: 当不得不进行深拷贝时，如果深拷贝数据源在拷贝后就不在使用，尽可能的用move操作代替，或者在参数传递时用move操作代替临时的实参变量。

## 2019-01-10

### 一、Kickstart Round E 2018

#### 1. Yogurt

##### 0) 问题描述

Lucy有N个Yogurt，第i个Yogurt有过期时间$A_i$，表示今天开始的第$A_i$天后过期；而Lucy每天最多只能吃K个Yogurt，问Lucy能吃这批Yogurt的最大值。

##### 1) 思路

这道题相对来说比较简单，将Yogurt过期时间排个序，使用贪心算法，将过期时间较早的先吃掉；计算最终结果即可；

##### 2) 总结

实现一遍过，没有遇到编译和调试问题。

#### 2. Milk Tea

##### 0) 问题描述

给定二进制字符串数组$A_n$，每个元素是一个由0和1组成的字符串，长度为L；表示n个人对yogurt的L个不同选择喜好。再给定相同类型的数组$L_m$，表示对商店能出售的yogurt类型的限制，每一个$L_m$中的元素表示商店不支持该种选择。求：二进制字符串S，使得S不被限制（即不在$L_m$中），且与$A_n$中每个元素的编辑距离的和最小。A和B编辑距离在此题情况下是指，A和B所有元素不同的位置个数。010与011的编辑距离为1，000与111的编辑距离为3；依此类推；

##### 1) 思路

这道题算法不难想到。首先需要考虑的是，在没有限制条件下，找到解S。很容易想到，对于$A_n$中的每个元素，我们以数位去考虑，第i位中可能有$Z_i$个人选择0，$O_i$个人选择1，$Z_i + O_i = n​$，那么，为了最终尽可能少修改，我们当然应当选择这个位置中出现较多的那个。从而找到最优的解S；

接下来考虑，如果S在限制集中呢？很显然，下一个应当是由S经过最少改动即可得到的字符串；由于改变S的第k位的代价是$|Z_i - O_i|​$，因此，我们只要选择其中最小的一个即可。那么再往下呢？依然按照改动最少的思路，我们借助于multimap的结构，每当做出一个选择，便将这个选择所有只改变一次会生成的下一个字符串及其距离记录，并存入map中。当需要做出新选择时，从set中取出最小距离及其字符串即可。

##### 2) 总结

这道题整体来说做的很快，没有太复杂的过程，主要有以下两点在调试过程中改正：

* 集合去重的情况，最终实现时是用multimap的数据结构，key是距离，value是字符串，那么，需要避免相同字符串重复入map；有很多种做法，最终采用记录初始S的做法，在选择新的字符串入栈时，不考虑已经改变了位置上的改变即可；
* 本题中输入是字符串，虽然某个位置仅由0和1构成，但!a并不能使字符串‘0’变成字符串'1'，或者相反；我犯了这个错误，所以一开始没有得到正确解。以后需要注意这类的错误，不要想当然。

#### 3. Board Game

(supplement this part at date Jan. 16th, 2019)

##### 0) 问题描述

原问题可简化为如下叙述：考虑两个3 * N (N <= 5)的数组A和B。把B随机分成三部分，每部分有N个元素，但此时并不知道B的具体分布。此时我们需要考虑把A也平均分成三部分，每部分有N个元素，使得至少有两个部分的总和大于对应B的部分的总和；此时称A获胜。问题是求解A最大的获胜概率，即求A采取某种分布后获胜的概率中的最大值。

##### 1) 思路

一开始被“田忌赛马”的故事代入，采用贪心算法的思路处理这道题，我是这样想的：既然获胜要两部分胜出即可，我只需要将最小的值通通放入最小的一部分，使另外两部分极大化，这样就能保证更多的B的可能分布小于这两部分，从而极大化获胜可能。至于剩下的两部分，可以使得和尽可能接近。

按照这个思路写完代码在N<=3的小样本集上测试都没有通过。此时才反应过来自己被套路了，贪心算法并不能用。于是开始考虑遍例所有的可能性。按照暴力算法，罗列A和B的所有可能数，找出A获胜最多的即可，但此时算法复杂度是$(C_{15}^5 C_{10}^5)^2 = 756756^2$，时间复杂度不能接受。于是想到，至少两部分大于算赢的话，可以用容斥原理解决。记A的其中一个和分布为$(U_1, U_2, U_3)$，B的所有和分布为{$(A_i, B_i, C_i)$，则：

$S(A > B) = S(A_i < U_1, B_i < U_2) + S(A_i < U_1, C_i < U_3) + S(B_i < U_2, C_i < U_3) - S(A_i < U_1, B_i < U_2, C_i < U_3)$

上述S表示满足条件的所有可能数。对于至少两部分小于的情况，用动态规划就可以解决，类似于[2018-12-28](#2018-12-28)中Funniest Word Search的求解。按照A的分布，动态规划计算至少两部分小于的情况。但复杂的是三维的情况，并不能直接应用动态规划得到解决。

一开始我是用multiset的方法，类似于解决二维的情况，由于计算时，在第三维方向上值是递减的，所以能满足的三个都小于的情况沿着x轴或者y轴方向的可能数都会减小。类似于动态二维计算，先计算每列的新的可能数，再在计算每一行时，用一个初始化空的multiset，依次插入当前列的剩余的第三列的数，再减去其中超过限制的部分，得到B所有分布中三个都小于A当前分布的可能情况数。

虽然算法是正确的，但遗憾的是，时间复杂度过高，在最坏的情况下仍然可能是一个$O(N^2)$的算法。

于是我意识到我现有的解决方法里只剩下线段树和k-d树解决三维的这个问题了。我一直在想直接用动态规划计算的方法，因为总觉得可以这样解决，但想了许久依然不得解。无奈，我参考答案的解法，却发现它并没有采用动态规划，确实是用线段树的方法解决。

最后，我实现了一遍线段树，以前只停留在理论上，现在终于自己实现了一遍。其实并没有原先想像的那样实现复杂，反而是写起来特别简单，因为相关的函数具有相似的结构。调试之后，终于解决了问题。

##### 2) 总结

思考这道题时大部分时思路都是正确的，主要错误在于太纠结于贪心算法及动态规划。由于这道题贪心算法错误的反例一开始没有想到（也确实有点难构造）；导致我从一开始就走了弯路。另外在计算三维计数时，太执著于用动态规划的方法解决，导致浪费了很多时间。

既然意识到线段树可以解决，就不该纠结于其实现复杂而不采用，而一直浪费时间在思考动态规划的计算方法上。思路上的误区有时是最难调整的，要提醒自己多注意。其他的对于这道题编程上的一些总结：

* 预存储技术，计算组合数，用数组保存；基本已掌握；
* long long的范围思考，好在仔细计算过，没有越界问题；
* 遍历所有可能分布的和；在这里按照排列递增的方式遍历所有可能；
* 学习到了std求和函数，与python中的reduce很像，头文件#include<numeric>中accumlate(begin, end, ini, func)；
* 一维线段树和二维线段树的编写实践，进一步加深对此数据结构的了解。

## 2019-01-18

### 一、Kickstart Round F, 2018

#### 1. Common Anagrams

##### 0) 问题描述

A和B是Anagram是指，字符串和B的组成相同，顺序可以不同；这道题的问题是，给定字符串A和B（均由26个大写字母组成），求解A中有多少个连续真子字符串可以与B的某个连续真子字符串构成Anagram？

##### 1) 思路

解题方法不难想。由于所有字符串只有26个大写构成，字符构成可以由长度为26的数组表示。按照题目要求，首先需要对字符串B进行预处理，处理B的每个真子字符串；可以将所有真子字符串排序后用map存储。这里我用了另一种方法，自己构建查询树。第一层表示A的个数，第二层表示B的个数，依次类推；每一层会有多个子节点，每个节点存储数值V，表示该节点有几个当前值。比如第一层中有三个节点，其V值分别为0、1、2；表示三个不同的字符串，其中分别含有0、1、2个字母A。

按照这样的方法构建树后，对于A的每个查询，最多不会超过查询字符串的长度，于是，解法是一个$O(n^3)$的算法，对于本题最长的L是50的限制，绰绰有余。

##### 2）总结

这道题如果用std::map容器实现会更为简单，自己写树实现使自己更加清楚了一些指针和树的实现细节。在表示子节点时用了vector，这是考虑到如果定长为26，深度为26的树很快就会超过了；所以用vector节省空间。

#### 2. **Specializing Villages**

##### 0） 问题描述

给定图G=(V, E)为简单图，不存在重边和自向边。给V中的每个节点分别染上黑白两种颜色，这样，每个黑节点到最近的白节点的距离称为补色距离，求所有节点补色距离和最小的染色方案，由于最小的方案可能有多种，题目最终要求输出的是所有最小染色方案的个数。

题目中提供了限制条件，一是保证必然存在最小染色方案，使得任意一点都可以找到补色点；二是E中的每条边的长度都不相同。

##### 1） 思路

这道题绕了些弯。一开始想着按照dfs的思路，因为我注意到这样一个事实：任意一点V的邻节点中至少有一点与V异色。这是因为，如若不然，记V的当前补色距离为K，则K必须经过V的一个邻节点O后才能到达，即K>dis(V, O)，此时，我只需要将V改为相反的颜色，则必有新的补色距离$K^{`}<K$，而其他点的补色距离均只会更小，于是得到更小的补色方案，与前提矛盾。称这个结论为限制1。

于是，我以为可以如下遍历：从节点1开始，于其子节点中先选距离最短的点作为异色，之后遍历整棵树；再按照距离顺序依次遍历，然后之前已经遍历过的节点置为与1同色；由于限制1的存在，可以去掉一些度为1的节点的重复遍历。但很显然，对于完全图，算法复杂度依然是爆炸的。而且，实现过程有些复杂，最重要的是，居然在测试集上的结果也不对。

不过也幸亏是在测试集上就发现了错误，让我很快定位到错误。原来两个节点的距离可以是0，但即便是0，题目中也指出这两个依然算是不同的节点。于是，限制1的结构就不在正确了，也导致这样做会减少可能性。并且由于完全图的算法复杂度会超，以及下面这个事实：当前点选的补色点不一定是它的邻节点，这使得第一种思路很难进行下去。

我开始考虑改进算法，很显然，题目中每条边的长度都不相同已经给足了暗示。我顺着这条路思考，终于想清楚了问题的关键，为了找到最小方案，使用加1法考虑，对已经有的子图$G_0$中的点，假设其已经找到了最小方案，那么，新加点如何才能找到其最小补色点，并且加入之后保证新子图仍是最优方案？按照边长度排列。

从最短边开始，选择其两端端点异色，则此时得到第一个最小方案，之后加入的点时，由于其边长必然大于已经在图中选择的边，且为剩下的边中的最小，因此不可能存在跨邻点方案使其补色距离更小；于是算法可以实施。

##### 2) 总结

在实现算法过程中，还是有很多细节的地方需要注意。一是，由于存在距离为0的邻节点，那么当前节点不一定要与子图中的某个点异色，当子图中的某个点补色距离为0时，需要考虑新加入点的两种可能性；

其二，不能直接在最终判断处对方案简单进行加加计数就完了，这道题最终的染色方案会超过int的限制，如果每个方案单独加加肯定是超时的；在这里，需要注意到染色方案的对称性这一点，这样很快就可以得到最后的答案；

其他一些总结：

* 在写遍历的时候，递归程序调用另一个程序再调用回自己时，写在main前会出错；应当先在main前声明，之后在main后实现；
* 由于对图的遍历算法还是不太熟悉，在dfs时，递归的终止条件在哪写想了很久；需要单独训练一下自己书写图遍历算法，减少应试时间。
* 题目算法几乎都能想到，但花费的时间还是有点多，需要考虑方式减少思考时间，加快算法思考过程。

#### 3. **Palindromic Sequence**

#####0）问题描述

给定字符表长度为L，表示字符表中有从小写字母a开始的L个词，接下来的字符串都由字符表中的字母构成。考虑所有长度不超过N，由L中字符构成的回文字符串，将其按照字典序排序，求第K个字符串的字符长度。

例：L = 2, N = 3, K = 4；此时所有回访字符串按照字典序依次是：`a`, `aa`, `aaa`, `aba`, `b`, `bab`, `bb`，`bbb`;

第四个是aba，输出3；

##### 1）思路

与上一题类似，绕了许多路。首先，题目给我的第一反应是，我可以借鉴问题**Sherlock and the Bit Strings，参见**[2018-12-12](#2018-12-12)；

不同的是，这道题的长度最长是N = 1e12，显然用不到bitmask技术了；但计数思路应当是差不多的，可以借鉴；

于是，算法的核心依然是试填法，试填一位后看剩下多少。于是问题的关键点在于：如何知道给定前缀后，以该前缀开头会有多少个回文字符串？

这个问题有点难，直接想我没什么思路，于是绕去想别的方法，但绕来绕去又绕回来了。迫不得已，我才决定在这个点上下功夫。其实回方字符串本身的规律性是足够强的，最容易注意到的事实就是：L个字母，长度不大于N的所有回文字符串总数，一定是以a开头，长度不大于N的所有回文字符串总数的L倍；这是字符本身的对称性，这提示我们尝试寻找L个字母，长度不超过N的所有回文字符串总数。

这个问题不难想出，记S(L, N)表示这个问题的解，再定义P(L, N)表示由L个字母，长度恰为N的所有回文字符串，则显然有：

$S(L, N) = \sum_{i = 1}^{N} P(L, i)$

同时，$P(L, N)$容易用加一法得到，有以下关系：

$$P(L, N + 2) = L * P(L, N) $$

初始条件是P(L, 1) = P(L, 2) = L；于是，S(L, N)的计算可以搞定了。

此时，注意到N最长是1e12，想到两个事实，一是不可能真的代入N=1e12进行计算，即便单单for循环到这么大的数也已经超时了，题目中存在简化的条件；二是，由于K最大也只会是1e12，也就是说，我们只要考虑小范围内的S(L, N)即可，大N需要转化到这个小数据集上考虑；为避免重复计算，需要预存储技术；

在这里需要注意的是：S(1, N) = N，且因为N过大，不应该计算L = 1的情况，其他情况依次计算到第一个超过1e12限制的数保存即可。

解决了S(L, N)，但给定前缀有多少仍然没解决。记M(x, L, n)表示给定前缀字符串x，剩余填不超过n个字符的所有可能字符串的总数（注意，这里需要考虑不填的情况）；

于是，将M(x, L, n)与S(L, N)联系起来。此时，思考了一会注意到：记x的长度为$l(x)$，我们在字符串末尾倒过来写x，即构成x的逆序，则中间剩余的$k = N - 2 * l(x)$位，只要是回文串就满足前缀条件，因此有：

$$M(x, L, n) > S(L, k) $$

于是，两者有了一个联系，这点也同时提示我们，虽然N可以很大，但要找到第K大的，即便L只有2，我只需要考虑不超过100个字符串即可，其余的位置全部填充a，因此无需考虑那么多，时间复杂度的问题也就可以解决了。

但M(x, L, n)必须给出具体计算方式，才能真正解决这道题。这又是一个花了不少时间才解决的点，其实没什么好的办法，就是硬算就可以了。以aba前缀为例，其接下来第一个回文串一定是aba本身，然后是ababa，abaaba，之后就变成了S(L, k)了。这告诉我们，需要解决S(L, k)没有解决的部分。

在这里有两个事实后续需要用到：一是，前缀本身如是回文字符串，则其一定是M(x,L,n)中的第一个字符串。二是，除了本身外，其他S(L, k)未计算到的字符串，不一定小于所有S(L, k)中有的字符串。

回到计算S(l, k)未统计部分的问题，注意到，这向是两个对称字符串相互向对方靠近的过程，我只需要花费$O(k^2)$的时间依然判断每个位置是否是回文串即可。由于真正需要考虑的k实际上很小，放宽估计不会超过100。因此可以这样计算。

于是，整个题的算法框架到此算是全部实现了。

##### 3） 总结

想完算法花了不少时间，实现加调试同样花了不少时间。总结一下坑：

* 计算S(l, k)未统计问题时，需要考虑带很长的前缀a问题，即前缀都由a构成，但其长度甚至超过int的限制，因此，不可能用平方算法计算这么长的前缀的未统计部分。不过幸好有规律，我只需要考虑前缀中相同长度的一部分即可，超出部分的可以全部计算。具体算法不描述了。

* 判断前缀x是否是回文串，与上一部分类似，由于加上了很长的前缀a，与小样本的写法也会不同；需要同时兼容pref长度小于x长度以及大于甚至远大于x长度的所有情况；

* 在小样本实现中，我甚至可以输出全部字符串，因为N <= 100；但大样本不允许这样，这时需要我们判断算法进行到什么时候就可以输出结果了。这又是编程时一个耗时点了。容易想到，我只需要考虑不勃勃N - pref * 2的长度即可，但中间的字符串如何提示我们构成最终答案呢？因为存在虽然给定了中间字符串，但以当前pref+中间字符串开关的新前缀，以新前缀开关的所有字符串数不一定为1。那我们应该选谁？

  想了一段时间才明白，记新前缀开关的所有字符串总个数为r，则r不等于1的情况仅可能在中间字符串全部是a的情况下才可能。很容易证明，不再详述；这样的话，问题就可以解决了: r > 1，提示我们答案全部由a构成；r == 1，提示我们找中间字符串的最长子回文串，加上两倍的pref长度即得解。

* 最后又是long long问题。这又使我花了不少调试的时间。在此再总结一下long long的点：

  * 读清题目要求，设计算法时需要考虑有没有超过int限制，是否需要用到long long；
  * 读清数据读入要求，读入的数是否需要long long接收。
  * scanf的时候，需要写%lld来接收long long, %d会出错，这道题就在这出错，cin时没有这人考虑；
  * 传入参数，返回值的类型定义，同样需要考虑long long问题；此题我同样犯了这个错误，long long的数值传入int参数类型，导致很隐秘的bug发生了。
  * 写乘法要注意，两个int的数据相乘会不会越界；另外，如果想用两个int相乘得到long long的数做法也是不可取的，必须要先转换。比较省时间的做法是，定义的时候就不用int定义，直接用long long；以前犯过在条件判断时用过int * int < int * int的情况，出错的原因就是数据越界了。
  * printf输出时同样用%lld，以前犯过类似的错误。



## 2019-01-22

### 一、leetcode总结

#### 1. First Missing Positive

问题是找一串数组中第一个丢失的正整数。即给一个数组{an}，找到正整数集中第一个不在{an}中的正整数。

算法要求是：O(n)的时间复杂度和O(1)的空间复杂度。

对于这道题的算法思考，我经历了以下几步：

* 桶排序，找到第一个空桶输出即可，时间复杂度为O(n)，但空间复杂度亦为O(n)；
* 先用一轮排序，再遍历数组找到丢失的数，时间复杂度为O(nlogn)， 空间复杂度为O(1)；
* 直接开大小为n的数组，记录第i个位置是否有值，做法类似于桶排序，空间复杂度会超；
* 第三个方法给了我提示，为什么要开这个数组呢？直接在数组内部实现不就行了？于是得到最终的算法。

```c++
    int firstMissingPositive(vector<int>& nums) {
      int i = 0;
      for (; i < nums.size(); ++i) 
        if (0 < nums[i] && nums[i] <= nums.size() && nums[i] != nums[nums[i] - 1]) {
          int m = nums[i];
          nums[i] = nums[m - 1]; 
          nums[m - 1] = m;
        }   
      for (i = 0; i < nums.size(); ++i)
        if (nums[i] != i + 1)  
          break;
      return i + 1;
    }   

```

在编写的时候，特别需要注意的地方在于第一个循环中的if判断式，在这里改了很久，总结一下：

* 0 < nums[i]，否则会出现nums[m - 1]中秩为负的情况；
* nums[i] != nums[nums[i] - 1]，这个是为了防止与自身交换，以及对于[1, 1]的情况类型设置的，如果不加if的判断，会形成死循环；

另外需要在此重点说明的一个bug是：

**int\*开的数组不能用sizeof来指明数组大小，因为此时sizeof指向的大小是一个指针的大小**。

#### 2.  Trapping Rain Water

给定数组${a_n}$，表示当前地基的高度，当降雨量足够大时，求数组间最大的积水量。例如：

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

算法不难想，稍微花点功夫，在此记下，以便以后对于这类问题能够立刻实现算法；

```c++
    int trap(vector<int>& height) {
      int l = 0, r = height.size() - 1;  
      int sum = 0;
      while (l < r) {
        if (height[l] <= height[r]) {
          int csum = 0, i = 0;
          for (i = l + 1; i <= r; ++i) {
            if (height[l] <= height[i]) break;
            csum += height[i];
          }   
          sum += height[l] * (i - l - 1) - csum;
          l = i;
        } else {
          int csum = 0, i = 0;
          for (i = r - 1; l <= i; --i) {
            if (height[r] <= height[i]) break;
            csum += height[i];
          }   
          sum += height[r] * (r - i - 1) - csum;
          r = i;
        }   
      }   
      return sum;
```



## 2019-02-13

### 一、xshell 命令行快捷命令

| 命令     | 作用                                 |
| -------- | :----------------------------------- |
| CTRL + d | 删除光标所在位置上的字符             |
| CTRL + h | 删除光标所在位置前的字符             |
| CTRL + k | 删除光标后面所有字符                 |
| CTRL + u | 删除光标前面所有字符                 |
| CTRL + w | 删除光标前一个单词                   |
| ALT  + d | 删除光标所在位置的后单词             |
| ctrl + ? | 撤消前一次输入                       |
| ALT  + r | 撤消前一次动作                       |
| CTRL + a | 光标移动到命令行开头                 |
| CTRL + e | 光标移动到命令行结尾                 |
| CTRL+ <- | 光标移动到前一个单词开头             |
| CTRL+ -> | 光标移动到前一个单词开头             |
| ALT  + u | 把光标当前位置单词变为大写           |
| ALT  + u | 把光标当前位置单词变为小写           |
| ALT  + u | 把光标当前位置单词头一个字母变为大写 |
| CTRL + s | 锁住终端                             |
| CTRL + s | 解锁终端                             |
|          |                                      |
|          |                                      |



## 2019-03-01

### 一、eval的使用

今天在用json加载单双引号混合的数据时出错，数据如下：

```
{'label': "{'song_3_8': '小兔子乖乖'}", 'text': '我要听小兔子乖乖'}
```

json不能加载单引号数据，因而如果硬用json加载的话，需要转换格式；或者使用一串split单独提取需要的数据，很麻烦。然后查到了eval可以直接处理这种类型的数据。使用：

```py
dd = eval(dstr)
print (dd["text"])
# 输出：我要听小兔子乖乖
print (dd["label"])
# 输出：{'song_3_8': '小兔子乖乖'}
```

## 2019-03-05

### 一、几种数据结构的总结对比：

#### 1 树状数组(BIT)

#### 2. 线段树

#### 3. 区间树



### 二、算法

#### 1. 插头DP

#### 2. CDQ分治





## 2019-03-06

### 一、Kickstart  Round G 2017

#### 1.  Huge Number

##### 0) 问题描述

给定三个正整数，A, N, P，计算$A^{N!}$模P。

##### 1) 思路

很明显可以意识到这题要用到[2018-11-20](#2018-11-20)中第三题中的大数幂次算法，这可以使复杂度降到O(nlogn)。



#### 2. Cards Game

##### 0) 问题描述

有N个卡片，正反面都有数字，分别用数组A和B表示，对N个卡片进行以下操作：

* 每次从卡堆中取出两个卡片，此时获得惩罚S，其值其中一个卡片正面数字A和另一个卡片背面数字B的异或，即： $S = A ^ B $；之后将其中一个卡片返回卡堆。
* 当卡堆中卡片数不足2时，游戏结束；

所有卡片正反面数字已知，每次可以按照自己的意愿选择卡片以及用哪张卡片的正面。求能获得的最小惩罚（即游戏结束时每轮惩罚的总和）。

##### 1) 思路

暴力算法很好想，我也是一下子就用他解决了简单Case的（N < 6）；记S(D)表示集合D对应的最小惩罚，则：

$$ S(D) =  min_{i \in D} (min_{j \in D - A_i}(min(A_i \bigotimes B_j, A_j  \bigotimes B_i) + S(D - A_i))) $$

但是，这个递推式并不适合于大Case(N < 101)。于是，想着用动态规划去book一些东西，以减少一些运算，比如尝试用$A[99][7]$表示选择第7个元素作为下一个元素，当前集合中已经有99个元素的最小惩罚，然后以此递推下去。遗憾的是，这样做并不对；贪心算法也尝试过，可惜也并不是正确答案。还尝试过二维矩阵上选择(x,y)点对的方法，依然不得解。

于是，我陷入了一个思维循环，知道这道题可能是一个$O(N^3)$或者$O(N^4)$的算法，而且递推式看起来很眼熟，但始终得不到正确的思路。

晚上散步的时候慢慢想这道题和什么类型的题最像，当往图这一点上想的时候，很快就意识到，这是一道最小支撑树题，可以在$O(N^3)$的时间内解决；当这个转化过程建立起来后，一切自然迎刃而解。看来我的归同能力还不够强，需要再加强一些总结和应用能力。

我使用的最小支撑树算法如下：

```
1. 初始状态：找到全图最小边，边长相等任选其一，建立当前最小边两个点的集合V，以及从这两个点出发能够达到的新节点的边集E；统计初始处罚S;
2. 循环：
   2.1 每次从边集E中取边长最小的边，此时会新加入一个节点入n；
   2.2 删除边集E中原先所有指向n的边，加入从n出发的所有有新节点的新边；将新边的惩罚加入S；
   2.3 得到新的集合V和集合E；
   2.4 当E为空，即V等于原集合时，终止。
3. 返回S；
```



#### 3. Matrix Cutting

##### 0) 问题描述

一个N*M的矩阵$\{A_{ij}\}_{n \cdot m}$，进行如下操作：

* 每次选择当前已经得到的一个子矩阵（初始时只能是全矩阵），选择一行或者一列进行分割，将当前子矩阵分成非空的两个更小的子矩阵；
* 此时给予奖励，奖励值为未分割前的子矩阵的最小值；
* 重复上述操作，直到不能再分割即所有子矩阵都已经是1*1为止。

求最大的奖励和。

##### 1) 思路

这道题的思路也不难，注意到：一个矩阵A分成新的B和C时，有：

$$ S(A) = min_{B \subsetneqq A }(S(B) + S(C) + min(A)) $$

S(A)表示对矩阵A能取得的最大奖励；min(A)表示矩阵A中的最小元素。可以看出，计算具有可分性，使用动态规则压缩状态可以得到计算结果。过程并不复杂。
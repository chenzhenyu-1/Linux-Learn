# Linux 操作命令

## ls命令

ls 命令是 linux 下最常用的命令，ls 命令就是 list 的缩写。 ls 用来打印出当前目录的清单。如果 ls 指定其他目录，那么就会显示指定目录里的文件及文件夹清单。 通过 ls 命令不仅可以查看 linux 文件夹包含的文件，而且还可以查看目录和文件权限等等信息。

### **命令格式**

> ls [选项][目录名]

#### **常用参数**

| 参数 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| -a   | –all 列出目录下的所有文件，包括以 . 开头的隐含文件           |
| -l   | 除了文件名之外，还将文件的权限、所有者、文件大小等信息详细列出来 |
| -h   | –human-readable 以容易理解的格式列出文件大小（例如 1K 234M 2G) |
| -t   | 以文件修改时间排序                                           |

#### **常用范例**

**例一：**列出`/home`文件夹下的所有文件和目录的详细资料，可以使用如下命令：

```sh
ls -a -l /home
ls -al /home
```

上面两个命令执行结果一样

**例二：**列出当前目录中所有以”d”开头的文件目录的详细内容，可以使用如下命令：

```sh
ls -l d*
```

## cd命令

cd 命令可以说是 Linux 中最基本的命令语句，其他的命令语句要进行操作，都是建立在使用 cd 命令上的。cd 命令是 change directory 的缩写，切换当前目录至指定的目录。

#### **命令格式**

> cd [目录名]

#### **常用范例**

**例一：**从当前目录进入系统根目录，可以使用如下命令：

```sh
cd  /
```

**例二：**从当前目录进入父目录，可以使用如下命令：

```sh
cd ..
```

.. 表示父目录。

**例三：**从当前目录进入当前用户主目录，可以使用如下命令：

```sh
cd ~
```

~ 表示当前用户主目录，注意它与系统根目录不是同一个概念。

**例四：**从当前目录进入上次所在目录，可以使用如下命令：

```sh
cd -
```

\- 表示上次进入的目录。

## pwd命令

Linux 中用 pwd 命令来查看“当前工作目录”的完整路径。简单的说，每当你在终端进行操作时，你都会有一个当前工作目录。在不太确定当前位置时，就可以使用 pwd 来判定当前目录在文件系统内的确切位置。 pwd 命令是 Print Working Directory 的缩写。

#### **命令格式**

> pwd [选项]

#### **常用参数**

| 参数 | 描述                                       |
| ---- | ------------------------------------------ |
| -P   | 显示实际物理路径，而非使用连接（link）路径 |
| -L   | 当目录为连接路径时，显示连接路径           |

#### **常用范例**

**例一：**显示当前目录所在路径，可以使用如下命令：

```sh
pwd
```

**例二：**显示当前目录的物理路径，可以使用如下命令：

```sh
pwd -P
```

**例三：**显示当前目录的连接路径，可以使用如下命令：

```sh
pwd -L
```

## mkdir命令

mkdir 命令用来创建指定名称的目录，要求创建目录的用户在当前目录中具有写权限，并且指定的目录名不能是当前目录中已有的目录。 mkdir 命令是 make directory 的缩写。

#### **命令格式**

> mkdir [选项] 目录

#### **常用参数**

| 参数           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| -m --mode=模式 | 设定权限<模式>                                               |
| -p --parents   | 可以是一个路径名称。若路径中的某些目录尚不存在，加上此选项后，系统将自动建立好那些尚不存在的目录，即一次可以建立多个目录 |
| -v --verbose   | 每次创建新目录都显示信息                                     |

#### **常用范例**

**例一：**递归创建多个目录 ，可以使用如下命令：

```sh
mkdir -p  zhou/test
```

**例二：**创建权限为 777 的目录，可以使用如下命令：

```sh
mkdir -m 777  zhou
```

**例三：**创建目录显示信息，可以使用如下命令：

```sh
mkdir -vp zhou/test
```

##  rm 命令 

rm 是常用的命令，该命令的功能为删除一个目录中的一个或多个文件或目录，它也可以将某个目录及其下的所有文件及子目录均删除。对于链接文件，只会删除链接，原文件均保持不变。

rm 是一个危险的命令，使用的时候要特别当心，尤其对于新手，否则整个系统就会毁在这个命令（比如在/（根目录）下执行 rm * -rf）。所以，我们在执行 rm 之前最好先确认一下在哪个目录，到底要删除什么东西，操作时保持高度清醒的头脑。

rm 命令是 remove 的缩写。

#### **命令格式**

> rm [选项] 文件或目录

#### **常用参数**

| 参数             | 描述                                               |
| ---------------- | -------------------------------------------------- |
| -f --force       | 忽略不存在的文件，从不给出提示                     |
| -i --interactive | 进行交互式删除                                     |
| -r --recursive   | 指示 rm 将参数中列出的全部目录和子目录均递归地删除 |
| -v --verbose     | 详细显示进行的步骤                                 |

#### **常用范例**

先来创建一个测试文本：

```sh
sudo touch shiyanlou.log
```

**例一：**删除文件，系统会先询问是否删除，可以使用如下命令：

```sh
rm shiyanlou.log
```

**例二：**强行删除文件，系统不再提示，可以使用如下命令：

```sh
rm -f shiyanlou.log
```

**例三：**删除后缀名为.log 的所有，删除前逐一询问，可以使用如下命令：

```sh
rm *.log 或 rm -i *.log
```

## mv命令

mv 命令功能是用来移动文件或更改文件名，是 Linux 系统下常用的命令，经常用来备份文件或者目录。 mv 命令根据第二个参数类型（目标是一个文件还是目录），决定执行将文件重命名或将其移至一个新的目录中。当第二个参数类型是文件时，mv 命令完成文件重命名，此时，源文件只能有一个（也可以是源目录名），它将所给的源文件或目录重命名为给定的目标文件名。当第二个参数是已存在的目录名称时，源文件或目录参数可以有多个，mv 命令将各参数指定的源文件均移至目标目录中。 mv 命令是 move 的缩写。

#### **命令格式**

> mv [选项] 源文件或目录 目标文件或目录

#### **常用参数**

| 参数             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| -b --back        | 若需覆盖文件，则覆盖前先行备份                               |
| -f --force       | 如果目标文件已经存在，不会询问而直接覆盖                     |
| -i --interactive | 若目标文件已经存在时，就会询问是否覆盖                       |
| -u --update      | 若目标文件已经存在，且源文件比较新，才会更新                 |
| -t --target      | 该选项适用于移动多个源文件到一个目录的情况，此时目标目录在前，源文件在后 |

#### **常用范例**

**例一：**将文件`shiyanlou.log`重命名为`zhou.log`，可以使用如下命令：

```sh
mv shiyanlou.log zhou.log
```

**例二：**将文件`zhou.log`移动到 test 目录下（test 目录必须已经存在，否则执行重命名），可以使用如下命令：

```sh
mv zhou.log test
```

**例三：**将文件`a.txt`移动到 test1 目录下，如果文件存在，覆盖前会询问是否覆盖，可以使用如下命令：

```sh
mv -i a.txt test1
```

## cp命令

cp 命令用来复制文件或者目录，是 Linux 系统中最常用的命令之一。一般情况下，shell 会设置一个别名，在命令行下复制文件时，如果目标文件已经存在，就会询问是否覆盖，不管你是否使用 -i 参数。但是如果是在 shell 脚本中执行 cp 时，没有 -i 参数时不会询问是否覆盖。这说明命令行和 shell 脚本的执行方式有些不同。 cp 命令是 copy 的缩写。

#### **命令格式**

> cp [选项] 源文件 目录 cp [选项] -t 目录 源文件

#### **常用参数**

| 参数                  | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| -t --target-directory | 指定目标目录                                                 |
| -i --interactive      | 覆盖前询问（使前面的 -n 选项失效）                           |
| -n --no-clobber       | 不要覆盖已存在的文件（使前面的 -i 选项失效）                 |
| -s --symbolic-link    | 对源文件建立符号链接，而非复制文件                           |
| -f --force            | 强行复制文件或目录，不论目的文件或目录是否已经存在           |
| -u --update           | 使用这项参数之后，只会在源文件的修改时间较目的文件更新时，或是对应的目的文件并不存在，才复制文件 |

#### **常用范例**

**例一：**对文件`shiyanlou.log`建立一个符号链接`syl.log`，可以使用如下命令：

```sh
cp -s shiyanlou.log syl.log
```

**例二：**将 test1 目录下的所有文件复制到 test2 目录下，覆盖前询问，可以使用如下命令：

```sh
cp -i test1/* test2
```

**例三：**将 test1 目录下的最近更新的文件复制到 test2 目录下，覆盖前询问，可以使用如下命令：

```sh
cp -iu test1/* test2
```

## cat命令

cat 命令的功能是将文件或标准输入组合输出到标准输出。这个命令常用来显示文件内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，它常与重定向符号配合使用。 cat 命令是 concatenate 的缩写。

#### **命令格式**

> cat [选项][文件]

#### **常用参数**

| 参数                  | 描述                                              |
| --------------------- | ------------------------------------------------- |
| -A --show-all         | 等价于 -vET                                       |
| -b --number-nonblank  | 对非空输出行编号                                  |
| -e                    | 等价于 -vE                                        |
| -E --show-ends        | 在每行结束处显示 $                                |
| -n --number           | 对输出的所有行编号，由 1 开始对所有输出的行数编号 |
| -s --squeeze-blank    | 有连续两行以上的空白行，就代换为一行的空白行      |
| -t                    | 与 -vT 等价                                       |
| -T --show-tabs        | 将跳格字符显示为 ^I                               |
| -u                    | （被忽略）                                        |
| -v --show-nonprinting | 使用 ^ 和 M- 引用，除了 LFD 和 TAB 之外           |

#### **常用范例**

**例一：**把`shiyanlou.log`的文件内容加上行号后输入`zhou.log`这个文件里，可以使用如下命令：

```sh
cat -n shiyanlou.log > zhou.log
```

**例二：**把`shiyanlou.log`的文件内容加上行号后输入`zhou.log`这个文件里，多行空行换成一行输出，可以使用如下命令：

```sh
cat -ns shiyanlou.log > zhou.log
```

**例三：**将`zhou.log`的文件内容反向显示，可以使用如下命令：

```sh
tac  zhou.log
```

说明：tac 是将 cat 反写过来，所以它的功能就跟 cat 相反，cat 是由第一行开始到最后一行连续显示在屏幕上，而 tac 则是由最后一行开始到第一行反向在屏幕上显示出来。

## nl命令

nl 命令在 linux 系统中用来计算文件中的行号。nl 可以将输出的文件内容自动加上行号，其默认的结果与 cat -n 有点不太一样。 nl 可以将行号做较多的显示设计，包括位数与是否自动补齐 0 等等的功能。
nl 命令是 number of lines 的缩写。

#### **命令格式**

> nl [选项][文件]

#### **常用参数**

| 参数  | 描述                                              |
| ----- | ------------------------------------------------- |
| -b    | 指定行号指定的方式，主要有两种：                  |
| -b a  | 表示不论是否为空行，也同样列出行号（类似 cat -n） |
| -b t  | 如果有空行，空的那一行不要列出行号（默认值）      |
| -n    | 列出行号表示的方法，主要有三种：                  |
| -n ln | 行号在屏幕的最左方显示                            |
| -n rn | 行号在自己栏位的最右方显示，且不加 0              |
| -n rz | 行号在自己栏位的最右方显示，且加 0                |
| -w    | 行号栏位的占用的位数                              |

#### **常用范例**

例一：把`shiyanlou.log`的文件内容加上行号后显示，空行不加行号，可以使用如下命令：

```sh
nl -b t shiyanlou.log
```

例二：把`shiyanlou.log`的文件内容加上行号后显示，行号分别在屏幕最左方、最右方不加 0 和最右方加 0 显示，可以使用如下命令：

```sh
nl -n ln shiyanlou.log
nl -n rn shiyanlou.log
nl -n rz shiyanlou.log
```

**例三：**把`shiyanlou.log`的文件内容加上行号后显示，行号在屏幕最右方加 0 显示，行号栏目占位数为 3，可以使用如下命令：

```sh
nl -n rz -w 3 shiyanlou.log
```

## more命令

more 命令，功能类似 cat ，cat 命令是将整个文件的内容从上到下显示在屏幕上。 more 命令会一页一页的显示，方便使用者逐页阅读，而最基本的指令就是按空格键（space）往下一页显示，按 B 键就会往回（back）一页显示，而且还有搜寻字串的功能。more 命令从前向后读取文件，因此在启动时就加载整个文件。

#### **命令格式**

> more [选项] 文件

#### **常用参数**

| 参数      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| +n        | 从笫 n 行开始显示                                            |
| -n        | 定义屏幕大小为 n 行                                          |
| +/pattern | 在每个档案显示前搜寻该字串（pattern），然后从该字串前两行之后开始显示 |
| -c        | 从顶部清屏，然后显示                                         |
| -d        | 提示“Press space to continue，’q’ to quiet”，禁用响铃功能    |
| -p        | 通过清除窗口而不是滚屏来对文件进行换页，与-c 选项相似        |
| -s        | 把连续的多个空行显示为一行                                   |
| -u        | 把文件内容中的下划线去掉                                     |

#### **常用操作**

| 符号   | 描述             |
| ------ | ---------------- |
| =      | 输出当前行的行号 |
| q      | 退出 more        |
| 空格键 | 向下滚动一屏     |
| b      | 返回上一屏       |

#### **常用范例**

请创建文件`shiyanlou.log`，文件内容如下：

```txt
2014-11-5 a
2014-11-5 b
2014-11-5 c
2014-11-5 d
2014-11-5 e
2014-11-5 f
2014-11-5 g
2014-11-5 h
2014-11-5 e
2014-11-5 a
2014-11-5 b
2014-11-5 c
2014-11-5 d
2014-11-5 e
2014-11-5 f
2014-11-5 g
2014-11-5 h
2014-11-5 a
2014-11-5 b
2014-11-5 c
2014-11-5 d
2014-11-5 e
```

**例一：**从第五行开始显示`shiyanlou.log`文件中的内容，可以使用如下命令：

```sh
more +5 shiyanlou.log
```

![Alt text](https://doc.shiyanlou.com/linux31.png)

**例二：**从`shiyanlou.log`文件中查找第一个出现“g”字符串的行，并从该处前两行开始显示输出，可以使用如下命令：

```sh
more +/g shiyanlou.log
```

![Alt text](https://doc.shiyanlou.com/linux32.png)

**例三：**设定每屏行数为 5，可以使用如下命令：

```sh
more -5 shiyanlou.log
```

![Alt text](https://doc.shiyanlou.com/linux33.png)

**例四：**使用 ll 和 more 命令显示`/etc`目录信息，可以使用如下命令：

```sh
ll /etc | more -10
```

![Alt text](https://doc.shiyanlou.com/linux34.png)

每页显示 10 个文件信息，按 Ctrl+F 或者 空格键 将会显示下 10 条文件信息。

## less命令

less 命令也是对文件或其它输出进行分页显示的工具，应该说是 linux 正统查看文件内容的工具，功能极其强大。

#### **命令格式**

> less [选项] 文件

#### **常用参数**

| 参数 | 描述                                                 |
| ---- | ---------------------------------------------------- |
| -e   | 当文件显示结束后，自动离开                           |
| -f   | 强迫打开特殊文件，例如外围设备代号、目录和二进制文件 |
| -i   | 忽略搜索时的大小写                                   |
| -m   | 显示类似 more 命令的百分比                           |
| -N   | 显示每行的行号                                       |
| -s   | 显示连续空行为一行                                   |

#### **常用操作**

| 符号    | 描述                                 |
| ------- | ------------------------------------ |
| /字符串 | 向下搜索“字符串”的功能               |
| ?字符串 | 向上搜索“字符串”的功能               |
| n       | 重复前一个搜索（与 / 或 ? 有关）     |
| N       | 反向重复前一个搜索（与 / 或 ? 有关） |
| b       | 向前翻一页                           |
| d       | 向后翻半页                           |
| q       | 退出 less 命令                       |
| 空格键  | 向后翻一页                           |
| 向上键  | 向上翻动一行                         |
| 向下键  | 向下翻动一行                         |

#### **常用范例**

**例一：**显示`shiyanlou.log`文件中的内容，并显示行号，可以使用如下命令：

```sh
less -N shiyanlou.log
```

![Alt text](https://doc.shiyanlou.com/linux35.png)

**例二：**显示`shiyanlou.log`文件中的内容，搜索字符串”shiyanlou”，可以使用如下命令：

```sh
less shiyanlou.log
/shiyanlou
```

![Alt text](https://doc.shiyanlou.com/linux226.png)

![Alt text](https://doc.shiyanlou.com/linux37.png)

**例三：**ps 查看进程信息并通过 less 分页显示，可以使用如下命令：

```sh
ps -f | less
```

![Alt text](https://doc.shiyanlou.com/linux38.png)

#### less 与 cat 和 more 的区别

cat 命令功能：用于显示整个文件的内容，因为单独使用没有翻页功能，所以经常和 more 命令搭配使用，cat 命令还有一个可以将数个文件合并成一个文件的功能。

more 命令功能：让画面在显示满一页时暂停，此时可按空格健继续显示下一个画面，或按 q 键停止显示。

less 命令功能：less 命令的用法与 more 命令类似，也可以用来浏览超过一页的文件。所不同的是 less 命令除了可以按空格键向下显示文件外，还可以利用上下键来滚动文件。当要结束浏览时，只要在 less 命令的提示符“：”下按 q 键即可。

其实这三个命令除了 cat 命令有合并文件的功能外，其余功能都很相近，只是在浏览习惯和显示方式上有所不同。

## grep命令

grep 是个很强大的命令，用来找到文件中的匹配文本，并且能够接受正则表达式和通配符，同时可以用多个 grep 命令选项来生成各种格式的输出。

grep 的工作方式是这样的，它在一个或多个文件中搜索字符串模板。如果模板包括空格，则必须被引用，模板后的所有字符串被看作文件名。搜索的结果被送到标准输出，不影响原文件内容。

grep 可用于 shell 脚本，因为 grep 通过返回一个状态值来说明搜索的状态，如果模板搜索成功，则返回 0，如果搜索不成功，则返回 1，如果搜索的文件不存在，则返回 2。我们利用这些返回值就可进行一些自动化的文本处理工作。

#### **命令格式**

> grep [选项] pattern [file]

#### **常用参数**

| 参数         | 描述                                     |
| ------------ | ---------------------------------------- |
| -c           | 计算找到‘搜寻字符串’（即 pattern）的次数 |
| -i           | 忽略大小写的不同，所以大小写视为相同     |
| -n           | 输出行号                                 |
| -v           | 反向选择，打印不匹配的行                 |
| -r           | 递归搜索                                 |
| --color=auto | 将找到的关键词部分加上颜色显示           |

#### **常用范例**

**例一：**将`/etc/passwd`文件中出现 root 的行取出来，关键词部分加上颜色显示，可以使用如下命令：

```sh
grep "root" /etc/passwd --color=auto
cat /etc/passwd | grep "root" --color=auto
```

![img](https://doc.shiyanlou.com/userid3372labid353time1419920596878)

**例二：**将`/etc/passwd`文件中没有出现 root 和 nologin 的行取出来，可以使用如下命令：

```sh
grep -v "root" /etc/passwd | grep -v "nologin"
```

![img](https://doc.shiyanlou.com/userid3372labid353time1419920644630)

**例三：**在当前目录下递归搜索文件中包含 main() 的文件，经常用于查找某些函数位于哪些源代码文件中，可以使用如下命令：

```sh
grep -r "main()".
```

![img](https://doc.shiyanlou.com/userid3372labid353time1419920683927)

### 正则表达式与 grep 命令

正则表达式是一种符号表示法，被用来识别文本模式。在某种程度上，它们与匹配文件和路径名的 shell 通配符比较相似，但其规模更大。许多命令行工具和大多数的编程语言都支持正则表达式，以此来帮助解决文本操作问题。

正则表达式元字符由以下字符组成：

```
^` `$` `.` `[` `]` `{` `}` `-` `?` `*` `+` `(` `)` `|` `\
```

![img](https://doc.shiyanlou.com/userid3372labid353time1419920809160)

**常用范例**

**例一：**利用 Linux 系统自带的字典查找一个五个字母的单词，第三个字母为 j,最后一个字母为 r，`/usr/share/dict`目录下存放字典文件（若没有可手动建立），可以使用如下命令：

```sh
grep '^..j.r$' words
```

![图片描述](https://doc.shiyanlou.com/courses/uid600404-20191230-1577697206638)

**例二：**验证固定电话，打印符合条件的电话，固定电话格式基本都是带有 0 的区号+连接符“-”＋电话号码，另外还有可能有分机号，区号有 3 位、4 位，电话号码有 7 位和 8 位的，可以使用如下命令：

```sh
grep -E "^0[0-9]{2,3}-[0-9]{7,8}(-[0-9]{3,4})?$" telphone.txt
```

区号：前面一个 0，后面跟 2-3 位数字 0[0-9]{2,3}

电话号码：7-8 位数字 [0-9]{7,8}

分机号：一般都是 3-4 位数字 [0-9]{3,4}

![img](https://doc.shiyanlou.com/userid3372labid353time1419920922420)

注意执行下面的命令时没有任何匹配输出，这是因为没有加 -E 选项，那例一没加为什么可以呢，这是因为 grep 把`.`当成 shell 通配符，不是正则表达式的元字符。

![img](https://doc.shiyanlou.com/userid3372labid353time1419920941988)

## sed命令

sed 命令是利用脚本来处理文本文件。

sed 可依照脚本的指令来处理、编辑文本文件。

Sed 主要用来自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等。

### 语法

```
sed [-hnV][-e<script>][-f<script文件>][文本文件]
```

**参数说明**：

- -e<script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
- -f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
- -h或--help 显示帮助。
- -n或--quiet或--silent 仅显示script处理后的结果。
- -V或--version 显示版本信息。

**动作说明**：

- a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
- c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
- d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
- i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
- p ：打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～
- s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！例如 1,20s/old/new/g 就是啦！

### 实例

在testfile文件的第四行后添加一行，并将结果输出到标准输出，在命令行提示符下输入如下命令：

```
sed -e 4a\newLine testfile 
```

首先查看testfile中的内容如下：

```
$ cat testfile #查看testfile 中的内容  
HELLO LINUX!  
Linux is a free unix-type opterating system.  
This is a linux testfile!  
Linux test 
```

使用sed命令后，输出结果如下：

```
$ sed -e 4a\newline testfile #使用sed 在第四行后添加新字符串  
HELLO LINUX! #testfile文件原有的内容  
Linux is a free unix-type opterating system.  
This is a linux testfile!  
Linux test  
newline 
```

### 以行为单位的新增/删除

将 /etc/passwd 的内容列出并且列印行号，同时，请将第 2~5 行删除！

```
[root@www ~]# nl /etc/passwd | sed '2,5d'
1 root:x:0:0:root:/root:/bin/bash
6 sync:x:5:0:sync:/sbin:/bin/sync
7 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
.....(后面省略).....
```

sed 的动作为 '2,5d' ，那个 d 就是删除！因为 2-5 行给他删除了，所以显示的数据就没有 2-5 行罗～ 另外，注意一下，原本应该是要下达 sed -e 才对，没有 -e 也行啦！同时也要注意的是， sed 后面接的动作，请务必以 '' 两个单引号括住喔！

只要删除第 2 行

```
nl /etc/passwd | sed '2d' 
```

要删除第 3 到最后一行

```
nl /etc/passwd | sed '3,$d' 
```

在第二行后(亦即是加在第三行)加上『drink tea?』字样！

```
[root@www ~]# nl /etc/passwd | sed '2a drink tea'
1 root:x:0:0:root:/root:/bin/bash
2 bin:x:1:1:bin:/bin:/sbin/nologin
drink tea
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
.....(后面省略).....
```

那如果是要在第二行前

```
nl /etc/passwd | sed '2i drink tea' 
```

如果是要增加两行以上，在第二行后面加入两行字，例如 **Drink tea or .....** 与 **drink beer?**

```
[root@www ~]# nl /etc/passwd | sed '2a Drink tea or ......\
> drink beer ?'
1 root:x:0:0:root:/root:/bin/bash
2 bin:x:1:1:bin:/bin:/sbin/nologin
Drink tea or ......
drink beer ?
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
.....(后面省略).....
```

每一行之间都必须要以反斜杠『 \ 』来进行新行的添加喔！所以，上面的例子中，我们可以发现在第一行的最后面就有 \ 存在。

### 以行为单位的替换与显示

将第2-5行的内容取代成为『No 2-5 number』呢？

```
[root@www ~]# nl /etc/passwd | sed '2,5c No 2-5 number'
1 root:x:0:0:root:/root:/bin/bash
No 2-5 number
6 sync:x:5:0:sync:/sbin:/bin/sync
.....(后面省略).....
```

透过这个方法我们就能够将数据整行取代了！

仅列出 /etc/passwd 文件内的第 5-7 行

```
[root@www ~]# nl /etc/passwd | sed -n '5,7p'
5 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
6 sync:x:5:0:sync:/sbin:/bin/sync
7 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
```

可以透过这个 sed 的以行为单位的显示功能， 就能够将某一个文件内的某些行号选择出来显示。

### 数据的搜寻并显示

搜索 /etc/passwd有root关键字的行

```
nl /etc/passwd | sed '/root/p'
1  root:x:0:0:root:/root:/bin/bash
1  root:x:0:0:root:/root:/bin/bash
2  daemon:x:1:1:daemon:/usr/sbin:/bin/sh
3  bin:x:2:2:bin:/bin:/bin/sh
4  sys:x:3:3:sys:/dev:/bin/sh
5  sync:x:4:65534:sync:/bin:/bin/sync
....下面忽略 
```

如果root找到，除了输出所有行，还会输出匹配行。

使用-n的时候将只打印包含模板的行。

```
nl /etc/passwd | sed -n '/root/p'
1  root:x:0:0:root:/root:/bin/bash
```

### 数据的搜寻并删除

删除/etc/passwd所有包含root的行，其他行输出

```
nl /etc/passwd | sed  '/root/d'
2  daemon:x:1:1:daemon:/usr/sbin:/bin/sh
3  bin:x:2:2:bin:/bin:/bin/sh
....下面忽略
#第一行的匹配root已经删除了
```

### 数据的搜寻并执行命令

搜索/etc/passwd,找到root对应的行，执行后面花括号中的一组命令，每个命令之间用分号分隔，这里把bash替换为blueshell，再输出这行：

```
nl /etc/passwd | sed -n '/root/{s/bash/blueshell/;p;q}'    
1  root:x:0:0:root:/root:/bin/blueshell
```

最后的q是退出。

### 数据的搜寻并替换

除了整行的处理模式之外， sed 还可以用行为单位进行部分数据的搜寻并取代。基本上 sed 的搜寻与替代的与 vi 相当的类似！他有点像这样：

```
sed 's/要被取代的字串/新的字串/g'
```

先观察原始信息，利用 /sbin/ifconfig 查询 IP

```
[root@www ~]# /sbin/ifconfig eth0
eth0 Link encap:Ethernet HWaddr 00:90:CC:A6:34:84
inet addr:192.168.1.100 Bcast:192.168.1.255 Mask:255.255.255.0
inet6 addr: fe80::290:ccff:fea6:3484/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
.....(以下省略).....
```

本机的ip是192.168.1.100。

将 IP 前面的部分予以删除

```
[root@www ~]# /sbin/ifconfig eth0 | grep 'inet addr' | sed 's/^.*addr://g'
192.168.1.100 Bcast:192.168.1.255 Mask:255.255.255.0
```

接下来则是删除后续的部分，亦即： 192.168.1.100 Bcast:192.168.1.255 Mask:255.255.255.0

将 IP 后面的部分予以删除

```
[root@www ~]# /sbin/ifconfig eth0 | grep 'inet addr' | sed 's/^.*addr://g' | sed 's/Bcast.*$//g'
192.168.1.100
```

### 多点编辑

一条sed命令，删除/etc/passwd第三行到末尾的数据，并把bash替换为blueshell

```
nl /etc/passwd | sed -e '3,$d' -e 's/bash/blueshell/'
1  root:x:0:0:root:/root:/bin/blueshell
2  daemon:x:1:1:daemon:/usr/sbin:/bin/sh
```

-e表示多点编辑，第一个编辑命令删除/etc/passwd第三行到末尾的数据，第二条命令搜索bash替换为blueshell。

### 直接修改文件内容(危险动作)

sed 可以直接修改文件的内容，不必使用管道命令或数据流重导向！ 不过，由於这个动作会直接修改到原始的文件，所以请你千万不要随便拿系统配置来测试！ 我们还是使用文件 regular_express.txt 文件来测试看看吧！

regular_express.txt 文件内容如下：

```
[root@www ~]# cat regular_express.txt 
runoob.
google.
taobao.
facebook.
zhihu-
weibo-
```

利用 sed 将 regular_express.txt 内每一行结尾若为 . 则换成 !

```
[root@www ~]# sed -i 's/\.$/\!/g' regular_express.txt
[root@www ~]# cat regular_express.txt 
runoob!
google!
taobao!
facebook!
zhihu-
weibo-
```

:q:q

利用 sed 直接在 regular_express.txt 最后一行加入 **# This is a test**:

```
[root@www ~]# sed -i '$a # This is a test' regular_express.txt
[root@www ~]# cat regular_express.txt 
runoob!
google!
taobao!
facebook!
zhihu-
weibo-
# This is a test
```
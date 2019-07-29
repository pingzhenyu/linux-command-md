~!#$%^&*这些符号怎么读? 当然是用英语（键盘特殊符号小结）

1. ~ 波浪号tilde，源于西班牙语和葡语中的发音符号。

2. ! 感叹号exclamation mark/exclamation point/bang，无需多解释，在这个 “咆哮体”盛行的时代，想不懂这个都难。

3. # 汉语中因形似“井”，通常读作井号，真正的含义是数字符号(Number sign)，如在一些国家‘#1’代表No.1的意思。在美式英语中一般称作pound sign，电话上的“#”叫做pound key，而加拿大英语则称之为number sign key；北美以外的其他英语国家一般称“#”为hash，相应的电话键叫做hash key。注意：数字符号（#）极易和乐谱中的升音符（? 读作sharp）相混淆。但是，乐谱的sharp和数字符号的字形不完全一样。标准数字符号(#)横线水平，而竖线向右倾斜；而乐谱的升号（?）为了在五线谱中容易识别，横线改为斜向上但竖线垂直。我猜此时有人就会举出一个极好的反例来否定上述说法，那就是C#（C Sharp）。的确，乍一看确实不相符！但事实上，C#并不违背上述结论，C Sharp中符号Sharp的创意正是来源于升音符?在乐谱中的含义——紧跟其后的音符的音高比实际标定的高半音，表示技术进一步提升之意（要不直接把C#本土化，翻译成“C优”算了^_^，这个命名方法有点类似于C++中“++”表示变量增1）。由于“?”在计算机显示、输入中不方便，因此在书写体中用“#”代替“?”，但读音保持不变。于是就出现了书写成“C#”但念作“C Sharp”的情形，了解渊源之后发现其实并不矛盾。

4. $ dollar/peso sign，我们通常把这个当作美元（USD）的符号，但拉丁美洲一些国家的人们会认为“$” 代表比索（peso），所以，不引起误解，最好用“US$”代表美元。这个符号的起源还存在争议，其中有一种说法是这样的：在18世纪末，货币单位比索的手写缩写符号是“ps”，随着时间推移，p和s感情渐进、关系日益密切，最后重叠在一起形成了现在的“$”。

 5. % 百分号，percent sign。

 6. ^ a读caret，表示间距符 “^ ”或 “?”，也称作wedge, up-arrow, hat，数学中通常叫做hat；b读circumflex (^)，是发音符号，常见用法如?。

 7. & ampersand/and，单词“and”的简写形式。

  8. * asterisk/star，计算机和数学中称作“star”更常见。

  9. () round brackets/open brackets; [ ] square brackets/closed brackets; { } curly brackets/definite brackets; < > angle brackets/triangular brackets，除了用作尖括号，也用作不等号，小于号<（less-than），大于号>（greater-than）。

  10. / 斜杠，slash，为与“\”相区别，通常也叫forward slash。

  11. \ 反斜杠，backslash。

  12. + 加号，plus sign； - 减号，minus sign。

  13. - – — dash，英文中dash

  --------------------------------------------------------------------------------------------------

   ; ;; . , / \ 'string'| ! $ ${} $? $$ $* "string"* ** ? : ^ $# $@ `command`{} [] [[]] () (()) || && {xx,yy,zz,...}~ ~+ ~- & \<...\> + - %= == !=


  /#：常出现在命令之前，或者命令之后，后面是注释文字，不会被执行
  当一个命令不想被执行的时候，前面加一个#就行了
  如果被用在指令中，或者被双引号括住的话，或者在双斜线后面，不具备以上功能
  ~ 账户中的home目录
  代表使用者的home目录
  ; 分号 (Command separator)
  在 shell 中，担任"连续指令"功能的符号就是"分号"。譬如以下的例子：cd ~/backup ; mkdir startup ;cp ~/.* startup/.


  ;; 连续分号 (Terminator)
  专用在 case 的选项，担任 Terminator 的角色。
  case "$fop" inhelp) echo "Usage: Command -help -version filename";;version) echo "version 0.1" ;;esac


  . 逗号 (dot,就是“点”)
  在 shell 中，使用者应该都清楚，一个 dot 代表当前目录，两个 dot 代表上层目录。
  CDPATH=.:~:/home:/home/web:/var:/usr/local
  在上行 CDPATH 的设定中，等号后的 dot 代表的就是当前目录的意思。
  如果档案名称以 dot 开头，该档案就属特殊档案，用 ls 指令必须加上 -a 选项才会显示。除此之外，在 regularexpression 中，一个 dot 代表匹配一个字元。


  'string' 单引号 (single quote)
  被单引号用括住的内容，将被视为单一字串。在引号内的代表变数的$符号，没有作用，也就是说，他被视为一般符号处理，防止任何变量替换。
  heyyou=homeecho '$heyyou' # We get $heyyou


  "string" 双引号 (double quote)
  被双引号用括住的内容，将被视为单一字串。它防止通配符扩展，但允许变量扩展。这点与单引数的处理方式不同。
  heyyou=homeecho "$heyyou" # We get home

  `command` 倒引号 (backticks)
  在前面的单双引号，括住的是字串，但如果该字串是一列命令列，会怎样？答案是不会执行。要处理这种情况，我们得用倒单引号来做。
  fdv=`date +%F`echo "Today $fdv"
  在倒引号内的 date +%F 会被视为指令，执行的结果会带入 fdv 变数中。


  , 逗点 (comma，标点中的逗号)
  这个符号常运用在运算当中当做"区隔"用途。如下例
  !/bin/bashlet "t1 = ((a = 5 + 3, b = 7 - 1, c = 15 / 3))"echo "t1= $t1, a = $a, b = $b"


  / 斜线 (forward slash)
  在路径表示时，代表目录。
  cd /etc/rc.dcd ../..cd /
  通常单一的 / 代表 root 根目录的意思；在四则运算中，代表除法的符号。
  let "num1 = ((a = 10 / 2, b = 25 / 5))"


  \ 倒斜线
  在交互模式下的escape 字元，有几个作用；放在指令前，有取消 aliases的作用；放在特殊符号前，则该特殊符号的作用消失；放在指令的最末端，表示指令连接下一行。
   type rmrm is aliased to `rm -i'# \rm ./*.log
  上例，我在 rm 指令前加上 escape 字元，作用是暂时取消别名的功能，将 rm 指令还原。
   bkdir=/home# echo "Backup dir, \$bkdir = $bkdir"Backup dir,$bkdir = /home
  上例 echo 内的 \$bkdir，escape 将 $ 变数的功能取消了，因此，会输出 $bkdir，而第二个 $bkdir则会输出变数的内容 /home。


  | 管道 (pipeline)
  pipeline 是 UNIX 系统，基础且重要的观念。连结上个指令的标准输出，做为下个指令的标准输入。
  who | wc -l
  善用这个观念，对精简 script 有相当的帮助。


  ! 惊叹号(negate or reverse)
  通常它代表反逻辑的作用，譬如条件侦测中，用 != 来代表"不等于"
  if [ "$?" != 0 ]thenecho "Executes error"exit 1fi
  在规则表达式中她担任 "反逻辑" 的角色
  ls a[!0-9]
  上例，代表显示除了a0, a1 .... a9 这几个文件的其他文件。


  : 冒号
  在 bash 中，这是一个内建指令："什么事都不干"，但返回状态值 0。
  :
  echo $? # 回应为 0
  : > f.
  上面这一行，相当于cat/dev/null>f.

  。不仅写法简短了，而且执行效率也好上许多。
  有时，也会出现以下这类的用法
  : ${HOSTNAME?} ${USER?} ${MAIL?}
  这行的作用是，检查这些环境变数是否已设置，没有设置的将会以标准错误显示错误讯息。像这种检查如果使用类似 test 或 if这类的做法，基本上也可以处理，但都比不上上例的简洁与效率。
  除了上述之外，还有一个地方必须使用冒号
  PATH=$PATH:$HOME/fbin:$HOME/fperl:/usr/local/mozilla
  在使用者自己的HOME 目录下的 .bash_profile或任何功能相似的档案中，设定关于"路径"的场合中，我们都使用冒号，来做区隔。


  ? 问号 (wild card)
  在文件名扩展(Filename expansion)上扮演的角色是匹配一个任意的字元，但不包含 null 字元。
  # ls a?a1
  善用她的特点，可以做比较精确的档名匹配。


  * 星号 (wild card)
  相当常用的符号。在文件名扩展(Filename expansion)上，她用来代表任何字元，包含 null 字元。
   ls a*a a1 access_log
  在运算时，它则代表 "乘法"。
  let "fmult=2*3"
  除了内建指令 let，还有一个关于运算的指令expr，星号在这里也担任"乘法"的角色。不过在使用上得小心，他的前面必须加上escape 字元。


  ** 次方运算
  两个星号在运算时代表 "次方" 的意思。
  let "sus=2**3"echo "sus = $sus" # sus = 8


  $ 钱号(dollar sign)
  变量替换(Variable Substitution)的代表符号。
  vrs=123echo "vrs = $vrs" # vrs = 123
  另外，在 Regular Expressions 里被定义为 "行" 的最末端 (end-of-line)。这个常用在grep、sed、awk 以及 vim(vi) 当中。


  ${} 变量的正规表达式
  bash 对 ${} 定义了不少用法。以下是取自线上说明的表列
  ${parameter:-word} ${parameter:=word} ${parameter:?word} ${parameter:+word} ${parameter:offset} ${parameter:offset:length} ${!prefix*} ${#parameter} ${parameter#word} ${parameter##word} ${parameter%word} ${parameter%%word} ${parameter/pattern/string} ${parameter//pattern/string}


  $*
  $* 引用script的执行引用变量，引用参数的算法与一般指令相同，指令本身为0，其后为1，然后依此类推。引用变量的代表方式如下：
  $0, $1, $2, $3, $4, $5, $6, $7, $8, $9, ${10}, ${11}.....
  个位数的，可直接使用数字，但两位数以上，则必须使用 {} 符号来括住。
  $* 则是代表所有引用变量的符号。使用时，得视情况加上双引号。
  echo "$*"
  还有一个与 $* 具有相同作用的符号，但效用与处理方式略为不同的符号。


  $@
  $@ 与 $* 具有相同作用的符号，不过她们两者有一个不同点。
  符号 $* 将所有的引用变量视为一个整体。但符号 $@ 则仍旧保留每个引用变量的区段观念。

  $#
  这也是与引用变量相关的符号，她的作用是告诉你，引用变量的总数量是多少。
  echo "$#"


  $? 状态值 (status variable)
  一般来说，UNIX(linux) 系统的进程以执行系统调用exit()来结束的。这个回传值就是status值。回传给父进程，用来检查子进程的执行状态。
  一般指令程序倘若执行成功，其回传值为 0；失败为 1。
  tar cvfz dfbackup.tar.gz /home/user > /dev/nullecho"$?"
  由于进程的ID是唯一的，所以在同一个时间，不可能有重复性的PID。有时，script会需要产生临时文件，用来存放必要的资料。而此script亦有可能在同一时间被使用者们使用。在这种情况下，固定文件名在写法上就显的不可靠。唯有产生动态文件名，才能符合需要。符号

  或许可以符合这种需求。它代表当前shell 的 PID。
  echo "$HOSTNAME, $USER, $MAIL" > ftmp.$$
  使用它来作为文件名的一部份，可以避免在同一时间，产生相同文件名的覆盖现象。
  ps: 基本上，系统会回收执行完毕的 PID，然后再次依需要分配使用。所以 script 即使临时文件是使用动态档名的写法，如果script 执行完毕后仍不加以清除，会产生其他问题。

  ( ) 指令群组 (command group)
  用括号将一串连续指令括起来，这种用法对 shell 来说，称为指令群组。如下面的例子：(cd ~ ; vcgh=`pwd` ;echo $vcgh)，指令群组有一个特性，shell会以产生 subshell来执行这组指令。因此，在其中所定义的变数，仅作用于指令群组本身。我们来看个例子
   cat ftmp-01#!/bin/basha=fsh(a=incg ; echo -e "\n $a \n")echo $a#./ftmp-01incgfsh
  除了上述的指令群组，括号也用在 array 变数的定义上；另外也应用在其他可能需要加上escape字元才能使用的场合，如运算式。


  (( ))
  这组符号的作用与 let 指令相似，用在算数运算上，是 bash 的内建功能。所以，在执行效率上会比使用 let指令要好许多。
  !/bin/bash(( a = 10 ))echo -e "inital value, a = $a\n"(( a++))echo "after a++, a = $a"

  { } 大括号 (Block of code)
  有时候 script 当中会出现，大括号中会夹着一段或几段以"分号"做结尾的指令或变数设定。
   cat ftmp-02#!/bin/basha=fsh{a=inbc ; echo -e "\n $a \n"}echo $a#./ftmp-02inbcinbc
  这种用法与上面介绍的指令群组非常相似，但有个不同点，它在当前的 shell 执行，不会产生 subshell。
  大括号也被运用在 "函数" 的功能上。广义地说，单纯只使用大括号时，作用就像是个没有指定名称的函数一般。因此，这样写 script也是相当好的一件事。尤其对输出输入的重导向上，这个做法可精简 script 的复杂度。

  此外，大括号还有另一种用法，如下
  {xx,yy,zz,...}
  这种大括号的组合，常用在字串的组合上，来看个例子
  mkdir {userA,userB,userC}-{home,bin,data}
  我们得到 userA-home, userA-bin, userA-data, userB-home, userB-bin,userB-data, userC-home, userC-bin,userC-data，这几个目录。这组符号在适用性上相当广泛。能加以善用的话，回报是精简与效率。像下面的例子
  chown root /usr/{ucb/{ex,edit},lib/{ex?.?*,how_ex}}
  如果不是因为支援这种用法，我们得写几行重复几次呀！


  [ ] 中括号
  常出现在流程控制中，扮演括住判断式的作用。if [ "$?" != 0 ]thenecho "Executes error"exit1fi
  这个符号在正则表达式中担任类似 "范围" 或 "集合" 的角色
  rm -r 200[1234]
  上例，代表删除 2001, 2002, 2003, 2004 等目录的意思。


  [[ ]]
  这组符号与先前的 [] 符号，基本上作用相同，但她允许在其中直接使用 || 与&& 逻辑等符号。
  #!/bin/bashread akif [[ $ak > 5 || $ak< 9 ]]thenecho $akfi


  || 逻辑符号
  这个会时常看到，代表 or 逻辑的符号。


  && 逻辑符号
  这个也会常看到，代表 and 逻辑的符号。


  & 后台工作
  单一个& 符号，且放在完整指令列的最后端，即表示将该指令列放入后台中工作。
  tar cvfz data.tar.gz data > /dev/null&

  \<...\> 单字边界
  这组符号在规则表达式中，被定义为"边界"的意思。譬如，当我们想找寻 the 这个单字时，如果我们用
  grep the FileA
  你将会发现，像 there 这类的单字，也会被当成是匹配的单字。因为 the 正巧是 there的一部份。如果我们要必免这种情况，就得加上 "边界" 的符号
  grep '\' FileA


  + 加号 (plus)
  在运算式中，她用来表示 "加法"。
  expr 1 + 2 + 3
  此外在规则表达式中，用来表示"很多个"的前面字元的意思。
   grep '10\+9' fileB109100910000910000931010009#这个符号在使用时，前面必须加上escape 字元。


  - 减号 (dash)
  在运算式中，她用来表示 "减法"。
  expr 10 - 2
  此外也是系统指令的选项符号。
  ls -expr 10 - 2
  在 GNU 指令中，如果单独使用 - 符号，不加任何该加的文件名称时，代表"标准输入"的意思。这是 GNU指令的共通选项。譬如下例
  tar xpvf -
  这里的 - 符号，既代表从标准输入读取资料。
  不过，在 cd 指令中则比较特别
  cd -
  这代表变更工作目录到"上一次"工作目录。


  % 除法 (Modulo)
  在运算式中，用来表示 "除法"。
  expr 10 % 2
  此外，也被运用在关于变量的规则表达式当中的下列
  ${parameter%word}${parameter%%word}
  一个 % 表示最短的 word 匹配，两个表示最长的 word 匹配。


  = 等号 (Equals)
  常在设定变数时看到的符号。
  vara=123echo " vara = $vara"
  或者像是 PATH 的设定，甚至应用在运算或判断式等此类用途上。


  == 等号 (Equals)
  常在条件判断式中看到，代表 "等于" 的意思。
  if [ $vara == $varb ]
  ...下略

  != 不等于
  常在条件判断式中看到，代表 "不等于" 的意思。
  if [ $vara != $varb ]
  ...下略


  ^
  这个符号在规则表达式中，代表行的 "开头" 位置，在[]中也与"!"(叹号)一样表示“非”


  输出/输入重导向
  > >> < << :> &> 2&> 2<>>& >&2

  文件描述符(File Descriptor)，用一个数字（通常为0-9）来表示一个文件。
  常用的文件描述符如下：
  文件描述符 名称 常用缩写 默认值
  0 标准输入 stdin 键盘
  1 标准输出 stdout 屏幕
  2 标准错误输出 stderr 屏幕
  我们在简单地用<或>时，相当于使用 0< 或 1>（下面会详细介绍）。
  * cmd > file
  把cmd命令的输出重定向到文件file中。如果file已经存在，则清空原有文件，使用bash的noclobber选项可以防止复盖原有文件。
  * cmd >> file
  把cmd命令的输出重定向到文件file中，如果file已经存在，则把信息加在原有文件後面。
  * cmd < file
  使cmd命令从file读入
  * cmd << text
  从命令行读取输入，直到一个与text相同的行结束。除非使用引号把输入括起来，此模式将对输入内容进行shell变量替换。如果使用<<- ，则会忽略接下来输入行首的tab，结束行也可以是一堆tab再加上一个与text相同的内容，可以参考後面的例子。
  * cmd <<< word
  把word（而不是文件word）和後面的换行作为输入提供给cmd。
  * cmd <> file
  以读写模式把文件file重定向到输入，文件file不会被破坏。仅当应用程序利用了这一特性时，它才是有意义的。
  * cmd >| file
  功能同>，但即便在设置了noclobber时也会复盖file文件，注意用的是|而非一些书中说的!，目前仅在csh中仍沿用>!实现这一功能。
  : > filename 把文件"filename"截断为0长度.# 如果文件不存在, 那么就创建一个0长度的文件(与'touch'的效果相同).
  cmd >&n 把输出送到文件描述符n
  cmd m>&n 把输出到文件符m的信息重定向到文件描述符n
  cmd >&- 关闭标准输出
  cmd <&n 输入来自文件描述符n
  cmd m<&n m来自文件描述各个n
  cmd <&- 关闭标准输入
  cmd <&n- 移动输入文件描述符n而非复制它。
  cmd >&n- 移动输出文件描述符 n而非复制它。
  注意： >&实际上复制了文件描述符，这使得cmd > file 2>&1与cmd 2>&1 >file的效果不一样。
  &&表并且 &\u 表首字母大写 &\l表首字母小写 &表示连接

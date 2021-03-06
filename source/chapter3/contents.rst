3.1 条件语句
============

3.1.1 做判断
------------

**找零案例**
就用分别减的方案，然后判断有没有需要借位，借位就需要用另一种算法求出它的值，这样可以吗？

-  借位的表现就是，分钟减的结果小于0

借位算法

.. code:: c

   if(m<0) {
       m= m+60;
       hour--;
   }

而在C语言中，我们有一个判断方法就是if语句

**如果**

.. code:: c

   if(条件成立) {
       ...
   }

如果条件是成立的，就会做括号里面的事情；如果是不成立的，则不会做括号里面的事情

求时间间隔的优化

-  条件分支语句中采用了“借位思想”
-  从小时中借出1小时（也就是60分钟）到分钟那边，再再小时这边-1即可

.. code:: c

   int hour1, minute1;
   int hour2, minute2;

   scanf("%d %d", &hour1, &minute1);
   scanf("%d %d", &hour2, &minute2);

   int ih = hour2 - hour1;
   int im = minute2 - minute1;

   if(im<0) {
       im  = im + 60;
       ih--;
   }



   printf("时间差是%d小时%d分。", ih, im);    

3.1.2 判断的条件
----------------

**条件**

-  我们把它称为运算，计算两个值之间的关系，就叫做关系运算，也叫做比较运算符，因为是做比较的
-  |10|
-  如果运算符是正确的（也就是条件成立），那么会输出布尔型数据，比如true或false，但在C语言中，它会是0（false）与1（true，或者叫非0），所以成立就是1，不成立就是0

**关系运算的结果**

-  布尔型的值只有两个：false（假）和true（真）。

-  当两个值的关系符合关系运算符的预期时，关系运算的结果为整数1，否则为整数0。且false的序号为0，true的序号是1（或者是非0）。

   .. code:: c

      printf("%d\n", 5==3);
      printf("%d\n",5>3);
      printf("%d\n",5<=3);

**优先级**

-  所有的关系运算符的优先级都比算术运算低，但是比赋值运算高

-  .. code:: c

        7>=3+4;
        int r = a>0;    

   如果上面的例子，是关系运算的优先级高，则它就会先算>=，那么就会得到1，然后再1+4，就会得到5，但正确的答案是1，因为是3+4先算
   再看第二个例子，如果它执行的是赋值（r=a），然后问r=a大于0吗，得出来的可能是0或者1，但这根本没有任何意义。只有a是否大于0，然后把值赋给左边才是个说得过去的做法
   所以这就是为什么优先级要比赋值运算符要高

-  判断是否相等的==与！=的优先级比其它运算符的优先级都要低，但连续的关系运算是从左到右进行的

   .. code:: c

      5>3==6>4（5>3的结果为1，6>4的结果也为1，那么它们相等，所以最终结果还是1）
      6>5>4（6>5的结果为1，1>4的结果为0，所以结果为0）
      a==b==6（无论a==b的结果是0，还是1，它的最终结果怎样都会是0，因为0与1都不等于6）
      a==b>0（无论a==b的结果是0（那么就是0），还是1（那么就是1），它的最终结果是0，也或者是1）

3.1.3 找零计算器
----------------

找零计算器需要用户做两个操作：输入购买的金额，输入支付的票面，而找零计算器则根据用户的输入做出相应的动作：计算并打印找零，或告知用户余额不足以购买。

从计算机程序的角度看，这就是意味着程序需要读用户的两个输入，然后进行一些计算和判断，最后输出结果

.. code:: c

   int price = 0;
   int bill = 0;

   printf("请输入金额：");
   scanf("%d", &price);

   printf("请输入票面：");
   scanf("%d", &bill);

   printf("应该找您：%d\n", bill - price)

这里的注释//，是C99的注释，ANSIC不支持

**注释**

-  以两个斜杠“//”这样开头的语句把程序分成了三个部分

   1.初始化

   2.读入金额和票面

   3.计算并打印找零

-  注释（comment）插入在程序代码中，用来向读者提供解释信息。它们对于程序的功能没有任何影响，但是往往能使得程序更容易被人类读者理解

.. raw:: html

   <p>

/\* \*/注释

.. raw:: html

   </p>

-  

   .. raw:: html

      <p>

   延续数行的注释，要用多行注释的格式来写。多行注释由一对字符序列“/*”开始，而以“*/”结束

   .. raw:: html

      </p>

-  

   .. raw:: html

      <p>

   也可以用于一行内的注释。两个符号中间的所有东西都是注释

   .. raw:: html

      </p>

   .. raw:: html

      <p>

   int ak = 47/36 /*36*/， y=9

   .. raw:: html

      </p>

-  单行的注释是C99独有的，多行的注释是C传统的，一开始就有

**对比**

.. code:: c

   int price = 0;
   int bill = 0;
   printf("请输入金额：");
   scanf("%d",&price);
   printf("请输入票面：");
   scanf("%d", &bill);
   printf("应该找您：%d\n", bill - price);

.. code:: c

   //初始化
   int price = 0;
   int bill = 0;
   //读入金额和票面
   printf("请输入金额：");
   scanf("%d",&price);
   printf("请输入票面：");
   scanf("%d", &bill);
   //计算找零
   printf("应该找您：%d\n", bill - price);

**判断票面够不够**

.. code:: c

   //初始化
   int price = 0;
   int bill = 0;
   //读入金额和票面
   printf("请输入金额：");
   scanf("%d",&price);
   printf("请输入票面：");
   scanf("%d", &bill);
   //计算找零
   if(bill>=price) {
       printf("应该找您：%d\n", bill - price);
   }

**流程图**

.. code:: flow

   st=>start: 开始
   op=>operation: 初始化
   io1=>inputoutput: 输入price和bill
   cond=>condition: bill>=price?
   io=>inputoutput: 输出bill-price
   e=>end: 停止
   st->op->io1->cond
   cond(yes)->io->e
   cond(no)->e

程序2：

.. code:: c

   const int MINOR = 35;

   int age = 0;

   printf("请输入你的年龄：");

   if(age < MINOR) {
       printf("年轻是美好的，");
   }

   printf("年轻决定了你的精神世界，好好珍惜吧。\n");
       

.. code:: flow

   st=>start: 开始
   op=>inputoutput: 输出“你的年龄” + age
   cond=>condition: age<MINOR?
   io=>inputoutput: 输出“年龄决定了你的精神世界，好好珍惜吧。”
   io2=>inputoutput: 输出“年轻是美好的，“
   e=>end: 结束
   st->op->cond
   cond(yes)->io->e
   cond(no)->io2->io

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021652.png
   :alt: 11

   11

3.1.4 否则的话
--------------

**如果条件不成立呢？**

.. code:: c

   //初始化
   int price = 0;
   int bill = 0;
   //读入金额和票面
   printf("请输入金额：");
   scanf("%d",&price);
   printf("请输入票面：");
   scanf("%d", &bill);
   //计算找零
   if(bill>=price) {
       printf("应该找您：%d\n", bill - price);
   }

-  如果在if语句后面还有语句，它们在if结束后会执行，无论条件如何

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021653.png
   :alt: 12

   12

-  像这个，如果是bill<price的话，那么运行成功；但如果不成立的话，那么它会有两个输出语句，最后得到的结果互相矛盾，这怎么可以呢？
-  所以我们需要else语句—否则的话

   -  你好

**Else**

-  Else=否则的话

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021654.png
   :alt: 13

   13

**比较数的大小**

.. code:: c

   printf("请输入两个整数：");
   scanf("%d %d", &a, &b);

   int max = 0;
   if(a>b) {
       max = a;
   }

   printf("大的那个是%d\n", max);

-  但它没有解决b大于a的问题，当a>b的条件不成立时，程序就结束了，max没有得到值

方案一：

.. code:: c

   int a, b;

   printf("请输入两个整数：");
   scanf("%d %d", &a, &b);

   int max = 0;
   if(a>b) {
       max = a;
   }
   if(b>a) {
       max = b;
   }

   printf("大的那个是%d\n", max);

-  这个方案的问题是，如果它们都相等呢？那不就输出0了吗？

方案二：

.. code:: c

   int a, b;

   printf("请输入两个整数：");
   scanf("%d %d", &a, &b);

   int max = 0;
   if(a>b) {
       max = a;
   } else {
       max = b;
   }

   printf("大的那个是%d\n", max);

方案三：

.. code:: c

   nt a, b;

   printf("请输入两个整数：");
   scanf("%d %d", &a, &b);

   int max = b;
   if(a>b) {
       max = a;
   }

   printf("大的那个是%d\n", max);

对比一下方案二与方案三：左边的容易理解，右边的得要有点聪明的人才能看懂

3.1.5 if语句再探
----------------

**if语句**

-  一个基本的if语句由一个关键字if开头，跟上在括号里的一个表示条件的逻辑表达式，然后是一对大括号｛｝之间的若干条语句。如果表示条件的逻辑表达式的结果不是0，那么就会执行后面跟着的这对大括号里面的语句，否则就跳过这些语句不执行，而继续下面的其它语句

-  还有另一种形式

   .. code:: c

      if(total>amount) 
          total += amount + 10;

-  if语句这一行结束的时候并没有表示语句结束的“;”，而后面的赋值语句写在if的下一行，并且缩进了，在这一行结束的时候有一个表示语句结束的“;”。这表明这条赋值语句是if语句的一部分，if语句拥有和控制这条赋值语句，决定它是否要被执行

-  既然if可以不用大括号，那么else语句也可以不用大括号

**0与1**

-  可以直接将if的条件判断处设为1，那就肯定会执行这个if语句

   .. code:: c

      int main() {
        int m = 0;
        if(1) {
            m = 2;
        } else {
            m = 0;
        }
        printf("%d\n", 5>4);
        printf("%d", m);
        system("pause");

        return 0;
      }

-  但你不能直接用true或者false，这在这里是行不通的

**计算薪水**

.. code:: c

   const double RATE = 8.25;
   const int STANDARD = 40;
   double pay = 0.0;
   int hours;

   printf("请输入工作的小时数：");
   scanf("%d", &hours);
   printf("\n");

   if(hours>STANDARD)
       pay = STANDARD*RATE + (hours-STANDARD)*(RATE*1.5);
   else
       pay = hours * RATE;

   printf("应付工资：%f\n", pay);

**判断成绩**

.. code:: c

   const int PASS = 60;
   int score;

   printf("请输入成绩：");
   scanf("%d", &score);

   printf("您输入的成绩是%d.\n", score);

   if(score<PASS)
       printf("很遗憾，这个成绩没有及格。");
   else
       printf("祝贺你，这个成绩及格了。");
   printf("再见\n");

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021655.png
   :alt: 14

   14

-  第一个和第二个是两个不一样的程序

3.2 循环
========

.. _循环-1:

3.2.1 循环
----------

**计算位数**

.. code:: c

   int num = 0;
   scanf("%d", &num);

   if(10>num) 
       printf("1位");
   else if(100>num)
       printf("2位");
   else if(1000>num) 
       printf("3位");
   else 
       printf("4位");

   return 0; 

-  要从小到大来判断，否则的话会出错

另一版本

.. code:: c

   int num = 0;
   scanf("%d", &num);

   if(num>1000) 
       printf("4位");
   else if(num>100)
       printf("3位");
   else if(num>10) 
       printf("2位");
   else 
       printf("1位");

   return 0; 

-  但是它这里出现一个小问题，就是当你属于10的时候，输入100的时候，它都会显示比正确答案-1

因此，需要进行改进

.. code:: c

   int num = 0;
   scanf("%d", &num);

   if(num>=1000) 
       printf("4位");
   else if(num>=100)
       printf("3位");
   else if(num>=10) 
       printf("2位");
   else 
       printf("1位");

   return 0;

-  因为题目明确了4位数及以下的正整数，所以可以简化一些判断
-  因为从高处往下判断，所以不需要判断上限了

   -  反过来不行

错误示例

.. code:: c

   if(num>0) 
       printf("1位");
   else if(num>10)
       printf("2位");
   else if(num>100)
       printf("3位");
   else
       printf("4位");

-  它这个都只会执行第一句

那么如何判断任意范围的正整数呢？

-  但你一直这样写无数个if语句也不是个办法啊，那怎么办？用while循环

我的版本

.. code:: c

   int num = 0, times=0, n=1, result = 1;
   scanf("%d", &num);
   scanf("%d", &times);

   while(times>0) {
       n*=10;
       if(num>=n)
           result++;
       times--;
   } 
   printf("%d, %d", result);

   return 0; 

最优版本

.. code:: c

   int num = 0, result = 0;
   scanf("%d", &num);
   while(num>0) {
       num /= 10;
       result++;
   } 
   printf("%d", result);

-  但超出int类型的最大值还是没有结果

-  .. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021656.png
      :alt: 15

      15

3.2.2 while循环
---------------

while循环是一种条件循环语句，当条件成立时，就会执行里面的循环体

要注意：循环体内一定要有改变条件的机会，否则就会出不来

-  如果没有这个机会，那么你在一些OJ上可能会得到超时错误

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021657.png
   :alt: 16

   16

**while循环**

-  如果我们把while翻译成“当”，那么一个while循环的意思就是：当条件满足时，不断的重复循环体内的语句

-  循环执行之前判断是否继续循环，所以有可能循环一次也没有被执行

-  条件成立的时候是继续循环的条件

**看程序运行的结果**

-  用人脑模拟计算机运行，把变量全部写在纸上，列出表格，模拟计算机的重新计算并赋值，最后在表格最后的就是最终结果

**验证**

-  测试程序常使用边界数据，如有效范围两端的数据，特殊的倍数等

   -  个位数
   -  10
   -  0
   -  负数

拿这个程序举例子

-  这个程序当我们输入0的时候，它会显示0位数，这不对啊，那怎么办？

第一种修改方法

.. code:: c

   int num = 0, result = 0;
   scanf("%d", &num);
   result++;
   num /= 10;
   while(num>0) {
       num /= 10;
       result++;
   } 
   printf("%d", result);

第二种修改方法

.. code:: c

   int num = 0, result = 0;
   scanf("%d", &num);
   if(num>0) {
       while(num>0) {
           num /= 10;
           result++;
       } 
   } else {
       result = 1;
   }

   printf("%d", result);

**调试手段**

-  看有没有执行循环

   .. code:: c

      int num = 0, result = 0;
      scanf("%d", &num);
      while(num>0) {
         printf("已经进入循环\n");
         num /= 10;
         result++;
      } 

      printf("%d", result);

-  看执行或者循环到哪里了

   .. code:: c

      int num = 0, result = 0;
      scanf("%d", &num);
      while(num>0) {
         num /= 10;
         result++;
         printf("num=%d, result=%d", num, result);
      } 

      printf("%d", result);

-  但当你提交上去OJ的时候，一定要把这些用来辅助调试的语句注释掉，否则就会出错

3.2.3 do-while循环
------------------

**数位数的算法**

1. 用户输入x；
2. 初始化n为0；
3. x=x/10，去掉个位；
4. n++；
5. 如果x>0，回到3；
6. 否则n就是结果。

**do-while循环**

-  在进入循环的时候不做检查，而是在执行完一轮循环体的代码之后，再来检查循环的条件是否满足，如果满足则继续下一轮循环，不满足则结束循环

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021658.png
   :alt: 17

   17

优化，这个版本就能识别0了

.. code:: c

   int num = 0, result = 0;
   scanf("%d", &num);

   do{
       num /= 10;
       result++;
   }while(num>0);  

   printf("%d", result);

**两种循环**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021659.png
   :alt: 18

   18

-  左边是do-while，右边是while

-  do-while循环和while循环很像，区别是在循环执行结束的时候才来判断条件。也就是说，无论如何，循环都会执行至少一次，然后再来判断条件。与while循环相同的是，条件满足时执行循环，条件不满足时结束循环

3.2.4 for循环
-------------

**阶乘**

-  n！=1×2×3×4×…×n

-  写一个程序，让用户输入n，然后计算输出n！

-  变量：

   -  第一种：显然读用户的输入需要一个int的n，然后计算的结果需要用一个变量保存，可以是int的factor，在计算中需要有一个变量不断的从1递增到n，那可以是int的i

      .. code:: c

         int n = 0, s = 1, i=1;
         scanf("%d", &n);
         while(i<=n) {
             s*=i;
             i++;
         }

         printf("%d", s);

   -  第二种，递减-for

      .. code:: c

         int n = 0, s = 1, i;
         scanf("%d", &n);
         for(i=n;i>0;) {
             s*=i;
             i--;
         }
         printf("%d", s);

   -  第三种，递减-while

      .. code:: c

         int n = 0, s = 1;
         scanf("%d", &n);
         while(n>0) {
             s*=n;
             n--;
         }
         printf("%d", s);

   -  第四种，递增-for

      .. code:: c

         int n = 0, s = 1, i;
         scanf("%d", &n);
         for(i=1;i<=n;i++) {
             s*=i;
         }
         printf("%d", s);

      第一个值是循环的初始值，第二个是循环的条件，第三个是循环的方式

**for循环**

-  for循环像一个计时循环：设定一个计时器，初始化它，然后在计数器到达某值之前，重复执行循环体，而每一执行一轮循环，计数器值以一定步进进行调整，比如加1或者减1

-  .. code:: c

        for(i=0;i<5;i=i+1) {
            printf("%d", i);
        }

-  对于i的定义可以也写在for里面，但是只有C99才支持

**for=对于**

-  for(count=10;count>0;count–)
-  就读成：“对于一开始的count=10，当count>0时，重复做循环体，每一轮循环在做完循环体内语句后，使得count–。”

**小套路**

-  做求和的程序时，记录结果的变量应该初始化为0，而做求积的变量时，记录结果的变量应该初始化为1，否则如果是0的话，那么它最终结果都会是0

**另一种用法**

-  .. code:: c

        int n = 0, s = 1;
        scanf("%d", &n);
        for(;n>0;n--) {
          s*=n;
        }
        printf("%d", s);

3.2.5 循环的选择
----------------

**循环次数**

-  for（i=0；i<n；i++）

-  则循环的次数是n，而循环结束以后，i的值是n。循环的控制变量i，是选择从0开始还是从1开始，是判断i<n还是判断i<=n，对循环的次数，循环结束后变量的值都有影响

   -  如果是i<n，那么循环结束后，i的值是n
   -  如果是i<=n，那么循环结束后，i的值是n+1

-  测试代码：

   .. code:: c

      int i;
      for(i=0;i<5;i++) {
          printf("i=%d ",i);
      }
      printf("\n最后i=%d\n", i);

   -  输出：i=0 i=1 i=2 i=3 i=4 最后i=5
   -  如果i=1开始，i<=5，会输出：i=1 i=2 i=3 i=4 i=5 最后i=6
   -  都能走5遍

两种循环相比较

-  .. code:: c

      int n;

      scanf("%d", &n);
      int fact =1;

      int i=1;
      while(i<=n) {
          fact *=i;
          i++
      }
      printf("%d!=%d\n", n, fact);

-  .. code:: c

      int n;

      scanf("%d", &n);
      int fact =1;

      int i=1;
      for(i=1;i<=n;i++) {
          fact *= i;
      }
      printf("%d!=%d\n", n, fact);

**for==while**

.. code:: c

   for(int i=1;i<=n;i++) {
       fact *= i;
   }

   int i=1;
   while(i<=n) {
       fact*=i;
       i++; 
   }

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021700.png
   :alt: 19

   19

**for循环**

-  for（初始动作；条件；每轮的动作）{

   }

   -  for中的每一个表达式都是可以省略的

-  for(;条件;)==while(条件)

   -  分号是不能省略的，是用来表示哪一个哪一个表达式的

**三种循环**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021701.png
   :alt: 20

   20

**Tips for loops**

-  如果有固定次数，用for
-  如果必须执行一次，用do_while
-  其它情况用while

.. |10| image:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021651.png

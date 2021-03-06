5.1 逻辑类型与逻辑运算
======================

5.1.1 逻辑类型
--------------

**bool类型**

-  #include<stdbool.h>
-  C89有这个雏形，到了C99之后才确定下来，就可以使用bool和true，false

.. code:: c

   #include <stdio.h>
   #include <stdbool.h>

   int main() {
       bool b=6>5;
       bool t=true;
       t=2;
       printf("%d\n",b);//这样得到的是1，而不是true还是false。
       return 0;
   }

-  我们没有一个特定的方法去得到它

我们一般判断一个条件语句，都是利用0与1判断执行还是不执行

5.1.2 逻辑运算
--------------

**逻辑运算**

-  逻辑运算是对逻辑量进行的运算，结果只有0或1
-  逻辑量是关系运算或逻辑运算的结果

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021733.png
   :alt: 24

   24

**应用**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021734.png
   :alt: 25

   25

如何判断一个字符c是否是大写字母？

-  .. code:: c

        c>='A'&&c<='Z'

**理解一下**

-  age>20&&age<30

   -  在20~30内就是true

-  index<0||index>99

   -  index小于0和大于99，而不在0~99这个区间内（也不是端点）

-  !age<20

   -  很多人会将其理解为“age不小于20“，但其实因为我们的“！”是单目运算符，它的优先级会比双目运算符还要高。所以它会先执行！age再执行下一步。
   -  而解决这个问题，只需要加个括号：！（age<20）

**优先级**

-  ！>&&>|\|

   -  !done && (count>Max)
   -  !done && count>Max

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021735.png
   :alt: 26

   26

-  必须要比>低，否则做不了a>6&&a<8

应用

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021736.png
   :alt: 27

   27

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021737.png
   :alt: 28

   28

**短路**

-  逻辑运算是自左向右进行的，如果左边的结果已经能够决定结果了，就不会做右边的计算

   -  .. code:: c

           a==6 && b==1;
           a==6 && b=+1;

-  对于&&，左边是false时就不做右边了

-  对于||，左边是true时，就不做右边了

-  不要把赋值，包括复合赋值组合进表达式

5.1.3 条件运算和逗号运算
------------------------

**条件运算符**

-  count=(count>20)?count-10:count+10

-  条件，条件满足时的值和条件不满足时的值。相当于下面：

   .. code:: c

      if(count>20) {
          count-=10;
      } else {
          count+=10;
      }

-  这个也是语言早期遗留下来的东西

**优先级**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021738.png
   :alt: 29

   29

**嵌套条件表达式**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021739.png
   :alt: 30

   30

-  条件运算符是左右向左结合的

   -  w<x? x+w: x<y? x:y

-  不建议使用嵌套条件表达式，因为这会使你的表达式变得复杂

**逗号运算符**

-  逗号用来连接两个表达式，并以其右边的表达式的值作为它的运算结果。逗号的优先级是所有运算符中最低的，所以它两边的表达式会先计算；
-  逗号的组合关系是自左向右的，所以左边的表达式会先计算，而右边的表达式的值会留下来作为逗号运算的结果

主要是在for中使用

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021740.png
   :alt: 31

   31

5.2 if else拓展
===============

5.2.1 嵌套的if-else
-------------------

求三个整数的最大值

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021741.png
   :alt: 32

   32

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021742.png
   :alt: 33

   33

**嵌套示例**

.. code:: html

   const int READY = 24;
   int code = 0;
   int count = 0;
   scanf("%d %d", &code, &count);
       
   if(code == READY) {
     if(count<20) {
       printf("达到要求"); 
     } else {
       printf("未达到要求");
     }
   }

-  这是我们要的效果

-  它可以转换为下面这种格式

   .. code:: html

      if(code == READY) 
        if(count<20)
          printf("达到要求");
        else 
        printf("未达到要求");

**嵌套的判断**

-  当if的条件满足或者不满足的时候要执行的语句也可以是一条if或if-else语句，这就是嵌套的if语句

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021743.png
   :alt: 34

   34

问题

.. code:: html

   if(code == READY) 
     if(count<20)
       printf("达到要求");
   else 
     printf("未达到要求");

-  当我们想要这样的时候，它却和上一个运行结果一模一样。那怎么办呢？

**else的匹配**

-  else总是和最近的那个if匹配

除非你加个大括号

.. code:: html

   const int READY = 24;
   int code = 0;
   int count = 0;
   scanf("%d %d", &code, &count);
       
   if(code == READY) {
     if(count<20)
       printf("达到要求");
   } else {
     printf("未达到要求");
   }

也知道了…

**缩进**

-  缩进格式不能暗示else的匹配

   .. code:: html

      if(code == READY) 
        if(count<20)
          printf("达到要求");
      else 
        printf("未达到要求");

**另一个例子**

程序一

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021744.png
   :alt: 35

   35

-  这个程序所要表达的意思是：当player2move不等于2时，就会输出那个else下的语句。当gameover不等于0的时候，将什么都不输出（所以它和else没有任何关系）。

程序二

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021745.png
   :alt: 36

   36

-  这个的话，就是当gameover不等于0的时候，最下面的那个else就会输出

程序三

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021746.png
   :alt: 37

   37

-  这个的话，它所要表达的与程序一一样。那个else与gameover等不等与0没有半毛钱关系。但我们想要的是，这个gameover是在gamerover不等于0的时候输出，那怎么办呢？

程序四

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021747.png
   :alt: 38

   38

-  加上大括号，就明了

tips

-  在if或else后面总是用｛｝
-  即使只有一条语句的时候

5.2.2 联级if-else
-----------------

**分段函数**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021748.png
   :alt: 39

   39

**级联的if-else if**

-  上面这段代码就是一个级联的if-else if

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021749.png
   :alt: 40

   40

早期的是这样的

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021750.png
   :alt: 41

   41

而如果这样下去，代码会越来越靠右，就很麻烦。所以人们想出了用级联的方法

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021751.png
   :alt: 42

   42

-  推荐使用左边的代码，因为它是单一出口
-  而且右边的也把代码写死了，不具有灵活性

5.3 多路分支
============

**switch-case**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021752.png
   :alt: 43

   43

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021753.png
   :alt: 44

   44

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021754.png
   :alt: 45

   45

**break**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021755.png
   :alt: 46

   46

**案例-转换成绩**

版本一

.. code:: c

   int score;
   scanf("%d",&score);
   score/=10;  

   switch(score) {
       case 10:
       case 9:
           printf("A");
           break;
       case 8:
           printf("B");
           break;
       case 7:
           printf("C");
           break;
       case 6:
           printf("D");
           break;
       default:
           printf("E");
           break;
       }

版本二

.. code:: c

   int score = 0;
   scanf("%d",&score);
       
   if(score>=90) {
       printf("A");
   } else if(score>=80) {
       printf("B"); 
   } else if(score>=70) {
       printf("C");
   } else if(score>=60) {
       printf("D");
   } else {
       printf("E");
   }

-  但这些代码都不符合我们的“单一出口”原则，因为我们还没学习字符或者字符串型数据的处理

switch的经常使用

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021756.png
   :alt: 47

   47

-  今后用数组来做更好

5.4 案例训练
============

程序语言无非就是输入输出，分支语句，调用函数等等。但编程难究竟是难在哪里呢？难在想问题，简单来说就是如何把一个问题转换为一个程序，一个算法

5.4.1 循环计算
--------------

**小套路**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021757.png
   :alt: 48

   48

一样

.. code:: c

   int x, ret=-1;
   scanf("%d",&x);
   int t = x;
   while(x>0) {
       x/=2;
       ret++;
   }
   printf("%d是2的%d次方",t,ret);
   return 0;

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021758.png
   :alt: 49

   49

-  有一种方法去模拟一下，就是你拿出一张纸，在上面写着运行结果。也就意味着，你需要写100多次。那太麻烦了，怎么办？
-  小套路：如果要模拟运行一个很大次数的循环，可以模拟较少的循环次数，然后作出推断

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021800.png
   :alt: 51

   51

5.4.2 算平均数
--------------

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021801.png
   :alt: 52

   52

**变量**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021802.png
   :alt: 53

   53

**算法**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021803.png
   :alt: 54

   54

**我的版本**

.. code:: c

   int x, sum;
   double n=0.0;
   do {
       scanf("%d",&x);
       sum+=x;
   } while(x!=-1);
   sum+=1;
   scanf("%lf",&n);
   printf("平均数是%f",sum/n);

老师的版本

.. code:: c

   int number;
   int sum = 0;
   int count=0;

   do {
       scanf("%d", &number);
       if(number != -1) {
           sum += number;
           count++;
       }
   }while(number != -1);//但这里有一个不好就是双重判断了

   printf("%f\n", 1.0*sum/count);

老师的版本2

.. code:: c

   int number;
   int sum = 0;
   int count=0;
   scanf("%d", &number);
   while(number != -1) {
       sum += number;
       count++;
       scanf("%d", &number);
   }

   printf("%f\n", 1.0*sum/count);

一个问题，可以用多种算法解决，条条大路通罗马

5.4.5 猜数游戏
--------------

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021804.png
   :alt: 55

   55

**算法**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021805.png
   :alt: 56

   56

**代码**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021806.png
   :alt: 57

   57

**随机数**

-  每次召唤rand（）就得到了一个随机的整数

**%100**

-  x%n的结果是[0，n-1]的一个整数

我的版本

.. code:: c

   #include <stdio.h>
   #include <stdlib.h>
   #include <time.h>

   int main() {
       srand(time(0));
       int a = rand()%10;
       int num;
       scanf("%d", &num);
       
       while(num!=a) {
           if(a>num) {
               printf("你猜小了\n");
           } else if(a<num){
               printf("你猜大了\n");
           }
           scanf("%d", &num);
       }
       
       printf("你猜对了\n");
       return 0;
   }

5.4.6 整数逆序
--------------

**整数的分解**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021807.png
   :alt: 58

   58

**数的逆序**

-  输入一个正整数，输出逆序的数

   -  结尾的0的处理

老师的版本（和我的一样-这个是包括0的版本）

.. code:: c

   int digit,x;
   x = 12345600;
   int ret = 0;
       
   while(x>0) {
       digit = x%10;
       printf("%d ", digit);
       x/=10;
   }
       return 0;

老师的版本（这个是不包括0的版本）

.. code:: c

   int digit,x;
   x = 12345600;
   int ret = 0;
       
   while(x>0) {
       digit = x%10;
       ret = ret*10+digit;
       x/=10;
   }
   printf("%d", ret);
       return 0;

我的版本-不包括0；

.. code:: c

   #include <stdio.h>

   int main() {
       int digit,x;
       x = 12345600;
       
       while(x>0) {
           digit = x%10;
       x/=10;
       if(digit!=0) 
           printf("%d ", digit);
       }
       
       return 0;
   }

5.5 if语句常见的错误
====================

**忘了大括号**

测试程序

.. code:: c

   int age = 0;
   double salay = 4000;

   age = 55;
   if(age>60)
       salary = salary*1.2;
       printf("%f\n", salary);//这句是无论是不是大于60都执行的，与你的缩进无关

所以解决方法：

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021809.png
   :alt: 60

   60

**if后面的分号**

这个代码是很多初学者会犯的错误

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021810.png
   :alt: 61

   61

.. code:: c

   if(age>60);//这个是会执行的，而下面的将会变成普通语句，不会跟随if
   {
       salary = salary * 1.2;
       printf("%f", salay);
   }

**错误使用==和=**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021811.png
   :alt: 62

   62

if（）这个框里面，如果你用的是“=”，那么它会变成赋值运算，当然这个等号右边的数必须是非零

代码示例

.. code:: c

   int age = 0;
   double salary = 4000;
   age = 55;
   if(age = 60) {
       salary*=1.2;
       printf("%f\n", salary);
   }

   //这段代码会提示你warning，但它能执行出结果，可是我们不要忽略它，要解决好每一个warning。

   //它会输出4800，也就是成功执行了if语句大括号内部的语句。

但是，当等号右边是0的时候呢？

.. code:: c

   int age = 0;
   double salary = 4000;
   age = 55;
   if(age = 0) {
       salary*=1.2;
       printf("%f\n", salary);
   }

   //程序会没有结果，因为这个0在if语句的意思是假，是false，所以不会执行if大括号内部的代码

**代码风格**

-  在if和else之后必须加上大括号形成语句块
-  大括号内的语句缩进一个tab的位置

三种if-else的风格

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021812.png
   :alt: 63

   63

-  我们有着这三种的风格，那么它们每一种有什么不一样呢？

   -  第一种：是因为一开始的编程的高很小，你只能看很少段，于是为了能够看到更多代码，就这样缩
   -  第二种：而由于我们现在使用的电脑屏幕较大了（有人把电脑转个90度，看的代码就多了），所以可以这样写了
   -  第三种：第三种的好处就是方便注释掉一个if else语句块
   -  一般大厂会对你的代码规范有要求

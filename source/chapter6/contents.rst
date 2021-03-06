6.1 数组基础
============

6.1.1 初试数组
--------------

求平均数的题目

.. code:: c

   int x;
   double sum = 0;
   int cnt = 0;
   scanf("%d", &x);
   while(x!=-1) {
       sum+=x;
       cnt++;
       scanf("%d", &x);
   }
   if(cnt>0) {
       printf("%f\n", sum/cnt);
   }

但是，如果题目变了呢？要求你写一个程序计算用户输入的数字的平均数，并输出所有大于平均数的数，那怎么办？

如何记录很多数呢？

-  int num1, num2, num3…

**数组**

-  int number[100];
-  scanf(“%d”, &number[i]);

.. code:: c

   int sum=0, x, count=0, number[100];//定义数组
   double average;
       
   scanf("%d", &x);
   while(x!=-1) {
       number[count] = x;//对数组中的元素赋值
       {
           int i;
           printf("%d\t",count);
           for(i=0;i<=count;i++) {
               printf("%d\t", number[i]);
           }
           printf("\n");
       }
       sum+=x;
       count++;
       scanf("%d", &x);
   }

   if(cnt>0) {
       int i;
       average = 1.0*sum/count;
       for(i=0;i<count;i++) {//遍历数组
           if(number[i]>average) {
               printf("%d", number[i]);//使用数组中的元素
           }
       }

   }
   return 0;

-  但个程序存在\ **安全隐患**\ ，是什么？

   -  看一下它的数组数量的定义，是固定的，所以当我们输入的数大于这个元素数量，那么就会出现问题。

6.1.2 定义数组
--------------

定义数组

-   变量名称[元素数量];

   -  int grades[100];
   -  double weight[20];

-  元素数量必须是整数
-  C99之前：元素数量必须是编译时刻确定的字面量

数组

-  数组是一种容器（放东西的东西），特点是：

   -  其中所有的元素具有相同的数据类型；
   -  一旦创建，不能改变大小
   -  （数组中的元素在内存中是连续依次排列的）

-  语言所能提供容器的大小，可以提现出语言能力的大小

int a[10]

-  一个int的数组
-  10个单元：a[0], a[1]…., a[9]
-  每个单元就是一个int类型的变量
-  可以出现在赋值的左边或右边；

   -  a[2] = a[1]+6;

-  在赋值左边的叫做左值（与指针有关）

数组的单元

-  数组的每一个单元救赎数组类型的一个变量
-  使用数组时放在[]中的数字叫做下标或索引，下标从0开始计数：

   -  grades[0]
   -  grades[99]
   -  average[5]

-  不只是C语言有数组，但是从0开始起，是从C语言起的

有效的下标范围

-  编译器和运行环境都不会检查数组下标是否越界，无论是对数组单元做读还是写
-  一旦程序运行，越界的数组访问可能造成问题，导致程序奔溃

   -  segmentation fault

-  但是也可能运气好，没造成严重的后果
-  所以这是程序员的责任来保证程序只使用有效的下标值：[0，数组大小-1]

所以上面的程序是有问题的，那么我们有两个解决方案：

-  一，局限性的一百个元素数量
-  二，在计算的过程中来计数（C99新功能）

计算平均数

-  如果先让用户输入有多少数字要计算，可以用C99的新功能来实现

.. code:: c

   int x;
   double sum = 0;
   int cnt;
   printf("请输入数字的数量：");
   scanf("%d", &cnt);
   if(cnt>0) {
       int number[cnt];
       scanf("%d", &x);
       while(x!=-1) {
           number[cnt]=x;
           sum+=x;
           cnt++;
           scanf("%d", &x);
       }
   }

-  这个数组创造了，就不能再改变了，这是数组的根本特点。

长度为0的数组？

-  int a[0];
-  可以存在，但是无用，也就是没有意义

.. code:: c

   int sum=0, x, count=0, number[100];
   double average;
   scanf("%d", &x);
   while(x!=-1) {
       number[count] = x;
       sum+=x;
       count++;
       scanf("%d", &x);
   }
   average = 1.0*sum/count;
   while(count!=0) {
       if(number[count-1]>average)
           printf("%d ", number[count-1]);
       count--;
   }
   return 0;

6.1.3 用数组做散列计算
----------------------

-  写一个程序，输入数量不确定的[0,9]范围内的整数，统计每一种数字出现的次数，输入-1表示结束；

**三种算法**

一，最优算法

.. code:: c

   const int number = 10;//数组的大小
   int num[number];
   int x;
   int i;
   for(i=0;i<number;i++) {//初始化，这是个安全的做法
       num[i]=0;
   }
   scanf("%d", &x);
   while(x!=-1) {
       if(x>=0&&x<=9) {
           num[x]++;//参与运算
       }
       scanf("%d", &x);
   }   
   for(i=0;i<number;i++) {
       printf("有%d个%d\n", num[i], i);
   }
   return 0;

-  要懂的掌握简单方法和技巧

二，我的版本

.. code:: c

   #include <stdio.h>

   int main() {
       int num[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
       int number[100];
       int x, count = 0;
       
       scanf("%d", &x);
       while(x!=-1) {
           number[count] = x;
           count++; 
           scanf("%d", &x);
       }
       
       int i, j;
       for(i=0;i<count;i++) {
           for(j=0;j<10;j++) {
               if(number[i]==j) {
                   num[j]++;
               }
           }
       }
       for(i=0;i<10;i++) {
           printf("有%d个%d\n", num[i], i);
       }
       
       return 0;
   }

三，分支思路

.. code:: c

   int number[100];
   int x,count=0;
   int one=0, two=0, three=0, four=0, five=0, six=0, seven=0, eight=0, nine=0, ten=0, zero=0;
       
   scanf("%d", &x);
   while(x!=-1) {
       number[count] = x;
       count++;
       scanf("%d", &x);
   }
       
   printf("%d", count);
   count--;
       while(count!=0) {
           switch(number[count]) {
               case 1:
                   one++;
                   break;
               case 2:
                   two++;
                   break;
               case 3:
                   three++;
                   break;
               case 4:
                   four++;
                   break;
               case 5:
                   five++;
                   break;
               case 6:
                   six++;
                   break;
               case 7:
                   seven++;
                   break;
               case 8:
                   eight++;
                   break;
               case 9:
                   nine++;
                   break;
               case 10:
                   ten++;
                   break;
               default:
                   zero++;
                   break;
           }
           count--;
       }
       
       printf("1:%d\n 2:%d\n 3:%d\n", one, two, three);
       return 0;

6.2 函数基础
============

6.2.1 初见函数
--------------

素数求和

.. code:: c

   int isPrime(int i) {
       int ret=1;
       int k;
       for(k=2;k<i-1;k++) {
           if(i%k==0) {
               ret=0;
           }
       }
       return ret;
   }

   int main() {
       int m, n;
       int i;
       int sum=0;
       scanf("%d %d", &m, &n);
       
       if(m==1) m=2;
       for(i=m;i<=n;i++) {
           if(isPrime(i)) {
               sum+=i;
           }
       }
       printf("%d", sum);
       return 0;
   }

"代码复制“是代码质量不好的表现

.. code:: c

   void sum(int a, int b) {
       int sum;
       int i;
       for(i=a;i<=b;i++) {
           sum+=i;
       }
       printf("从%d到%d的和是%d\n", a, b, sum); 
   }

   int main() {
       int m, n;
       scanf("%d %d", &m, &n);
       sum(m, n);
       return 0;
   }

-  要把代码相同，或者重复的部分取出来封装成函数

6.2.2 函数的定义和使用
----------------------

什么是函数？

-  函数是一块代码，接收零个或多个参数，做一件事情，并返回零个或一个值
-  可以先想象成是数学中的函数

   -  y=f(x)

函数定义

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021936.png
   :alt: 64

   64

调用函数

-  函数名（参数值）
-  （）起到了表示函数调用的重要作用

   -  即使没有参数也需要（）

-  如果有参数，则需要给出正确的数量和顺序
-  这些值会被按照顺序依次用来初始化函数中的参数
-  sum与sum（），分清楚

函数返回

-  函数知道每一次是哪里调用它，会返回到正确的地方

6.2.3 从函数中返回
------------------

从函数中返回值

-  我们都知道C语言有个原则“单一出口”

   -  .. code:: c

           int max(int a, int b) {
               int ret;
               if(a>b) {
                   ret = a;
               } else {
                   ret = b;
               }
               return ret;
           }

-  .. code:: c

        int max(int a, int b) {
            if(a>b) {
                return a;
            } else {
                return b;
            }
        }//这个程序不好，就是因为有多个出口，这个可以，但这个不太好

-  return停止函数的执行，并送回一个值

   -  return；
   -  return 表达式；

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021937.png
   :alt: 65

   65

-  丢弃那种比较常见，有时候我们没有返回值，就是这种了

没有返回值的函数

-  void函数名（参数表）
-  不能使用带值的return

   -  可以没有return

-  调用的时候不能做返回值赋值

   -  而如果函数是有返回值的，那就必须带return返回值

6.3 函数深入
============

6.3.1 函数原型
--------------

函数先后关系

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021938.png
   :alt: 66

   66

-  如果你在它调用之前，而没有声明过sum，那它会一脸懵逼的

如果不知道

-  也就是把要调用的函数放到下面了

.. code:: c

   int main() {
       sum(1, 10);
       sum(20, 30);
       sum(35, 45);
       return 0;
   }

   void sum(int begin, int end) {
       int t;
       int sum = 0;
       for(i=begin;i<=end;i++) {
           sum+=i;
       }
       printf("%d到%d的和是%d\n", begin, end, sum);
   }

-  会出现错误（在LLVM编译器下的结果，可能也是因为它是一个严格的编译器）

-  而我们不想把函数放在前面，因为它会太繁杂，而挡住了主函数，那怎么办呢？这个时候我们就用到了函数的原型声明：

   .. code:: c

      void sum(int begin, int end);//把函数头移到前面

      int main() {
          sum(1, 10);
          sum(20, 30);
          sum(35, 45);
          return 0;
      }
      //这下面这一块叫函数的定义
      void sum(int begin, int end) {
          int t;
          int sum = 0;
          for(i=begin;i<=end;i++) {
              sum+=i;
          }
          printf("%d到%d的和是%d\n", begin, end, sum);
      }

   -  我们也要确保它的声明和定义的函数头是相同的，否则就是白费

函数原型

-  函数头，以分号“；“结尾，就构成了函数的原型

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021939.png
   :alt: 67

   67

-  函数原型的目的是告诉编译器这个函数长什么样

   -  名称
   -  参数（数量及类型）
   -  返回类型

-  旧标准习惯把函数原型写在调用它的函数里面。旧版的会像下面一样：

   .. code:: c


      int main() {
          int i;
          void sum(int begin, int end);//把函数头移到前面

          sum(1, 10);
          sum(20, 30);
          sum(35, 45);
          return 0;
      }
      //这下面这一块叫函数的定义
      void sum(int begin, int end) {
          int t;
          int sum = 0;
          for(i=begin;i<=end;i++) {
              sum+=i;
          }
          printf("%d到%d的和是%d\n", begin, end, sum);
      }

   -  旧版的会像上面这个一样，它的所有初始化或者声明（无论是变量还是函数这些）都是在前面的

-  现在一般写在调用它的函数前面

-  再深入

   .. code:: c

      void sum(int , int );//这样也不会有影响，因为只是提醒它有这个函数存在
      //void sum(int a, int b);也可以，但为了对人类有意义，最好还是和下面的函数头相匹配（相同的）
      int main() {
          sum(1, 10);
          sum(20, 30);
          sum(35, 45);
          return 0;
      }

      void sum(int begin, int end) {
          int t;
          int sum = 0;
          for(i=begin;i<=end;i++) {
              sum+=i;
          }
          printf("%d到%d的和是%d\n", begin, end, sum);
      }

6.3.2 参数传递
--------------

**调用函数**

-  如果函数有参数，调用函数时必须传递给它数量，类型正确的值
-  可以传递给函数的值是表达式的结果，这包括：

   -  字面量
   -  变量
   -  函数的返回值
   -  计算的结果

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021940.png
   :alt: 68

   68

类型不匹配？

-  调用函数时给的值与参数的类型不匹配是C语言传统上最大的漏洞

-  编译器总是悄悄替你把类型转换好，但是这很可能不是你所期望的

   -  .. code:: c

         void cheer(int i) {
             printf("cheer %d\n", i);
         }

         int main() {
             cheer(2.0);//输出2
             double f = 2.4;
             cheer(f);//输出2

             return 0;
         }

-  后续的语言，C++/Java在这方面很严格

传过去的是什么？

.. code:: c

   void swap(int a, int b);

   int main() {
       int a=5, b=5;
       swap(a, b);
       printf("a=%d, b=%d\n", a, b);
       
       return 0;
   }

   void swap(int a, int b) {//这里的a和b和上面的a和b没有任何关系
       int swap;
       int t = a;
       a = b;
       b = t;
   }

-  这样完全不能交换a和b的值
-  所以C语言在调用函数时，永远只能传值给函数

传值

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021941.png
   :alt: 69

   69

-  这个传参与实参来源于Fortran，而有些语言的确能在调用函数的时候传入变量。
-  我们认为它们是参数和值的关系

6.3.3 本地变量
--------------

本地变量

-  函数的每次运行，就产生了一个独立的变量空间，在这个空间中的变量，是函数这次运行所独有的，称作本地变量
-  定义在函数内部的变量就是本地变量
-  参数也是本地变量，在参数表里面的这些参数与本地变量一样具有相同的作用域

变量的生存期和作用域

-  生存期：什么时候这个变量开始出现，到什么时候它消亡了

-  作用域：在（代码的）什么范围内可以访问这个变量（这个变量可以起作用）

-  对于本地变量，这两个问题的答案是统一的：大括号内—快

-  自己的结论：而当两个函数拥有着相同变量名且相同类型的变量时，它们其实都互不相关

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021942.png
   :alt: 70

   70

本地变量的规则

-  本地变量是定义在块内的

   -  它可以是定义在函数的块内

   -  也可以是定义在语句的块内（If语句）

   -  定义在大括号内也一样，例如下面这一句。

      .. code:: c

         //例一
         {
             int i = 888;
         }

         printf("%d", i);//它会出现error说你没有声明定义这个变量；

         //例二
         int i = 999;
         {
             int i = 888;
         }

         printf("%d", i);//它会输出999，而不是888.为什么呢？因为它的生存周期与作用域只在大括号里面

-  也就是程序运行进入这个块之前，其中的变量不存在，离开这个块，其中的变量就消失了

-  块外面定义的变量在里面仍然有效，例如

   .. code:: c

      int i = 999;
      {
         printf("%d", i);//它会输出999
      }

-  块里面定义了和外面同名的变量则掩盖了外面的

   .. code:: c

      int a = 5;
      int b = 6;

      {
          int a = 0;
          printf("a=%d\n", a);//输出0
      }
      printf("a=%d, b=%d\n", a, b);//输出a=5，b=6。因为在这里的话，里面括号的那个a就消失了，不见了

-  不能在块内定义同名的变量

-  本地变量不会被默认初始化

-  但参数在进入函数的时候就会被初始化了（就是在调用函数的时候输入的实参）

6.3.4 杂事
----------

没有参数时

-  void f（void）；

-  还是void f（）；

   -  在传统C中，它表示f函数的参数表未知，并不表示没有参数

      .. code:: c

         void swap();

         int main() {
             int a=5, b=5;
             swap(a, b);//因为函数是需要两个int的传递
             printf("a=%d, b=%d\n", a, b);

             return 0;
         }

         void swap(int a, int b) {能编译
             int swap;
             int t = a;
             printf("a=%f, b=%f", a, b); 
             a = b;
             b = t;
         }

      例二

      .. code:: c

         void swap();//2.所以不要写出这样的原型来
         //void swap(void);要这样写

         int main() {
             int a=5, b=5;
             swap(a, b);
             printf("a=%d, b=%d\n", a, b);

             return 0;
         }

         void swap(double a, double b) {//1.得到的数字很奇怪
             int swap;
             int t = a;
             printf("a=%f, b=%f", a, b); 
             a = b;
             b = t;
         }

逗号运算符？

-  调用函数时的逗号和逗号运算符怎么区分？

   -  f(a, b)这个是函数的标点符号
   -  f((a, b))这个是逗号运算，是一个结果

-  调用函数时的圆括号里的逗号是标点符号，而不是运算符

函数里的函数？

-  C语言不允许函数嵌套定义
-  但可以放另一个函数的声明

这是什么？

-  int i, j, sum(int a, int b);

   -  C语言支持这样的写法，但不推荐

-  return (i);

   -  这个括号可以加也可以不加都行
   -  而加上了会让人类误以为i是函数

关于main

-  int main()也是一个函数
-  要不要写成int main(void)？
-  return的0有人看吗？

   -  Windows：if error level 1…
   -  Unix Bash：echo $?
   -  Csh: echo $status
   -  return 0是有意义的

-  main函数不是程序第一条运行的代码，在mian函数前还有其它东西，这些东西是为你的运行做准备的，当做好准备后，会调用main函数

6.4 数组进阶
============

6.4.1 二维数组
--------------

二维数组

-  .. code:: c

        int a[3][5];
        //int a[行][列]

-  通常理解为a是一个3行5列的矩阵

   .. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021943.png
      :alt: 71

      71

二维数组的遍历

.. code:: c

   for(i=0;i<3;i++) {
       for(j=0;j=5;j++) {
           a[i][j]  = i*j;
       }
   }

   //a[i][j]是一个int

-  表示第i行第j列上的单元

   -  a[i, j]是什么？

      -  这个不是一个正确的表达二元数组的方式，在这里，它是个逗号运算，其结果是j。所以它表达a[j]

二维数组的初始化

.. code:: c

   int a[][5] = {
       {0, 1, 2, 3, 4},
       {2, 3, 4, 5, 6},
   };

-  列数是必须给出的，行数可以由编译器来数
-  每行一个｛｝，逗号分隔
-  最后的逗号可以存在，有古老的传统
-  如果省略，表示补零
-  也可以用定位（\* C99 ONLY）

tic-tac-toe游戏（井字棋）

-  读入一个3*3的矩阵，矩阵中的数字为1表示该位置上有一个X，为0表示为O
-  程序判断这个矩阵中是否有获胜的一方，输出表示获胜一方的字符X或O，或输出无人获胜

.. code:: c

   //1.读入矩阵 
       const int size = 3;
       int board[size][size];
       int i, j;
       int numOfX;
       int numOfO;
       int result = -1;

       for(i=0;i<size;i++) {
           for(j=0;j<size;j++) {
               scanf("%d", &board[i][j]);
           }
       }

   //2.判断是否赢了（检查行）
       for(i=0;i<size&&result==-1;i++) {
           numOfO=numOfX=0;
           for(j=0;j<size;j++) {
               if(board[i][j]==1) {
                   numOfX++;
               } else {
                   numOfO++;
                   printf("执行了%d, numOfO=%d\n", i, numOfO);
               }
           }
           
           if(numOfO==size) {
               result = 0;
               printf("执行了？\n");
           } else if(numOfX==size) {
               result = 1;
           }
       }


   //3.检查列
   if(result == -1) {
       for(j=0;j<size&&result==-1;j++) {
           numOfX=numOfO=0;
           for(i=0;i<size;i++) {
               if(board[i][j]==1) {
                   numOfX++;
               } else {
                   numOfO++;
               }
           }
           
           if(numOfO==size) {
               result = 0;
           } else if(numOfX==size) {
               result = 1;
           }
       }
       
       
   }


       printf("%d", result);
       

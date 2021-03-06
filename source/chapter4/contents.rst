4.1 循环控制及其应用
====================

4.1.1 循环控制
--------------

**找到从2到100的素数**

-  .. code:: c

        int i, j, num = 0, n=0;
        for(i=2;i<=100;i++) {
            for(j=1;j<=i;j++) {
                if(i%j==0) {
                    num++;
                }
            }
            if(num==2) {
                printf("%d ", i);
                n++;
            } else {
                num = 0;
            }
            num = 0;
        }
        printf("有%d个素数", n);

-  素数是只能被1和自己整除的数，不包括1

**判断一个数是不是素数**

-  .. code:: c

        int x, i, isPremer = 1;
        scanf("%d", &x);
        for(i=2;i<x;i++) {
            if(x%i==0) {
                isPremer = 0;
                break;
            }
        } 
        if(isPremer) {
            printf("%d是素数", x);
        } else {
            printf("%d不是素数", x);
        }

**break vs continue**

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021713.png
   :alt: 21

   21

-  break：跳出循环
-  continue：跳过循环这一轮剩下的语句进入下一轮

另一个版本的求素数：但不推荐这样做

.. code:: c

   int x, i;
   scanf("%d", &x);
   for(i=2;i<x;i++) {
       if(x%i==0) {
           break;
       }
   } 
   if(i<x) {
       printf("%d不是素数", x);
   } else {
       printf("%d是素数", x);
   }

4.2 嵌套的循环
==============

4.2.1 循环的嵌套与跳出循环
--------------------------

**找到从2到100的素数**

.. code:: c

   int i, j, isPrime = 1, n=0;
   for(i=2;i<=100;i++) {
       for(j=2;j<i;j++) {
           if(i%j==0) {
               isPrime = 0;
               break;
           }
       }
       if(isPrime) {
           printf("%d ", i);
           n++;
       } else {
           isPrime = 1;
       }    
   }
   printf("有%d个素数", n);

**求素数算法总结**

-  第一种：遍历1~n的数，用它们除以，记录能整除的次数有多少，如果是2，那么就是素数，否则就不是素数
-  第二种：不除1，不除n，但只要在2~n-1这个范围里面发现它能整除另一个整数，那么就不是素数
-  第二种方法节省时间

**嵌套的循环**

-  在循环里面还有循环

**凑硬币（跳出多层循环）**

-  用1角，2角，5角凑出10元以下

-  .. code:: c

        int x, one, two, five, n, times=1;
        scanf("%d", &x);
        n=x*10;
        for(one = 1; one<n/1;one++) {
            for(two = 1; two<n/2;two++) {
                for(five = 1; five<n/5;five++) {
                    if(five*5 + one*1 + two*2 == n) {
                        printf("%d、%d张1角 + %d张2角 + %d张5角 可以凑出%d元\n", times, one, two, five, x);
                        times++;
                    }
                }
            }
        }

-  但这样的话，我们会得到很多结果，但我们只需要一个就够了，那怎么办呢？

   -  用break？

      -  行不通，还是那么多结果，所以我们可以知道，break和continue只能对它所在的那层循环做，而做不到所有循环

      -  我们就有了第二种方法，给每层都加个break

         .. code:: c

            int x, one, two, five, n, times=1;
            scanf("%d", &x);
            n=x*10;
            for(one = 1; one<n/1;one++) {
                for(two = 1; two<n/2;two++) {
                    for(five = 1; five<n/5;five++) {
                        if(five*5 + one*1 + two*2 == n) {
                            printf("%d、%d张1角 + %d张2角 + %d张5角 可以凑出%d元\n", times, one, two, five, x);
                            times++;
                            break;
                        }
                    }
                    break;
                }
                break;
            }

         -  但也是行不通，那么它每层都会break

那么我们就有另一条思路：判断，if语句

**接力break**

.. code:: c

   int x, one, two, five, n, exit=0;
   scanf("%d", &x);
   n=x*10;
   for(one = 1; one<n/1;one++) {
       for(two = 1; two<n/2;two++) {
           for(five = 1; five<n/5;five++) {
               if(five*5 + one*1 + two*2 == n) {
                   printf("%d张1角 + %d张2角 + %d张5角 可以凑出%d元\n", one, two, five, x);
                   exit = 1;
                   break;
               }
           }
           if(exit)break;
       }
       if(exit)break;
   }

**goto语句**

.. code:: c

   int x, one, two, five, n;
   scanf("%d", &x);
   n=x*10;
   for(one = 1; one<n/1;one++) {
       for(two = 1; two<n/2;two++) {
           for(five = 1; five<n/5;five++) {
               if(five*5 + one*1 + two*2 == n) {
                   printf("%d张1角 + %d张2角 + %d张5角 可以凑出%d元\n", one, two, five, x);
                   goto out;
               }
           }
       }
   }
   out:

-  go to的原理是：设置一个标号，这个标号就放在你想要go to跳到的地方
-  go to在历史上是有不好的，会破坏程序的结构性，所以很多人不会推荐去用go
   to
-  但在某种场合下，还是可以使用的，比如需要从多层循环中跳到最外层

4.3 案例
========

4.3.1 前n项求和
---------------

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021714.png
   :alt: 22

   22

.. code:: c

   int i, n;
   double sum = 0.0;
   scanf("%d", &n);
   for(i=1;i<=n;i++) {
       sum += 1.0/i;
   }
   printf("%f", sum);

.. figure:: https://raw.githubusercontent.com/Yuanfeng123/PicBed/main/2021/season2/20210412021715.png
   :alt: 23

   23

**算法一**

.. code:: c

   int i, n;
   double sum = 0.0;
   scanf("%d", &n);
   for(i=1;i<=n;i++) {
       if(i&1) {
           sum += 1.0/i;
       } else {
           sum -=1.0/i;
       }
   }
   printf("%f", sum);

**算法二**

.. code:: c

   int i, n;
   double sum = 0.0, sign = 1.0;
   scanf("%d", &n);
   for(i=1;i<=n;i++) {
       sum+=sign/i;
       sign = -sign;
   }
   printf("%f", sum);

**算法三**

.. code:: c

   int i, n;
   double sum = 0.0, sign = 1;
   scanf("%d", &n);
   for(i=1;i<=n;i++) {
       sum+=sign*1.0/i;
       sign = -sign;
   }
   printf("%f", sum);

易错点

.. code:: c

   int main() {
       int n=0, i = 1;
       double sum = 0;
       scanf("%d", &n);
       for(;i<=n;i++) {
           sum += 1.0/i;//这里的1一定要是个浮点数
       }
       printf("%f", sum);
   }

4.3.2 求最大公约数
------------------

输入两个数a和b，输出它们的最大公约数

-  输入：12 18
-  输出：6

**算法一**

.. code:: c

   int t, n1, n2;
   printf("第一个数字：");
   scanf("%d", &n1);
   printf("第二个数字：");
   scanf("%d", &n2);
   while(n2>0) {
       t=n2;
       n2=n1%n2;
       n1=t;
   }
   printf("%d", t);

算法二

.. code:: c

   int

4.3.3 整数分解
--------------

**反转整数**

.. code:: c

   int a, t;
       
   a=1234560;

   while(a!=0) {
       printf("%d ",a%10);
       a=a/10;
   }

.. code:: c

       int x, t, i;
       
       x=1234560;
       t = x;
       int b, arr=0;
       while(t>0) {
           b=t%10;
           t=t/10;
           arr=arr*10+b;
       }
       
       printf("%d\n", arr);
       
       while(arr!=0) {
           printf("%d ",arr%10);
           arr=arr/10;
       }

我们有两种算法解决这个问题

-  一，先算出位数，再求解
-  二，先把需要求得数进行反转，再求解

.. code:: c

   int x, mask=1, t;
   t=x;
   while(t>0) {
       t%10;
       mask*=10;
   }

   while(x!=0) {
       printf("%d ",x%mask);
       x=x/10;
       mask/=10;
   }

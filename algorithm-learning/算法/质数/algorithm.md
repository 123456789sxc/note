algorithm

> 什么是质数和合数
>
> 质数大于1，且只能被1和自身整除的整数
>
> 合数大于1，不是质数的整数是合数

1. 判断某一个数n是否为质数(试除法):

```c++
bool is_prime(int n)
{
    if(n<2) return false;
    else{
        for(int i = 2;i<n;i++)                    //改进：for(int i = 2;i<=n/i;i++)
        {
            if(n%i == 0) return false;
        }
        return true;
    }
}
```

思路：如果n小于2，一定不是质数。如果n大于1，判断 $[2,n)$ 里是否存在一个数能整除n，如果存在就不是质数，如果循环结束(即不存在)，那么n就是质数。

改进：如果数n不是质数，那么一定存在两个因数，一个大于等于sqrt(n)，另一个小于等于sqrt(n)，那么如果在$[2,sqrt(n)]$ 范围内找不到能整除n的因数，那么n就是质数。

改进的好处是直接少判断一半





> 什么是质因数
>
> 质因数，既是因数又是质数。

> 分解质因数：
>
> 将一个数分解成多个因数相乘，每个因数都是质数。即将一个数分解成多个质因数相乘的形式
>
> 举例 8的质因数有2. 分解质因数为8 = 2 * 2 * 2

> 算术的基本定理：
>
> 任意大于1的整数N，如果N不是质数，那么就能分解成 **唯一一个** 有限个质数相乘的形式。

算术的基本定理来源于质数的定义，因为质数要求本身不能被除1和自身之外的数整除，那么大于1的整数除了质数，剩下的就是合数，合数就是能被其他数整除的数。合数能分解成质数*质数，或者合数 * 合数，或者合数 * 质数，质数不能再分，而合数可以再分成质数，即任意一个不是质数的数，都能分解成有限个质数相乘的形式。



根据以上定义，考虑如何求解一个数N分解成多个质因数相乘的形式：

举一个例子，当N=100时，

从2遍历到100，左闭右开，找出100的所有因数，第一个因数一定是质因数，100的一个质因数是2，即 100可以分解成  2 *  50，50又能分解成 2 * 25，即100  =  2 * 2 * 25。25分不出来2了。 

现在又变成了找25的分解质因数，找25的因数，3、4都不行，5可以。25 一个质因数是5，另一个因数也是5

即100 = 2^2 * 5^2  

100找到**第一个质因数**2，然后找**2的指数** ，然后  剩下 25， **接着找质因数** 5  ，再找**5的指数**  

思路：一个数N先找到质因数i，然后 x =  N/i     ，判断x还能不能分解出 i ，

**我们从2遍历到N ，左闭右开，找出N的所有因数，第一个因数一定是质因数。**

```c++
void divide(int n)
{
    for(int i = 2;i<n;i++)
    {
        if(n%i == 0)
        {
            int s = 0;
            while(n % i == 0)
            {
                n = n/i;       //既然i是n的一个质因数，那么n/i就是另一个因数。这个while循环是判断
                s++;           //  n/i这个因数还能分解出几个 i   ，s是分解出来i的个数。
            }
            printf("%d %d\n",i,s)
        }
    }
    if(n>1) printf("%d 1\n",n);
}
```

最后一条if语句是，最后会有一个质数，即以下这种情况，可以跟100的对比理解。

当N = 90 时， N = 2 * 45， 45 = 3* 3 * 5

即 90 = 2 * 2 * 3 * 3 * 5；



2. 求小于n的质数的个数

暴力枚举：依次判断 $[1,n)$ 的质数个数

```c++
bool is_prime(int n)
{
    if(n<2) return false;
    for(int i = 2;i<=n/i;i++) if(n%i == 0) return false;
    return true;
}

void find_prime(int n)
{
    int res = 0;
    for(int i = 2;i<n;i++)
    {
        if(is_prime(i)) res++;
    }
}
```

朴素筛质数法：

小知识：

> **!**运算符被称为逻辑非运算符，执行逻辑 NOT 操作。它可以反转一个操作数的真值或假值。换句话说，如果表达式为 true，那么 !运算符将返回 false，如果表达式为 false，则返回 true。

> 定义在全局中的int变量和bool变量，初始值为0

![1679039269526](algorithm.assets/1679039269526.png)

```c++
const int N = 100010;
int primes[N],cnt;     //primes存放质数，cnt是primes最后一个元素后面一个位置的下标
bool st[N];         //st是标记数组，false表示对应的下标值是质数,true对应合数

void get_primes(int n)
{
    for(int i = 2;i<=n;i++)
    {
        if(!st[i]) primes[cnt ++ ] = i;     //数i如果是质数，就放到primes中
        for(int j = i + i;j <= n;j += i) st[j] = true;   //将2到n所有的数 的倍数标记成合数。
    }
}
```

思路：从2到n，将所有数的倍数(1的倍数不算)全部标记成 合数。

埃式筛质数法(优化版朴素筛质数法)：

```c++
void get_primes(int n)
{
    for(int i = 2;i<=n;i++)
    {
        if(!st[i])         //唯一区别是只对质数的所有倍数标记为合数，更优化了，很易理解。
        {
            primes[cnt ++ ] = i;     
        	for(int j = i + i;j <= n;j += i) st[j] = true;  
        }
    }
}
```

埃式筛法的缺陷在于，同一个合数可能会被两个质数筛，比如，6 = 2 * 3

在上述代码中，当i = 2 时，筛掉了 6，当 i  = 3 时 ，又筛了一次 6

线性筛法在被最小质因数筛去之后就不再筛了。

线性筛法:

```c++
void get_primes(int n)
{
    for(int i = 2;i<=n;i++)   //for循环是用来判断每一个数是不是质数的
    {
        if(!st[i]) primes[cnt ++ ] = i;  //如果i是质数就放入primes中
        for(int j = 0;primes[j] <= n / i;j++)   //从小到大遍历质数数组primes
        { //循环条件是指 primes[j] * i <= n,即合数筛到小于n就可以了。
            st[primes[j] * i] = true;  //  循环中j在增加，质数在变，primes[j] * i 是筛合数
            if(i % primes[j] == 0) break;    //因为i是用来遍历每一个数的，如果这个数已经被筛出来了，只要i是这些质数的倍数就可以直接下一个i了。
        }
    }
}
```

最下面的算法最优！



质数定理： $[1,n]$ 中有 $\frac{n}{\ln n}$ 个质数




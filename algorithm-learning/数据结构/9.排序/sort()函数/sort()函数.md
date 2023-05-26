`#include <algorithm>`

sort()函数

1.排序可以使用sort()函数

[C++ sort()排序详解_晴空๓的博客-CSDN博客](https://blog.csdn.net/qq_41575507/article/details/105936466)

sort()函数

sort(begin,end,cmp);

begin 是待排序数组的第一个元素位置的指针

end 是待排序数组的最后一个元素的后一个位置的指针

cmp 是 排序准则，默认是从小到大排序，如果我们想从大到小排序可以将cmp参数写为`greater<int>()`就是对int数组进行排序，当然`<>`中我们也可以写double、long、float等等。

sort()是对原数组进行操作。

`#include <cmath>`

- abs()函数和fabs()函数
  头文件为cmath，分别用于整数和浮点数的取绝对值

```c++
#include <iostream>//输入输出
#include <cmath>
using namespace std;

const int N = 100010;

void main() {
	int a;
	float b;
	cin >> a >> b;
	a = abs(a);
	b = fabs(b);
	cout << a << endl << b << endl;
}
```

自定义排序函数练习：

按照绝对值的从小到大排序

```c++
bool cmp(int x,int y)
{
    return abs(x)<abs(y);   
}
```

自定义函数接收两个*来自要排序的数组中* 的两个元素,返回一个*bool* 值，返回值为*true* 时，表示，第一个元素排在第二个元素前面。


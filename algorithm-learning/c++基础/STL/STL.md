STL

STL 是“Standard Template Library”的缩写，中文译为“标准模板库”。STL 是 C++ 标准库的一部分，不用单独安装。从根本上说，STL 是一些容器、算法和其他一些组件的集合，所有容器和算法都是总结了几十年来算法和数据结构的研究成果，汇集了许多计算机专家学者经验的基础上实现的，因此可以说，STL 基本上达到了各种存储方法和相关算法的高度优化。

STL库有很多内容，刷算法题只需要学习其中三个：容器、迭代器、适配器

> 不用管这个几字什么意思，学会了用了就知道什么意思了



容器、迭代器



在C++中，可迭代通常通过迭代器（iterator）来实现。迭代器是一种对象，它允许按序访问容器（如数组、向量、链表等）中的元素，而不暴露容器内部的表示方式。

迭代器为容器提供了一种统一的访问接口，使得可以使用通用的算法和循环结构来处理不同类型的容器。通过迭代器，我们可以遍历容器中的元素、访问元素的值、修改元素的值以及进行元素的插入和删除操作。

C++标准库提供了一组通用的迭代器类型，例如，输入迭代器（Input Iterator）、输出迭代器（Output Iterator）、前向迭代器（Forward Iterator）、双向迭代器（Bidirectional Iterator）和随机访问迭代器（Random Access Iterator）。不同类型的迭代器具有不同的功能和限制，可以根据具体的需求选择合适的迭代器类型。

除了使用标准库提供的迭代器，我们还可以自定义迭代器来实现特定类型的可迭代。自定义迭代器需要定义适当的成员函数和运算符重载，以提供迭代器所需的功能，例如`begin()`和`end()`函数来返回迭代器的起始位置和结束位置，`operator++()`函数用于迭代器的前进操作等。

总的来说，C++的可迭代是通过迭代器来实现的，迭代器提供了一种统一的访问方式，使得可以对容器中的元素进行遍历和操作。



| 容器                               | 对应的迭代器类型   |
| ---------------------------------- | ------------------ |
| array                              | 随机访问迭代器     |
| vector                             | 随机访问迭代器     |
| deque                              | 随机访问迭代器     |
| list                               | 双向迭代器         |
| set / multiset                     | 双向迭代器         |
| map / multimap                     | 双向迭代器         |
| forward_list                       | 前向迭代器         |
| unordered_map / unordered_multimap | 前向迭代器         |
| unordered_set / unordered_multiset | 前向迭代器         |
| stack                              | 适配器不支持迭代器 |
| queue                              | 适配器不支持迭代器 |

1) 前向迭代器（forward iterator）

假设 p 是一个前向迭代器，则 p 支持 ++p，p++，*p 操作，还可以被复制或赋值，可以用 == 和 != 运算符进行比较。此外，两个正向迭代器可以互相赋值。

2) 双向迭代器（bidirectional iterator）

双向迭代器具有正向迭代器的全部功能，除此之外，假设 p 是一个双向迭代器，则还可以进行 --p 或者 p-- 操作（即一次向后移动一个位置）。

3) 随机访问迭代器（random access iterator）

随机访问迭代器具有双向迭代器的全部功能。除此之外，假设 p 是一个随机访问迭代器，i 是一个整型变量或常量，则 p 还支持以下操作：

- p+=i：使得 p 往后移动 i 个元素。
- p-=i：使得 p 往前移动 i 个元素。
- p+i：返回 p 后面第 i 个元素的迭代器。
- p-i：返回 p 前面第 i 个元素的迭代器。
- p[i]：返回 p 后面第 i 个元素的引用。

此外，两个随机访问迭代器 p1、p2 还可以用 <、>、<=、>= 运算符进行比较。另外，表达式 p2-p1 也是有定义的，其返回值表示 p2 所指向元素和 p1 所指向元素的序号之差（也可以说是 p2 和 p1 之间的元素个数减一）。



关于最重要的一点：正向和双向迭代器都没有 p+i 这样的操作

原因如下：

关联式容器，元素可能是散落在内存各个地方的。联系这些元素的，是元素内指向其它元素的成员指针。

如此一来，指向这些元素的迭代器不像vector之类的序列式容器的迭代器以及指针那样能实现**随机访问（Random Access）**。









`*迭代器名`就表示迭代器指向的元素



正向迭代器和反向迭代器

- 对正向迭代器进行 ++ 操作时，迭代器会指向容器中的后一个元素；
- 而对反向迭代器进行 ++ 操作时，迭代器会指向容器中的前一个元素。



# container

## 序列式容器

容器内的元素是有线性顺序的，而且这个线性顺序就是存储顺序。

### vector

vector 实现的是一个动态数组，即可以进行元素的插入和删除，在此过程中，vector 会动态调整所占用的内存空间，整个过程无需人工干预。

头文件

```c++
#include <vector>
using namespace std;
```

创建一个vector

```c++
vector<数据类型> 变量名; 
```

数据类型有很多，比如int、float、double、struct、vector等等

`vector<int> a;`

`vector<vector<int>> b;`  //二维动态数组

#### vector常用的成员函数

| 函数成员     | 函数功能                                                     |
| ------------ | ------------------------------------------------------------ |
| begin()      | 返回指向容器中第一个元素的迭代器。(迭代器理解为指针即可)     |
| end()        | 返回指向容器最后一个元素所在位置后一个位置的迭代器，通常和 begin() 结合使用。 |
| rbegin()     | 返回指向最后一个元素的迭代器。                               |
| rend()       | 返回指向第一个元素所在位置前一个位置的迭代器。               |
| size()       | 返回实际元素个数。                                           |
| empty()      | 判断容器中是否有元素，若无元素，则返回 true；反之，返回 false。 |
| operator[ ]  | 重载了 [ ] 运算符，可以向访问数组中元素那样，通过下标即可访问甚至修改 vector 容器中的元素。 |
| push_back(x) | 在序列的尾部添加一个元素x。                                  |
| pop_back()   | 移出序列尾部的元素。                                         |
| insert()     | 在指定的位置插入一个或多个元素。                             |
| erase()      | 移出一个元素或一段元素。                                     |
| clear()      | 移出所有的元素，容器大小变为 0。                             |
| swap()       | 交换两个容器的所有元素。                                     |
| front()      | 返回第一个元素的引用。                                       |
| back()       | 返回最后一个元素的引用。                                     |

insert()函数每次插入的时候都需要将后面的元素往后移一位，会非常慢。如果多次使用insert()函数会导致时间复杂度会非常高，消耗的时间也会非常多。

| 语法格式                        | 用法说明                                                     |
| :------------------------------ | :----------------------------------------------------------- |
| iterator insert(pos,elem)       | 在迭代器 pos 指定的位置之前插入一个新元素elem，并返回表示新插入元素位置的迭代器。 |
| iterator insert(pos,n,elem)     | 在迭代器 pos 指定的位置之前插入 n 个元素 elem，并返回表示第一个新插入元素位置的迭代器。 |
| iterator insert(pos,first,last) | 在迭代器 pos 指定的位置之前，插入其他容器（不仅限于vector）中位于 [first,last) 区域的所有元素，并返回表示第一个新插入元素位置的迭代器。 |

```cpp
iterator erase (const_iterator position);
iterator erase (const_iterator first, const_iterator last);
```


从vector中删除一个元素（position），或者范围元素( [first, last) )

![1680753898787](STL.assets/1680753898787.png)

访问vector元素的方法：

1.用 `[]`

```c++
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> vi;
    vi.push_back(1);
    cout<<vi[0]<<endl;
    return 0;
}
```

2.用迭代器(指针)

```c++
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> v;
    for (int i = 0; i < 5; i++)
    {
        v.push_back(i);
    }
    //v.begin()返回v的首元素地址
    vector<int>::iterator it=v.begin();
    for (int i = 0; i < v.size(); i++)
    {
       cout<<it[i]<<" ";
    }
    return 0;
}
```

在定义迭代器时，可以用auto:

```c++
vector<int> v;
vector<int>::iterator it = v.begin();
//等价于 auto it = v.begin();
```

### auto

auto 的作用是，根据变量被赋予的值，自动判断变量的类型；

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> v;
    for (int i = 0; i < 5; i++)
    {
        v.push_back(i);
    }
    //vector的迭代器不支持it<v.end()的写法，因此循环条件只能it!=v.end()
    for (auto it=v.begin(); it!=v.end();it++)
    {
        cout<<*it<<" ";
    }
    return 0;
}
```

### deque

双端队列容器

- deque 容器也擅长在序列尾部添加或删除元素（时间复杂度为`O(1)`），而不擅长在序列中间添加或删除元素。
- deque 容器也可以根据需要修改自身的容量和大小。
- 和 vector 不同的是，deque 还擅长在序列头部添加或删除元素，所耗费的时间复杂度也为常数阶`O(1)`。
- deque 容器中存储元素并不能保证所有元素都存储到连续的内存空间中。

头文件

```cpp
#include <deque>
using namespace std;
```

创建一个deque

```cpp
deque<int> 变量名;
```

基于 deque 双端队列的特点，该容器包含一些 array、vector 容器都没有的成员函数。

| 函数成员        | 函数功能                                                     |
| --------------- | ------------------------------------------------------------ |
| begin()         | 返回指向容器中第一个元素的迭代器。                           |
| end()           | 返回指向容器最后一个元素所在位置后一个位置的迭代器，通常和 begin() 结合使用。 |
| rbegin()        | 返回指向最后一个元素的迭代器。                               |
| rend()          | 返回指向第一个元素所在位置前一个位置的迭代器。               |
| size()          | 返回实际元素个数。                                           |
| empty()         | 判断容器中是否有元素，若无元素，则返回 true；反之，返回 false。 |
| push_back()     | 在序列的尾部添加一个元素。                                   |
| push_front()    | 在序列的头部添加一个元素。                                   |
| pop_back()      | 移除容器尾部的元素。                                         |
| pop_front()     | 移除容器头部的元素。                                         |
| insert()        | 在指定的位置插入一个或多个元素。                             |
| erase()         | 移除一个元素或一段元素。                                     |
| clear()         | 移出所有的元素，容器大小变为 0。                             |
| swap()          | 交换两个容器的所有元素。                                     |
| emplace()       | 在指定的位置直接生成一个元素。                               |
| emplace_front() | 在容器头部生成一个元素。和 push_front() 的区别是，该函数直接在容器头部构造元素，省去了复制移动元素的过程。 |
| emplace_back()  | 在容器尾部生成一个元素。和 push_back() 的区别是，该函数直接在容器尾部构造元素，省去了复制移动元素的过程。 |



## 关联式容器

容器内的元素是<key，value>的形式,关联式容器默认情况下会对存储的元素做升序排序.

### pair类模板

头文件

```cpp
#include <utility>
using namespace std;
```

创建对象

```cpp
pair<数据类型，数据类型> p;  //数据类型可以是基本数据类型、结构体、类自定的类型
```

输入值，创建成一个新元素`<first, second>`

```cpp
pair<int,int> p;
scanf("%d%d",&p.first,&p.second);   // pair类对象p的第一个元素用 p.first 访问，第二个元素用 p.second 访问
```

pair类型的使用相当的繁琐，如果定义多个相同的pair类型对象，可以使用typedef简化声明：

```cpp
typedef pair<string,string> Author;
Author proust("March","Proust");
Author Joy("James","Joy");
```

### pair类数组

有时候，我们会需要创建一个pair类的数组，然后用sort函数对pair类进行排序。

**当使用sort函数对pair进行排序的时候，会先对first进行排序，如果first相同再对second进行排序。**



pair类数组和map/unordered_map的异同：

先说相同点，存放的元素都是pair类的对象。

不同点：

先说，map和unordered_map 的区别，map会自动根据key进行字典序排序，unordered_map不会，如果要遍历map或者unordered_map的时候，用的是迭代器。

pair类数组遍历的方式是使用 `[]` 下标运算符，而且也不会自动排序。可以用sort

**非常重要的一点：如果只是简单的存储pair类对象，用 pair类数组，如果要根据key进行value的合并要用map/unordered_map**



```cpp
vector<pair<int,int>> v;        //用vector就可以，别用静态的，vector更灵活。
int l,r;
cin >> l >> r;
v.push_back({l,r});           //记住这种方式
```





### map

```cpp
#include <map>
using namespace std;
```

使用该容器存储的数据，其各个元素的键必须是唯一的（即不能重复），该容器会根据各元素键的大小，默认进行升序排序。

```cpp
#include <iostream>
#include <map> //使用 map 容器，必须引入该头文件
#include <string>
using namespace std;
int main()
{
    //创建一个空的 map 关联式容器，该容器中存储的键值对，其中键为 string 字符串，值也为 string 字符串类型
    map<string, string> mymap;
    //向 mymap 容器中添加数据
    mymap["http://c.biancheng.net/c/"] = "C语言教程";
    mymap["http://c.biancheng.net/python/"] = "Python教程";
    mymap["http://c.biancheng.net/java/"] = "Java教程";
    //使用 map 容器的迭代器，遍历 mymap 容器，并输出其中存储的各个键值对
    for (map<string, string>::iterator it = mymap.begin(); it != mymap.end(); ++it) {
        //输出各个元素中的键和值
        cout << it->first << " => " << it->second << '\n';
    }
    return 0;
}
```

各个键值对的键和值可以是任意数据类型，包括 C++ 基本数据类型（int、double 等）、使用结构体或类自定义的类型。

C++ STL 标准库为 map 容器配备的是双向迭代器（bidirectional iterator）。这意味着，map 容器迭代器只能进行 ++p、p++、--p、p--、*p 操作，并且迭代器之间只能使用 == 或者 != 运算符进行比较。

| 成员方法   | 功能                                                         |
| ---------- | ------------------------------------------------------------ |
| begin()    | 返回指向容器中第一个（注意，是已排好序的第一个）键值对的双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
| end()      | 返回指向容器最后一个元素（注意，是已排好序的最后一个）所在位置后一个位置的双向迭代器，通常和 begin() 结合使用。如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
| rbegin()   | 返回指向最后一个（注意，是已排好序的最后一个）元素的反向双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。 |
| rend()     | 返回指向第一个（注意，是已排好序的第一个）元素所在位置前一个位置的反向双向迭代器。如果 map 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。 |
| empty()    | 若容器为空，则返回 true；否则 false。                        |
| size()     | 返回当前 map 容器中存有键值对的个数。                        |
| operator[] | map容器重载了 [] 运算符，通过指定的键，我们可以轻松获取 map 容器中该键对应的值。 |
| clear()    | 清空 map 容器中所有的键值对，即使 map 容器的 size() 为 0。   |
| find(key)  | 在 map 容器中查找键为 key 的键值对，如果成功找到，则返回指向该键值对的双向迭代器；反之，则返回和 end() 方法一样的迭代器。另外，如果 map 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
|            |                                                              |

#### map索引不存在的key可能导致的后果

```cpp
#include <map>
#include <iostream>
using namespace std;

int main()
{
	map<int, int> map1;
	cout << map1[1] << endl;
	map<int, char> map2;
	cout << map2[1] << endl;
	map<int, bool> map3;
	cout << map3[1] << endl;
}
-------
0
                 //其实打印了'\0'
0
```

**发现不存在的key在被索引后被添加到了map中并被赋予了一个默认值（一般的，整数为0，字符为'\0'，字符串为空）**可以拿这个性质去作判断

```cpp
#include <map>
using namespace std;

int main()
{
    map<int,bool> map1;
    if(map1[1])   //map[1] 如果不存在，会将(关键字1,0)加入到map1这个字典中，然后if根据map1[1]的值是否为0，选择是否执行if内的语句
        //如果map中没有这个元素，返回false，if内的语句就不执行。
}
```

注意，只有当 map 容器中确实存有包含该指定键的键值对，借助重载的 [ ] 运算符才能成功获取该键对应的值；反之，若当前 map 容器中没有包含该指定键的键值对，则此时使用 [ ] 运算符将不再是访问容器中的元素，而变成了向该 map 容器中增添一个键值对。其中，该键值对的键用 [ ] 运算符中指定的键，其对应的值取决于 map 容器规定键值对中值的数据类型，如果是基本数据类型，则值为 0；如果是 string 类型，其值为 ""，即空字符串（即使用该类型的默认值作为键值对的值）。



### set



使用 set 容器存储的各个键值对，要求键 key 和值 value 必须相等。

我并不知道上面的描述是否正确， 因为set存储的单个元素的数据类型 和 map并不一样，map元素的数据类型是pair类，但是set的单个元素并不是pair类，我们可以认为跟vector一样，那上面这句话有什么意义吗？显然没有

举个例子，如下有 2 组键值对数据：

> {<'a', 1>, <'b', 2>, <'c', 3>}
> {<'a', 'a'>, <'b', 'b'>, <'c', 'c'>}

显然，第一组数据中各键值对的键和值不相等，而第二组中各键值对的键和值对应相等。对于 set 容器来说，只能存储第 2 组键值对，而无法存储第一组键值对。

通过前面的学习我们知道，map、multimap 容器都会自行根据键的大小对存储的键值对进行排序，set 容器也会如此，只不过 set 容器中各键值对的键 key 和值 value 是相等的，根据 key 排序，也就等价为根据 value 升序排序。

头文件

```cpp
#include <set>
using namespace std;
```

使用 set 容器存储的各个元素的值必须各不相同。更重要的是，从语法上讲 set 容器并没有强制对存储元素的类型做 const 修饰，即 set 容器中存储的元素的值是可以修改的。但是，C++ 标准为了防止用户修改容器中元素的值，对所有可能会实现此操作的行为做了限制，使得在正常情况下，用户是无法做到修改 set 容器中元素的值的。

> 对于初学者来说，切勿尝试直接修改 set 容器中已存储元素的值，这很有可能破坏 set 容器中元素的有序性，最正确的修改 set 容器中元素值的做法是：先删除该元素，然后再添加一个修改后的元素。

set 容器的类模板定义如下：

```cpp
template < 
			class T,                        // 键 key 和值 value 的类型
			class Compare = less<T>,        // 指定 set 容器内部的排序规则  
			class Alloc = allocator<T>      // 指定分配器对象的类型       
          > class set;
```

创建容器：

```cpp
set<string> s;
set<string,greater<string>> s;   //可以修改排序规则
```

成员函数



注意看：这个返回的是正向迭代器，如果我需要返回set的最后一位（最大值），或者unordered_set的最后一位（最后插入的元素），该怎么办？

```cpp
set<int> s;
for(auto i = s.begin();i < i.end();i++) 行不通，因为最后的i是 set的end指针，是后面的那个位置

for(auto i = s.begin();i < i.end()-1;i++) 行不通，因为这是正向迭代器，没法进行减法

只有这样了
cout << s.rbegin();   /// 记住了，之前有道题卡在这好久，不知道该怎么找最后一位元素。
```



| 成员方法   | 功能                                                         |
| ---------- | ------------------------------------------------------------ |
| begin()    | 返回指向容器中第一个（注意，是已排好序的第一个）元素的双向迭代器。如果 set 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
| end()      | 返回指向容器最后一个元素（注意，是已排好序的最后一个）所在位置后一个位置的双向迭代器，通常和 begin() 结合使用。如果 set 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
| rbegin()   | 返回指向最后一个（注意，是已排好序的最后一个）元素的反向双向迭代器。如果 set 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。 |
| rend()     | 返回指向第一个（注意，是已排好序的第一个）元素所在位置前一个位置的反向双向迭代器。如果 set 容器用 const 限定，则该方法返回的是 const 类型的反向双向迭代器。 |
| find(val)  | 在 set 容器中查找值为 val 的元素，如果成功找到，则返回指向该元素的双向迭代器；反之，则返回和 end() 方法一样的迭代器。另外，如果 set 容器用 const 限定，则该方法返回的是 const 类型的双向迭代器。 |
| empty()    | 若容器为空，则返回 true；否则 false。                        |
| size()     | 返回当前 set 容器中存有元素的个数。                          |
| insert()   | 向 set 容器中插入元素。                                      |
| erase()    | 删除 set 容器中存储的元素。                                  |
| swap()     | 交换 2 个 set 容器中存储的所有元素。这意味着，操作的 2 个 set 容器的类型必须相同。 |
| clear()    | 清空 set 容器中所有的元素，即令 set 容器的 size() 为 0。     |
| emplace()  | 在当前 set 容器中的指定位置直接构造新元素。其效果和 insert() 一样，但效率更高。 |
| count(val) | 在当前 set 容器中，查找   值为 val 的元素的个数，并返回。注意，由于 set 容器中各元素的值是唯一的，因此该函数的返回值最大为 1。  要么为0要么为1嘛，可以用来判断容器中是否有这个键值对 |



set不能用下标来访问





## 无序关联式容器

无序关联式容器，又称**哈希容器**。和关联式容器一样，此类容器存储的也是键值对元素；不同之处在于，关联式容器默认情况下会对存储的元素做升序排序，而无序关联式容器不会。



和关联式容器一样，无序容器也使用键值对（pair 类型）的方式存储数据。不过，本教程将二者分开进行讲解，因为它们有本质上的不同：

- 关联式容器的底层实现采用的树存储结构，更确切的说是红黑树结构；
- **无序容器的底层实现采用的是哈希表的存储结构。**

基于底层实现采用了不同的数据结构，因此和关联式容器相比，无序容器具有以下 2 个特点：

- 无序容器内部存储的键值对是无序的，各键值对的存储位置取决于该键值对中的键
- 和关联式容器相比，无序容器擅长通过指定键查找对应的值（平均时间复杂度为 O(1)）；但对于使用迭代器遍历容器中存储的元素，无序容器的执行效率则不如关联式容器。

| 无序容器           | 功能                                                         |
| ------------------ | ------------------------------------------------------------ |
| unordered_map      | 存储键值对 <key, value> 类型的元素，其中各个键值对键的值不允许重复，且该容器中存储的键值对是无序的。 |
| unordered_multimap | 和 unordered_map 唯一的区别在于，该容器允许存储多个键相同的键值对。 |
| unordered_set      | 不再以键值对的形式存储数据，而是直接存储数据元素本身（当然也可以理解为，该容器存储的全部都是键 key 和值 value 相等的键值对，正因为它们相等，因此只存储 value 即可）。另外，该容器存储的元素不能重复，且容器内部存储的元素也是无序的。 |
| unordered_multiset | 和 unordered_set 唯一的区别在于，该容器允许存储值相同的元素。 |

可能读者已经发现，以上 4 种无序容器的名称，仅是在前面所学的 4 种关联式容器名称的基础上，添加了 "unordered_"。如果读者已经学完了 map、multimap、set 和 multiset 容器不难发现，以 map 和unordered_map 为例，其实它们仅有一个区别，即 map 容器内存会对存储的键值对进行排序，而 unordered_map 不会。**C++ 11 标准的 STL 中，在已提供有 4 种关联式容器的基础上，又新增了各自的“unordered”版本（无序版本、哈希版本），提高了查找指定元素的效率。**



### unordered_map

存储键值对 <key, value> 类型的元素，其中各个键值对键的值不允许重复，且该容器中存储的键值对是无序的。

与map的唯一区别：即 map 容器内存会对存储的键值对进行排序，而 unordered_map 不会。

```cpp
#include <unordered_map>
using namespace std;
```

C++ STL 标准库中，unordered_map 容器迭代器的类型为前向迭代器（又称正向迭代器）。这意味着，假设 p 是一个前向迭代器，则其只能进行 *p、p++、++p 操作，且 2 个前向迭代器之间只能用 == 和 != 运算符做比较。

| 成员方法  | 功能                                                         |
| --------- | ------------------------------------------------------------ |
| begin()   | 返回指向容器中第一个键值对的正向迭代器。                     |
| end()     | 返回指向容器中最后一个键值对之后位置的正向迭代器。           |
| find(key) | 查找以 key 为键的键值对，如果找到，则返回一个指向该键值对的正向迭代器；反之，则返回一个指向容器中最后一个键值对之后位置的迭代器（如果 end() 方法返回的迭代器）。 |

### unordered_set

unordered_set 容器，可直译为“无序 set 容器”，即 unordered_set 容器和 set 容器很像，唯一的区别就在于 set 容器会自行对存储的数据进行排序，而 unordered_set 容器不会。

总的来说，unordered_set 容器具有以下几个特性：

1. **不再以键值对的形式存储数据，而是直接存储数据的值；**
2. 容器内部存储的各个元素的值都互不相等，且不能被修改。
3. 不会对内部存储的数据进行排序（这和该容器底层采用哈希表结构存储数据有关)

> 对于 unordered_set 容器不以键值对的形式存储数据，读者也可以这样认为，即 unordered_set 存储的都是键和值相等的键值对，为了节省存储空间，该类容器在实际存储时选择**只存储每个键值对的值。**

**哈哈，有了unordered_set，谁还用set**

```cpp
#include <unordered_set>
using namespace std;
```

unordered_set 容器的类模板定义如下：

```cpp
template < class Key,            //容器中存储元素的类型     
class Hash = hash<Key>,    //确定元素存储位置所用的哈希函数    
class Pred = equal_to<Key>,   //判断各个元素是否相等所用的函数          
class Alloc = allocator<Key>   //指定分配器对象的类型    
> class unordered_set;
```

可以看到，以上 4 个参数中，只有第一个参数没有默认值，这意味着如果我们想创建一个 unordered_set 容器，至少需要手动传递 1 个参数。事实上，在 99% 的实际场景中最多只需要使用前 3 个参数（各自含义如表 1 所示），最后一个参数保持默认值即可。

| 参数                  | 含义                                                         |
| --------------------- | ------------------------------------------------------------ |
| Key                   | 确定容器存储元素的类型，如果读者将 unordered_set 看做是存储键和值相同的键值对的容器，则此参数则用于确定各个键值对的键和值的类型，因为它们是完全相同的，因此一定是同一数据类型的数据。 |
| Hash = hash\<Key>     | 指定 unordered_set 容器底层存储各个元素时，所使用的哈希函数。需要注意的是，默认哈希函数 hash<Key> 只适用于基本数据类型（包括 string 类型），而不适用于自定义的结构体或者类。 |
| Pred = equal_to\<Key> | unordered_set 容器内部不能存储相等的元素，而衡量 2 个元素是否相等的标准，取决于该参数指定的函数。 默认情况下，使用 STL 标准库中提供的 equal_to<key> 规则，该规则仅支持可直接用 == 运算符做比较的数据类型。 |

创建容器

```cpp
unordered_set<string> s;
```

| 成员方法           | 功能                                                         |
| ------------------ | ------------------------------------------------------------ |
| begin()            | 返回指向容器中第一个元素的正向迭代器。                       |
| end();             | 返回指向容器中最后一个元素之后位置的正向迭代器。             |
| cbegin()           | 和 begin() 功能相同，只不过其返回的是 const 类型的正向迭代器。 |
| cend()             | 和 end() 功能相同，只不过其返回的是 const 类型的正向迭代器。 |
| empty()            | 若容器为空，则返回 true；否则 false。                        |
| size()             | 返回当前容器中存有元素的个数。                               |
| max_size()         | 返回容器所能容纳元素的最大个数，不同的操作系统，其返回值亦不相同。 |
| find(key)          | 查找以值为 key 的元素，如果找到，则返回一个指向该元素的正向迭代器；反之，则返回一个指向容器中最后一个元素之后位置的迭代器（如果 end() 方法返回的迭代器）。 |
| count(key)         | 在容器中查找   值为 key 的元素的个数。  要么为0要么为1嘛，可以用来判断容器中是否有这个键值对 |
| equal_range(key)   | 返回一个 pair 对象，其包含 2 个迭代器，用于表明当前容器中值为 key 的元素所在的范围。 |
| emplace()          | 向容器中添加新元素，效率比 insert() 方法高。                 |
| emplace_hint()     | 向容器中添加新元素，效率比 insert() 方法高。                 |
| insert()           | 向容器中添加新元素。                                         |
| erase()            | 删除指定元素。                                               |
| clear()            | 清空容器，即删除容器中存储的所有元素。                       |
| swap()             | 交换 2 个 unordered_set 容器存储的元素，前提是必须保证这 2 个容器的类型完全相等。 |
| bucket_count()     | 返回当前容器底层存储元素时，使用桶（一个线性链表代表一个桶）的数量。 |
| max_bucket_count() | 返回当前系统中，unordered_set 容器底层最多可以使用多少桶。   |
| bucket_size(n)     | 返回第 n 个桶中存储元素的数量。                              |
| bucket(key)        | 返回值为 key 的元素所在桶的编号。                            |
| load_factor()      | 返回 unordered_set 容器中当前的负载因子。负载因子，指的是的当前容器中存储元素的数量（size()）和使用桶数（bucket_count()）的比值，即 load_factor() = size() / bucket_count()。 |
| max_load_factor()  | 返回或者设置当前 unordered_set 容器的负载因子。              |
| rehash(n)          | 将当前容器底层使用桶的数量设置为 n。                         |
| reserve()          | 将存储桶的数量（也就是 bucket_count() 方法的返回值）设置为至少容纳 count 个元（不超过最大负载因子）所需的数量，并重新整理容器。 |
| hash_function()    | 返回当前容器使用的哈希函数对象。                             |



哈希表不能让vector作为数据的元素，也就是

```cpp
unordered_set<vector<int>> s;  //会报错
```

因为c++没有提供

# adapter

### stack

头文件

```cpp
#include <stack>
using namespace std;
```



```cpp
stack<T,Container=deque<T>>
```

上面有两个参数，第一个T表示数据类型；第二个container表示stack使用的底层容器，默认是deque；还可以是vector和list  。。。 不知道有啥用

创建一个stack

```cpp
stack<int> s;   //创建一个底层是deque的int类型的stack
```

创建stack的方法有很多，先用最简单最常用的。



| 成员函数                     | 功能                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| empty()                      | 当 stack 栈中没有元素时，该成员函数返回 true；反之，返回 false。 |
| size()                       | 返回 stack 栈中存储元素的个数。                              |
| top()                        | 返回一个栈顶元素的引用，类型为 T&。如果栈为空，程序会报错。  |
| push(const T& val)           | 先复制 val，再将 val 副本压入栈顶。这是通过调用底层容器的 push_back() 函数完成的。 |
| push(T&& obj)                | 以移动元素的方式将其压入栈顶。这是通过调用底层容器的有右值引用参数的 push_back() 函数完成的。 |
| pop()                        | 弹出栈顶元素。返回值为void                                   |
| emplace(arg...)              | arg... 可以是一个参数，也可以是多个参数，但它们都只用于构造一个对象，并在栈顶直接生成该对象，作为新的栈顶元素。 |
| swap(stack<T> & other_stack) | 将两个 stack 适配器中的元素进行互换，需要注意的是，进行互换的 2 个 stack 适配器中存储的元素类型以及底层采用的基础容器类型，都必须相同。 |

弹出栈顶元素

1. 栈顶元素 = stack.top()
2. stack.pop()



### queue

队列

```cpp
#include <queue>
using namespace std;
```

创建一个队列

```cpp
queue<int> s; 
```

底层采用 deque 容器的 queue 容器适配器。也可以手动指定 queue 容器适配器底层采用的基础容器类型。queue 容器适配器底层容器可以选择 deque 和 list。

> 作为 queue 容器适配器的基础容器，其必须提供 front()、back()、push_back()、pop_front()、empty() 和 size() 这几个成员函数，符合条件的序列式容器仅有 deque 和 list。

在手动指定基础容器的类型时，其存储的数据类型必须和 queue 容器适配器存储的元素类型保持一致。

| 成员函数                    | 功能                                                         |
| --------------------------- | ------------------------------------------------------------ |
| empty()                     | 如果 queue 中没有元素的话，返回 true。                       |
| size()                      | 返回 queue 中元素的个数。                                    |
| front()                     | 返回 queue 中第一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。 |
| back()                      | 返回 queue 中最后一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。 |
| push(const T& obj)          | 在 queue 的尾部添加一个元素的副本。这是通过调用底层容器的成员函数 push_back() 来完成的。 |
| emplace()                   | 在 queue 的尾部直接添加一个元素。                            |
| push(T&& obj)               | 以移动的方式在 queue 的尾部添加元素。这是通过调用底层容器的具有右值引用参数的成员函数 push_back() 来完成的。 |
| pop()                       | 删除 queue 中的第一个元素。                                  |
| swap(queue<T> &other_queue) | 将两个 queue 容器适配器中的元素进行互换，需要注意的是，进行互换的 2 个 queue 容器适配器中存储的元素类型以及底层采用的基础容器类型，都必须相同。 |

















有关stl的问题：

1. unordered_map 和 unordered_set 没有  rbegin() 和 rend() 成员函数。map和set有

有什么用呢？

访问最后一个元素的时候用

```cpp

```


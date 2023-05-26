实践中遇到STL的问题

<font size = 5>报错原因：vector在还没有分配任何空间时还不能像数组一样用下标形式去访问vector的（v[0]也不行）！！！否则编译通过但报运行错误runtime error！</font>



```cpp
bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {

}
```

🤣写leetcode时遇到的题，给了我一个二维vector类型的matrix，我想按行遍历矩阵

```cpp
bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
    for(int i = 0;i<matrix.size();i++){}
}
```

> matrix.size()是行数；matrix[0].size()是列数





🤣同样是这个题，有这样一个样例 matrix = [[]]

可知matrix.size() == 1, matrix[0].size == 0

因为matrix[0]中没有元素，因此 matrix\[0][0]是没有意义的，对吧。因此，编译器会报错

`runtime error: reference binding to null pointer of type 'int' (stl_vector.h)` 

解决办法：**在使用了matrix\[i][j]的语句前，加上判断 if(matrix.size()!=0&&matrix[i].size()!=0)**

第一个matrix.size()!=0是防止这样的样例，matrix = []

第二个matrix[i].size() !=0是防止这样的样例，matrix=[ [1,2] , [] ]  或者 matrix = [[]] 等





🤣题目是这样的，给我一个二维数组，要求我用vector<vector\<int>>来存储，按行输入

```cpp
int main()
{
    int n,m;
    cin >> n >> m;  //n表示行数,m表示列数
    vector<vector<int>> s;
    for(int i = 0;i < n;i++)
    	for(int j = 0;j < m;j++)
            cin >> s[i][j];
    //上述代码是错误的，能看出来哪里错了吗
}
```

我们定义的二维数组s并没有进行初始化，我们定义的这个s没有给他分配存储空间

正确的代码如下，应该再定义一个临时一维数组

```cpp
int main()
{
    int n,m;
    cin >> n >> m;
    vector<vector<int>> s;
    vector<int> t;
    for(int i = 0;i < n;i++)
    {
        t.clear();
        for(int j = 0;j < m;j++)
        {
            int a;
            cin >> a;
            t.push_back(a);
        }
        s.push_back(t);
    }
}
```


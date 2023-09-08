### STL

#### vector

创建：

``vector<int> num;  // 长度为0``

``vector<int> num(n);  // 长度为n``

``vector<int> num(n, value);  // 长度为n，初始值为value``

``vector<vector<int>> tmp(m, vector<int> (n));  // m 行 n 列``

`vector<int> a(b); // b也是vector，创建a时把b的元素全部复制给a`

`vector<vector<int>>dp = vector<vector<int>>(n, vector<int>(n, -1));` // 用构造函数创建

```c++
1、size()  // 返回元素个数
2、empty()  // 返回是否为空
3、clear()  // 清空（直接删除空间）
4、front()/back()  // 首尾元素
5、push_back()/pop_back()  //在尾部插入、去除元素
6、begin()/end()  // 首尾迭代器
7、[]  // 根据下标取值
8、支持比较运算，按字典序 vector<int> a, b; (二者可直接比较 ，如a > b)   
int id = lower_bound(nums.begin(), nums.end(), tmp) - nums.begin() //获得第一个大于等于tmp的元素下标
int id = upper_bound(nums.begin(), nums.end(), tmp) - nums.begin() //获得第一个大于tmp的元素下标
    对于数组 int id = upper_bound(a, a + n, tmp) - a
    这个查找函数返回的是迭代器
9、a.assign(nums.begin(), nums.end() + k);  // 截取nums的片段赋值给a
vector<int> a(nums.begin(), nums.end());  // 创建a时直接截取片段进行赋值
截取区间都是左闭右开
10、复制
copy(shuffled.begin(), shuffled.end(), nums.begin());
copy(shuffled.begin(), shuffled.begin() + cnt, nums.begin());
11、
```

#### string

```c++
//创建
1、string res(m+n,'0');  
2、//判断是否包含子串
str.find(p) == string::npos  相等则找不到 不相等则找得到，返回的是下标(0开始)
3、截取
    str.substr(pos, len); //起始下标、子串长度; 返回子串
	str.substr(pos); //返回从起始下标到末尾的子串
4、比较
    str1 == str2
5、size()/length() 、empty()、clear()
6、c_str() //返回字符串所在字符数组的起始地址 将string转换为char*
7、insert(pos, "str") // 在pos插入字符串
8、删除 
   string.erase(pos,n) //删除从pos开始的n个字符 s.erase(2, 2) 删除s[2] s[3]
   string.erase(pos) //从pos开始删除所有的  s.erase(2) 删除 s[2]一直到后面的
   string.erase(first,last) //删除从first到last中间的字符（first和last都是string类型的迭代器）
9、string = s; 
s.push_back(1);s.push_back(2);s.push_back(3); // 用string存储数字  转字符串只需要遍历整个string，给每个元素加上'0'即可
s[0] += '0';
10、push_back()、pop_back() 添加、删除字符
```

```c++
//char 转 string
-----------------------------------------------
char c = 'A';
string s; 
s = c;
// 注意 不存在 string s = c; 这样的写法，因为没有这样的构造函数。
-----------------------------------------------
char c = 'A';
string s;
stringstream ss;
ss << c;
ss >> s;    // or s = ss.str();
-----------------------------------------------
//利用填充构造函数 string(size_t n, char c)
//该函数将填充 char c 的 n 个拷贝到string中。
char c = 'A'; 
string s(1, c); // s = "A"
string s(3, c); // s = "AAA"


```

```c++
//int 转string
int a;
string s = to_string(a);
```



#### map 有序

```c++
map<int, int> list_map;  //最终得到的map是按照 键 排序
find();  // 查找一个元素  返回迭代器 
begin();  // 指向map头部的迭代器
count();  // 还回指定元素出现的次数
clear();  // 删除所有元素，注意是所有元素
empty();  // 如果map为空则还回true
end();  // 指向map末尾的迭代器
erase()  // 删除一个元素
insert();  // 插入一个元素
max_size();  // 可以容纳的最大元素个数
size();  // map中元素的个数
swap();  // 交换两个map
```

#### hashmap

**无序**

```c++
unordered_map<int, int> hashmap;
```

**判断哈希表中是否存在某元素**

```c++
hashmap.count(num); // 返回元素个数
比如存储的是 hashmap[1]=0; 则 hashmap.count(1) = 1;
用 hashmap[num] == 0 判断会出问题：某些中键值对中值为 0，导致误判
```



#### set /multiset

```c++
// 元素不重复
#include <set> // 有序
#include <unordered_set>  // 无序

unordered_set<int> hashset;  
set<int> a;
multiset<int> a;

s.max_size()  // 返回容器最大尺寸
s.begin()  // set中第一个元素的引用 	指针
s.end()    // set中最后一个元素后面的引用	指针
s.size()	 // 返回set的个数
s.empty()	 // 判断集合是否为空,为空返回true
s.find(x)	 // 返回一个指向元素x的迭代器;如果x不存在,则返回的迭代器等于end （指针）
s.upper_bound(x)	// 从x后面开始查找，返回一个大于x的迭代器（指针） 
s.lower_bound(x)  // 从x处开始查找 返回一个迭代器指向大于等于x（指针）
s.clear()	  // 清空集合元素
    
s.rbegin()  // 返回一个反向迭代器,指向末尾元素的后一个 一般用于降序输出set元素 因为set默认是升序的
s.rend()	  // 返回一个迭代器,指向向量起始元素
        for (auto it = s.rbegin(); it != s.rend(); it ++)
erase
	s.erase(i)  // i 是元素值，删除该元素
	s.erase(s.begin(), it2)	// 删除指定迭代器之间的元素,注意是左闭右开
	s.erase(iterator)   // 删除迭代器iterator指向的值

s.insert(value)  // 将value插入到容器中  无序集合采用的是头插法 如 1 2 3 输出是 3 2 1
s.insert(it1, it2)   // 将迭代器之间的元素插入到集合中，迭代器对应的区间左闭右开
set1.insert(set1.end(), 4)	// 在迭代器指定位置插入元素
swap(a, b)	//交换2个集合的内容
```

```c++
// 取值
1、for (auto it: hash_set)
    it // it就是元素值
2、for (auto it = hash_set.begin(); it != hash_set.end(); it ++)
    *it // it是指针，需要用取值的 * 取元素值
3、迭代器（set、multiset 有序）
	next(it,n)  返回迭代器第n个后迭代器（指针）,默认为 1（即后一个）, n=0时返回本身,负数时反方向
	prev(it,n)  返回迭代器it第n个前驱迭代器（指针）,默认为1,负数时为反方向
```

#### pair<int, int> 

```c++
first;  //第一个元素
second;  //第二个元素
支持比较运算，以first为第一关键字，second为第二
```

#### queue 

```c++
size()
empty()
push()  向队尾插入一个元素
front()  返回队头元素
back()  返回队尾元素
pop()  弹出队头元素
```

#### priority_queue 

**优先队列，默认是大根堆(降序)**    

`priority_queue<Type, Container, Functional>`，元素类型  容器  排序函数

`priority_queue<int,vector<int>,greater<int>> q1` 小根堆(升序)

`priority_queue<int, vector<int>, less<int>> q2` 大根堆（降序）

简写：`priority_queue<int>`，默认使用vector容器，降序

**用pair做优先队列元素：**

`priority_queue<pair<int, int> > a;` // 先比较第一个元素，在比较第二个  降序

```c++
size()
empty()
push()  插入一个元素
top()  返回堆顶元素
pop()  弹出堆顶元素
```

**存储结构体并排序**：

```c++
1.自定义排序函数
struct node {
    int cnt, t;
}
bool cmp(node a, node b) {
    return a.cnt < b.cnt; // 降序
    return a.cnt > b.cnt; // 升序
}
priority_queue<node, vector<node>, function<bool(node,node)> > p(cmp); 
2.使用运算符重载 < 
struct node {
    int cnt, t;
    bool operator < (const node& a) const {
        return cnt < a.cnt; //降序
        return cnt > a.cnt; //升序
    }
}
priority_queue<node> p; 
// 注意
对运算符<重载：<被重载后在该类使用<都被重载了，而不只是对sort里的<进行重载，他是对整个类的<都产生了影响。
必须注意的是可以加const就必须要加const，否则可能编译出错。
3.自定义排序对象
struct cmp {
	bool operator() (const node & a, const node& b) const{
		return a.cnt > b.cnt;
	}
};
priority_queue<node, vector<node>, cmp > p; 
// 与sort比较
sort的重载需要的是一个对象，queue重载需要的是一个类型
sort(nums.begin(), nums.end(), cmp()); // cmp() 调用构造函数创建对象
// 平时使用的时候传入的函数名是指针，实际也是一个对象
```



#### stack 

```c++
stack, 栈
size()
empty()
push()  向栈顶插入一个元素
pop()  弹出栈顶元素
top()  返回栈顶元素
```

#### deque

**双端队列**

   ```c++
size()
empty()
clear()
front()/back()
push_back()/pop_back()
push_front()/pop_front()
begin()/end()
[]
   ```

#### lower_bound/upper_bound

**作用**：

​	**lower_bound**用于查找容器中**大于等于某**值的数，返回这个数的**指针**。
​	**upper_bound**用于查找容器中**大于**某值的数，返回这个数的**指针**。

**vector容器内的使用**

```c++
auto it = lower_bound(nums.begin(), nums.end(), 3);
auto it = upper_bound(nums.begin(), nums.end(), 10);
```

**set和multiset自带lower_bound和upper_bound函数**

```c++
set<int> st;
multiset<int> st;
t1 = st.lower_bound(3);
set<int>::iterator it2 = st.upper_bound(3);
```


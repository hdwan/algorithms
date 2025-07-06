# Collection

**`Collection`主要结构树**：

![image-20231108140423271](./typora文档图片/image-20231108140423271.png)

## List

常用的有：ArrayList、LinkedList、Vector（不常用）。

### 公共常用方法

| 方法                              | 说明                                                     |
| --------------------------------- | -------------------------------------------------------- |
| `boolean add(E e)`                | 添加元素到末尾                                           |
| `boolean add(int index, E e)`     | 在指定位置插入元素                                       |
| `boolean addAll(Collection coll)` | 添加所有元素到另一个集                                   |
| `get(int index)`                  | 获取指定位置的元素                                       |
|`indexOf(Object o)`|返回索引或者-1|
| `set(int index, E e)`             | 修改指定位置的元素                                       |
| `remove(int index)`               | 删除指定位置元素                                         |
| `remove(Object o)`                | 删除指定对象，只会默认删除第一次出现的元素，后面的不删除 |
| `boolean removeAll(Collection coll)` | 取当前集合的差集 |
| `contains(Object o)`              | 判断是否包含某元素                                       |
|`boolean containsAll(Collection coll)`|是否包含指定集合所有元素|
| `size()`                          | 返回元素个数                                             |
| `isEmpty()`                       | 是否为空                                                 |
| `clear()`                         | 清空所有元素                                             |

### 遍历

四种遍历方式

- **普通for循环**

  ```java
  List<Integer> list = new ArrayList<>();
  for (int i = 0; i < list.size(); i ++)
      System.out.println(list.get(i));
  ```

- **迭代器**

  Java迭代器（`Iterator`）是 Java 集合框架中的一种机制，是一种**用于遍历集合**（如列表、集合和映射等）的**接口**。

  `Iterator`（迭代器）不是一个集合，它是一种用于访问集合的方法。

  **不能直接创建`Iterator`对象（通过new），该对象是以内部类的形式存在于每个集合类的内部。**

  **获取方式**：`Collection`接口中定义了获取集合类迭代器的方法 `iterator()`，返回对应集合的迭代器对象。（所有`Collection`接口的容器类都有一个`iterator`方法）

  ```java
  1.boolean hasNext(); // 判断集合中是否有元素，如果有元素则可以迭代就返回true
  2.E next();  // 返回迭代的下一个元素 注意：如果没有下一个元素时，调用next元素会抛出NoSuchElementException异常
  
  List<Integer> list = new ArrayList<>();
  Iterator<Integer> it = list.iterator();
  while (it.hasNext()) {
      System.out.println(it.next());
  }
  ```
  
- **增强for**

  ```java
  for (Integer i: list)
      System.out.println(i);
  ```

- **Lambda表达式**

  ```java
  list.forEach(i->System.out.println(i)); 
  ```

### ArrayList

适用于**频繁获取元素值**的情况。

#### 初始化

```java
// 初始化一个空列表
List<Integer> list = new ArrayList<>();

// 初始化固定元素（Java 9+）
List<Integer> list = List.of(1, 2, 3);  // 不可变
// 或可变列表
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));
```

### LinkedList

适用于需要**频繁的插入或删除元素**操作的情况。

`LinkedList`**实质**是一个**链表**。底层通过**双向链表**实现。

**不支持随机存取**，只能从一端开始遍历，直到找到需要的元素后，`get` 方法实现也是用遍历实现，源码：

#### 常用 API

用于**普通队列**、**双端队列**、栈等

| 方法            | 说明                 |
| --------------- | -------------------- |
| `addFirst(E e)` | 从头部添加元素       |
| `addLast(E e)`  | 从尾部添加元素       |
| `removeFirst()` | 移除并返回头部元素   |
| `removeLast()`  | 移除并返回尾部元素   |
| `getFirst()`    | 获取头部元素，不移除 |
| `getLast()`     | 获取尾部元素，不移除 |

遍历同上。

### Vector

### Stack

## Set

主要包含`HashSet`、`LinkedHashSet`、`TreeSet`。

`Set`集合底层都是由`Map`实现。

### HashSet

无序、不重、无索引。因为元素没有顺序，所以无法通过索引来访问元素。

`HashSet`底层实现是一个哈希表（由 `HashMap` 实现），按`Hash`算法来存储集合中的元素，不是线程安全的，集合元素可以是`null`。

**适用场合**：元素不需要排序，想快速判断一个元素是否存在于集合中。

#### 常用方法

```java
HashSet<String> hashSet = new HashSet<>();
hashSet.add("apple"); // 增
hashSet.remove("apple"); // 删
hashSet.add("apple");
System.out.println(hashSet.contains("apple")); // 查
System.out.println(hashSet.size()); // 元素个数
System.out.println(hashSet); // 格式：[a, b]
hashSet.clear(); // 清空
hashSet.isEmpty(); // 是否空
```

#### 遍历

```java
// 增强for循环遍历
for (String item: hashSet) {
    System.out.println(item);
}

// forEach循环遍历
hashSet.forEach(item-> System.out.println(item));

// 迭代器循环遍历
Iterator<String> it = hashSet.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

### LinkedHashSet

**有序**（存储和取出顺序一致）、不重复、无索引。

底层数据结构**依然继承自** `HashSet`，只是每个元素又额外多了一个**双链表的机制**记录存储的**顺序**。

**无参构造**

调用父类构造方法，即`HashSet`()，然后父类`HashSet`又调用`LinkedHashMap`构造。

```java
public LinkedHashSet() {
    super(16, .75f, true); // 调用父类构造方法，即HashSet()，如下
}

HashSet(int initialCapacity, float loadFactor, boolean dummy) {
    map = new LinkedHashMap<>(initialCapacity, loadFactor);
}
```

#### 常用方法

```java
LinkedHashSet<String> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add("apple"); // 增
linkedHashSet.add("banana");
linkedHashSet.size(); // 元素个数
linkedHashSet.remove("apple"); // 删
linkedHashSet.contains("banana"); // 查
System.out.println(linkedHashSet); // 输出
```

一般最好使用`HashSet`（效率较高），如果要求**存取有序**，使用`LinkedHashSet`（效率较低）。

### TreeSet

不重、无索引、可排序（实现了 `SortedSet` 接口，可以排序）。

`TreeSet`集合底层是基于**红黑树**的数据结构实现排序的，增删改查性能较好。

默认排序规则：

- 对于**数值类型**：Integer，Double，默认按照**从小到大**的顺序进行排序；
- 对于字符、字符串类型：按照字符**在ASCII码表中的数字升序**进行排序；

自定义排序规则：

- 默认排序/自然排序：实现`Comparable`接口指定比较规则；
- **比较器排序**：创建TreeSet对象的时候，传递比较器`Comparator`指定规则；

`TreeSet`是由`TreeMap`实现的，无参构造方法如下：

```java
public TreeSet() {
    this(new TreeMap<>()); // 调用TreeMap的构造方法
}
```

**常用方法**

```java
 TreeSet<String> treeSet = new TreeSet<>();
 treeSet.add("apple"); // 增
 treeSet.add("banana");
 treeSet.remove("apple"); // 删
 treeSet.clear(); // 清空
 treeSet.contains("apple"); // 查
 System.out.println(treeSet.isEmpty());
 System.out.println(treeSet);
```

**注意**：`TreeSet` 不允许插入 `null` 元素。

## Queue

| 实现类                  | 说明                                   |
| ----------------------- | -------------------------------------- |
| `LinkedList`            | 最常用的通用队列实现（也可当双端队列） |
| `ArrayDeque`            | 数组实现的双端队列，更高效             |
| `PriorityQueue`         | 优先队列，元素自动按优先级排序         |
| `ConcurrentLinkedQueue` | 并发队列（多线程）                     |

`Queue`接口（先进先出）：

```java
boolean add(E e); // 队尾插入
boolean offer(E e); // 队尾插入

E remove(); // 删除并返回队头，为空则抛出异常
E poll(); // 删除并返回队头，为空则返回null
    
E element(); // 返回队头，为空则抛出异常
E peek(); // 返回队头，为空则返回null

E size(); // 返回队列长度
boolean isEmpty(); //队列是否为空

boolean contains(E e); // 是否包含
void clear(); // 清空
```

`Deque`接口（双端队列，队首队尾都可以出队、入队）：

```java
public interface Deque<E> extends Queue<E> {
    void addFirst(E e);
    void addLast(E e);

    boolean offerFirst(E e);
    boolean offerLast(E e);

    E removeFirst(); 
    E removeLast();

    E pollFirst();
    E pollLast();

    E getFirst();
    E getLast();

    E peekFirst();
    E peekLast();

    boolean removeFirstOccurrence(Object o);
    boolean removeLastOccurrence(Object o);
}
```

### `ArrayDeque`

基于**数组实现**的**双端**队列，队首队尾都可以出队、入队。

### PriorityQueue

**优先队列**，默认小根堆。**基于数组**实现。

增删改查同`Queue`。

**自定义优先级排序**

元素需要实现 `Comparable` 接口或者 `Comparator` 接口。

#### 构建

```java
// 默认小根堆
PriorityQueue<Integer> pq = new PriorityQueue<>();

// 大根堆
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

// 自定义
class Node {
    int dist;
}

PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.dist - b.dist);// 按距离升序排列
PriorityQueue<Node> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.dist));
```

#### 常用 API

| 方法                 | 说明                                        |
| -------------------- | ------------------------------------------- |
| `offer(E e)`         | 添加元素到队列（推荐，失败不抛异常）        |
| `add(E e)`           | 添加元素（队列满时抛异常）                  |
| `poll()`             | 取出并删除堆顶（最小值/最大值）             |
| `peek()`             | 只查看堆顶元素，但不删除                    |
| `isEmpty()`          | 是否为空                                    |
| `size()`             | 当前队列中元素个数                          |
| `clear()`            | 清空队列                                    |
| `contains(Object o)` | 判断是否包含某元素（复杂度 O(n)，效率较低） |
| `remove(Object o)`   | 删除某元素（复杂度 O(n)，仅适用于少量元素） |

# Map

**`Map`结构树**：

![image-20231113220945178](./typora文档图片/image-20231113220945178.png)

## Tips

### 🔹 `Map.merge()`（频次统计神器）

```java
map.merge(5, 1, Integer::sum);  // 如果存在 key=5，就 +1；否则设为 1


default V merge(K key, V value, BiFunction<? super V, ? super V, ? extends V> remappingFunction)
```

- **key**：要插入或合并的键
- **value**：如果 key 不存在，直接插入的初始值
- **remappingFunction**：如果 key 存在，用旧值和新值合并的函数（返回合并后的值）

 如果 key 不存在：

```java
map.merge("apple", 1, Integer::sum);  
// map中没有"apple"，所以直接放入："apple" → 1
```

 如果 key 存在：

```java
map.merge("apple", 1, Integer::sum);
// map中已有"apple"=1 → 调用 Integer::sum(1, 1) → 结果2 → 更新为 "apple" → 2
```

自定义合并函数的写法：

```java
map.merge("apple", 1, (oldVal, newVal) -> oldVal + newVal);
map.merge("apple", 1, (a, b) -> Math.max(a, b));
map.merge("apple", 1, (a, b) -> a); // 保留旧值
```

# 工具类

### 

## Collections

操作 `List`、`Map`、`Set` 等。

### 🔹 查找

```java
// 排序
Collections.sort(list);  // 默认升序
Collections.sort(list, (a, b) -> b - a);  // 降序

// 查找
Collections.max(list);
Collections.min(list);
int idx = Collections.binarySearch(list, target); // list需有序

//其他
Collections.reverse(list);       // 反转
Collections.shuffle(list);       // 洗牌
Collections.swap(list, i, j);    // 交换元素
Collections.fill(list, 0);       // 所有元素设为0
```

**注意**：`fill` 一般用来填充基本数值，比如 `0`、`a`等，不能用来填充对象，比如 `new ArrayList<>()`，因为 `fill` 填充的时候只创建了一个对象，所有元素都指向该引用！

## Arrays

适用于 `int[]`、`String[]` 等数组。

```java
// 数组排序
Arrays.sort(arr);  // 升序
Arrays.sort(arr, Collections.reverseOrder());  // 包装类才能降序，如 Integer[]

// 转换为 List
List<Integer> list = Arrays.asList(1, 2, 3);  // 固定长度，不可增删
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));  // 可修改

// 比较、填充
Arrays.equals(arr1, arr2);
Arrays.fill(arr, 0);  // 全部填 0
```


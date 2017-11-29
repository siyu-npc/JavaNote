## 集合
### 1.数组
数组可以存储基本数据类型和类类型
### 2.Arrays类
Arrays类有一套static方法，提过数组操作的使用功能
		1. equals()：比较两个数组是否相等
		2. fill()：用某个值填充整个数组
		3. sort()：对数组排序
		4. binarySearch()：在有序数组中查找元素
		5. asList()：接受任意的数组为参数，并将其转变为List容器

### 3.容器
Java中将容器分为两类：
1. Collection：一组独立的元素
	- List：元素有特定的顺序
	- Set：不能有重复元素
2. Map：一组成对的键值对（key-value）对象

**Collection的功能方法：**

|方法|功能|
|----|--------|
|add(Object)|添加元素|
|addAll(Collection)|添加另一个Collection|
|clear()|清除所有元素|
|contains(Object)|判断容器中是否有某个元素|
|containsAll(Collection)|判断容器中是否有另一个容器的所有元素|
|isEmpty()|容器是否为空|
|iterator()|返回一个迭代器|
|remove(Object)|移除某个元素|
|removeAll(Collection)|移除另一个容器中包含的元素|
|retainAll(Collection)|求交集|
|size()|容器中元素个数|
|toArray()|返回一个包含容器中所有元素的数组|

**List的功能方法：**
常用的List有两种：**ArrayList**和**LinkedList**
List使用get(id)方法获取某个元素

**常用的Set：**

|类型|简介|
|----|----|
|HashSet|为快速查找而设计的Set，存入其中的类型必须实现hashCode()函数|
|TreeSet|保持次序的Set，底层为树结构|
|LinkedHashSet|具有HashSet的查询速度，且内部使用链表维护元素的顺序|

**常用的Map：**

|类型|简介|
|---|---|
|HashMap|基于散列表的实现，可以通过构造器设置容量capacity和负载因子load factor|
|TreeMap|基于红黑树，得到的结果是经过排序的|
|LinkedHashMap|使用链表维护内部次序，因此迭代遍历时取得key-value的顺序是插入顺序|

### 4.迭代器（Iterator）
### 5.集合接口：Collection、List、Set、Map
**Vector不再被使用。**


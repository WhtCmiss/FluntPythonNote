# Fluent Python
## 第一章 数据模型

主要是一些魔术方法的使用
```
特殊方法的创建
__getitem__ 列表[]
__len__ len()
__bool__ bool()
__str__ str，若无__str__,则会使用__repr__
__repr__ 主要供开发人员使用
```
---
## 第二章 序列

1. 针对大量数据，使用列表占用大量内存，可以使用生成器。生成器仅可使用一次，到达末尾后生成器生命结束
```
   针对列表
   [[]]*3 内部的列表只是一个引用，若进行修改则会修改所有
```
2. 使用简单列表推导式，同样生成生成器。相对于filter与map，列表推导式可能会有更好的性能，更易读
3. 元组作为不可变序列，更强大的功能是作为少量字段的记录功能。
```  
  具名元组 namedtuple
  from collections import namedtuple
  Name = namedtuple("Name","name1 name2")
  or
  Name = namedtuple("Name",["name1","name2"])

```
4. 切片，自定义slice方法，可以对切片进行命名.`slice(start,end,step)`，与[start,end,step]具有相同的效果
5. 对于内置函数sorted()和list.sort()，后者会就地排序而不会产生新的列表，返回值为None,前者会返回一个新的列表。关键字参数key定义排序方法
6. bisect与insort使用二分查找对有序序列进行快速的查找与插入。
7. 针对序列，可以选择使用其它不同的数据结构
```
  array.array() 数字数组，节省空间，速度更快。数组有Numpy和Scipy，提供高阶数组和矩阵操作。
  collections.deque() 双向队列
  queue 标准队列，队列可限制大小。满之后则会锁定队列
  multiprocessing 进程间通信队列
  asyncio 异步编程任务管理
  heapq 类似栈结构的实现，作为堆队列或优先队列
```

---
## 第三章 集合与字典

1. 可散列的映射类型，字典的键必须是可散列的。字典同样可用推导式来生成。
2. 常见的映射方法
```
  dict 普通字典映射
  collections.defaultdict 带有默认值的字典，__getitem__取不到值则返回默认值
  collections.OrderedDict 带顺序的字典，根据插入顺序

  特殊方法__missing__，针对映射找不到键的情况,只会在__getitem__找不到键时调用，对get()和in无效
  collections.ChainMap 接受多个映射对象，查找时逐一映射进行查找
  collections.Counter 计数器，统计每个键出现的次数
  collections.UserDict 实现自己的dict
  types.MappingProxyType 生成一个只读属性的映射
```
3. 集合无序且不能散列，frozenset集合不可变
4. 字典与集合使用散列表进行存储与查找，字典是以空间换时间的存储方式。散列表会根据存储动态修改，因此无序，并且不能在循环的同时修改。

---
## 第四章 文本和字节序列

1. Chardet 可检测编码，不过达不到完全准确
2. 尽量全部使用utf-8
3. 在遇到具体问题时根据具体问题进行解决！！！
4. 二进制字符串与字符串问题，通过decode解码，encode转码
5. 读写文件使用相同编码，尽量明确指定编码
6. normalize 规范化，特殊情况下使用
7. 根据区域进行unicode排序，PyUCA,Unicode排序算法

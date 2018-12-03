# Fluent Python

## 第十四章 可迭代，迭代器与生成器

1. 迭代器惰性获取数据，从可迭代对象中获取迭代器。标准迭代器实现__next__方法获取下一个可用元素，实现__iter__方法返回self。迭代器自身也可以进行迭代。
2. 函数中含有yield关键字，就是生成器函数。调用生成器函数返回生成器对象。每一次调用next()，会执行完成yield并在这个地方暂停，等待下一次的调用
3. 需要生成简单的生成器可以使用生成器表达式，当需要多次使用，定义生成器函数更为优先
4. 标准库中的生成器函数
```
   用于过滤
   itertools.compress(it,selector_it)    并行处理可迭代对象，如果selector_it中为真值，产出it中元素
   itertools.dropwhile(predicate,it)     跳过predicate计算结果为真的值，产出剩余元素
   filter 过滤
   filterfalse 与filter相反
   islice 类似切片，惰性产出
   itertools.takewhile(predicate,it)     产出真值时产出对应元素并立即停止

   用于映射
   itertools.accumulate(it,[func])       产出累计总和，生成每一次累积的值
   itertools.starmap(func,it)            可迭代对象产出可迭代的元素iit，供func(*iit)使用
   enumberate()                          为迭代出来的元素编号

   用于合并
   chain()                               合并多个可迭代对象
   itertools.from_iterable(it)           it中仍然全是可迭代对象
   itertools.product(it1,it2,...,repeat=1)  计算笛卡儿积
   zip_longest and zip

   将输入元素扩展成多个输出元素
   itertools.combinations(it,out_len)    将it产出的out_len个元素组合(排列组合)在一起输出
   itertools.combinations_with_replacement(it,out_len)    包含相同元素的组合
   itertools.count(start=0,step=1)       从start开始按照step产出元素
   itertools.cycle(it)                   按顺序循环重复不断的产出元素
   itertools.permutations(it,out_len=None)  按照排列的方式输出
   itertools.repeat()                    重复产生指定元素

   重新进行排列
   itertools.groupvy(it,key=None)
   itertools.tee(it,n=2)                产出多个生成器
```
5. 当iter()函数传入两个参数时，第二个值是标记值，当调用对象返回该值，触发StopIteration异常


## 第十五章 上下文管理器与else

1. else语句不仅可以跟在if后面还可以在for，while，try后面使用。for：当循环运行完毕且没有break。while：当循环因False而退出，没有break。try：当try块中没有异常存在。
2. 上下文管理器协议包含__enter__和__exit__两个方法，with语句开始，调用enter，结束调用exit。实现这两个方法，即实现了一个上下文管理器
3. contextlib模块中的@contextmanager装饰器可以把简单的生成器函数变为上下文管理器。通过yield进行__enter__和__exit__的分割。yield之前为__enter__。
4. 上下文管理器inplace可以生成两个文件句柄，同时对文件进行读写。

## 第十六章 协程

1. 协程增加了yield语句的赋值，协程与生成器一样需要先激活，激活后可以使用send方法发送数据给协程，生成器在收到send发送的数据之后继续运行到下一个yield处暂停。使用close方法可以关闭协程。遇到无法处理的异常，协程同样会终止
2. 协程可以通过装饰器进行预激活
3. 协程的返回值会在协程运行结束后跟随在StopIteration的错误信息中
4. yield from 作为中间层，可以连接两个协程，使之间进行通信。多个yield from连接多个，可以完成更多的前置

## 第十七章 使用future处理并发

```
  python3 中使用concurrent.futures
  python2 中需要安装futures包
  多线程
  futures.ThreadPoolExecutor() 线程池 I/O密集型  threading完成更复杂的设定
  多进程
  futures.ProcessPoolExecutor() 进程池 CPU密集型  multiprocessing完成更复杂的设定
  也可以自己添加future实例
  executor.submit()提交实例
  executor.as_completed()运行所有实例
  executor.map(func,items)  对每一个元素执行func函数的调用
```

## 第十八章 使用asyncio处理并发

1. python3 最新版本增加了async 和 await关键字来代替@asyncio.coroutine装饰器和yield from语句
2. 协程需要启动事件循环loop
3. 理解协程，更多的需要在实践方面的使用。

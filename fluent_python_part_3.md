# Fluent Python
## 第五章 一等函数

1. 函数也是对象并且可以作为参数进行传递，也可以作为函数的返回值，同样可以赋值给新的参数使用.
2. 高阶函数接受函数作为参数,例如sorted函数中key参数就是接收一个函数，目前仍然广泛使用的高阶函数为map函数
```
   all(iterable) 若每个元素均为真值，返回True all([]) True
   any(iterable) 含有真值即返回True  any([]) False
```
3. lambda匿名函数，使用简单语句，若过于复杂应转换为def定义一个函数
4. 在类中定义改方法__call__，则实例可调用，用户可以自己实现调用方法
5. (*) 定位参数，(**) 关键字参数。函数中__defaults__中保存定位参数与关键字参数的默认值。仅保存关键字参数默认值__kwdefaults__
6. python3 支持函数的注解，在参数后面加:给定注解类型，以及函数:之前添加->注解类型，可以方便使用编辑器与用户自己阅读代码
7. functools.partial 冻结一个函数的参数，例如add(a,b).通过partial(add,3)，即生成一个新的函数，第一个参数永远为3.


## 第六章 使用一等函数实现设计模式

动态语言实现设计模式会有简化，根据设计模式设计代码结构与方法可以是程序很好的进行复用。在python中，因为函数同样可以作为参数传递并进行调用，一些只实现一个方法的类，可以使用一个函数来进行代替。python类中可以定义__call__方法，从而使得该类的实例可以直接当作函数进行使用,实现单接口实例方法，可以优化使用方式。


## 第七章 装饰器与闭包

1. 装饰器，用来增强函数的行为。并返回修改后的函数。装饰器在被装饰的函数被定义之后机运行
```
   装饰器
   @functools.wraps
   def fun(*args,**kwargs):
       pass
   即类似于使用functools.wraps(fun)，返回被修改后的fun
```
2. 作用域问题，global 在函数中使用，声明全局变量， nonlocal 在函数中使用，将变量标记为自由变量，可以在闭包中进行赋值，仍然是局部变量
3. 标准库中装饰器
```
   @functools.wraps 复制原函数相关属性,从而使装饰器可以处理关键字参数
   @functools.lru_cache() 优化函数从而避免重复的耗时计算，韩式函数计算结果进行缓存，可带配置参数
   @functools.singledispatch 将普通函数变为泛函数
   举个栗子：
   @singledispatch
   def fun(obj):
       return type(obj)

   @fun.register(str)
   def _(str):
       return 'str'

   @fun.register(int)
   def _(int):
       return 'int'
```
4. 装饰器可重叠使用，从下往上依次对函数进行处理。装饰器可以带参数，实现方式为在装饰器函数内增加一个工厂函数对传入函数进行处理，从而使用装饰器的参数。
```
   举个栗子(重叠使用)：
   @a
   @b
   def fun():
       pass
   f = a(b(fun))
   举个栗子(带参数):
   def wrap(obj=""):
       @functools.wraps
       def active(func):
           if obj:
               dosometing to fun
           else:
               pass
           return new_func
       return active
   @wrap
   def func():
       pass
```

# 属性相关

## 15-python-面向对象-类属性-上

1. 类也是对象

2. 给类增加一个属性（在类的外面通过赋值的方法）：

   ```python
   class Money:
   	pass
   one=Money()
   Money.count=1 #给类增加一个属性
   print(Money.count)
   print(Money.__dict__)
   ```

## 16-python-面向对象-类属性-下

1. 类增加属性的方式二（在类的内部通过赋值的方法）：

   ```python
   class Money:
   	age=28
       count=1
       num=666
       
   one=Money()
   print(Money.count)
   print(Money.age)
   print(Money.__dict__)
   ```

## 17-python-面向对象-类属性-查询属性

1. 通过对像访问类属性:优先从对像自身上查找属性，找到则结束，如果没有找到，根据class找到对象对应的类，到这个类里面查找。

   ```python
   print(one.age)
   print(one.aount)
   ```

2. 可以更改对象的类：

   ```python
   class text:
       pass
   one.__class__ = text#更改对象的类
   print(one.age)#不能访问
   ```

## 18-python-面向对象-类属性-修改属性

1. 通过类名修改

   ```python
   class Money:
   	age=28
           count=1
           num=666
           
   Money.age=22
   print(Money.age)
   ```

2. 不能通过对象修改类属性

## 19-python-面向对象-类属性-删除属性

1. del 类名 类属性

   ```python
   del  Money.age
   ```

2. 不能通过对象删除，del语句只能删除直系属性

3. 类的属性的增、删、改只能通过类来访问，查询的时候可以通过对象和类来访问！

## 20-python-面向对象-类属性的内存存储

1. 类属性的内存存储问题：一般情况下，属性存储在`__dict__`字典当中，有些内置对象没有这个属性，一般对象可以直接修改`__dict__`属性，类对象的`__dict__`为只读，默认无法修改。

   ```python
   class Money:
   	age=28
       count=1
       num=666
           
   one=Money()
   one.__dict__['age'] = 999#对象的__dict__可以被修改
   print(one.age)
   ```

## 21-python-面向对象-类属性被各个对象所共享

1. ```python
   class Money:
   	age=28
       count=1
       num=666
           
   one=Money()
   two=Money()
   print(one.age)
   print(two.age)
   ```

2. 查看一个类的所有属性通过`类名.__dict__`来查看

## 22-python-面向对象-**类属性**和**对象属性**总结对比

## 23-python-面向对象-限制对象属性的添加`__slots__`

1. ```python
   class Person:
       __slots__=['age']  #只有slots所限定的属性
       pass
   p1 = Person()
   p1.age = 18
   p1.name = '小狗' #将报错
   ```

# 方法相关

## 24-python-面向对象-方法的讲解说明

## 25-python-面向对象-方法的概念和作用

1. 描述一个目标的行为动作

2. 和函数非常类似，都封装了一系列动作，都可以被调用之后执行一系列行为动作，最主要的时调用方式

   ```python
   class Person：
   	def eat2(self):
           print(1)
           print(2)
           print(3)
   p = Person()
   p.eat2()
   ```

## 26-python-面向对象-类、对象、类对象、实例对象、实 例的叫法规范

## 27-python-面向对象-方法的划分依据

1. 实例方法：默认第一个参数需要接收到一个实例

2. 类方法：默认第一个参数需要接收到一个类

3. 静态方法：一个默认参数也不接受

4. 注意：1.划分依据是：方法第一个参数必须要接受的的数据类型。2.不管是哪一种给类型方法，都储存在类当中，没有在示例当中的。3.不同类型方法调用方式不同。

   ```python
   class Person:
   	def eat2(self):
           print('这是一个实例方法',self)
       @classmethod
       def leifangfa(cls):
           print('这是一个类方法',cls)
       @staticmethod
       def jiangtaifanfa():
           print('这是一个静态方法')
   ```

   

## 28-python-面向对象-方法的储存问题

1. 函数也是对象
2. 方法也保存在类的`__dict__`中，没有在实例当中的

## 29-python-面向对象-小节掌握说明

## 30-python-面向对象-实例方法

1. 标准的调用方法：使用实例调用实例方法，不用手动调，解释器会把调用对象（实例）本身传递过去。如果实例方法没有接受任何单数则会报错。

   ```python
   class Person:
       def eat(self,food):#self可以是aa、bb 等，一般是self
           print('在吃饭',food)
   
   p = Person()
   p.eat('土豆')
   #-------------------------------
   class Person:
       def eat(): #报错，因为实例方法必第一个必须接收实例作为第一个参数
           print('在吃饭')
   
   p.eat()
           
   ```

2. 其他的的调用方法：使用类调用、间接调用，他们的本质就是直接找到函数本身来调用。

## 31-python-面向对象-类方法

1. 类方法可以被实例调用，也可以被类调用。

   ```python
   class Person:
       @classmethod #装饰器的作用：在保证原函数不变的情况下，直接给这个函数增加一些功能
       def leifangfa(cls,a):
           print("这是一个类方法" , a)
           
   Person.leifangfa(123)
   
   p = person()
   p.leifangfa(666)
   
   func = Person.leifangfa
   func(111)
   ```

## 32-python-面向对象-静态方法

1. 既可以通过类调用，也可以通过示例调用

   ```python
   class Person:
       @staticmethod #装饰器的作用：在保证原函数不变的情况下，直接给这个函数增加一些功能
       def jingtai(cls):
           print("这是一个类方法")
           
   Person.jingtai()
   
   p = Person()
   p.jingtai()
   
   func = Person.jingtai
   func()
   ```

## 33-python-面向对像-不同类型的方法中访问不同类型的属性的权限问题

1. 访问类属性：通过类和实例

   访问实例属性：只能通过实例

   ```python
   class Person:
       age = 0
       def shilifangfa(self):
           print(self)
           print(self.age)
           print(self.num)
       @classmethod
       def leifangfa(cls):
           print(cls)
           print(cls.age)
           print(cls.num)   #不能通过类访问实例属性
       @staticmethod
       def jingtaifangfa():
           print(Person.age) #可以通过类访问类属性
   P = person()
   P.num = 10
   ```

## 34-python-面向对象-补充-元类

1. 元组：创建类对象的类

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\Screenshot_20200830_101925_tv.danmaku.bili.png" alt="Screenshot_20200830_101925_tv.danmaku.bili" style="zoom:50%;" />

```python
num = 1
print(num.__class__)  #输出int
%------------------------------------------
s = "abc"
print(s.__class__)   #输出str
%------------------------------------------
class Person:
	pass
p = Person()
print(p.__class__)  #输出Person
%------------------------------------------
print(int.__class__)  #输出type
```

## 35-python-面向对象-补充-类对象的创建方式

1. 调用type函数创建

   ```python
   def run(self):
       print(self)
   xxx = type("Dog",(),{"count":0,"run":run})
   print(xxx)
   print(xxx.__dict__)
   
   d.xxx()   #不是d.Dog
   print(d)
   d.run()
   ```

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\Screenshot_20200830_104601_tv.danmaku.bili.png" alt="Screenshot_20200830_104601_tv.danmaku.bili" style="zoom:67%;" />

## 36-python-面向对象-补充-类对象创建时，元类的查找机制

1. 类的创建流程:

   1. 检测类对象是否有明确的`__mateclass__`属性。
   2. 检测父类中是否存在`__mateclass__`属性。
   3. 检测模块中是否存在`__mateclass__`属性。
   4. 通过内置的type这个元类来创建这个类对象。

   ```python
   #1模块的指定
   __metaclass__ = xxx
   #2
   class Animal:
       pass
   #3
   class Dog(Animal):
       pass
   #4
   class Dog:
       __metaclass__ = xxx
       pass
   ```

## 37-python-面向对象-补充-类的描述

1. ```python
   class Person:
       """
       关于这个类的描述，类的作用，类的构造函数等等；类属性的描述
       Attributes:
       	count: int 代表人的个数
       """
       count = 1
       def run(self, disance, step):
           """
           这个方法的作用效果
           :param distance:blahblah
           :param step:blahblah
           :return:
           """
           print("跑步")
           return  distance,step
   help(Person)  #
   ```

## 38-python-面向对象-补充-注释文档的生成(抽取源文件的注释)

1. 注释文档不包括源码，只包括函数名和它的描述

   方式1.使用内置的模块：pydoc。具体步骤：

   1. 查看文档描述：`python3 -m pydoc 模块名称`
   2. 启动本地服务，浏览文档 ：`python3- m pydoc-p 666`
   3. 生成指定模块html文件：`python3 -m pydoc -w 模块名称`

   命令行命令：

   ``` python
   cd <代码路径>
   python --help
   python -m pydoc <文件名>      #
   python -m pydoc -k <关键字>   #列出文件名中包含关键字的文件
   python -m pydoc -p <端口号>   #指定一个未用的端口号
   python -m pydoc -b           #自动指定端口号
   python -m pydoc -w <文件名>   #在当前目录生成一个html文件
   ```

2. 还有其他方法，只是要安装第三方模块。

# 私有属性

## 39-python-面向对象-补充-私有化属性的概念和意义

1. 概念：限定属性的访问的方法。

## 40-python-面向对象-补充-访问权限测试区域划分

1. 注意：python并没有真正的私有化支持，但是，可以使用下划线完成伪私有的效果。如`_y`、`__z`。

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\Screenshot_20200830_230817_tv.danmaku.bili.png" style="zoom: 50%;" />



## 41-python-面向对象-私有化属性-共有属性

1. 共有属性可以通过

   1. 类的内部访问，也就是类的实例方法中
   2. 子类(延伸类)内部访问
   3. 模块其他位置访问
      1. 类访问（父类，派生类）
      2. 实例访问（父类实例，派生类实例）
   4. 跨模块访问
      1. import形式导入
      2. from 模块 import * 导入

   ```python
   class Animal:
       x = 10
       def test(self):
           print(Animal.x)
           print(self.x)
           pass
   %----------------------
   class Dog(Animal):
       def test2(self):
           print(Dog.x)
           print(self.x)
           pass
   
   a = Animal()
   a.test()		#类的内部访问，通过类内部定义的函数访问
   
   d = Dog()
   d.test2()		#延伸类的访问（通过延伸类内部定义的函数访问）
   
   print(Animal.x)		#模块的其他部分
   print(Dog.x)
   print(a.x)
   print(b.x)
   
   import xxx              #模块的其他部分访问
   print(xxx.a)
   from xxx import *
   print(a)
   
   ```

## 42-python-面向对象-补充-私有化属性-受保护的属性

1. ```python
   class Animal:
       _x = 10
       def test(self):
           print(Animal._x)
           print(self._x)
        pass
   #--------------------
   class Dog(Animal):
       def test2(self):
           print(Dog._x)
           print(self._x)
        pass
   
   a = Animal()
   a.test()		#类的内部访问
   
   d = Dog()
   d.test2()		#延伸类的访问
   
   print(Animal._x)		#模块的其他部分,可以强行访问，有警告
   print(Dog._x)
   print(a._x)
   print(b._x)
   
   import xxx              #模块的其他部分访问,不可访问
   print(xxx.a)
   from xxx import *
   print(a)
   ```

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\Screenshot_20200831_074523_tv.danmaku.bili.png" style="zoom:50%;" />

   

## 43-python-面向对象-私有化属性-私有属性

1. ```python
   class Animal:
       __x = 10
       def test(self):         #定义一个实例方法
           print(Animal.__x)
           print(self.__x)
        pass
   
   #--------------------
   
   class Dog(Animal):
       def test2(self):
           print(Dog.__x)
           print(self.__x)
        pass
   
   a = Animal()
   a.test()		#类的内部访问，可以访问
   
   d = Dog()
   d.test2()		#延伸类的访问，不可以访问
   
   print(Animal.__x)		# 模块的其他部分,不可访问
   print(Dog.__x)
   print(a.__x)
   print(d.__x)
   
   a = 1
   import xxx              #模块的其他部分访问,不可访问
   print(xxx.a)
   from xxx import *
   print(a)
   ```

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\Screenshot_20200831_075343_tv.danmaku.bili.png" style="zoom: 67%;" />

## 44-python-面向对象-补充-私有化属性-私有属性-名字重整机制

1. 名字重整：改`_x`为另外一个名称，如：`_类名_x`。

2. 目的：

   1. 防止外界直接访问
   2. 防止被子类同名称属性覆盖

3. 可以用重整后的名字访问

   ```python
   class Animal:
       __x = 10
       def test(self):
           print(Animal.__x)
           print(self.__x)
           pass
   
   print(Animal.__dict__)
   ptint(Animal,_Animal__x)
   ```

## 45-python-面向对象-补充-私有属性的应用场景

1. 数据保护     2.数据过滤

   ```python
   class Person:
       #作用：当我们创建好一个实例对对象之后，会自动调用这个方法，来初始化这对象
       #init是单词初始化initialization的省略形式
       def __init__(self)
       	self.__age = 18
       def setAge(self,value):
           if isinstance(value,int) and 0<value<200:
           	self.__age = value
           else:
               print("您输入的数据有误，请重新输入")
       def getAge(self):
           return self.__age
       
           
   p1 = Person()
   p1.setAge(20)
   p2 = Person()
   print(p1.getAge())   #访问age
   
   print(p1.__age)      #报错，只能在类内部访问
   print(p2.__age)
   ```

## 46-python-面向对象-补充-变量添加下划线的规范

1. `xx_`：避免与系统关键字冲突
2. `__xx__`：系统内置

# 只读属性

## 47-python-面向对象-补充-只读属性的概念和意义

1. 只读属性的概念：一个属性只能读取，不能写入

## 48-python-面向对象-补充-只读属性-方案一

1. 全部隐藏，通过私有化，即不能读取，也不能写入; 部分公开，通过方法实现（有弊端）

   ```python
class Person:
       def __init__(self):   #初始化方法，通过方法设置属性
           self.__age = 18
       def getAge(self):     #部分公开，通过方法实现
           return self.__age
   p1 = person()
   print(p1.getAge())
   ```

## 49-python-面向对象-只读属性-方案一的优化

1. ```python
   class Person(object):
       def __init__(self):
           self.__age = 18
        # 主要作用：可以以使用属性的方法来使用这个方法
       @property
       def age(self):   #部分公开，通过方法实现
           return self.__age
   p1 = person()
   print(p1.age())
   ```

## 50-python-面向对象-property的作用

1. property的作用:将“一些属性的操作方法”关联到另一个属性，**间接地管理私有属性**。

   ```python
   class C(object):
       def getx(self): return self._x
       def setx(self,value): self._x = value
       def delx(self): del self._x
       x = property(getx, setx, delx)
   ```

## 51-python-面向对象-补充-经典类和新式类

1. 经典类：没有继承object

2. 新式类：继承object

   ```python
   class Person:
       pass
   
   print(Person.__bases__)  #查看父类（基类）k
   ```

3. 在python2中，定义一个类，没有显式的继承自object，那么这个类就是一个继承类，显式的继承自object，他才是一个新式类。

   在python3中，定义一个类，会隐式的继承object，所以默认情况下，就已经是一个新式类。

   建议，无论在python2和3，都显式的继承object。

## 52-python-面向对象-补充-property在新式类中的使用

1. property函数方法
  
   ```python
   class Person(object):
       def __init__(self):
           self.__age = 18
       def get_age(self):
           ruturn self.__age
       def set_age(self, value):
           self.__age = value
       age = property(get_age, set_age)
       
   p = Person()
   print(p.age)
   
   p.age = 30
   print(p.age)
   print(p.__dict__) #输出只有_person__age: 
   
   ```
   
    2.装饰器的方式
   
   ```python
    class Person(object):
       def __init__(self):
           self.__age = 18
              @property
              def age(self):
                  return self.__age
              @age.setter
              def age(self, value):
                  delf.__age = value
   
       p = Person()
       p.age = 20    #既可以读取也可以设置
   ```
   
   

## 53-python-面向对象-补充-property在经典类中的使用(切换版版本为python2)

1. 在经典类中，property只会关联读取方法，不会关联设置和删除方法。
  
   ```python
   class Person(object):
       def __init__(self):
           self.__age = 18
       def get_age(self):
           ruturn self.__age
       def set_age(self, value):
           self.__age = value
       age = property(get_age, set_age)
       
   p = Person()
   print(p.age)   #可以读取，不会报错
   
   p.age = 30     #不会设置属性，而是增加了一个age属性
   print(p.age)
   print(p.__dict__) #输出_person__age和age
   
   #--------------------------
   
   #         装饰器方法
   
   #--------------------------
   class Person(object):
          def __init__(self):
              self.__age = 18
          @property
          def age(self):
              return self.__age
          @age.setter
          def age(self, value):
              delf.__age = value
             
      p = Person()
      print(p.age)   #可以读取，不会报错
   
      p.age = 30     #不会设置属性，而是增加了一个age属性
      print(p.age)
   
      print(p.__dict__) #输出_person__age和age
   ```



## 54-python-面向对象-只读属性-方案二

1. 虽然是私有属性，任然可以通过两种方法设置__age属性：

   `p._Person__age=xxx`

   `p.__dict__['_Person__age']=xxx`

2. 做只读属性的方式二：

   ```python
    class Person:
       #当我们通过实例.属性 = 值，给一个实力增加一个属性，或者修改属性的时候，就会自动调用这个方法，
       #在这个方法内部才会正真地把这个属性，以及对应的数据存储到__dict__字典里面
       def __settter__(self, key, value):
           print(key, value)
           #1.判定，key，是否是我们要设置的只读属性
           if key = "age" and key in self.__dict__.keys():#只能新增属性，不能修改属性
              print("这个属性是只读属性，不能设置数据")
           #2.如果不是只读属性，就给他添加到实例里面去
           else:
              #self.key = value  #这样会陷入死循环
              self.__dict__[key] = value
   ```

# 常用的内置属性

## 55-python-面向对象-常用内置属性

1. 类属性：

   1. `__dict__`:类属性
   2. `__bases__`:类的所有父类构成元组
   3. `__doc__`类的文档字符
   4. `__name__`类名
   5. `__module__`类定义所在模块

2. 实例属性：

   1. `__dict__`:类的实例
   2. `__class__`:实例对应的类

## 56-python-面向对象-补充-私有方法

1. 方法：在函数名前加两个下划线，与属性私有化相同，名字重整机制是相同的。

   ```python
   class Person:
       def __run(self):
           print("run")
   p = Person()
   print(Person.__dict__)
   ```

# 内置方法

## 57-python-面向对象-补充-内置特殊方法-使用意义

1. 内置方法的作用；完成一些特定的功能

## 58-python-面向对象-内置特殊方法-`__str__`

1. 给初始化方法`__init__`里边传递参数，即可创建不同的对象

   ```python
   class Person:
       def __init__(self,n,a):
           self.name = n
           self.age = a
   p1 = Person("zpc", 18) #可创建不同的对象
   ```

2. <u>通过定义`__str__`，就可以通过`print(<对象>)`来查看指定的返回值</u>

   ```python
   class Person:
       def __init__(self,n,a):
           self.name = n
           self.age = a
       def __str__(self):
           return "这个人的姓名是%s，这个人的年龄是%s"%(self.name, self.age)
   p1 = Person("zpc",18) #可创建不同的对象
   
   s=str(p1)
   print(s)
   ```

## 59-python-面向对象-内置的特殊方法-`__repr__`

1. `__repr__`面向的对象是开发人员（解释器）；`__str__`面向的对象是用户。

   ```python
   def Person:
       def __init__(self):
           return"repr"
   ```

2. 如果没有定义`__str__`,那么`str`也返回的是`__repr__`的内容

3. 触发`__str__`的方法：

   1. 直接打印：`print(p1)`
   2. str方法：`s=str(p1)     print(s)`

4. 触发`__repr__`的方法：

   1. `s=repr(p1)     print(s)`
   2. 在交互模式里面将对象名称写出，敲回车

## 60-python-面向对象-内置特殊方法-`__call__`-概念和作用

1. `__call__`的作用：使得对象具有当作函数来调用的能力(将对象变为可调用对象)

   ```python
   class Person:
       def __call__(self):
           print("xxx")
       pass
   p = Person()
   p()            #调用__call__函数
   ```

## 61-python-面向对象-`__call__`应用场景的简单案例

1. 首先创建一个类，类的属性只有一个（p_type），然后创建一个`__call__`方法（只接收一个参数p_color）,这样就可以通过`<实例>(p_color)`。

   ```python
   class PenFactory:
       def __init__(self, p_type):
           self.p_type = p_type       #这个类只有一个属性
       def __call__(self, p_color):
           print("创建了一个%s类型的画笔，他是%s颜色的"%(self.p_type, p_color))
   gangbiF = penFactory("钢笔")       #创建一个对象
   gangbiF('红色')
   ```

# 一些操作

## 62-python-面向对象-索引操作（使对象具有像字典一样的索引操作）

1. 以索引的方式操作python序列：

   1. 增、改：`p[1] =  666`、`p['name'] = sz`
   2. 查：`p[name]`、`p[1]`
   3. 删除：`del p[name]`、`del p[1]`

2. 需要一个字典属性，才可以对对象进行索引操作。
  
   ```python
   class Person:
       def __init__(self):
           self.cache = {}              #定义cache属性，为一个字典
       def __setitem__(self, key, value):
           self.cache[key] = value
       def __getitem__(self, key):
           return self.cache[key]
       def __delitem__(self, key):
           del self.cache[key]
   p = Person()
   p['name'] = 'sz'  #执行这行代码的时候，会调用第一个方法
   print(p['name'])  #调用第二个方法
   ```

## 63-python-面向对象-切片操作

1. 索引是对一个进行增、删、改、查；切片是对多个进行增、删、改、查。
2. python3中，‘切片操作’统一由‘索引操作’进行管理！
   1. `def __setitem__(self, key, value)`:
   2. `def __getitem__(self, item)`:
   3. `def __delitem__(self, key)`:

```python
class Person:
    def __init__(self):
        self.items = [1, 2, 3, 4, 5, 6, 7, 8]  #定义了一个items属性
        
    def __setitem__(self, key, value):
        if isinstance(key,silce):
        self.items[key] = value           #注意切片操作只能修改，不能新增
        #self.items.[key.start: key.stop: key.step] = value  #这样赋值也可以
    def __getitem__(self, key):
        return(key.items[key])            #这里可能有错
    def __delitem__(self, key):
        del self[key]
p = Person()
p[0: 4: 2] = ["a","b"]
print(p.items[0: 4: 2])
```

## 64-python-面向对象-比较操作-映射的内置方法、65-python-面向对象-比较操作-映射的内置方法



1. 为对象定义比较操作，调用此方法，就可以使对象可以向数一样比较大小！
   
   ```python
   class Person:
       def __init__(self, age, height):
           self.age = age
           self.height = height
       def __eq__(self, other):
           return self.age == other.age   #指定相等的比较通过哪个属性比较，
       def __ne__(self, other):
           return self.age != other.age   #指定相等的比较通过哪个属性比较，
   p1 = Person(18, 180)
   p2 = Person(19, 183)
   print(p1 == p2)
   #类似的还有：
   #gt >
   #ge >=
   #lt <
   #le <=  
   #可以通过调换参数的方式定义比较方法，进而简化代码
   ```

## 66-面向对象-比较操作-方案2（通过装饰器自动补全）

1. ```python
   import functools
   
   @functools.total_ordering      #此装饰器会自动补全所需要的方法
   class Person 
       def __lt__(self, other):
           pass
       def __eq__(self, other):
           pass
   ```

## 67-python-面向对象-比较操作-上下文布尔值

1. 非空即为`True`

2. 此方法使对象可以被作为一个布尔值使用。

   ```python
   class Person():
       def __bool__(self):    #通过bool值判定实例是True或False
           return False       #这里也可以是一个返回布尔值的语句
       pass
   
   p = Person()
   if p:
       print("xx")
       
   ```

## 68-python-面向对象-遍历操作-`__getitem__`

1. 遍历操作：
   1. 让我们创建的对象可以使用for循环进行遍历
      1. 实现`__getitem__`方法
      2. 实现`__iter__`方法
   2. 让我们创建的对象可以使用next函数进行访问(迭代器)
   
   ```python
   class Person:
       def __init__(self):
           self.result = 1
       def __getitem__(self, item):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")
               
           return relf.result
       pass
   p = person()
   
   for i in p:    #当执行for循环时，自动进入__getitem__方法，使用这个方法的返回值作为数据
       print(i)
   ```

## 69-python-面向对象-遍历操作-`__iter__`

1. `__iter__`的优先级高于`__getitem__`

   ```python
   class Person:
       def __init__(self):
           self.result = 1
       def __getitem__(self, item):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")
               
           return relf.result
       def __iter__(self):
           print("hfkjasdf")
   p = person()
   
   for i in p:    #当执行for循环时，自动进入__geritem__方法，使用这个方法的返回值作为数据
       print(i)
   ```

2. **可迭代对象**：列表、元组等等；**迭代器**：`iter([1, 2, 3])`

   <img src="C:\Users\HP\Desktop\python面向对象笔记\picture\可迭代对象与迭代器.png" alt="可迭代对象与迭代器" style="zoom: 67%;" />

3. 首先调用`__iter__`,返回一个迭代器，然后调用`__next__`方法；

   ```python
   class Person:
       def __init__(self):
           self.result = 1
       def __getitem__(self, item):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")
           #return iter([1,2,3,4])    如果返回是迭代器，则自动进入迭代器的__next__方法   
           return relf.result
       def __iter__(self):
           return self
       def __next__(self):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")    
           return relf.result
   p = person()
   
   for i in p:    #当执行for循环时，自动进入__geritem__方法，使用这个方法的返回值作为数据
       print(i)
   ```

## 70-python-面向对象-遍历操作-`__next__`

1. 通过next函数访问迭代器：

   ```python
   class Person:
       def __init__(self):
           self.result = 1
       def __getitem__(self, item):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")
           #return iter([1,2,3,4])    如果返回是迭代器，则自动进入迭代器的__next__方法   
           return relf.result
       
       def __next__(self):
           self.result += 1
           if self.result >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")    
           return relf.result
   p = person()
   
   print(next(p))   #直接进入__next__方法
   print(next(p))
   print(next(p))
   print(next(p))
   print(next(p))   #抛出异常，停止遍历
   ```

## 71-python-面向对像-遍历操作-迭代器的复用

1. ```python
   class Person:
       def __init__(self):
           self.age = 1
           
       def __inter__(self):
           self.age = 1   # 如果没有这行命令，那么迭代器只能使用一次
           return self
       
       def __next__(self):
           self.age += 1
           if self.age >=6:   #不满足时，跳出循环
               raise StopIteration("停止遍历")    
           return relf.age
       
   p = person()
   for i in p:
       print(i)
   import collection
   print(isinstance(p, collection.Iterator))  
   #返回值为True，表明确实是一个迭代器，需要同时有两个方法__iter__、__next__
   next(p)  #只要有一个方法__next__就可以访问
   ```

## 72-python-面向对象-遍历操作-迭代器-可迭代的判定依据

1. ```python
   import collection
   print(isinstance(p, collection.Iterable))#判定是否为可迭代对象，只要一个方法__iter__就可以 
   ```

2. 一个可迭代对象一定可以通过`for in`访问，可以通过`for in`访问的不一定是可迭代对象

## 73-python-面向对象-遍历操作-iter的使用（没听懂）

1. 通过`next()`函数访问对象，要想让`iter()`对创建的对象起作用，需要在类里边定义方法：`__getitem__`或者：`__iter__`和`__next__`（这两个方法必须同时都需要）。
2. `iter(<要转换的对象>,<停止数值>)`

## 74-面向对象-描述器-概念和作用

1. 概念：


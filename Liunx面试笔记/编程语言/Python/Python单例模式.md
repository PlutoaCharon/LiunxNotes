单例模式是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例类的特殊类。通过单例模式可以保证系统中一个类只有一个实例而且该实例易于外界访问，从而方便对实例个数的控制并节约系统资源。如果希望在系统中某个类的对象只能存在一个，单例模式是最好的解决方案。

`__new__()`在`__init__()`之前被调用，用于生成实例对象。利用这个方法和类的属性的特点可以实现设计模式的单例模式。单例模式是指创建唯一对象，单例模式设计的类只能实例 这个绝对常考啊.绝对要记住1~2个方法,当时面试官是让手写的.

[__call__函数](https://www.jianshu.com/p/e1d95c4e1697)

### 1、 使用**new**方法

```python
class Singleton(object):

    def __new__(cls, *args, **kw):
        if not hasattr(cls, '_instance'):
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kw)

        return cls._instance


class MyClass(Singleton):
    a = 1


if __name__ == '__main__':
    a = MyClass()
    b = MyClass()
    print('a:', id(a))
    print('b:', id(b))
    print(a is b)
```

运行结果：

```text
a: 1995200289352
b: 1995200289352
True
```

### 2、 装饰器版本

```python
class Singleton(object):
    def __init__(self, cls):
        self._cls = cls
        self._instance = {}

    def __call__(self, *args, **kwargs):
        if self._cls not in self._instance:
            self._instance[self._cls] = self._cls(*args, **kwargs)
        return self._instance[self._cls]


# 使用函数装饰器实现单例
def singleton(cls):
    instances = {}

    def get_instance(*args, **kw):
        if cls not in instances:
            instances[cls] = cls(*args, **kw)

        return instances[cls]

    return get_instance


@Singleton
class MyClass:
    a = 1


if __name__ == '__main__':
    a = MyClass()
    b = MyClass()
    print('a:', id(a))
    print('b:', id(b))
    print(a is b)
```

运行结果：

```text
a: 3077134387656
b: 3077134387656
True
```
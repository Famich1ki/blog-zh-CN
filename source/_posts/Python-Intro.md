---
title: Python Intro
date: 2026-03-13 15:41:19
tags:
  - Python
categories:
  - [Python, Fundamentals]
cover: https://pics.findfuns.org/python.jpg
---



# 列表 (List)

### 使用 `join()` 方法将列表中的所有元素连接成一个字符串。

    list = ["this", "is", "an", "example", "of", "using", "join()", "method"]

    seperator = " - "
    new_list = seperator.join(list)

    print(new_list)
    # this - is - an - example - of - using - join() - method


### 使用 `split()` 方法将字符串拆分为列表。

    print(new_list.split(seperator))
    # ['this', 'is', 'an', 'example', 'of', 'using', 'join()', 'method']


# 集合 (Set)

`intersection()` , `difference()` , `union()`

    set_1 = {1, 2, 3}
    set_2 = {2, 3, 4}

    print(set_1.intersection(set_2))
    print(set_1.difference(set_2))
    print(set_2.difference(set_1))
    print(set_1.union(set_2))

    #{2, 3}
    #{1}
    #{4}
    #{1, 2, 3, 4}


# 字典 (Dictionary)

### 索引访问 VS `get()`

`get()` 在键不存在时会返回 `None`，而不是抛出 `KeyError`。

    dict_1 = {
        "name": "4pril",
        "age": 24,
    }

    print(dict_1.get("phone") is None)
    #True
    print(dict_1["phone"])
    #Traceback (most recent call last):
    #  File "C:\Users\Administrator\PyCharmMiscProject\test.py", line 24, in <module>
    #    print(dict_1["phone"])
    #          ~~~~~~^^^^^^^^^
    #KeyError: 'phone'


### `keys()` , `values()` , `items()`

    print(dict_1.keys())
    #dict_keys(['name', 'age'])
    print(dict_1.values())
    #dict_values(['4pril', 24])
    print(dict_1.items())
    #dict_items([('name', '4pril'), ('age', 24)])

    for k, v in dict_1.items():
        print(k, v, sep=" - ")

    #name - 4pril
    #age - 24


# `format()`

    name = '4pril'

    print("name is {}".format(name))
    # name is 4pril


# `*` 和 `**`

    def func(*args, **kwargs):
        print(args)
        print(kwargs)

    func(1,2,3, name = '4pril', age = 24)
    print('--------------------------------------')

    func([1,2,3], {'name': '4pril', 'age': 24})
    print('--------------------------------------')

    func(*[1,2,3], **{'name': '4pril', 'age': 24})
    print('--------------------------------------')


    #(1, 2, 3)
    #{'name': '4pril', 'age': 24}
    #--------------------------------------
    #([1, 2, 3], {'name': '4pril', 'age': 24})
    #{}
    #--------------------------------------
    #(1, 2, 3)
    #{'name': '4pril', 'age': 24}
    #--------------------------------------

# Comprehensions

### List Comprehension（列表推导式）

    nums = [1, 2, 3, 4]

    list_1 = [n * n for n in nums if n % 2 == 0]
    list_2 = list(map(lambda n: n * n, filter(lambda n: n % 2 == 0, nums)))
    list_3 = [(a, b) for a in 'ab' for b in range(2)]
    print(list_1)
    print(list_2)
    print(list_3)

    #[4, 16]
    #[4, 16]
    #[('a', 0), ('a', 1), ('b', 0), ('b', 1)]

---

### Set Comprehension（集合推导式）

    nums = [1, 2, 3, 4, 5, 1, 3]
    set_1 = {n for n in nums}
    set_2 = set(map(lambda n: n, nums))
    print(set_1)
    print(set_2)

    #{1, 2, 3, 4, 5}
    #{1, 2, 3, 4, 5}

---

### Dictionary Comprehension（字典推导式）

    name = ['Tom', 'Bob', 'Andy']
    age = [24, 18, 30]

    dict_1 = {k: v for k, v in zip(name, age)}
    print(list(zip(name, age)))
    print(dict_1)

    #[('Tom', 24), ('Bob', 18), ('Andy', 30)]
    #{'Tom': 24, 'Bob': 18, 'Andy': 30}

---

### Generator Comprehension（生成器推导式）

    list = [1, 2, 3, 4, 5]

    def square(list):
        for num in list:
            yield num * num

    for i in square(list):
        print(i)
        
    #1
    #4
    #9
    #16
    #25

在 `square` 函数中使用了 `yield`，这意味着它是一个 **生成器函数（generator function）**。当调用该函数时，它返回一个 `generator` 对象。

在使用 **for** 循环调用 **square** 函数时，Python 实际执行的逻辑类似于：

    g = square(list)

    while True:
        i = next(g)
        print(i)

`next()` 是一个 **内置函数（built-in function）**，用于获取生成器产生的下一个值。

第一次调用 `next(g)` 时，生成器会运行直到遇到 `yield`，返回 `1`，然后函数在该位置暂停。

下一次调用 `next(g)` 时，执行会从暂停的位置继续，因此变量 `num` 会从 `2` 开始，而不是重新从 `1` 开始。

---

# `sorted()`

数据结构的准备

    class Student:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def __repr__(self):
            return f'{self.name} {self.age}'


    students = [Student('Cindy', 23), Student('Bob', 21), Student('John', 24)]

`sorted()` 函数有多种使用方式：

- 使用普通函数作为 key
- 使用 lambda 表达式指定 key
- 使用内置函数 `attrgetter()` 获取用于排序的属性

  def get_name(student)
  return student.name

  from operator import attrgetter

  sorted_students_1 = sorted(students, key=get_name)
  sorted_students_2 = sorted(students, key=lambda student: student.age, reverse=True)
  sorted_students_3 = sorted(students, key=attrgetter('age'), reverse=True)

  print(sorted_students_1)
  print(sorted_students_2)
  print(sorted_students_3)

  #[Bob 21, Cindy 23, John 24]
  #[John 24, Cindy 23, Bob 21]
  #[John 24, Cindy 23, Bob 21]

---

# Generator（生成器）

生成器是 Python 中一个非常重要的特性。任何想深入理解 Python 的人都应该掌握它。

为什么生成器如此重要？我们来看下面这个例子。

    '''假设我们想获取一个列表中每个数字的平方，
    一种简单的方法是遍历列表并将每个平方值添加到一个新列表中'''

    list = [1, 2, 3, 4, 5]
    list_square = []

    for num in list:
        list_square.append(num * num)
        
    print(list_square)
    # [1, 4, 9, 16, 25]

在这种情况下，所有值会一次性被计算出来。如果列表中有 10,000,000 个数字，那么将这么多数据全部存入内存是低效且冗余的。

为了提高效率，我们可以使用生成器。

    def square(list):
        for num in list:
            yield num * num
        
    square_numbers = square(list)
    print(square_numbers)

    print(next(square_numbers))
    print(next(square_numbers))
    print(next(square_numbers))
    print(next(square_numbers))
    print(next(square_numbers)) 
    # ps: 如果再调用一次 next()，会抛出 StopIteration 异常，
    # 因为生成器中的数据已经耗尽。

    #<generator object square at 0x00000242DB6DA400>
    #1
    #4
    #9
    #16
    #25

使用生成器时，值是**按需逐个生成**的，而不是一次性全部计算。

生成器也可以通过 for 循环进行迭代：

    for num in square_numbers:
        print(num)

此外，我们还可以使用圆括号来创建生成器：

    nums = (n * n for n in [1, 2, 3, 4, 5])
    print(nums)
    print(list(nums)) # 将生成器转换为列表

    #<generator object <genexpr> at 0x000001F765779700>
    #[1, 4, 9, 16, 25]

现在我们来看列表和生成器在内存使用和执行时间上的差异。

    import sys
    import time

    N = 10_000_000

    start = time.time()

    numbers = [i * i for i in range(N)]

    end = time.time()

    print('List:')
    print('duration:', end - start)
    print('memory usage:', sys.getsizeof(numbers))

    start = time.time()

    numbers = (i * i for i in range(N))

    end = time.time()

    print('Generator:')
    print('duration:', end - start)
    print('memory usage:', sys.getsizeof(numbers))

    #List:
    #duration: 0.501561164855957
    #memory usage: 89095160
    #Generator:
    #duration: 0.04305219650268555
    #memory usage: 208

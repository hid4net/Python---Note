
<h1 style="text-align:center">数据类型和结构</h1>

--------------------------------------------------------------------------------
[返回 Outline](outline.md)

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. Python 数据类型的抽象基类](#1-python-数据类型的抽象基类)
  - [1.1. 标准库 collections.abc](#11-标准库-collectionsabc)
  - [1.2. 标准库 numbers](#12-标准库-numbers)
- [2. 标准库 collections 的数据类型](#2-标准库-collections-的数据类型)
  - [2.1. deque](#21-deque)
- [3. 队列](#3-队列)
  - [3.1. 内建类型 list](#31-内建类型-list)
  - [3.2. 标准库 collections](#32-标准库-collections)
- [4. stack](#4-stack)
  - [4.1. 内建类型 list](#41-内建类型-list)
  - [4.2. 标准库 collections](#42-标准库-collections)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. Python 数据类型的抽象基类

## 1.1. 标准库 collections.abc
|       ABC       |           继承自           |                              抽象方法                              |                                                     混合方法                                                      |
| :-------------: | :------------------------: | :----------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------: |
|    Container    |             -              |                           \_\_contains__                           |                                                         -                                                         |
|    Hashable     |             -              |                             \_\_hash__                             |                                                         -                                                         |
|    Iterable     |             -              |                             \_\_iter__                             |                                                         -                                                         |
|    Iterator     |          Iterable          |                             \_\_next__                             |                                                    \_\_iter__                                                     |
|   Reversible    |          Iterable          |                           \_\_reversed__                           |                                                         -                                                         |
|    Generator    |          Iterator          |                            send, throw                             |                                           close, \_\_iter__, \_\_next__                                           |
|      Sized      |             -              |                             \_\_len__                              |                                                         -                                                         |
|    Callable     |             -              |                             \_\_call__                             |                                                         -                                                         |
|   Collection    | Sized, Iterable, Container |               \_\_contains__, \_\_iter__, \_\_len__                |                                                         -                                                         |
|    Sequence     |   Reversible, Collection   |                      \_\_getitem__, \_\_len__                      |                             \_\_contains__, \_\_iter__, \_\_reversed__, index, count                              |
| MutableSequence |          Sequence          |   \_\_getitem__, \_\_setitem__, \_\_delitem__, \_\_len__, insert   |                    继承自Sequence的方法,</br>append, reverse, extend, pop, remove, \_\_iadd__                     |
|   ByteString    |          Sequence          |                      \_\_getitem__, \_\_len__                      |                                               继承自Sequence的方法                                                |
|       Set       |         Collection         |               \_\_contains__, \_\_iter__, \_\_len__                | \_\_le__, \_\_lt__, \_\_eq__, \_\_ne__, \_\_gt__, \_\_ge__, \_\_and__, \_\_or__, \_\_sub__, \_\_xor__, isdisjoint |
|   MutableSet    |            Set             |        \_\_contains__, \_\_iter__, \_\_len__, add, discard         |            继承自Set的方法,</br>clear, pop, remove, \_\_ior__, \_\_iand__, \_\_ixor__, and \_\_isub__             |
|     Mapping     |         Collection         |                \_\_getitem__, \_\_iter__, \_\_len__                |                           \_\_contains__, keys, items, values, get, \_\_eq__, \_\_ne__                            |
| MutableMapping  |          Mapping           | \_\_getitem__, \_\_setitem__, \_\_delitem__, \_\_iter__, \_\_len__ |                         继承自Mapping的方法,</br>pop, popitem, clear, update, setdefault                          |
|   MappingView   |           Sized            |                                 -                                  |                                                     \_\_len__                                                     |
|    ItemsView    |      MappingView, Set      |                                 -                                  |                                            \_\_contains__, \_\_iter__                                             |
|    KeysView     |      MappingView, Set      |                                 -                                  |                                            \_\_contains__, \_\_iter__                                             |
|   ValuesView    |  MappingView, Collection   |                                 -                                  |                                            \_\_contains__, \_\_iter__                                             |
|    Awaitable    |             -              |                            \_\_await__                             |                                                         -                                                         |
|    Coroutine    |         Awaitable          |                            send, throw                             |                                                       close                                                       |
|  AsyncIterable  |             -              |                            \_\_aiter__                             |                                                         -                                                         |
|  AsyncIterator  |       AsyncIterable        |                            \_\_anext__                             |                                                    \_\_aiter__                                                    |
| AsyncGenerator  |       AsyncIterator        |                           asend, athrow                            |                                         aclose, \_\_aiter__, \_\_anext__                                          |

## 1.2. 标准库 numbers
|   类别   | 说明   |
| :------: | :----- |
| Complex  | 复数   |
|   Real   | 实数   |
| Rational | 有理数 |
| Integral | 整数   |

--------------------------------------------------------------------------------
# 2. 标准库 collections 的数据类型
|   数据类型   | 说明                                                                 |
| :----------: | :------------------------------------------------------------------- |
| namedtuple() | 创建一个命名元组对象                                                 |
|    deque     | 类似list的双端队列                                                   |
|   ChainMap   | dict-like class for creating a single view of multiple mappings      |
|   Counter    | dict subclass for counting hashable objects                          |
| OrderedDict  | 有序dict                                                             |
| defaultdict  | dict subclass that calls a factory function to supply missing values |
|   UserDict   | 便于用户继承, 内建dict使用C语言实现, 用户继承后不易修改              |
|   UserList   | 便于用户继承, 内建list使用C语言实现, 用户继承后不易修改              |
|  UserString  | 便于用户继承, 内建string使用C语言实现, 用户继承后不易修改            |

## 2.1. deque
* into queue: `.append()`, `.appendleft()`, `.insert()`, `.extend()`, `extendleft()`
* out form queue: `.popleft`, `pop()`


--------------------------------------------------------------------------------
# 3. 队列

## 3.1. 内建类型 list
* push:
    * 添加一个对象: `list.append(对象))`或`list.insert(len(列表), 对象)`
    * 添加一组对象: `list.extend(iterable)`
* pop: `list.pop(0)`

## 3.2. 标准库 collections
* 使用`collections.deque`

--------------------------------------------------------------------------------
# 4. stack

## 4.1. 内建类型 list
* push:
    * 添加一个对象: `list.append(对象))`或`list.insert(len(列表), 对象)`
    * 添加一组对象: `list.extend(iterable)`
* pop: `list.pop()`

## 4.2. 标准库 collections
* 使用`collections.deque`
* init: deque([iterable[, maxlen]]) --> deque object
* 方法和 list 类似, 不同之处:
    * appendleft
    * extendleft
    * maxlen
    * popleft
    * rotate



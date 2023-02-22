
<h1 style="text-align:center">进程、线程、协程</h1>

--------------------------------------------------------------------------------
[返回目录](outline.md)

tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本概念](#-1-基本概念-)
- [2. 多进程](#-2-多进程-)
  - [2.1. 基于标准库 multiprocessing](#-21-基于标准库-multiprocessing-)
    - [2.1.2. 创建进程](#-212-创建进程-)
    - [2.1.3. 运行控制](#-213-运行控制-)
    - [2.1.4. 进程间通信](#-214-进程间通信-)
    - [2.1.5. 进程同步](#-215-进程同步-)
    - [2.1.6. 共享状态](#-216-共享状态-)
    - [2.1.7. 其他](#-217-其他-)
  - [2.2. 基于标准库 concurrent.futures](#-22-基于标准库-concurrentfutures-)
    - [2.2.1. 基本流程](#-221-基本流程-)
    - [2.2.2. ProcessPoolExecutor 对象](#-222-processpoolexecutor-对象-)
    - [2.2.3. Future 对象](#-223-future-对象-)
    - [2.2.4. Module 函数](#-224-module-函数-)
- [3. 多线程](#-3-多线程-)
  - [3.1. 基于标准库 threading](#-31-基于标准库-threading-)
    - [3.1.1. 基本流程](#-311-基本流程-)
    - [3.1.2. 创建线程](#-312-创建线程-)
    - [3.1.3. 运行控制](#-313-运行控制-)
    - [3.1.4. 线程间通信](#-314-线程间通信-)
    - [3.1.5. 线程同步](#-315-线程同步-)
    - [3.1.6. 数据保护](#-316-数据保护-)
    - [3.1.7. 其他](#-317-其他-)
  - [3.2. 基于标准库 concurrent.futures](#-32-基于标准库-concurrentfutures-)
    - [3.2.1. 基本流程](#-321-基本流程-)
    - [3.2.2. ThreadPoolExecutor 对象](#-322-threadpoolexecutor-对象-)
    - [3.2.3. Future 对象](#-323-future-对象-)
    - [3.2.4. Module 函数](#-324-module-函数-)
- [4. 协程](#-4-协程-)
  - [4.1. 基础](#-41-基础-)
  - [4.2. 基于标准库 asyncio](#-42-基于标准库-asyncio-)
    - [4.2.1. Python提供了原生的协程支持](#-421-python提供了原生的协程支持-)
    - [4.2.2. 简单示例](#-422-简单示例-)
    - [4.2.3. 基础](#-423-基础-)
    - [4.2.4. 创建协程](#-424-创建协程-)
    - [4.2.5. 运行控制](#-425-运行控制-)
    - [4.2.6. 协程同步](#-426-协程同步-)
    - [4.2.7. 协程通信](#-427-协程通信-)
    - [4.2.8. 其他](#-428-其他-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本概念
* 多进程 vs 多线程
    * 多进程适用于计算密集型任务, 不适用于 IO 密集型任务
    * 多线程适用于 IO 密集型任务, 不适用于计算密集型任务
* 进程/线程间通信
    * 队列
    * 管道
    * ...
* 进程/线程间同步
    * 互斥锁
    * 信号量
    * ...
* `daemon` 守护进程/线程
    * 其结束后, 其他正在运行的进程/线程也会被结束
* 并行 vs 并发
* 同步 vs 异步
* 阻塞 vs 非阻塞

--------------------------------------------------------------------------------
# 2. 多进程
==特别注意==: 代码必须运行在 `__main__` 命名空间, 即必须使用 `if __name__ == "__main__":`

## 2.1. 基于标准库 multiprocessing

### 2.1.2. 创建进程
* 方法 1: 使用 Process 类
    * Process 类
        * 示例
            ```Python
            # step 1: 导入 Process 类
            from multiprocessing import Process
            import os, time
            # step 2: 定义 task
            def long_time_task(i):
                print(f"子进程 (pid={os.getpid()}) 开始")
                time.sleep(2)
                print(f"子进程 (pid={os.getpid()}) 完成, 结果: 2**{i} = {2 ** i}")
            # 必须在 `__main__` 命名空间中运行
            if __name__ == "__main__":
                print(f"当前母进程: {os.getpid()}")
                start = time.time()
                p1 = Process(target=long_time_task, args=(16,)) # step 3: 创建 Process_对象
                p2 = Process(target=long_time_task, args=(32,)) # step 3: 创建 Process_对象
                print("等待所有子进程完成")
                p1.start()  # step 4: 启动进程
                p2.start()  # step 4: 启动进程
                p1.join()   # step 5: 等到结束
                p2.join()   # step 5: 等到结束
                print(f"总共用时 {time.time() - start}秒")
            # 控制台输出
            # >>> 当前母进程: 8072
            # >>> 等待所有子进程完成
            # >>> 子进程 (pid=19196) 开始
            # >>> 子进程 (pid=13628) 开始
            # >>> 子进程 (pid=13628) 完成, 结果: 2**32 = 4294967296
            # >>> 子进程 (pid=19196) 完成, 结果: 2**16 = 65536
            # >>> 总共用时 2.0736515522003174秒
            ```
        * 构造函数: `Process(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)`
            * 必须用关键词传参
            * 参数
                * `group`: 必须为 None
                * `target`: 需要执行的任务名 (被调函数名)
                * `name`: 进程名
                * `args`: 传入被调函数的参数
                * `daemon`: 是否为守护进程
        * 主要方法
            * `start()`: 启动
            * `join([timeout])`: 等待所有进程完成
                * `timeout`: 可选, 设置超时 (单位: s)
                * 可以被多次调用
            * `run()`: 派生类通过重写该方法以运行所需的任务
            * `terminate()`: 终止进程
            * `kill()`: 终止进程, 与 `terminate()` 类似, 但在 Unix 系统中使用 `SIGKILL`
            * `is_alive()`: 是否正在执行
            * `close()`: 关闭线程, 释放资源, 一旦调用, Process_对象将被注销, 不可访问
        * 主要属性:
            * `name`: 进程名
            * `daemon`: 是否为守护进程
            * `pid`: 进程号
            * `exitcode`: 退出码
                * 如果进程还没被终止, 返回 None
                * 如果正常结束, 返回 0
                * 如果被 `sys.exit(N)` 方法终止, 返回 N
                * 如果由于异常退出, 返回 1
                * 如果被 `signal N` 终止, 返回 -N
            * `authkey`: 认证码
            * `sentinel`
* 方法 2: 创建一个 Process 子类, 并实现 `run()` 方法
    * 示例
        ```Python
        # step 1: 导入 Process 类
        from multiprocessing import Process
        import os, time
        # step 2: 创建 Process_子类
        class myProcess(Process):
            def __init__(self, i):
                super().__init__()  # 必须调用父类的构造方法
                self.i = i  # 内部变量
            # 重写 run 函数
            def run(self) -> None:
                print(f"子进程 (pid={os.getpid()}) 开始")
                time.sleep(2)
                print(f"子进程 (pid={os.getpid()}) 完成, 结果: 2**{self.i} = {2 ** self.i}")
        # 必须在 `__main__` 命名空间中运行
        if __name__ == "__main__":
            print(f"当前母进程: {os.getpid()}")
            start = time.time()
            p1 = myProcess(16)  # step 3: 创建 Process_子类对象
            p2 = myProcess(32)  # step 3: 创建 Process_子类对象
            print("等待所有子进程完成")
            p1.start()  # step 4: 启动进程
            p2.start()  # step 4: 启动进程
            p1.join()   # step 5: 等到结束
            p2.join()   # step 5: 等到结束
            print(f"总共用时 {time.time() - start}秒")
        # 控制台输出
        # >>> 当前母进程: 5768
        # >>> 等待所有子进程完成
        # >>> 子进程 (pid=6640) 开始
        # >>> 子进程 (pid=15476) 开始
        # >>> 子进程 (pid=6640) 完成, 结果: 2**16 = 65536
        # >>> 子进程 (pid=15476) 完成, 结果: 2**32 = 4294967296
        # >>> 总共用时 2.063387393951416秒
        ```
* 方法 3: 使用进程池
    * 示例
        ``` python
        # step 1: 导入 Pool
        from multiprocessing import Pool
        # step 2: 定义 task
        def f(x):
            return x*x
        # 必须在 `__main__` 命名空间中运行
        if __name__ == '__main__':
            with Pool(5) as p:              # step 3: 创建 Pool
                print(p.map(f, [1, 2, 3]))  # step 4: 启动进程
        # 输出: [1, 4, 9]
        ```
    * Pool 容器: `Pool([processes[, initializer[, initargs[, maxtasksperchild[, context]]]]])`
        * 支持异步结果、超时、回调、并行映射
        * 参数
            * `processes`: 进程数, 如果不设置, 将使用 `os.cpu_count()` 的值 (即 CPU 核心数)
    * 主要方法
        * `apply(func[, args[, kwds]])`: 调用任务
        * `apply_async(func[, args[, kwds[, callback[, error_callback]]]])`: 调用任务, 返回 `AsyncResult_对象`
        * `map(func, iterable[, chunksize])`: 调用多个任务, 任务数与参数列表的个数相同, 类似内建 `map` 函数
            * 占用内存较大, 可使用 `imap()` 或 `imap_unordered()` 代替
        * `map_async(func, iterable[, chunksize[, callback[, error_callback]]])`: 类似 `map`, 返回  `AsyncResult_对象`
        * `imap(func, iterable[, chunksize])`: 类似 `map`, 可通过设置 `chunksize` 控制一次送入进程池的数量
        * `imap_unordered(func, iterable[, chunksize])`: 类似 `imap`, 乱序
        * `starmap(func, iterable[, chunksize])`: 类似 `map`, `iterable` 是不展开的参数, 如: 参数为 *[(1,2), (3, 4)]* 时, 表示调用 *[func(1,2), func(3,4)]*
        * `starmap_async(func, iterable[, chunksize[, callback[, error_callback]]])`, 类似 `starmap`, 返回  `AsyncResult_对象`
        * `join()`: 等到进程完成
        * `terminate()`: 终结进程
        * `close()`: 关闭进程池, 释放资源
    * `AsyncResult` 对象: 用于获取进程池中各个进程的返回值
        * 主要方法
            * `get([timeout])`: 返回结果
            * `wait([timeout])`: 等待进程结束
            * `ready()`: 进程是否完成
            * `successful()`: 进程是否成功完成
        * 示例
            ```Python
            from multiprocessing import Pool
            import time

            def f(x):
                return x*x

            if __name__ == '__main__':
                with Pool(processes=4) as pool:         # start 4 worker processes
                    result = pool.apply_async(f, (10,)) # 异步调用进程
                    print(result.get(timeout=1))        # 输出: 100

                    print(pool.map(f, range(10)))       # 输出: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

                    it = pool.imap(f, range(10))
                    print(next(it))                     # 输出:  0
                    print(next(it))                     # 输出:  1
                    print(it.next(timeout=1))           # 输出:  4

                    result = pool.apply_async(time.sleep, (10,))
                    print(result.get(timeout=1))        # 触发异常: multiprocessing.TimeoutError
            ```

### 2.1.3. 运行控制
* 守护进程: 主进程结束时, 强制子进程结束
    * 设置为守护进程:
        * 方法 1: 创建 Process 对象或 Process 子类时初始化
        * 方法 2: 设置 *Process_对象* 或 *Process_子类对象* 的 `daemon` 属性为 True
    * 必须在`.start()` 之前设置好
* 启动: `.start()`方法
* 阻塞, 等待进程结束: `.join(timeout=None)`
* 终结进程: `.kill()`
* 查新进程信息: `pid`, `exitcode`

--------
==继续==

### 2.1.4. 进程间通信
* 消息队列: `multiprocessing.Queue`
    * 类似与线程中的消息队列
* 管道: `multiprocessing.Pipes`
    * 本质是一对儿`Connection`对象: (conn1, conn2)
        * 使用示例`main_pipe, sub_pipe = multiprocessing.Pipes()`
    * `Connection`对象:
        * 支持上下文管理器
        * 主要方法:
            * `send(obj)`, `send_bytes(buffer[, offset[, size]])`
            * `recv()`, `recv_bytes([maxlength])`, `recv_bytes_into(buffer[, offset])`
            * `poll([timeout])`
            * `close()`

### 2.1.5. 进程同步
* 支持的类:
    * `multiprocessing.Lock`
    * `multiprocessing.RLock`
    * `multiprocessing.Semaphore`
    * `multiprocessing.Condition`
    * `multiprocessing.Event`
    * `multiprocessing.Barrier`
* 使用方法和`threading`库中的一样

### 2.1.6. 共享状态
进程使用自己的内存空间, 变量不能直接共享, 没有全局变量, 需通过以下方法:
* 方法1: 共享内存方式: `multiprocessing.Value`, `multiprocessing.Array`
* 方法2: 管理器: `multiprocessing.Manager`
    * Manager对象支持 list, dict, Namespace, Lock, RLock, Semaphore, BoundedSemaphore, Condition, Event, Barrier, Queue, Value and Array

### 2.1.7. 其他
* 获取 CPU 核心数: `multiprocessing.cpu_count()`


## 2.2. 基于标准库 concurrent.futures
==特别注意==: 代码必须运行在`__main__`命名空间, 即必须使用`if __name__ == "__main__":`

### 2.2.1. 基本流程
1. 创建 ProcessPoolExecutor 对象
    * 直接创建: `pool = concurrent.futures.ProcessPoolExecutor()`
    * 使用上下文管理器 with, 如: `with concurrent.futures.ProcessPoolExecutor() as pool:`
1. 提交多线程 (注意: 提交后会立即执行)
    * 可以使用`.submit`提交不同或相同的多个线程
    * 可以通过列表推导式批量提交, 如`task_list = pool.submit(func, [1,2,3])`
    * 可以通过`.map`批量提交
1. 等待运行结束
    * 方法1: `concurrent.futures.wait(fs, timeout=None, return_when=ALL_COMPLETED)`
        * `return_when`参数控制主线程的阻塞模式: `FIRST_COMPLETED`, `FIRST_EXCEPTION`, `ALL_COMPLETED`
    * 方法2: `concurrent.futures.as_completed(fs, timeout=None)`
        * 任意一个线程完成, 都将返回一次
    * 可以调用`Future`对象的`done()`方法查看某个线程是否结束
1. 处理返回结果【可选】
    * 调用`Future`对象的`result(timeout=None)`方法

* 示例
    ``` python {.line-numbers}
    import concurrent.futures
    import math

    PRIMES = [
        112272535095293,
        112582705942171,
        112272535095293,
        115280095190773,
        115797848077099,
        1099726899285419]

    def is_prime(n):
        if n % 2 == 0:
            return False

        sqrt_n = int(math.floor(math.sqrt(n)))
        for i in range(3, sqrt_n + 1, 2):
            if n % i == 0:
                return False
        return True

    def main():
        with concurrent.futures.ProcessPoolExecutor() as executor:
            for number, prime in zip(PRIMES, executor.map(is_prime, PRIMES)):
                print('%d is prime: %s' % (number, prime))

    if __name__ == '__main__':
        main()
    ```

### 2.2.2. ProcessPoolExecutor 对象
* 构造函数
    * `concurrent.futures.ProcessPoolExecutor(max_workers=None, mp_context=None, initializer=None, initargs=())`
        * max_workers: 最大进程数, 默认为 CPU数量, 最大不超过 61
* 主要方法
    * `submit(fn, *args, **kwargs)`: 提交可调用对象, 返回一个`Future`对象
    * `map(func, *iterables, timeout=None, chunksize=1)`: 批量提交可调用对象, 返回`Future`对象的迭代器
    * `shutdown(wait=True)`: 关闭线程池

### 2.2.3. Future 对象
* 主要方法
    * 控制: `add_done_callback`, `cancel`
    * 运行状态: `running`, `done`, `cancelled`
    * 异常: `exception`

### 2.2.4. Module 函数
* `concurrent.futures.wait(fs, timeout=None, return_when=ALL_COMPLETED)`
* `concurrent.futures.as_completed(fs, timeout=None)`


--------------------------------------------------------------------------------
# 3. 多线程

## 3.1. 基于标准库 threading

### 3.1.1. 基本流程
1. 创建 Thread
1. 运行
1. 等到结束
1. 收集结果【可选】(建议使用派生类实现)

### 3.1.2. 创建线程
* 方法1: 将可调用对象 (如: 函数) 传入Thread类的构造器
    * 示例:
        ``` python {.line-numbers}
        import threading

        def foo(num):
            for i in range(5):
                print(f"Thread {num}: {i}")

        t1 = threading.Thread(target=foo, args=(1,))
        t2 = threading.Thread(target=foo, args=(2,))
        t1.start()
        t2.start()
        t1.join()   # 可选
        t2.join()   # 可选
        """ 输出
        Thread 1: 0
        Thread 1: 1Thread 2: 0

        Thread 2: 1Thread 1: 2
        Thread 1: 3
        Thread 1: 4

        Thread 2: 2
        Thread 2: 3
        Thread 2: 4
        """
        ```
        注意: 程序运行成功, 但字符串输出格式错误, 证明 print 不是线程安全的, 建议使用 logging
* 方法2: 创建一个Thread子类, 并实现`run()`方法
    ``` python
    def foo(n): return n**2

    class MyThread(threading.Thread):
        def __init__(self, a):
            super().__init__(name="foo线程类")  # 参数包括: group, target, name, daemon
            self.a = a

        def run(self):
            self.result = foo(self.a)

        def get_result(self):
            try:
                return self.result
            except Exception:
                return None

    t1 = MyThread(3)
    t2 = MyThread(7)

    t1.start()
    t2.start()
    t1.join()
    t2.join()

    print(t1.get_result())
    print(t2.get_result())
    ```
### 3.1.3. 运行控制
* 守护线程: 主线程结束时, 强制子线程结束
    * 使用`.setDaemon(bool)`方法设置
    * 必须在`.start()` 之前调用, 默认为False
* 线程启动: `.start()`方法
* 等待结束: `.join(timeout=None)`

### 3.1.4. 线程间通信
* 全局变量
    * 多个线程同时读, 需要保护
    * 如果仅一个写, 其余读, 可不加保护
* 消息队列: queue.Queue
    * 常用方法:
        * `put(item, block=True, timeout=None)`
        * `get(block=True, timeout=None)`
        * `join()`
        * `task_done()`
    * 其他类似: queue.LifoQueue, queue.PriorityQueue, queue.SimpleQueue
    * 示例
        ``` python
        import queue

        q = queue.Queue()
        threads = []

        def worker(q):
            while True:
                item = q.get()
                if item is None:
                    break
                do_work(item)
                q.task_done()

        for i in range(num_worker_threads):
            t = threading.Thread(target=worker)
            t.start()
            threads.append(t)

        for item in source():
            q.put(item)

        # block until all tasks are done
        q.join()
        # stop workers
        for i in range(num_worker_threads):
            q.put(None)
        for t in threads:
            t.join()
        ```
### 3.1.5. 线程同步
* 互斥锁: threading.Lock, threading.RLock (可重入)
    * 获取 Lock/RLock 后必须释放
    * Lock在获取一次后必须释放, RLock可以连续获取多次, 但必须释放相同次数
    * ==特别注意==: 防止死锁
        * 例如: A 线程对 a,b 加速, 而 B 线程对 b,a 加锁, 则可能导致死锁
    * 示例
        ``` python
        global_var = 0
        myLock = threading.Lock()
        # myRLock = threading.RLock()

        def thread_func(myLock):
            # myRLock.acquire()
            # myRLock.acquire() # RLock可以连续获取多次
            myLock.acquire()    # 方法原型 acquire(blocking=True, timeout=-1) -> bool
            global_var += 1
            myLock.release()    # 必须释放, 否则会阻塞其他线程
            # myRLock.release()
            # myRLock.release() # 需要释放相同次数

            with myLock:
                global_var += 1
            """上述写法等效于
            myLock.acquire()
            global_var += 1
            myLock.release()
            """
        ```
* 信号量: threading.Semaphore
    * 管理一个计数器
    * 每次调用`.acquire()`, 计数器减1
    * 每次调用`.release()`, 计数器加1
    * 计数器为0时, 阻塞
    * 可以使用上下文管理器
* 条件: threading.Condition
    * 方法: acquire, release, wait, notify, ...
    * 可以使用上下文管理器
    * 示例
        ``` python
        # Consume one item
        with cv:
            while not an_item_is_available():
                cv.wait()   # 阻塞, 等待通知
            get_an_available_item()

        # Produce one item
        with cv:
            make_an_item_available()
            cv.notify()     # 发出通知
        ```
* Event
* Barrier

### 3.1.6. 数据保护
* 线程本地变量
    ``` python {.line-numbers}
    mydata = threading.local()
    mydata.x = 1
    ```
### 3.1.7. 其他
* 定时启动子线程: `threading.Timer(interval, function, args=None, kwargs=None)`

## 3.2. 基于标准库 concurrent.futures

### 3.2.1. 基本流程
1. 创建 ThreadPoolExecutor 对象
    * 直接创建: `pool = concurrent.futures.ThreadPoolExecutor()`
    * 使用上下文管理器 with, 如: `with concurrent.futures.ThreadPoolExecutor() as pool:`
1. 提交多线程 (注意: 提交后会立即执行)
    * 可以使用`.submit`提交不同或相同的多个线程
    * 可以通过列表推导式批量提交, 如`task_list = pool.submit(func, [1,2,3])`
    * 可以通过`.map`批量提交
1. 等待运行结束
    * 方法1: `concurrent.futures.wait(fs, timeout=None, return_when=ALL_COMPLETED)`
        * `return_when`参数控制主线程的阻塞模式: `FIRST_COMPLETED`, `FIRST_EXCEPTION`, `ALL_COMPLETED`
    * 方法2: `concurrent.futures.as_completed(fs, timeout=None)`
        * 任意一个线程完成, 都将返回一次
    * 可以调用`Future`对象的`done()`方法查看某个线程是否结束
1. 处理返回结果【可选】
    * 调用`Future`对象的`result(timeout=None)`方法

* 示例
    ``` python
    import concurrent.futures
    import urllib.request

    URLS = ['http://www.foxnews.com/',
            'http://www.cnn.com/',
            'http://europe.wsj.com/',
            'http://www.bbc.co.uk/',
            'http://some-made-up-domain.com/']

    # Retrieve a single page and report the URL and contents
    def load_url(url, timeout):
        with urllib.request.urlopen(url, timeout=timeout) as conn:
            return conn.read()

    # We can use a with statement to ensure threads are cleaned up promptly
    with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
        # Start the load operations and mark each future with its URL
        future_to_url = {executor.submit(load_url, url, 60): url for url in URLS}
        for future in concurrent.futures.as_completed(future_to_url):
            url = future_to_url[future]
            try:
                data = future.result()
            except Exception as exc:
                print('%r generated an exception: %s' % (url, exc))
            else:
                print('%r page is %d bytes' % (url, len(data)))
    ```

### 3.2.2. ThreadPoolExecutor 对象
* 构造函数
    * `concurrent.futures.ThreadPoolExecutor(max_workers=None, thread_name_prefix='', initializer=None, initargs=())`
* 主要方法
    * `submit(fn, *args, **kwargs)`: 提交可调用对象, 返回一个`Future`对象
    * `map(func, *iterables, timeout=None, chunksize=1)`: 批量提交可调用对象, 返回`Future`对象的迭代器
    * `shutdown(wait=True)`: 关闭线程池

### 3.2.3. Future 对象
* 主要方法
    * 控制: `add_done_callback`, `cancel`
    * 运行状态: `running`, `done`, `cancelled`
    * 异常: `exception`

### 3.2.4. Module 函数
* `concurrent.futures.wait(fs, timeout=None, return_when=ALL_COMPLETED)`
* `concurrent.futures.as_completed(fs, timeout=None)`

--------------------------------------------------------------------------------
# 4. 协程

## 4.1. 基础

* 生成器
    * 生成器: yield, yield from
        * 典型应用: 生产者-消费者循环
            ``` python
            def consumer():
                status = True
                while True:
                    n = yield status
                    print("我拿到了{}!".format(n))
                    if n == 3:
                        status = False

            def producer(consumer):
                n = 5
                while n > 0:
                # yield给主程序返回消费者的状态
                    yield consumer.send(n)
                    n -= 1

            if __name__ == '__main__':
                c = consumer()
                c.send(None)
                p = producer(c)
                for status in p:
                    if status == False:
                        print("我只要3,4,5就行啦")
                        break
                print("程序结束")
            ```
* 事件循环
* 演进
    * 问题: 同步程序处理IO时, 需要等待IO完成, 才能继续, 非常耗时
        * 使用多线程可以解决少并发的问题, 大量并发时, 需要大量线程, 影响性能
    * 希望: 发出IO请求后, 程序可以进行其他任务, IO完成后接着运行IO处理任务
    * 解决方法:
        * 轮询: 发出IO操作后, 不停查询IO执行结果, 查询期间可以进行其他任务
            * 缺点: 效率低, 编程困难
        * 事件循环 + 回调: 事件轮询可以检查多个IO的状态, 哪个好了就执行对应的程序 (通过回调方式)
            * 缺点: 回调函数影响程序维护
        * 协程
## 4.2. 基于标准库 asyncio

### 4.2.1. Python提供了原生的协程支持
* `async`和`await`关键词
    * `async`用于声明协程
    * `await`让出控制权
        * 等效于`yield`或`yield from`
        * 只对`Awaitables`对象 (coroutines, Tasks, Futures) 有用, 对普通函数无效
* 标准库 asyncio
    * 具有特定系统实现的事件循环 (event loop)
    * 数据通讯和协议抽象 (类似Twisted中的部分)
    * TCP, UDP, SSL, 子进程管道, 延迟调用和其他
    * Future类
    * yield from的支持
    * 同步的支持
    * 提供向线程池转移作业的接口


### 4.2.2. 简单示例
* 示例
    ``` python
    import asyncio

    async def compute(x, y):        # 声明为协程
        print(f"Compute {x} + {y} ...")
        await asyncio.sleep(1.0)    # 让出控制权
        return x + y

    async def print_sum(x, y):          # 声明为协程
        result = await compute(x, y)    # 让出控制权, 等compute完成
        print(f"{x} + {y} = {result}")

    asyncio.run(print_sum(1, 2))    # 创建事件循环, 运行协程, 完成后关闭事件循环
    ''' 与下列代码功能相同
    loop = asyncio.get_event_loop()             # 创建事件循环
    loop.run_until_complete(print_sum(1, 2))    # 等待协程完成
    loop.close()                                # 关闭事件循环
    '''
    ```
* 调用过程
![协程示例1](/assets/协程示例1.png)

### 4.2.3. 基础
* 事件循环
    * `asyncio`库的核心, 运行异步任务和回调, 运行网络IO, 运行子进程
    * `asyncio`库的底层, 用户应尽量调用高层接口
    * 主要方法:
        * 获取事件循环
            * `asyncio.get_running_loop()`
            * `asyncio.get_event_loop()`
            * `asyncio.set_event_loop(loop)`
            * `asyncio.new_event_loop()`
        * 启动和停止
            * `loop.run_until_complete(future)`
            * `loop.run_forever()`
            * `loop.is_running()`
            * `loop.stop()`
            * `loop.close()`
            * `loop.is_closed()`
            * `coroutine loop.shutdown_asyncgens()`
        * 调度回调、延迟的回调
        * 创建 Futures 和 Tasks
        * 打开网络连接, 创建网络服务器
        * 传说文件
        * TLS Upgrade
        * 监视文件描述符
        * Working with socket objects directly
        * DNS
        * Working with pipes
        * Unix signals
        * Executing code in thread or process pools
        * Error Handling API
        * Enabling debug mode
        * Running Subprocesses
* asyncio.Future
    * 本质是一个回调管理器
    <!-- * 主要方法:
        * `result()`
        * `set_result(result)`
        * `done()`
        * `add_done_callback(callback, *, context=None)`
        * `remove_done_callback(callback)`
        * `cancel()`
        * `cancelled()`
        * `exception()`
        * `set_exception(exception)`
        * `get_loop()` -->
* asyncio.Task
    * Future的派生类
    * 主要方法:
        * `result()`
        * `done()`
        * `add_done_callback(callback, *, context=None)`
        * `remove_done_callback(callback)`
        * `cancel()`
        * `cancelled()`
        * `exception()`
        * `get_loop()`
        * `get_stack(*, limit=None)`
        * `print_stack(*, limit=None, file=None)`
        * `classmethod all_tasks(loop=None)`
        * `classmethod current_task(loop=None)`

### 4.2.4. 创建协程
* 用`async def`声明程序
    * 等效于`@asyncio.coroutine`装饰器

### 4.2.5. 运行控制
1. 声明协程
    * 动态创建: `asyncio.create_task(coro)`
        * 返回Task对象
        * 参数coro也可以是普通函数
2. 调度任务【可选】
    * `asyncio.create_task(coro, *, debug=False)`【推荐】
        * 创建一个 Task, 返回 Task 对象
    * `await asyncio.gather(*aws, loop=None, return_exceptions=False)`【推荐】
        * 调度并等待多个任务完成
        * 注意: 如果 tasks 是列表, 需要使用 `* 变量` 解包
    * `await asyncio.wait_for()`
        * 调度并等待一个任务完成, 或超时退出
        * 如果超时, 抛出异`TimeoutError`异常
        * 如果超时, 执行 cancel, 协程退出
        * 为防止协程从 cancellation 退出, 可使用 `await asyncio.shield()`
    * `await asyncio.wait()` 调度并等待多个任务完成 (可选退出模式) , 或超时退出
        * 如果超时, 抛出异`TimeoutError`异常
        * 退出模式: FIRST_COMPLETED, FIRST_EXCEPTION, ALL_COMPLETED
    * `for i in asyncio.as_completed(...)`
        * 调度并等待多个任务完成
    * 示例
        ``` python
        async def func(name, x):
            print(f"Task {name} start")
            await asyncio.sleep(1)
            print(f"Task {name}: get result")
            return {name: x + x**2}

        # result =  asyncio.run(func("A",2))
        # print(f"result = {result}")

        async def main():
            # # 方式1: create_task
            # _r = await asyncio.create_task(func("A", 2))

            # # 方式2.1: gather
            # _r = await asyncio.gather(func("A", 2),
            #                           func("B", 3),
            #                           func("C", 4)
            #                           )

            # # 方式2.2: gather
            tasks = [func("A", 2),
                     func("B", 3),
                     func("C", 4)]
            _r = await asyncio.gather(*tasks)

            # # 方式3: wait_for
            # _r = await asyncio.wait_for(func("A", 2), 10)

            # # 方式4: wait
            # task_done, _ = await asyncio.wait([func("A", 2),
            #                                    func("B", 3),
            #                                    func("C", 4)
            #                                    ])
            # _r = []
            # for t in task_done:
            #     _r.append(t.result())

            # # 方式5: as_completed
            # tasks = [asyncio.create_task(func(name, x))
            #          for name, x in zip("ABC", [2, 3, 4])]
            # _r = []
            # for t in asyncio.as_completed(tasks):
            #     b = await t
            #     _r.append(b)

            # 返回值
            return _r

        result = asyncio.run(main())
        print(f"result = {result}")
        ```
3. 启动任务:
    * `asyncio.run(coro, *, debug=False) `
        * 基本等效于
            ``` python
            loop = asyncio.get_event_loop()
            loop.run_until_complete(coro)
            loop.close()
            ```
        * 不是进程安全的
    * 从其他线程调度: `asyncio.run_coroutine_threadsafe(coro, loop)`
        * 进程安全的

* 其他
    * 查看当前任务: `asyncio.current_task(...)`
    * 查看所有任务: `asyncio.all_tasks(...)`

### 4.2.6. 协程同步
* `asyncio.Lock`
* `asyncio.Semaphore`
    * `asyncio.BoundedSemaphore`
* `asyncio.Condition`
* `asyncio.Event`

### 4.2.7. 协程通信
* `asyncio.Queue`
    * `asyncio.PriorityQueue`
    * `asyncio.LifoQueue`

### 4.2.8. 其他
* 延时: `asyncio.sleep(delay, result=None, *, loop=None)`

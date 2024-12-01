# 异常与async

异常会让整个async程序宕机，如下面的代码：
```python
# 设置让延迟为2的task抛出异常

import asyncio

async def task(delay : int) -> None:
    await asyncio.sleep(delay);
    if (delay == 2):
        raise Exception("task.raise.exception")
    else:
        print("task.delay:", delay)

async def main():
    await asyncio.gather(
            task(1),
            task(2),
            task(3))

asyncio.run(main())
```
运行结果如下
```bash
task.delay: 1
Traceback (most recent call last):
  File "raise_exception.py", line 18, in <module>
    asyncio.run(main())
  File "/home/thuang/miniconda3/envs/web/lib/python3.8/asyncio/runners.py", line 44, in run
    return loop.run_until_complete(main)
  File "/home/thuang/miniconda3/envs/web/lib/python3.8/asyncio/base_events.py", line 616, in run_until_complete
    return future.result()
  File "raise_exception.py", line 13, in main
    await asyncio.gather(
  File "raise_exception.py", line 8, in task
    raise Exception("task.raise.exception")
Exception: task.raise.exception
```
可以看到"task.day: 3"并没有打印出来。

因此编写异步程序时一定要非常小心异常。

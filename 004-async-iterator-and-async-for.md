# 异步迭代器与async for

```python
import asyncio

class AsyncCounter:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __aiter__(self):
        return self

    async def __anext__(self):
        if self.current >= self.end:
            raise StopAsyncIteration
        await asyncio.sleep(1)
        self.current += 1
        return self.current - 1

async def main():
    async for num in AsyncCounter(1,5):
        print(num)

asyncio.run(main())
```

# 异常与Sanic

之前提到过异常会导致整个异步程序宕机，那么如果在Sanic的请求处理逻辑中抛出异常，程序会宕掉吗？

编写如下测试代码：
```python
from sanic import Sanic
from sanic.response import text

app = Sanic("MyHelloWorldApp")

@app.get("/")
async def hello_world(request):
    raise Exception("hello_world.exception")
    return text(str(result))
```

然后执行
```bash
curl http://127.0.0.1:8000/
```
会返回结果：
```bash
⚠️ 500 — Internal Server Error
==============================
The application encountered an unexpected error and could not continue.
```
而且处理这个请求的进程不会宕掉。

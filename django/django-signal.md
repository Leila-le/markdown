```python
class MySignalReceiver:
    @staticmethod
    @receiver(post_save, sender=Customer)
    def Customer_post_save_handler(sender, instance, created, **kwargs):
        # 接收额外关键字参数
        print(kwargs)  # 可以查看传递的额外参数
        if created:
            print("A new instance of Customer was created.")
        else:
            print("An existing instance of Customer was updated.")

    @staticmethod
    @receiver(post_save, sender=Contract)
    def Contract_post_save_handler(sender, instance, created, **kwargs):
        if created:
            print("A new instance of Model2 was created.")
        else:
            print("An existing instance of Model2 was updated.")

    @staticmethod
    @receiver(post_save, sender=Customer)
    def Customer_pre_delete_handler(sender, instance, **kwargs):
        print("Deleting instance of MyModel:", instance)

    @staticmethod
    @receiver(post_save, sender=Visitation)
    def Visitation_post_save_handler(sender, instance, created, **kwargs):
        if created:
            print("A new instance of Model2 was created.")
        else:
            print("An existing instance of Model2 was updated.")

    @staticmethod
    @receiver(post_save, sender=Visitation)
    def Visitation_pre_delete_handler(sender, instance, **kwargs):
        print("Deleting instance of MyModel:", instance)

```
# 使用中间件获取当前用户：

在utils.py中
```Python
import threading
thread_local = threading.local()
```
在middleware.py中

```Python
from utils import thread_local

class CurrentUserMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        # 将当前用户存储在线程本地存储对象中
        thread_local.current_user = request.user
        response = self.get_response(request)
        # 清除线程本地存储中的用户信息
        del thread_local.current_user

        return response
```
在model.py（我是将信号处理放到了model.py中，所以在model.py）
```python
from utils import thread_local
current_user = getattr(thread_local, 'current_user', None)
```

在settings.py中的中间件添加
``` Python
'middlewares.CurrentUserMiddleware',
```

注意点：'current_user'要和thread_local.current_user对应。

# 使用inspect获取当前用户：
在要获取当前用户的函数中使用：
```Python
request = next((frame[0].f_locals['request'] for frame in inspect.stack() if frame[3] == 'get_response'), None)
current_user=request.user
```

注意：监听pre_save和post_save信号的回调函数不能再调用save()方法，否则回出现死循环。
    另外Django的update方法不会发出pre_save和post_save的信号。

    page=3,pagesize=4,pre_page=2
    pagesize%page

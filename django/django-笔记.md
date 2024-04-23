# static的路径设置疑问:

    STATIC_URL = 'static/'
    STATIC_ROOT = BASE_DIR / 'shortman/static'
    STATICFILES_DIRS = [BASE_DIR / 'static']
    分别是什么情况

    这里的配置做了以下事情：

    STATIC_URL 设置为 'static/'，意味着静态文件的 URL 前缀将以 static/ 开头。
    STATIC_ROOT 设置为 BASE_DIR / 'shortman/static'，即将静态文件收集到项目中的 shortman/static 目录中。
    STATICFILES_DIRS 设置为 [BASE_DIR / 'static']，即在项目的根目录下的 static 目录中查找静态文件。
这样的设置允许你在项目中的模板或代码中引用静态文件，并在运行 collectstatic 命令时将这些文件从 STATICFILES_DIRS 中的目录复制到 STATIC_ROOT 目录中，以供在生产环境中提供静态文件服务.

Django 项目的设置文件（通常是 settings.py）中，STATIC_URL、STATIC_ROOT 和 STATICFILES_DIRS 是与静态文件相关的设置。

   - STATIC_URL 设置了静态文件的基本 URL。它定义了在模板或代码中引用静态文件时使用的 URL 前缀。例如，如果 STATIC_URL 设置为 'static/'，那么在模板中引用静态文件时，可以使用类似于 {{ STATIC_URL }}css/style.css 的路径。

   - STATIC_ROOT 是用于收集静态文件的根目录。当你运行 collectstatic 命令时，Django 将从所有已安装的应用和 STATICFILES_DIRS 中收集静态文件，并将它们复制到 STATIC_ROOT 目录中。这个目录通常是你的项目文件结构中的一个具体位置。

   - STATICFILES_DIRS 是一个包含用于查找静态文件的目录列表。它可以包含你的项目中的任何其他目录。当你运行 collectstatic 命令时，Django 会在这些目录中查找静态文件，并将其复制到 STATIC_ROOT 目录中。

**在测试环境中，通常不需要设置 STATIC_ROOT。STATIC_ROOT 是用于收集静态文件并在生产环境中提供静态文件服务的目录。**

生产环境的时候,一般情况下是只有`STATIC_URL`和`STATIC_ROOT`,但是如果还有其他静态文件目录,可能需要设置`STATICFILES_DIRS`并将这些目录添加到列表中.

总结起来，在生产环境中，你需要设置以下静态文件相关的设置：

    STATIC_URL：静态文件的基本 URL。
    STATIC_ROOT：用于收集静态文件的根目录。
    STATICFILES_DIRS：包含其他静态文件目录的列表（可选，如果有额外的静态文件目录）。

# @api_view(["POST"])的作用
表示在其下面的对应的函数只能在POST请求的情况下使用

# 关于CSRF:
疑问:在Django设置中启用CSRF保护：确保在Django的设置文件（settings.py）中启用了CSRF保护。确认以下设置已配置为以下值不是只要在MIDELWARE中添加'django.middleware.csrf.CsrfViewMiddleware',就可以了吗,为什么要

    CSRF_COOKIE_SECURE = True # 仅在HTTPS连接中使用CSRF cookie
    CSRF_COOKIE_HTTPONLY = True # 限制通过JavaScript访问CSRF cookie
    CSRF_USE_SESSIONS = True # 将CSRF令牌存储在会话中而不是cookie中
解答:在Django的设置文件中，启用CSRF保护需要确保添加'django.middleware.csrf.CsrfViewMiddleware'到MIDDLEWARE设置中。这个中间件是用于处理CSRF保护的关键组件，它负责验证和处理CSRF令牌。

至于其他设置项的说明如下：

    CSRF_COOKIE_SECURE = True：将CSRF cookie标记为仅在HTTPS连接中使用。这意味着浏览器只会在使用HTTPS协议（安全连接）时发送CSRF cookie，防止在非安全连接中进行CSRF攻击。

    CSRF_COOKIE_HTTPONLY = True：限制通过JavaScript访问CSRF cookie。将此设置为True可以防止通过客户端的脚本代码访问CSRF cookie，提高安全性。

    CSRF_USE_SESSIONS = True：将CSRF令牌存储在会话中而不是cookie中。默认情况下，Django将CSRF令牌存储在cookie中，但在某些情况下，存储在会话中可能更安全。这样，CSRF令牌不会在浏览器的cookie中可见，减少了被恶意脚本获取的风险。

这些设置项的目的是增强CSRF保护，并提高应用程序的安全性。通过配置这些设置，你可以根据你的应用程序需求和安全级别来决定是否启用HTTPS连接、限制JavaScript访问CSRF cookie以及选择存储CSRF令牌的位置。

## 禁用csrf验证
class CsrfExemptSessionAuthentication(SessionAuthentication):
    def enforce_csrf(self, request):
        return


如果你的视图没有渲染包含 csrf_token 模板标签的模板，Django 可能不会设置 CSRF 令牌 cookie。这种情况常见于表单被动态添加到页面的情况。针对这种情况，Django 提供了一个视图装饰器来强制设置 cookie： sure_csrf_cookie()。

# http的各种请求

### 1. head

    获取资源的元数据：通过发送HEAD请求，可以获取与特定资源相关的元数据信息，如文件大小、最后修改时间、内容类型等。这对于某些情况下只需要资源的元数据而不需要完整内容的场景非常有用。

    验证资源的存在：通过发送HEAD请求，可以验证特定资源是否存在，而无需下载整个资源内容。如果服务器返回200状态码，表示资源存在；如果返回404状态码，表示资源不存在。

    检查资源的更新状态：通过HEAD请求，可以检查资源是否已更改，而无需获取完整的响应内容。通过比较Last-Modified或ETag等响应头字段的值，可以确定资源的更新状态，并决定是否需要重新下载资源。

    获取响应的头信息：HEAD请求返回的响应中只包含响应头信息，不包含响应体。这对于仅需要获取响应头部分的应用程序有用，可以节省带宽和处理时间。

# 关于不同版本版本的库间的问题:
django在4.0+废弃掉dajngo.conf.urls.url(),所以可以使用`from django.urls import re_path as url`代替`from django.urls import url`

解决403错误:https://www.hostinger.com/tutorials/what-is-403-forbidden-error-and-how-to-fix-it#What_Is_the_403_Forbidden_Error


### Django DRF序列化器
序列化器的作用是将模型实例(比如用户、文章)序列化和反序列化为诸如json之类的表示形式。一个模型实例可能有许多字段属性，但一般情况下你不需要把所有字段信息以JSON格式数据返回给用户。**序列化器定义了需要对一个模型实例的哪些字段进行序列化/反序列化, 并可对客户端发送过来的数据进行验证和存储。**

使用了DRF提供的@api_view这个非常重要的装饰器，实现了以下几大功能：

    与Django传统函数视图相区分，强调这是API视图，并限定了可以接受的请求方法。
    拓展了django原来的request对象。新的request对象不仅仅支持request.POST提交的数据，还支持其它请求方式如PUT或PATCH等方式提交的数据，所有的数据都在request.data字典里。这对开发Web API非常有用。
```
request.POST  # 只处理表单数据, 只适用于'POST'方法
request.data  # 处理任意数据, 适用于'POST'，'PUT'和'PATCH'方法
```

  注意: 我们不再显式地将请求或响应绑定到特定的内容类型比如`HttpResponse`和`JSONResponse`，我们统一使用`Response`方法返回响应，该方法支持内容协商，可根据客户端请求的内容类型返回不同的响应数据。    


```python
def get_queryset(self):
  ```
  的作用一般是用于选择数据库中的数据



# django内外网访问同一个地址连接不同页面

在Django中实现内外网访问同一个地址但连接到不同页面，你可以使用Django的路由和视图来进行处理。

下面是一个示例，展示了如何在Django中实现内外网访问同一个地址连接到不同页面：

    首先，在你的项目的urls.py文件中定义路由规则：

```python

from django.urls import path
from . import views

urlpatterns = [
    path('my-page/', views.my_page, name='my_page'),
]

    接下来，在你的应用的views.py文件中定义视图函数：

python

from django.shortcuts import render

def my_page(request):
    if is_internal_network(request):
        # 在内网，渲染内网页面
        return render(request, 'internal_page.html')
    else:
        # 在外网，渲染外网页面
        return render(request, 'external_page.html')
```
    在templates目录下创建internal_page.html和external_page.html模板文件，分别包含内网和外网页面的内容。

在上述代码中，我们假设存在一个名为is_internal_network(request)的函数来判断用户是否在内网。根据这个判断，我们在my_page视图中渲染不同的页面模板。

通过这种方式，当用户访问/my-page/地址时，Django会根据内外网的不同，渲染并返回相应的页面模板。

请注意，is_internal_network(request)函数的实现取决于你的具体环境和要求。你可以根据你的内外网判断逻辑来实现该函数，例如通过检查请求的IP地址或其他标识来判断用户所处的网络环境。

# 缓存方式选择：
1. 站点缓存
```python
MIDDLEWARE = [
    "django.middleware.cache.UpdateCacheMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.cache.FetchFromCacheMiddleware",
]
```
     虽然最简便，但是不适用于视图的结果依赖于许多费时查询，要随着时间变化而变化的情况下。

2. 底层缓存API：
    * 访问缓存：重复请求同一个线程里的同一个别名将返回同一个对象。
      ```Python
      >>> from django.core.cache import caches
      >>> cache1 = caches['myalias']
      >>> cache2 = caches['myalias']
      >>> cache1 is cache2
      True
      ```
    * 缓存键前缀：当一个特殊的缓存键被保存或检索时，Django 会为缓存键自动添加 KEY_PREFIX 缓存设置的前缀值。
    * 缓存版本控制：Django 提供更好的方式来指向单个缓存值。Django 缓存框架有一个系统范围的版本标识，需要在 VERSION 缓存配置中指定。这个配置的值将自动与缓存前缀和用户提供的缓存键组合起来获取最终的缓存键。`默认情况下，任何键请求都会自动包含站点默认的缓存键版本。但是，原始缓存函数都包括一个 version 参数，因此您可以指定要设置或获取的特定缓存键版本`。例如：
      ```Python
      >>> # Set version 2 of a cache key
      >>> cache.set("my_key", "hello world!", version=2)
      >>> # Get the default version (assuming version=1)
      >>> cache.get("my_key")
      None
      >>> # Get version 2 of the same key
      >>> cache.get("my_key", version=2)
      'hello world!'
      ```
      可以使用 `incr_version()` 和 `decr_version()` 方法递增和递减特定键的版本。这使得可以将特定键提升到新版本，而不影响其他键。继续我们之前的示例：
      ```python
      >>> # Increment the version of 'my_key'
      >>> cache.incr_version("my_key")
      >>> # The default version still isn't available
      >>> cache.get("my_key")
      None
      # Version 2 isn't available, either
      >>> cache.get("my_key", version=2)
      None
      >>> # But version 3 *is* available
      >>> cache.get("my_key", version=3)
      'hello world!'
      ```
    * 缓存键转换
    * 缓存键警告

3. 模板片段缓存
4. 视图缓存

  # 中间件顺序
  如果使用缓存中间件，重要的是将每一半放在 MIDDLEWARE 设置的正确位置。这是因为缓存中间件需要知道哪些头可以改变缓存存储。中间件总是可以在 Vary 响应头中添加一些东西。

UpdateCacheMiddleware 在响应阶段运行，其中中间件以相反的顺序运行，因此列表顶部的项目在响应阶段的*最后*运行。因此，您需要确保 UpdateCacheMiddleware 出现在任何其他可能添加到 Vary 标头的其他中间件*之前*。下面的中间件模块类似：

    - SessionMiddleware 添加 Cookie
    - GZipMiddleware 添加 Accept-Encoding
    - LocaleMiddleware 添加 Accept-Language

另一方面，FetchFromCacheMiddleware 在请求阶段运行，从头到尾应用中间件，因此列表顶部的条目首先在请求阶段运行。在其他中间件更新 Vary 头部后，FetchFromCacheMiddleware 也需要运行，因此 FetchFromCacheMiddleware 必须在任何条目之后运行。


# 使用其他标头控制高速缓存
缓存的其他问题是数据的隐私和数据应该存储在缓存的级联中的问题。
这对于敏感数据带来了问题——您不希望例如，您的银行账号号码存储在公共缓存中。因此，Web 应用程序需要一种方法来告诉缓存哪些数据是私有的，哪些是公共的。

解决方案是指出一个页面的缓存应该是“私有的”。在 Django中，使用 cache_control() 。例子：
```python
from django.views.decorators.cache import cache_control


@cache_control(private=True)
def my_view(request):
    ...
```
注意，缓存控制设置“私有”和“公共”是互斥的。装饰器确保“公共”指令被移除，如果应该设置“私有”（反之亦然）。这两个指令的一个示例使用将是一个提供私人和公共条目的博客站点。公共条目可以缓存在任何共享缓存上。下面的代码使用 patch_cache_control()，手动修改缓存控制头的方法（内部调用的是 cache_control() 装饰器）：
```Python
from django.views.decorators.cache import patch_cache_control
from django.views.decorators.vary import vary_on_cookie


@vary_on_cookie
def list_blog_entries_view(request):
    if request.user.is_anonymous:
        response = render_only_public_entries()
        patch_cache_control(response, public=True)
    else:
        response = render_private_and_public_entries(request.user)
        patch_cache_control(response, private=True)

    return response
```
即使您不使用 Django 的服务器端缓存框架，您仍然可以使用 max-age 指令告诉客户端在一定时间内缓存一个视图：
```python
from django.views.decorators.cache import cache_control


@cache_control(max_age=3600)
def my_view(request):
    ...
```
（如果你使用缓存中间件，它已经使用 CACHE_MIDDLEWARE_SECONDS 设置的值设置了 max-age 。在这个例子里，cache_control() 装饰器里自定义的 max_age 将被优先使用，头值将被正确合并。）

任何有效的 Cache-Control 响应指令在 cache_control() 中是有效的。这里有很多例子：

    no_transform=True
    must_revalidate=True
    stale_while_revalidate=num_seconds
    no_cache=True

已知指令的列表在 IANA registry 都能被找到（注意不是所有的都适用于响应）。

如果你想使用头部来完全禁用缓存，never_cache() 是一个视图装饰器，用来添加头部确保响应不被浏览器或其他缓存进行缓存。比如：
```python
from django.views.decorators.cache import never_cache


@never_cache
def myview(request):
    ...
```




    ref="oldPassword"：这是普通的 HTML 属性语法，表示将 oldPassword 作为 ref 属性的值。这可能是为了将 oldPassword 作为引用传递给 JavaScript 或其他前端框架的某些逻辑。

    :ref="oldPassword"：这是 Vue.js 框架中的属性绑定语法，使用冒号 : 表示动态绑定属性。在这种情况下，oldPassword 可能是 Vue 组件中的一个响应式数据属性，并且通过动态绑定将其值绑定到 ref 属性。


# django中的命名格式：
1. 在model中的字段名称一般例如：foo_bar,而不是骆驼命名格式。

# django中的技巧
1. 对于一个字段要每天变化，例如每天变化+1,便不适合写成数据库字段，可以使用@property进行处理。
2. 一般来说，restful api接口里面的get请求（例如get(),list())这些方法是不允许修改model的，即要遵循restful的幂等，要保持每次请求结果是一致的。

```
restful的幂等

在 RESTful 架构中，幂等是指对同一资源的多次请求具有相同的结果，不会导致资源状态的变化。换句话说，如果对同一资源进行多次相同的操作，无论执行多少次，结果都应该是相同的，并且不会对资源产生副作用。

幂等性是 RESTful 设计的一个重要原则，具有以下特点：

    相同的请求重复执行：无论对同一资源的请求执行多少次，结果都应该是一致的。
    不会产生副作用：执行一次或多次请求对资源的状态不会产生变化。
    安全性：幂等操作不会对服务器端数据产生破坏性的影响。

幂等性对于设计和实现 RESTful API 非常重要，确保在网络通信中的各种情况下，如网络错误、请求超时、重试等，都能保证请求的安全性和可靠性。

以下是一些常见的示例，说明了幂等性的概念：

    GET 请求：获取资源的操作是幂等的，多次执行 GET 请求应该返回相同的资源表示。
    PUT 请求：更新资源的操作是幂等的，多次执行相同的 PUT 请求应该对资源进行相同的更新，不会产生额外的副作用。
    DELETE 请求：删除资源的操作是幂等的，多次执行相同的 DELETE 请求应该返回相同的结果，即资源不存在。

需要注意的是，POST 请求通常不被认为是幂等的，因为多次执行相同的 POST 请求可能会导致重复创建相同的资源。

在设计 RESTful API 时，应该尽量遵循幂等性原则，确保 API 的行为符合预期，并且在多次执行相同请求时不会产生意外的结果。


```

# django REST Framework中的序列化和反序列化的作用：
   在Django REST Framework中，序列化（serialization）是将模型对象转换为可传输或存储的数据格式，例如JSON或XML。而反序列化（deserialization）则是将接收到的数据转换回模型对象的过程。

   在序列化器中，你可以定义字段和验证规则，以指定如何从请求数据中提取值并将其转换为模型对象。当你调用序列化器的 save() 或 create() 方法时，就会执行反序列化操作，将请求数据转换为模型对象，并进行验证和保存。
   总结来说，反序列化是将接收到的数据转换为模型对象的过程，允许你在处理请求数据时进行验证、转换和存储.


   在 VisitationSerializer 类下直接创建的字段，默认情况下是可读写的字段。但是，你可以通过不同的选项来控制字段的读写行为。

以下是一些常见选项：

    read_only: 设置为 True 以将字段设置为只读。只读字段只会在序列化输出时显示，而在反序列化输入时被忽略。


field_name = serializers.CharField(read_only=True)

    write_only: 设置为 True 以将字段设置为只写。只写字段只会在反序列化输入时使用，而在序列化输出时被忽略。


field_name = serializers.CharField(write_only=True)

    read_only_fields: 如果你希望将多个字段设置为只读，你可以将它们添加到 read_only_fields 列表中。


class VisitationSerializer(serializers.ModelSerializer):
    field1 = serializers.CharField()
    field2 = serializers.CharField()

    class Meta:
        model = Visitation
        fields = ['field1', 'field2']
        read_only_fields = ['field2']

在上述代码中，field1 是一个可读写字段，而 field2 是一个只读字段。

需要注意的是，如果你在序列化器中定义了一个模型字段（例如，customer_name = models.CharField(max_length=100)），那么该字段将具有默认的读写行为，即可读写。

总结起来，通过在序列化器中直接创建字段，它们默认是可读写的。如果你希望某个字段只读或只写，可以使用相应的选项进行设置。

# 协程和并发
协程和并发是两个相关但不完全相同的概念。它们都涉及到在程序中同时执行多个任务，但是在实现和工作方式上有一些区别。

并发是指程序的多个部分在同一时间段内同时运行。在并发编程中，多个任务可以在同一时刻被启动和执行，**但并不一定是同时执行**。操作系统或编程语言的调度器会在任务之间切换执行，以实现并发。并发编程可以利用多核处理器的优势，提高程序的执行效率。

协程（Coroutine）是一种轻量级的线程，也被称为用户级线程或纤程。**协程是一种协作式的并发模型**，其中多个协程共享同一个线程，并通过协作的方式进行任务切换。与传统的线程或进程相比，协程的切换开销更小，因为它们不需要进行内核级的上下文切换。协程可以在代码中显式地定义切换点，以便在适当的时候进行切换。

协程和并发之间的关系是，协程可以用于实现并发编程。在使用协程的编程模型中，程序可以通过协作的方式在单个线程中同时执行多个任务。当一个任务需要等待某个事件或操作完成时，它可以暂时挂起，并让其他任务执行。这种方式可以有效地利用计算资源，并简化了并发编程的复杂性。

在一些编程语言中，如Python的asyncio库和Go语言的goroutine，协程得到了内置的支持。这些语言提供了特定的语法和工具，使得编写和管理协程更加方便。协程的使用可以简化并发编程的逻辑，提高程序的可读性和可维护性。

总结来说，协程和并发都是为了实现多任务同时执行的目的，但协程更加轻量级和高效，可以用于实现并发编程，并且可以简化编程模型。


# cpu资源限制
如果你的服务器只有一颗核心的 CPU，并且持续接收 URL 请求并将数据存储到数据库中，可能会遇到以下一些问题：

    性能瓶颈：单核 CPU 的处理能力有限，当持续接收大量请求时，可能会导致性能瓶颈。这可能会导致请求处理时间延长，响应变慢或请求丢失。你可以考虑升级服务器硬件，使用多核 CPU 或增加服务器数量来提高处理能力。

    数据库连接池：当持续接收请求并将数据存储到数据库时，数据库连接管理非常重要。频繁地打开和关闭数据库连接可能会导致性能下降。你可以考虑使用连接池技术，如连接池库或数据库连接池功能来管理数据库连接，以减少连接的开销。

    并发处理：如果服务器处理请求的速度比请求到达的速度慢，可能会导致请求排队等待处理。你可以考虑使用异步处理或多线程/多进程技术来实现并发处理，以提高请求的处理速度。

    数据库优化：频繁的数据库写操作可能会导致性能下降。你可以考虑使用批量插入或事务来优化数据库写入操作，减少每个请求的数据库交互次数。

    监测和调优：定期监测服务器性能参数，如 CPU 使用率、内存占用、数据库连接数等，并进行调优。根据监测结果，优化代码、调整服务器配置或进行硬件升级等。


## 数据压缩传输给前端
使用django REST FRAMEWORK后只需要在中间件中添加'django.middleware.gzip.GZipMiddleware',使用其要注意放置位置'django.middleware.security.SecurityMiddleware',
    'django.middleware.gzip.GZipMiddleware',...
    一般来说，GZipMiddleware 需要在中间件列表的较早位置，这样它可以在其他中间件处理响应之前对响应进行压缩。

    响应类型：GZipMiddleware 默认仅对指定的 MIME 类型进行压缩，例如 text/html、text/plain、text/css、application/javascript 等。如果你希望对其他类型的响应进行压缩，可以通过 GZipMiddleware 的 GZIP_CONTENT_TYPES 设置进行配置


## 自定义模板后要在前端显示media中的头像
在前端使用{{ MEDIA_URL }}需要在settings.py的template的配置中添加：'django.template.context_processors.media',
如同：
``` python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
                'django.template.context_processors.media',
            ],
        },
    },
]
```

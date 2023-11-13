### 1. @api_view(["POST"])
@api_view(["POST"])装饰器被应用于一个函数视图，该视图函数可以处理 HTTP POST 请求。这意味着该函数视图只会在收到 POST 请求时被执行，而对于其他 HTTP 请求方法（如 GET、PUT、DELETE 等），将会返回 "405 Method Not Allowed" 响应。

### 2. @staticmethod
用于将一个方法定义为类的静态方法。
在 Python 中，静态方法是属于类的方法，与实例无关，并且可以直接通过类名来调用，而不需要创建类的实例。静态方法通常用于执行与类相关的操作，但不需要访问类的实例或实例属性。

### 3. 变量类型声明
```python
class CrmViewMixin:
    @staticmethod
    def perform_authentication(request):
        if not request.user.is_authenticated:
            raise Http401()

    @staticmethod
    def check_customer(user: RichMan, customer: Customer):
        if user.role in (CrmRole.Admin.value, CrmRole.Engineer.value, CrmRole.Programmer.value):
            return
        else:
            if user.username not in customer.responsibles:
                raise Http404()
```
其中user: RichMan表示user的类型为RichMan,customer: Customer同理.

### 4. @classmethod 
是一个装饰器，用于将一个方法定义为类方法。
类方法是属于类的方法，而不是类的实例。类方法可以直接通过类名来调用，而不需要创建类的实例。类方法通常用于执行与类相关的操作，但不需要访问实例属性或方法。
```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1, arg2):
        # 在类方法中的逻辑
        pass

# 调用类方法，无需创建类的实例
MyClass.my_class_method(arg1, arg2)
```
与普通方法不同，类方法的第一个参数被约定为 cls，它表示类本身，而不是实例。通过 cls 参数，类方法可以访问类的属性和其他类方法。

### 5. class Meta
元数据类 Meta 用于定义序列化器的行为和属性。通过在 Meta 类中指定各种选项，可以影响序列化器的字段、模型、验证规则等方面。

以下是 class Meta 的一些常见选项及其作用：

    model: 指定该序列化器所关联的模型类，即 Customer 模型。序列化器将使用该模型类来执行序列化和反序列化操作。

    fields: 指定要包含在序列化器中的字段列表。只有指定的字段才会被序列化和反序列化。可以是模型字段的名称或序列化器自定义的字段。

    exclude: 指定要排除在序列化器中的字段列表。在序列化和反序列化过程中，这些字段将被忽略。

    read_only_fields: 指定只读字段的列表。这些字段只会在序列化输出中显示，而在反序列化时会被忽略。

    write_only_fields: 指定只写字段的列表。这些字段只会在反序列化时使用，而在序列化输出中不会显示。

    validators: 指定要应用于该序列化器的验证器列表。验证器可以用于对序列化和反序列化的数据进行验证。

    extra_kwargs: 指定对特定字段应用的额外选项。可以用于自定义字段的行为，如指定字段的显示名称、验证规则、输入格式等。

    其他选项：list_serializer_class、depth、ordering 等。这些选项用于进一步配置序列化器的行为。

通过使用 class Meta，可以在序列化器中定义和配置各种选项，以便根据需要进行定制化的序列化和反序列化操作。

### 6. def get_queryset(self) -> List[Contract]
get_queryset 方法位于一个类中，并且返回一个类型为 List[Contract] 的查询集对象。
根据方法的命名和返回类型注释，可以推断该方法是用于获取 Contract 类的查询集。

List[Contract] 表示一个包含 Contract 对象的列表。Contract 可能是一个 Django 模型类，表示与合同相关的数据。

通常，get_queryset 方法用于在视图类中定义数据查询的逻辑。它可以通过对模型进行过滤、排序、关联等操作，返回符合特定条件的对象列表。
```python
from typing import List
from django.views import View
from myapp.models import Contract

class ContractListView(View):
    def get_queryset(self) -> List[Contract]:
        # 执行查询逻辑，返回符合条件的 Contract 对象列表
        queryset = Contract.objects.filter(status='active')
        return queryset
```
在上述示例中，ContractListView 是一个继承自 Django 的基本视图类 View 的自定义视图。get_queryset 方法被重写，并根据特定条件（例如合同状态为'active'）过滤并返回合同对象的查询集。

### 7. @transaction.atomic()
@transaction.atomic() 是一个装饰器，用于将一个方法或函数包装在数据库事务中执行。

在 Django 中，数据库事务用于确保一组数据库操作要么全部成功提交，要么全部回滚到初始状态，从而保持数据的一致性和完整性。使用 @transaction.atomic() 装饰器可以将一段代码块标记为一个原子操作，以便在执行期间自动启用事务。
如果在方法执行过程中发生异常或错误，所有对数据库的修改将被回滚，不会对数据库产生影响。
装饰器可以应用于函数或方法，但不能应用于类。

### 8. 关于Vue创建组件的疑问
#### i. 在.js中一个class中包含了构造函数,mounted()是不是就可以算是组件呢?
在 Vue.js 中，一个组件可以由一个类（可以是普通的 JavaScript 类或 Vue 组件类）来表示，类中包含构造函数以及其他生命周期钩子函数（如 mounted）。因此，可以将一个包含构造函数和生命周期钩子函数的类视为一个 Vue 组件。
在 Vue 组件中，构造函数和生命周期钩子函数的定义方式略有不同。构造函数通常用于初始化组件的数据和状态，而生命周期钩子函数用于在组件的不同生命周期阶段执行特定的操作。

在 Vue 组件类中，可以使用 mounted 钩子函数来定义组件在挂载到 DOM 后执行的操作。mounted 钩子函数会在组件实例被挂载到 DOM 之后调用。
```js
Vue.component('my-component', {
  mounted() {
    console.log('Component mounted');
    // 在组件挂载到 DOM 后执行的操作
  }
});
```
总结来说，一个类中包含构造函数和生命周期钩子函数（如 mounted）可以被视为一个组件的定义。在 Vue.js 中，组件是由类或组件类来表示的，并且可以通过生命周期钩子函数来定义组件在不同生命周期阶段的行为。

#### ii. $emit
$emit 是 Vue.js 中实例的一个方法，用于在子组件中触发自定义事件，并向父组件传递数据。
使用 $emit 方法可以在子组件中定义自定义事件，并在需要的时候触发该事件。父组件可以监听并响应该事件，并获取子组件传递的数据。

#### iii. $nextTick
$nextTick 是 Vue.js 实例的一个方法，用于在下次 DOM 更新循环结束后执行回调函数。

在 Vue.js 中，DOM 更新是异步执行的，当数据发生变化时，Vue.js 会对 DOM 进行重新渲染。而 $nextTick 方法允许你在 DOM 更新循环结束后执行特定的代码，以确保在对更新后的 DOM 进行操作时获取到最新的 DOM 结构
在 Vue 3 中，$nextTick 方法已被移除，并被替换为新的 API。Vue 3 采用了 Composition API，通过使用 await 和 nextTick 函数来实现类似的功能。
但是这是使用setup()的前提下
#### vi. $refs
是Vue.js 实例的一个属性，用于访问在模板中通过 ref 属性声明的子组件或 DOM 元素。
通过在模板中给子组件或 DOM 元素添加 ref 属性，Vue.js 将会在组件实例或父组件的 $refs 属性中创建一个引用。

### v. setup()
在 Vue 3 中，通过 setup() 函数来定义组件的配置和逻辑。setup() 函数是一个特殊的函数，它在组件实例创建之前执行，并且在组件实例创建过程中被调用

    vue中setup的作用：setup的设计是为了使用组合式api
    setup在生命周期中的位置：setup位于created 和beforeCreated之前,用于代替created 和beforeCreated,但是在setup函数里不能访问到this,另外setup内可以通过以下hook操作整个生命周期
    setup参数：setup可接受props,context,其中props由于是响应式数据,不能直接解构赋值,context不是响应式数据,可以直接解构赋值;setup必须返回一个对象,一旦return,就可以像vue2.x的方式使用该属性

=====================================================================================================
1. function roleName(role):处理账号的角色(权限),返回中文角色名称;
2. function trapEscape(callback):用于监听按键事件
    在最新的 Web 标准中，keyCode 属性已被废弃，推荐使用 event.key 或 event.code 属性来替代。如果要使用最新的标准，可以将 event.keyCode === 27 改为 event.key === 'Escape' 或 event.code === 'Escape'。
    此外，使用 jQuery 的 $(document.body).on("keyup", myself) 绑定事件监听器，可以在整个文档中捕获按键事件。
3. function findCustomer(customers, customerId):用于寻找客户信息.
4. function today():用于获取当前时间 .
5. function showLoading():用于显示加载画面 .
6. function hideLoading():用于隐藏加载画面 .
7. class NotFound:404页面的url .
8. class Pagination :用于分页 .
   * 构造函数:  constructor(kwargs)
   * 计算属性:
     * get count()
     * get pageSize() 
     * get current() 
     * get previous()
     * get next()
   * 方法:
     * goFirst()
     * goLast()
     * goPrevious()
     * goNext()
9. class CustomerViewer:
   * 构造函数:constructor()
   * 方法:
     * mounted()
     * close():含有关闭窗口
     * getRichman(richmanId):含有获取管理员信息(预计是用来判断是否有权限)
     * switchTab(tabName):一个用于切换选项卡的JavaScript函数 [暂未使用]
       - 这个函数的目的是根据给定的tabName参数切换选项卡。函数的实现步骤如下：

               通过$(this.$el)获取父元素（通常是一个包含选项卡的容器）。
               使用parent.find(".nav-tabs li")选择所有选项卡标签的列表项，并使用.removeClass("active")移除它们的"active"类，即取消选中状态。
               使用parent.find(".tab-pane")选择所有选项卡内容的容器，并使用.removeClass("active")移除它们的"active"类，即隐藏它们。
               使用parent.find("#" + tabName)选择具有给定tabName ID 的选项卡内容容器，并使用.addClass("active")为其添加"active"类，即显示该选项卡内容。
               使用$(window.event.target)获取事件的目标元素（即触发了选项卡切换的元素）。
               使用.parents("li")选择目标元素的父级列表项，并使用.addClass("active")为其添加"active"类，即将该列表项标记为选中状态。
     * checkCtrlEnter():用于检查用户是否同时按下Ctrl键和Enter键的JavaScript函数 [暂未使用]
   * 含有提交拜访记录:async sendVisitationContent() [暂未使用]

10. class CustomerEditor:
    * 方法:
      * 含有mounted()
      * focusName():将焦点置于名字输入框上方
        
            在方法内部，首先使用this.$nextTick()方法来确保在DOM更新后执行后续操作。$nextTick()是Vue.js提供的一个异步方法，用于在DOM更新周期结束后执行回调函数。
            在回调函数中，通过this.$refs.txtName获取名字输入框的引用。$refs是Vue.js提供的一个特殊属性，用于获取组件或元素的引用。
            接下来，通过检查txtName是否存在，即确保找到了名字输入框的引用。如果存在，则调用focus()方法将焦点设置在名字输入框上。
            通过执行这些步骤，方法将在DOM更新后将焦点设置在名字输入框上，以便用户可以直接在该输入框中输入内容。
            请注意，这段代码是基于Vue.js框架编写的。
      * updateIcon(event):用于更新头像的方法.
      * 含有关闭窗口函数:close(force).
    * 构造函数:constructor()
    * 计算属性:
      * get isAdding()其中这被称为 isAdding 的getter属性,检查是否正在添加客户.
      * get isFull()其中这被称为isFull的getter属性,检查当前的模式是否为 "full"
    * 含有添加用户信息功能:async save(),使用到前面的isAdding(),以及clear(),clearAndAssign()
    * 含有判断是否保存成功:async saveAndNext()[未使用]
          - saveAndNext 函数中的代码执行了以下步骤：

                  - 调用 this.save() 方法进行保存操作。
                  - 使用 await 关键字等待保存操作的结果，直到 save() 方法返回一个 Promise 对象的解析值。
                  - 对 await this.save() 的结果使用双重否定运算符 !! 进行类型转换，将其转换为布尔值。

    * 含有保存和关闭操作:async saveAndClose()[未使用]
          - saveAndClose 函数中的代码执行了以下步骤：

                 调用 this.save() 方法进行保存操作。
                 使用 await 关键字等待保存操作的结果，直到 save() 方法返回一个 Promise 对象的解析值。保存操作的结果被赋值给 errorMessage 变量。
                 检查 errorMessage 是否不为空字符串。如果不为空字符串，表示保存操作发生错误。
                 如果保存操作发生错误，将错误消息赋值给 this.errorMessage，并通过 console.debug() 打印错误消息。
                 返回 false 表示保存和关闭操作失败。
                 如果保存操作成功（errorMessage 为空字符串），则清除 this.customer 对象的内容。
                 返回 true 表示保存和关闭操作成功。

11. class Dashboard:首页
    * 构造函数: constructor()
    * 方法:
      * reload(): 重新加载数据(包括团队成员,客户,图表)
      * wantToView(customerId):设置要查看的顾客的方法
    * async fetchRichmen():获取团队成员
    * async fetchMyCustomers():获取最新的新客户
    * async showChart() :获取图表
12. class CustomerPage :销售管理
    * 构造函数: constructor()
    * 计算属性(Vue.js中的一个特性): get pageTitle()
    * 方法: 
      * reload()
      * unshiftCustomer(customer, isAdding)
      * wantToAdd()
      * wantToEdit(customerId)
      * wantToView(customerId)
      * leftBarColor(customer)
    * async loadCustomers():加载列表
13. class ServicePage: 售后管理
    * 构造函数: constructor()
    * 方法:
      * reload()
      * unshiftCustomer(customer)
      * wantToEdit(customerId)
      * wantToView(customerId)
    * 计算属性:
      * get pageTitle()
    * async loadCustomers():加载列表
14. class ProcessService[未使用]
15. class UpdatePassword:修改密码
    * 构造函数:constructor()
    * 方法:
      * setError(message)
      * cancelEditing():撤销修改
    * async updatePassword():设置密码
16. class RichmanPage:内部管理??
    * 构造函数:constructor() 
    * 方法
      *  roleColor(role)
    * async reload():重新加载用户列表
    * async disableRichman(richmanId):删除用户
    * async enableRichman(richmanId):启用用户
17. class CrmMain:管理主页面包括上面各页面的跳转链接
    * 构造函数:constructor(profile)
    * 方法:
      * provide()
      * getRoleName()
      * mounted()
      * handleEnterKey(event)
      * searchCustomer():搜索用户
    * async logout():登出
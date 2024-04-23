# Model
User:

    id
    password
    last_login
    is_superuser
    username
    first_name
    last_name
    email
    is_staff
    is_active
    data_joined
    nickname
    create_at
    update_at
    role


图表过滤条件:

    filter_by_time = self.request.query_params.get("time")


暂时:
```python
def get_chart_data(self):
    # 搜索请求
    search_value = self.request.GET.get("keywords", None)
    if search_value:
        query = Q(license_name=search_value) | Q(name=search_value)
        self.request.session['search_value'] = search_value
    else:
        query = Q()
    # 获取匹配的唯一名称列表
    unique_names = TableInfo.objects.filter(query).values_list('name', 'license_name').order_by('id')
    # 时间选择请求
    value = self.request.GET.get('value', "last_day")
    time_ranges = {
        "last_hour": last_hour(),
        "last_day": last_day(),
        "last_week": last_week(),
    }
    start_time, current = time_ranges.get(value, (None, None))
    if start_time and current:
        if "search_value" in self.request.session:
            search_value = self.request.session['search_value']
            query = Q(license_name__startswith=search_value) | Q(name__startswith=search_value)
        query &= Q(time__range=(start_time, current))

    if not unique_names:
        return JsonResponse({"message": "未找到相关结果"})
    # 获取请求中的页码和每页限制数
    page = self.request.GET.get('pageNum', 1)
    limit = 1
    # 使用分页器进行分页
    paginator = Paginator(unique_names, limit)
    try:
        page_data = paginator.page(page)  # 获取指定页码的数据
    except PageNotAnInteger:
        page_data = paginator.page(1)  # 如果页码超过范围,则默认返回第一页的数据
    except EmptyPage:
        page_data = paginator.page(paginator.num_pages)  # 如果页码超过范围,则返回最后一页数据

    datas = []
    for unique_name in page_data:
        name = unique_name[0]
        license_name = unique_name[1]
        data = self.get_chart(query & Q(name=name), license_name, name)
        if data is not None:
            datas.append(data)
    message = {
        "code": 0,
        "msg": "",
        "pages": paginator.num_pages,
        "item": datas,
        "time_value": values.get(value, None),
        "search_value": search_value,
    }
    return JsonResponse(message)
```
```python
def get_chart(self, query, license_name, unique_name):
    chart = Chart()  # 创建图表对象
    server_info_query = SeverInfo.objects.filter(query).only("time",
                                                             "percent",
                                                             "memory_percent",
                                                             "disk_percent")
    if server_info_query.exists():  # 查询服务器信息
        server_infos = server_info_query.order_by('id')
    else:
        return None
    # 获取服务器信息数据
    x_time = []
    y_cpu = []
    y_memory = []
    value_disk = None
    for server_info in server_infos:
        x_time.append(timezone.localtime(server_info.time).strftime('%Y-%m-%d %H:%M:%S'))
        y_cpu.append(server_info.percent)
        y_memory.append(server_info.memory_percent)
        value_disk = server_info.disk_percent  # 获取磁盘百分比
    # 生成图表数据
    license_name = license_name.replace('(', '_')
    license_name = license_name.replace(')', '_')
    data_line = chart.lines_chart(f'{license_name}_{unique_name}',
                                  f'Usage_{license_name}_{unique_name}',
                                  x_time, y_cpu, y_memory)
    data = {
        "title": "Usage_" + license_name + "_" + unique_name,
        "appId": unique_name,
        "data_line": data_line,
        "value_disk": str(value_disk) + "%",
    }
    return data
```

# 未加分页前：
```python
class SystemChart(mixins.ListModelMixin, viewsets.GenericViewSet):
    queryset = SeverInfo.objects.all()
    serializer_class = SystemChartsSerializer

    def get_queryset(self):
        timeFilter = ""
        filter_by_text = self.request.query_params.get("query")
        filter_by_time = self.request.query_params.get("timerFilter")
        page = self.request.query_params.get("page", 1)
        per_page = self.request.query_params.get("per_page", 1)
        if filter_by_time == "last-hour":
            timeFilter = last_hour()
        elif filter_by_time == "last-day":
            timeFilter = last_day()
        elif filter_by_time == "last-week":
            timeFilter = last_week()
        current = current_time()
        q = SeverInfo.objects.filter(time__range=(timeFilter, current)).order_by("id")
        if filter_by_text:
            q = q.filter(Q(name=filter_by_text) | Q(license_name=filter_by_text))

        return q


    def list(self, request, *args, **kwargs):
        queryset = self.filter_queryset(self.get_queryset())
        serializer = self.get_serializer(queryset, many=True)
        # 根据名称对数据进行分类
        data_by_name = defaultdict(list)
        for item in serializer.data:
            print("item", item)
            data_by_name[item['name']].append(item)

        # 构造包含分类结果的字典数据
        categorized_data = []
        for name, data in data_by_name.items():
            license_name = [item['license_name'] for item in data][-1]
            cpu_percent = [item['percent'] for item in data]
            memory_percent = [item['memory_percent'] for item in data]
            disk_percent = [item['disk_percent'] for item in data][-1]
            time = [item['time'] for item in data]
            categorized_data.append({
                'name': name,
                'data': {
                    "license_name": license_name,
                    "cpu_percent": cpu_percent,
                    "memory_percent": memory_percent,
                    "disk_percent": disk_percent,
                    "time": time,
                }})
        return Response(categorized_data)
```

    <a class="toUp" type="button" @click="toUp" ><i class="fa fa-chevron-circle-up" aria-hidden="true" ></i></a>


    {#                <th>CPU/%#}
{#                    <div class="box-icon">#}
{#                        <div class="up"#}
{#                             :class="item.status === 1 ? 'opacity-5' : ''"></div>#}
{#                        <div class="down"#}
{#                             :class="item.status === 1 ? 'opacity-1' : ''"></div>#}
{#                    </div>#}
{#                </th>#}
{#                <th>内存/%#}
{#                    <div class="box-icon">#}
{#                        <div class="up"#}
{#                             :class="item.status === 1 ? 'opacity-5' : ''"></div>#}
{#                        <div class="down"#}
{#                             :class="item.status === 1 ? 'opacity-1' : ''"></div>#}
{#                    </div>#}
{#                </th>#}
{#                <th>磁盘/%#}
{#                    <div class="box-icon">#}
{#                        <div class="up"#}
{#                             :class="item.status === 1 ? 'opacity-5' : ''"></div>#}
{#                        <div class="down"#}
{#                             :class="item.status === 1 ? 'opacity-1' : ''"></div>#}
{#                    </div>#}
{#                </th>#}

drawCharts() {
            try {
                let parentDiv = document.getElementById("parentChartContainer");
                for (let num = 0; num < this.charts_data.length; num++) {
                    let linechart = {};
                    const disk_percent = this.charts_data[num].data['disk_percent'];
                    const chartContainer_id = "chartContainer_" + this.charts_data[num].name;
                    let chartContainer = document.getElementById(chartContainer_id)
                    chartContainer = document.createElement('div');
                    chartContainer.setAttribute('id', chartContainer_id);
                    chartContainer.style.padding = "16px";
                    chartContainer.style.border = "1px solid #dddddd";
                    parentDiv.appendChild(chartContainer);
                    progressbar(chartContainer_id, disk_percent, this.charts_data[num].name, true);

                    const chartDiv = document.createElement('div');
                    let chartId = 'id-' + this.charts_data[num].name;
                    chartDiv.setAttribute('id', chartId);
                    chartDiv.style.width = "100%";
                    chartDiv.style.height = "450px";
                    chartDiv.style.padding = "10px 0";
                    chartContainer.appendChild(chartDiv);
                    chartOption(this.charts_data, num, chartDiv);
                }
            } catch (error) {
                console.error("出错了！", error);
            }
        }

        function chartOption(data, num, chartDiv) {
        let linechart = echarts.init(chartDiv);
        const option = {
            title: {text: data[num].name + "-" + data[num].data["license_name"]},
            tooltip: {trigger: 'axis'},
            legend: {data: ["CPU使用率", "内存使用率"]},
            toolbox: {
                feature: {
                    dataZoom: {
                        yAxisIndex: 'none'
                    }, restore: {}, saveAsImage: {}
                }
            },
            dataZoom: [{
                show: true, realtime: true, start: 70, end: 100, xAxisIndex: [0, 1]
            }, {
                type: 'inside', realtime: true, start: 30, end: 70, xAxisIndex: [0, 1]
            }],
            grid: {left: '3%', right: '4%', bottom: '10%', containLabel: true},
            xAxis: {
                type: 'category', boundaryGap: false, data: data[num].data['time'],
            },
            yAxis: {
                type: 'value',
            },
            series: [{
                name: 'CPU使用率',
                type: 'line',
                // stack: 'Total',
                data: data[num].data['cpu_percent'],
            }, {
                name: '内存使用率',
                type: 'line',
                // stack: 'Total',
                data: data[num].data['memory_percent'],
            },]
        }
        linechart.setOption(option);
        window.addEventListener("resize", () => {
            linechart.resize();
        });
    }

    function progressbar(parentDiv, data, name, isChart) {
        const parent = document.getElementById(parentDiv);
        let progressbarId = parentDiv + name;
        let progressbarContainerExit = document.getElementById(progressbarId);
        if (!progressbarContainerExit) {
            progressbarContainerExit = document.createElement('div');
            progressbarContainerExit.style.width = "100%";
            progressbarContainerExit.className = "progress";
            progressbarContainerExit.style.display = "flex";
        }
        if (isChart) {
            const diskDiv = document.createElement('span');
            diskDiv.innerHTML = "磁盘使用率：";
            diskDiv.style.display = "inline-block";
            diskDiv.style.float = "left";
            progressbarContainerExit.appendChild(diskDiv);
        }
        const percentContainer = document.createElement('div');
        percentContainer.style.flexGrow = '1';
        const progressbarDiv = document.createElement('div');
        progressbarDiv.setAttribute('id', progressbarId);
        progressbarDiv.classList.add('progress-bar');
        progressbarDiv.setAttribute('role', 'progressbar');
        progressbarDiv.setAttribute('aria-valuenow', data);
        progressbarDiv.setAttribute('aria-valuemin', '0');
        progressbarDiv.setAttribute('aria-valuemax', '100');
        progressbarDiv.style.width = data + '%';
        progressbarDiv.style.color = "#23292e";
        progressbarDiv.innerText = data + '%';
        percentContainer.appendChild(progressbarDiv);
        progressbarContainerExit.appendChild(percentContainer);
        parent.appendChild(progressbarContainerExit);
        const progressbarElement = document.getElementById(progressbarId);
        if (data >= 90) {
            progressbarElement.style.backgroundColor = "#ff5722";
        } else if (70 < data && data < 90) {
            progressbarElement.style.backgroundColor = "#ffb800";
        } else {
            progressbarElement.style.backgroundColor = "#16b777";
        }
    }


    <div class="card" id="parentChartContainer">
        <div v-if="chartDataList">
            <div v-for="chartData in chartDataList" :key="chartData.name" class="chart-wrapper">
                <div class="progressbar-wrapper">
                    <span class="disk-usage-title">磁盘使用率：</span>
                    <div class="progressbarContainer">
                        <div :id="getProgressbarId(chartData.name)"></div>
                    </div>
                </div>
                <div :ref="chartData.name" class="chartContainer" :id="chartData.name">
                </div>
            </div>
        </div>
    </div>
=================================
```Python
class SystemChart(SystemResourceModelViewSet):
    queryset = SeverInfo.objects.all()
    serializer_class = SystemChartsSerializer

    def get_queryset(self):
        timeFilter = ""
        filter_by_text = self.request.query_params.get("query")
        filter_by_time = self.request.query_params.get("timerFilter", "last-day")
        if filter_by_time == "last-hour":
            timeFilter = last_hour()
        elif filter_by_time == "last-day":
            timeFilter = last_day()
        elif filter_by_time == "last-week":
            timeFilter = last_week()
        current = current_time()
        if filter_by_text:
            q = SeverInfo.objects.filter(Q(name=filter_by_text) | Q(license_name=filter_by_text))
            q = q.filter(time__range=(timeFilter, current)). \
                values('name', 'license_name', 'percent', 'disk_percent', 'memory_percent', 'time')
        else:
            q = SeverInfo.objects.filter(time__range=(timeFilter, current)). \
                values('name', 'license_name', 'percent', 'disk_percent', 'memory_percent', 'time')

        return q.order_by('name', 'id')

    def list(self, request, *args, **kwargs):
        queryset = self.filter_queryset(self.get_queryset())
        serializer = self.get_serializer(queryset, many=True)
        data_by_name = cache.get("data_by_name")
        if data_by_name is None :
            # 根据名称对数据进行分类
            data_by_name = defaultdict(list)
            for item in serializer.data:
                data_by_name[item['name']].append(item)
            # 更新缓存
            cache.set("data_by_name", data_by_name, 30)

        # 构造包含分类结果的字典数据
        categorized_data = []
        for name, data in data_by_name.items():
            license_name = [item['license_name'] for item in data][-1]
            cpu_percent = [item['percent'] for item in data]
            memory_percent = [item['memory_percent'] for item in data]
            disk_percent = [item['disk_percent'] for item in data][-1]
            time = [item['time'] for item in data]
            categorized_data.append({
                'name': name,
                'data': {
                    "license_name": license_name,
                    "cpu_percent": cpu_percent,
                    "memory_percent": memory_percent,
                    "disk_percent": disk_percent,
                    "time": time,
                }})
        total_categories = len(data_by_name)
        pagination = self.pagination_class()
        page = pagination.paginate_queryset(categorized_data, request)
        page_data = {'count': total_categories, 'page': page}
        return Response(page_data)

```
shortman修改进度:
1. 对于csrf错误问题的修复
2. views.py中设置了用户的权限职能;
3. 需要更改model中的user,添加role字段(已添,但是感觉有点多余,因为有设置is_superuser字段);
    其中要怎么设置流加载(或者是说分批加载数据)-->分页功能的实现（完成）

4. 分页将一个图表作为一个整体而不是将图表中的数据作为要分页的内容。（完成）
5. list中的分页功能完善。（排序似乎没有必要，其余完成）
6. 修改密码页面，功能(完成)
7. 注册账号页面，功能（注册人要填写字段：username，password）
8. 管理账号页面，功能（管理员要管理账号的管理权限role/is_superuser、账号状态is_active,is_staff)

tips:想要在登陆界面添加时间变化,登陆界面需要美化
网页获取最新数据（需要一直更新数据且要展示，不适合用站点缓存）

现数据表有超24966625条数据，考虑
数据库分区使用：
创建一张用户的id索引表。(完成)
将每个用户的资源使用情况各为一张表（没有这个用户的id则动态创建）(完成)。
假设将表的不常用内容存储到一张合起来的表，其他常用信息存储到各自分表。---》
修改为： 将常用的数据按name进行分表，分表中包含name_id、percent、memory_percent、disk_percent和time，然后另外建立一张全部数据的存储表，存储没有用到的数据。然后都只保留7天的数据。（完成）
每个资源表中只保存近7天内容。（已完成）
但是假设有100个客户，会不会导致资源表过多。

1.




def install(custom_model):
    from django.db import connection
    from django.db.backends.base.schema import BaseDatabaseSchemaEditor

    """
    fix:
        editor = BaseDatabaseSchemaEditor(connection)
        try:
            editor.create_model(model=custom_model) # 会抛出个异常，不知为啥,但表会创建
        except AttributeError as error:
            print(error)
        在BaseDatabaseSchemaEditor类中有一个__enter__方法，
        需要通过with上下文打开以后deferred_sql变量才会在实例化后赋值给editor
        这样就不会有'BaseDatabaseSchemaEditor' object has no attribute 'deferred_sql'

    """
    with BaseDatabaseSchemaEditor(connection) as editor:
        editor.create_model(model=custom_model)



echarts:
time=[]
percent=[]
memory_percent=[]

数据库读取:
<QuerySet [{'percent': 12.8, 'memory_percent': 3.33, 'disk_percent': 94.65, 'time': datetime.datetime(2024, 2, 26, 7, 49, 21, 287478, tzinfo=datetime.timezone.utc)},




[2024-03-04 17:45:52,820: ERROR/ForkPoolWorker-2] Task shortman.tasks.delete_old_records[464a8dac-42da-4bd2-9104-7bc2bfc619fd] raised unexpected: TypeError('can only concatenate str (not "tuple") to str')
Traceback (most recent call last):
File "/home/tempo/demo/lib/python3.10/site-packages/celery/app/trace.py", line 477, in trace_task
R = retval = fun(*args, **kwargs)
File "/home/tempo/demo/lib/python3.10/site-packages/celery/app/trace.py", line 760, in __protected_call__
return self.run(*args, **kwargs)
File "/home/tempo/demo/djangoproject/shortman/shortman/tasks.py", line 94, in delete_old_records
MainBlock = getBlockModel("ops_shift__server_" + model)
TypeError: can only concatenate str (not "tuple") to str

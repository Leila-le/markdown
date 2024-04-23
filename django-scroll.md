1.添加滚动监听事件
知识点：addEventListener() 方法，事件监听
用法：element.addEventListener(event, function, useCapture);
第一个参数是：事件的类型。这个项目是滚动监听，所以event是写“scroll”。（其他项目可根据需求，如果是点击就写“click”，以此类推）；
第二个参数是：监听事件时调用的函数。这里调用的是 this.menu 这个函数。
第三个参数是：布尔值。即true/false，这个参数是与事件捕获和事件冒泡有关，与这两个有关一般是点击事件，这个项目是滚动事件，所以第三个参数可以不写。
————————————————
版权声明：本文为CSDN博主「houqiqi_0826」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/houqiqi_0826/article/details/82706376

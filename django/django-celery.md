用python启动celery的定时任务功能（日志级别为INFO）：python3 -m celery -A shortman beat -l INFO
用python启动celery的worker（日志级别为INFO）：python3 -m celery -A shortman worker -l INFO
shortman为django的项目app名称

配置按celery官网来：https://docs.celeryq.dev/en/v5.3.6/django/first-steps-with-django.html   （其中可以选择对应版本）

同时启动worker和beat：
使用 Python 的 multiprocessing 模块来同时启动 Celery Beat 和 Celery Worker：
``` python
import multiprocessing
import subprocess

def start_celery_beat():
    subprocess.call(['python3', '-m', 'celery', '-A', 'shortman', 'beat', '-l', 'INFO'])

def start_celery_worker():
    subprocess.call(['python3', '-m', 'celery', '-A', 'shortman', 'worker', '-l', 'INFO'])

if __name__ == '__main__':
    beat_process = multiprocessing.Process(target=start_celery_beat)
    worker_process = multiprocessing.Process(target=start_celery_worker)

    beat_process.start()
    worker_process.start()

    beat_process.join()
    worker_process.join()
```


使用命令行：manage.py同目录下，使用celery -A cfehome worker --beat -l info
其中`cfehome`为app名称

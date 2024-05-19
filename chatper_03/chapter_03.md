### Ch03. Airflow 의 스케줄링 

- schedule_interval 
```python
import datetime as df 
from pathlib import Path 
from airflow import DAG

dag=DAG(
    dag_id="unscheduled",
    start_date=dt.datetime(2024, 5, 19),
    schedule_interval=None, # 스케줄 되지 않는 DAG
)
```

- @daily 는 매일 자정에 실행하도록 하는 매크로이다. 단 이 경우 end_date 가 없으므로 이론적으로는 영원히 실행될 것이다. 
```python

dag=DAG(
    dag_id="scheduled",
    start_date=dt.datetime(2024, 5, 19),
    schedule_interval=@daily, # 매일 자정에 실행 
)
```

- 종료 날짜를 정의할 수 있다. 또한 스케줄링을 빈도 기반으로 지정할 수 있다. 
```python

dag=DAG(
    dag_id="scheduled_with_end_date",
    schedule_interval=dt.timedelta(days=3), # timedelta 로 3일에 한번씩 스케줄링 지정
    start_date=dt.datetime(year=2024, month=5, day=19),
    end_date=dt.datetime(year=2024, month=5, day=25),
)
```
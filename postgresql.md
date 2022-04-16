## postgresql

### 1、将数据库查询出的时间数据格式化

24小时制；注意：不可以 用 ‘yyyy-MM-dd HH:mm’

```sql
select TO_CHAR(create_time ,'yyyy-MM-dd HH24:MI') from user_info;
```

### 2、创建触发器

1、先建一个触发器的执行函数

```sql
CREATE OR REPLEASE FUNCTION student_delete_trigger_fun()//函数名
returns trigger as $$
begin
	//要执行的逻辑语句
    delete from score where student_no = old.student_no;
    return old;
end;
$$
language plpgsql;
```

2、再创建这个触发器

```sql
CREATE TRIGGER delete_student_trigger
after delete on student //在哪张表设置什么触发器
for each row execute procedure student_delete_trigger_fun();
```


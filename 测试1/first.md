# 查询2好，因为查询2优化为零；
# 建议是为查询1的语句添加多个索引。

```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
GROUP BY department_name
ORDER BY department_name ASC;
```
#服务器炸了=-=

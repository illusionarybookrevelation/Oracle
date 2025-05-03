# 通过FOR语句循环游标
#### 简介：
使用FOR语句遍历游标中的数据时，可以把它的计时器看作是一个自动的RECORD类型的变量。

#### 1，隐式游标遍历
通常在关键字IN后面提供由SELECT语句检索的结果集，在检索结果集的过程中，Oracle系统会自动提供一个隐式的游标SQL。
``` sql
begin
  for emp_record in (select empno,ename,sal from emp where job='SALESMAN')
  loop
    dbms_output.put('员工编号：'||emp_record.empno);
    dbms_output.put('；员工姓名：'||emp_record.ename);
    dbms_output.put_line('；员工工资：'||emp_record.sal);
  end loop;
end;
```
#### 2，显式游标遍历
通常在关键字IN后面提供游标的名称，其语法格式如下：
``` sql
for var_auto_record in cur_name loop
    plsql_sentence;
  end loop;
```
- var_auto_record：自动的RECORD类型的变量，可以是任意合法的变量名称。
- cur_name：指定的游标名称。
- plsql_sentence：PL/SQL语句。
``` sql
declare
  cursor cur_emp is select * from emp where deptno = 30;
begin
  for emp_record in cur_emp
  loop
    dbms_output.put('员工编号：'||emp_record.empno);
    dbms_output.put('；员工姓名：'||emp_record.ename);
    dbms_output.put_line('；员工工资：'||emp_record.sal);
  end loop;
end;
```
---
**结语**：在使用游标(包括显式和隐式)的FOR循环中，可以声明游标，但不用进行打开游标，读取游标和关闭游标等操作，这些由Oracle系统自动完成。

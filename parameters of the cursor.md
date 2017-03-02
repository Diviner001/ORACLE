# ORACLE
Water flowing out in a trickle takes a long time to exhaust!

/*指定部门编号，显示部门中工资最高的前3名（不足3名的全部显示）。输出：部门编号 姓名 工资。*/

declare
   cursor emp_sal_cur(p_department_id number) is
   select department_id,last_name,salary
   from employees
   where department_id=p_department_id
   order by salary desc;

begin 
   for v_emp_rec in emp_sal_cur(&department_id)
   loop
     exit when emp_sal_cur%rowcount>3;
     dbms_output.put_line('部门编号为: '||v_emp_rec.department_id||' 姓名: '||
    v_emp_rec.last_name || ' 工资： '||v_emp_rec.salary);
   end loop;
end;


/*对所有部门，做同样的工作*/   
declare
   cursor emp_sal_cur(p_department_id number) is
   select department_id,last_name,salary
   from employees
   where department_id=p_department_id
   order by salary desc;

begin 
   for v_dept_rec in (select distinct department_id from employees 
     where department_id is not null)
   loop 
     for v_emp_rec in emp_sal_cur(v_dept_rec.department_id)
     loop
     exit when emp_sal_cur%rowcount>3;
     dbms_output.put_line('部门编号为: '||v_emp_rec.department_id||' 姓名: '||
    v_emp_rec.last_name || ' 工资： '||v_emp_rec.salary);
     end loop;
   end loop;
end;

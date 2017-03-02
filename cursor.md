# ORACLE
--Water flowing out in a trickle takes a long time to exhaust!

//some practices
/*普通显式游标练习：
指定员工的工号
如果高于或等于所在部门的平均工资，输出first_name(列) last_name（列）’s salary: (显示员工的工资) higher or equal than avgrage salary of department department_name（列）: (显示部门工资).
如果低于所在部门的平均工资，输出first_name last_name’s salary lowerer than avgrage salary of department department_name.
如果员工不属于任何部门，输出first_name last_name no department！*/

declare
   v_empno employees.employee_id%type :=&grade;
   v_dept_sal employees.salary%type;
   v_allms employees%rowtype;
   v_dept_name departments.department_name%type;
   
begin
   select *
   into v_allms
   from employees
   where employee_id =v_empno;   
   
   select avg(salary)
   into v_dept_sal
   from employees
   where department_id=v_allms.department_id;
   
   select department_name
   into v_dept_name
   from departments
   where department_id=v_allms.department_id;
   
   if v_allms.salary>=v_dept_sal
     then 
     dbms_output.put_line(v_allms.first_name||','||v_allms.last_name||q'['s salary higher or equal than avgrage salary of department ]'
     ||v_dept_name||' salary: '|| v_dept_sal);
     elsif v_allms.salary<v_dept_sal
     then
        dbms_output.put_line(v_allms.first_name||','||v_allms.last_name||q'['s salary lower or equal than avgrage salary of department ]'||v_dept_name||' salary: '|| v_dept_sal);
    end if;
exception 
   when no_data_found then
   dbms_output.put_line(v_allms.first_name||','||v_allms.last_name||' no department！');
end;    

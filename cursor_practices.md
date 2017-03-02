# ORACLE
Water flowing out in a trickle takes a long time to exhaust!

/*对所有员工检查工资，输出和上面练习相同的内容。*/
 
 declare
    v_dept_sal employees.salary%type;
    v_emp_rec employees%rowtype;
    v_dept_name departments.department_name%type;
 begin
   for v_emp_rec in (select * from employees) 
   loop
     if v_emp_rec.department_id is null then
     dbms_output.put_line(v_emp_rec.first_name||','||v_emp_rec.last_name||' no department！');
     else
       select avg(salary)
       into v_dept_sal
       from employees
       where department_id=v_emp_rec.department_id;
        
       select department_name
       into v_dept_name
       from departments
       where department_id=v_emp_rec.department_id;
       
       if v_emp_rec.salary>=v_dept_sal
       then
       dbms_output.put_line(v_emp_rec.first_name||','||v_emp_rec.last_name||q'['s salary higher or equal than avgrage salary of department ]'
     ||v_dept_name||' salary: '|| v_dept_sal);
       elsif v_emp_rec.salary<v_dept_sal
       then
        dbms_output.put_line(v_emp_rec.first_name||','||v_emp_rec.last_name||q'['s salary lower or equal than avgrage salary of department ]'
     ||v_dept_name||' salary: '|| v_dept_sal);
       end if;
     end if;
   end loop;    
 end;
 

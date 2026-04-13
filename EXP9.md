<center>Experiment 9</center>
<h2>Experiment 9</h2>
<h4>Queries:</h4>

1.Display the name of employee who earns highest salary
~~~sql
SELECT ename
FROM EMPLOYEE
WHERE sal = (SELECT MAX(sal) FROM EMPLOYEE);
~~~

2.Display the employee number and name of employee working as clerk and earning highest salary among clerks
~~~sql
SELECT empno, ename
FROM EMPLOYEE
WHERE job = 'CLERK'
AND sal = (SELECT MAX(sal) FROM EMPLOYEE WHERE job = 'CLERK');
~~~

3.Display the names of the salesman who earn a salary more than the highest salary of any clerk
~~~sql
SELECT ename
FROM EMPLOYEE
WHERE job = 'SALESMAN'
AND sal > (SELECT MAX(sal) FROM EMPLOYEE WHERE job = 'CLERK');
~~~

4.Display the names of clerks who earn salary more than that of JAMES and less than that of SCOTT
~~~sql
SELECT ename
FROM EMPLOYEE
WHERE job = 'CLERK'
AND sal > (SELECT sal FROM EMPLOYEE WHERE ename = 'JAMES')
AND sal < (SELECT sal FROM EMPLOYEE WHERE ename = 'SCOTT');
~~~

5.Display the names of employees who earn salary more than that of JAMES or more than that of SCOTT
~~~sql
SELECT ename
FROM EMPLOYEE
WHERE sal > (SELECT sal FROM EMPLOYEE WHERE ename = 'JAMES')
OR sal > (SELECT sal FROM EMPLOYEE WHERE ename = 'SCOTT');
~~~

6.Display the names of employees who earn highest salary in their respective departments
~~~sql
SELECT ename, deptno, sal
FROM EMPLOYEE E
WHERE sal = (
    SELECT MAX(sal)
    FROM EMPLOYEE
    WHERE job = E.job
);
~~~

7.Display the names of employees who earn highest salaries in their respective job groups
~~~sql
SELECT ename, job, sal
FROM EMPLOYEE E
WHERE sal = (
    SELECT MAX(sal)
    FROM EMPLOYEE
    WHERE job = E.job
);
~~~

8.Display the employee names who are working in ACCOUNTING department
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'ACCOUNTING';
~~~

9.Display the employee names who are working in CHICAGO
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.LOCATION = 'CHICAGO';
~~~

10.Display the job groups having total salary greater than the maximum salary for managers
~~~sql
SELECT job, SUM(sal) AS total_salary
FROM EMPLOYEE
GROUP BY job
HAVING SUM(sal) > (
    SELECT MAX(sal)
    FROM EMPLOYEE
    WHERE job = 'MANAGER'
);
~~~
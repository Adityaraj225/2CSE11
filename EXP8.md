<center>Experiment 8</center>
<h2>Experiment 8</h2>
<h4>Queries:</h4>

1.Display all employees with their department name
~~~sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
~~~

2.Display employees whose manager is JONES, also show manager name
~~~sql
SELECT E.ENAME AS EMPLOYEE, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M
ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
~~~

3.Display employee name, job, department name, manager name, and grade (department-wise)
~~~sql
SELECT E.ENAME, E.JOB, D.DNAME,
       M.ENAME AS MANAGER, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
ORDER BY D.DNAME;
~~~

4.List employees (except clerks) with name, job, department, and grade sorted by highest salary
~~~sql
SELECT E.ENAME, E.JOB, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.JOB != 'CLERK'
ORDER BY E.SAL DESC;
~~~

5.Display employee name, job, and manager (including employees without manager)
~~~sql
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
~~~

6.List employees with name, job, annual salary, dept no, dept name, and grade (salary = 36000/year OR not clerk)
~~~sql
SELECT E.ENAME, E.JOB, (E.SAL * 12) AS ANNUAL_SAL,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL * 12 = 36000 OR E.JOB <> 'CLERK');
~~~

7.List employees earning 30000/year and not clerks
~~~sql
SELECT E.ENAME, E.JOB, (E.SAL * 12) AS ANNUAL_SAL,
       E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL * 12 = 30000 AND E.JOB <> 'CLERK');
~~~

8.List employee number, name, manager number & name (show 'NO MANAGER' if none)
~~~sql
SELECT E.EMPNO, E.ENAME,
       IFNULL(M.EMPNO, 'NO MANAGER') AS MANAGER_NO,
       IFNULL(M.ENAME, 'NO MANAGER') AS MANAGER_NAME
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
~~~

9.Display department name, department number, and total salary
~~~sql
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SAL
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DEPTNO, D.DNAME;
~~~

10.Display employee number, name, and department location
~~~sql
SELECT E.EMPNO, E.ENAME, D.LOCATION
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
~~~

11.Display employee name and department name
~~~sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
~~~
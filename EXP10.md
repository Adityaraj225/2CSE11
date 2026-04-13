<center>Experiment 10</center>
<h2>Experiment 10</h2>
<h4>Queries:</h4>

1.Display the names of employees from department number 10 with salary greater than that of any employee working in other departments
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (
    SELECT SAL FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
~~~

2.Display the names of employees from department number 10 with salary greater than that of all employees working in other departments
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (
    SELECT SAL FROM EMPLOYEE
    WHERE DEPTNO <> 10
);
~~~

3.Display the details of employees who are in SALES department and grade is 3
~~~sql
SELECT E.*
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
AND S.GRADE = 'C';
~~~

4.Display employees who are not managers (i.e., not managing anyone)
~~~sql
SELECT ENAME
FROM EMPLOYEE
WHERE EMPNO NOT IN (
    SELECT MGR FROM EMPLOYEE
    WHERE MGR IS NOT NULL
);
~~~

5.Display employees whose manager name is JONES
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
~~~

6.Display employee names who are working in SALES department
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME = 'SALES';
~~~

7.Display employee name, department name, salary and commission for salary between 2000 and 5000 and location is CHICAGO
~~~sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
AND D.LOCATION = 'CHICAGO';
~~~

8.Display employees whose salary is greater than their manager's salary
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
~~~

9.Display employees who are working in the same department as their manager
~~~sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
~~~

10.Display employee name and grade for dept no 10 or 30, excluding grade 4, and hired before 31-Dec-82
~~~sql
SELECT E.ENAME, S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
AND S.GRADE <> 4
AND E.HIREDATE < '1982-12-31';
~~~
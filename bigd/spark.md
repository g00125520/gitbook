## spark sql
- inner join
- full outer join
- left outer join
- right outer join
- left semi join，SELECT * FROM emp LEFT SEMI JOIN dept ON emp.deptno = dept.deptno等价于SELECT * FROM emp WHERE deptno IN (SELECT deptno FROM dept)
- left anti join，SELECT * FROM emp LEFT ANTI JOIN dept ON emp.deptno = dept.deptno等价于SELECT * FROM emp WHERE deptno NOT IN (SELECT deptno FROM dept)
- cross join
- natural join

传统数据库，left join返回左表所有记录和右表中关联字段相等得记录，right join则返回右表所有记录和左表中关联字段相等得记录，inner join则只返回两个表中关联字段相等得记录。

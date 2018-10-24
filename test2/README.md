# 实验2：用户管理 - 掌握管理角色、权根、用户的能力，并在用户之间共享对象。

#第一步：角色创建;

```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_gundam;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO con_gundam;
Grant succeeded.
```

#第二步：用户gundam创建并且分配空间和授权;

```sql
SQL> CREATE USER gundam IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER new_user QUOTA 50M ON users;
User altered.
SQL> GRANT con_gundam TO gundam;
Grant succeeded.
SQL> exit
```

#第三步：表空间的创建;
```sql
$ sqlplus gundam/123@pdborcl
SQL> show user;
USER is "gundam"
SQL> CREATE TABLE mytable (id number,name varchar(50));
Table created.
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
1 row created.
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
1 row created.
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
View created.
SQL> SELECT * FROM myview;
NAME
--------------------------------------------------
zhang
wang
SQL>exit
```
#第四步：对象创建以及共享的设置；

```sql
$ sqlplus gundam/123@pdborcl
SQL> GRANT SELECT ON myview TO wq;
Grant succeeded.
SQL>exit

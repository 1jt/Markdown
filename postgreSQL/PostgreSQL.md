# PostgreSQL 学习笔记

## 一、介绍

PostgreSQL 是一种开源的关系型数据库管理系统，它具有高度的可扩展性、稳定性和安全性。

Linux安装成功
![Alt text](assets/PostgreSQL/image-8.png)

### 使用技巧

1. 通过执行以下命令来检查 PostgreSQL 是否正在运行：

   ```text
   service postgresql status
    ```

    ![Alt text](assets/PostgreSQL/image-11.png)
    可以看到服务处于`active`状态，也就是可以登陆。另外，也可以看到主服务进程的PID。
2. 默认情况下，PostgreSQL 会创建一个拥有所权限的特殊用户`postgres`。要实际使用 PostgreSQL，你必须先登录该账户：

   ```text
   sudo su postgres
    ```

3. 使用 `psql` 来启动 PostgreSQL Shell：
4. 查看现有的所有表

    ```text
    \l
     ```

    按 `q` 键退出
    ![Alt text](assets/PostgreSQL/image-12.png)
5. 使用 \du 命令，可以查看 PostgreSQL 用户：

    ```text
   \du
    ```

    ![Alt text](assets/PostgreSQL/image-13.png)
6. 你可以使用以下命令更改任何用户（包括 `postgres`）的密码：

    ```text
    ALTER USER postgres WITH PASSWORD 'my_password';
    ```

    psql包含了一个命令`\password`，他可以用来修改密码而不暴露明文口令
    ![Alt text](assets/PostgreSQL/image-14.png)
    **注意**：将 `postgres` 替换为你要更改的用户名，`my_password` 替换为所需要的密码。另外，不要忘记每条命令后面的 ;（分号）。
7. 建议另外创建一个用户（不建议使用默认的 postgres 用户）。为此，请使用以下命令：

    ```text
    CREATE USER my_user WITH PASSWORD 'my_password';
    ```

    ![Alt text](assets/PostgreSQL/image-15.png)
    **注意**：将 `my_user` 替换为所需的用户名，`my_password` 替换为所需的密码。另外，不要忘记每条命令后面的 ;（分号）。
    可以使用以下命令删除用户：

    ```text
    DROP USER my_user;
    ```

8. 但是，`my_user` 用户没有任何的属性。来让我们给它添加超级用户权限：

    ```text
    ALTER USER my_user WITH SUPERUSER;
    ```

     ![Alt text](assets/PostgreSQL/image-16.png)
    **注意**：将 `my_user` 替换为所需的用户名。另外，不要忘记每条命令后面的 ;（分号）。
9. 要使用其他用户登录，使用 `\q` 命令退出，然后使用以下命令登录：

    ```text
    psql -U my_user
    ```

    如果遇到如下错误：

    ```text
    psql: FATAL: Peer authentication failed for user "my_user"
    ```

    原因：安装完 PostgresQL 后， PostgresQL 连接时的默认认证方式为 peer。官方的解释：
    > The peer authentication method works by obtaining the client’s operating system user name from the kernel and using it as the allowed database user name (with optional user name mapping). This method is only supported on local connections.

    简单翻译：
    > Peer认证方法的工作原理是：从内核中获取客户的操作系统用户名，并将其作为允许的数据库用户名（可选择用户名映射）。这种方法只支持本地连接。

    由于我们登录的Linux系统用户名（即postgres）并不是等于登录PG数据库的用户名（my_user）， 因此出现了以上认证失败的信息。

    **解决方法**：更改配置文件,修改认证方式为md5，即密码认证方式。

    ```text
    sudo vim /etc/postgresql/16/main/pg_hba.conf
    ```

    对于第一条local配置信息，为了意外操作导致默认用户不能登录，所以不建议更换。建议第二个local的认证为md5,替换后的内容如下：
    ![Alt text](assets/PostgreSQL/image-17.png)
    然后重启 PostgreSQL：

    ```text
    sudo service postgresql restart
    ```

10. 重新尝试登录

    直接指定用户名进行登录
    ![Alt text](assets/PostgreSQL/image-18.png)
    会提示数据库不存在
    **注意**：我们必须指定一个数据库（默认情况下，它将尝试将你连接到与登录的用户名相同的数据库）。
    因此我们就用`-d`参数指定数据库，如下：

    ```linux
    postgres@ljt-virtual-machine:/etc/postgresql/16/main$ psql -U my_user -d postgres
    Password for user my_user: 
    psql (16.0 (Ubuntu 16.0-1.pgdg22.04+1))
    Type "help" for help.

    postgres=# 
    ```

    也可在linux下的命令行中直接输入`psql -U my_user -d postgres`，如下：

    ```linux
    postgres=# \q
    postgres@ljt-virtual-machine:/etc/postgresql/16/main$ exit
    exit
    ljt@ljt-virtual-machine:/etc/postgresql/16/main$ psql -U my_user -d postgres
    Password for user my_user: 
    psql (16.0 (Ubuntu 16.0-1.pgdg22.04+1))
    Type "help" for help.

    postgres=# 
    ```

11. 

## 二、 查询

### 1. 图形化SQL查询入口

如图所示：
![PostgreSQL](assets/PostgreSQL/image.png){width=500}
查询实例：
![Alt text](assets/PostgreSQL/image-1.png){width=500}

### 2. 命令行SQL查询入口

如图所示：
![Alt text](assets/PostgreSQL/image-2.png)
查询实例：
![Alt text](assets/PostgreSQL/image-3.png)

linux下的命令行查询入口：
![Alt text](assets/PostgreSQL/image-9.png)


## 三、 远程访问

### 1. 查看主机ip地址

如图所示：

- 主机ip
![Alt text](assets/PostgreSQL/image-4.png){height=500}
- 虚拟机ping主机ip（-c 限定数量，不然会ping不停）
![Alt text](assets/PostgreSQL/image-5.png){width=500}
- 虚拟机ping
![Alt text](assets/PostgreSQL/image-6.png){width=500}
- 主机ping虚拟机ip
![Alt text](assets/PostgreSQL/image-7.png)

### 2. 



在 PostgreSQL 中，我们可以使用 SQL 语句来创建、修改和删除数据库。以下是一些常用的 SQL 命令：

- `CREATE DATABASE dbname;`：创建一个名为 `dbname` 的数据库。
- `DROP DATABASE dbname;`：删除一个名为 `dbname` 的数据库。
- `ALTER DATABASE dbname RENAME TO new_dbname;`：将一个名为 `dbname` 的数据库重命名为 `new_dbname`。

## 表

在 PostgreSQL 中，我们可以使用 SQL 语句来创建、修改和删除表。以下是一些常用的 SQL 命令：

- `CREATE TABLE tablename (column1 datatype1, column2 datatype2, ...);`：创建一个名为 `tablename` 的表。
- `ALTER TABLE tablename ADD COLUMN column datatype;`：向一个名为 `tablename` 的表中添加一个名为 `column` 的列。
- `DROP TABLE tablename;`：删除一个名为 `tablename` 的表。

## 查询

在 PostgreSQL 中，我们可以使用 SQL 语句来查询数据。以下是一些常用的 SQL 命令：

- `SELECT column1, column2, ... FROM tablename;`：查询一个名为 `tablename` 的表中的所有列。
- `SELECT column1, column2, ... FROM tablename WHERE condition;`：查询一个名为 `tablename` 的表中符合条件 `condition` 的所有列。
- `SELECT column1, column2, ... FROM tablename ORDER BY column ASC/DESC;`：查询一个名为 `tablename` 的表中的所有列，并按照 `column` 列进行升序或降序排序。

## 索引

在 PostgreSQL 中，我们可以使用索引来提高查询效率。以下是一些常用的 SQL 命令：

- `CREATE INDEX indexname ON tablename (column);`：在一个名为 `tablename` 的表的 `column` 列上创建一个名为 `indexname` 的索引。
- `DROP INDEX indexname;`：删除一个名为 `indexname` 的索引。

## 总结

在本文中，我们介绍了 PostgreSQL 的基础知识和一些高级概念，包括安装、数据库、表、查询和索引。希望这些内容能够帮助你更好地理解和使用 PostgreSQL。

# do some mark work

## Mac m1 postgresql的安装和使用 
### 利用 homebrew 来安装 postgresql, 此次我选择的是 postgresql@16 版本
#### 1. 安装 
    brew install postgresql@16
#### 2. 环境变量
    echo 'export PATH="/opt/homebrew/opt/postgresql@16/bin:$PATH"' >> ~/.zshrc
#### 3. 编译需要(未做)
    export LDFLAGS="-L/opt/homebrew/opt/postgresql@16/lib"
    export CPPFLAGS="-I/opt/homebrew/opt/postgresql@16/include"
#### 4. 版本检查
    check the version use 'psql --version'
#### 5. 初始化
    initdb /Users/msw/Databases/postgres
#### 6. 默认启动
    brew services start postgresql@16
#### 7. mac安装PostgreSQL后不会创建用户名数据库，
    以当前用户名创建一个数据库
    createdb 
#### 8. 然后登录PostgreSQL控制台：
    登录数据库
    psql

### 创建数据库和用户
#### 一、创建uamself用户
    CREATE USER uamself WITH PASSWORD 'uamself';
#### 二、删除默认生成的postgres数据库
    DROP DATABASE postgres;
#### 三、创建属于uamself用户的postgres数据库
    CREATE DATABASE postgres OWNER uamself;
#### 四、将数据库所有权限赋予uamself用户
    GRANT ALL PRIVILEGES ON DATABASE postgres to uamself;
#### 五、给uamself用户添加创建数据库的属性
    ALTER ROLE uamself CREATEDB;


### PostgreSQL常用指令
#### 通过psql 连接指定的数据库
    psql -U [user] -d [database] -h [host] -p [port]

    -U指定用户，-d指定数据库，-h指定服务器ip默认本地localhost，-p指定端口，默认是5432

#### 完整的登录命令，比如使用postgres用户登录
    psql -U postgres -d postgres

#### 下面是一些比较常用的控制台命令：
 ```
\password：设置当前登录用户的密码
\h：查看SQL命令的解释，比如\h select。
\?：查看psql命令列表。
\l：列出所有数据库。
\c [database_name]：连接其他数据库。
\d：列出当前数据库的所有表格。
\d [table_name]：列出某一张表格的结构。
\du：列出所有用户。
\e：打开文本编辑器。
\conninfo：列出当前数据库和连接的信息。
\password [user]: 修改用户密码
\q：退出
```

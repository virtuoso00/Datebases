# 书店管理系统中的数据库模块

## 1.书店管理系统的简单介绍以及数据库中包含的表的内容：

>书店管理系统调用数据库来存储租赁图书用户的信息，图书的信息以及注册的用户信息。当然此书店管理系统还会记录读者对于一本树各个方面的评价星级，以便于用户搜索某一类型的图书时可以由系统推荐评价星级较高的图书，以便读者租赁和购买。一个简单的书店管理系统包括书店内书籍的信息、注册用户的信息、用户的租赁信息以及用户购买图书的信息。此系统功能分为面向注册用户、面向管理员和面向书店派送员三部分，其中用户可以进行租赁、续租、归还、购买书籍以及查询书籍等操作，管理员可以完成书籍和用户的增加，删除和修改以及对用户租赁、续租、归还、购买的确认、快递公司的派送员可以查看到用户购买和租赁书籍的订单信息并从总中获取用户的姓名、联系电话、以及住址。

## 2. 需求分析：

针对一般书店管理信息系统的需求，通过对书店管理工作过程的内容和数据流程分析，设计如下面所示的数据项：

>注册用户信息

属性：**用户ID**，用户姓名，用户性别，用户电话，用户住址，生效日期，失效日期，违章状况，累计租赁书籍，备注

主键：**用户ID**

>书籍信息

属性：**ISBN**，书名，书籍类型，书籍是否有包装，作者，出版社，出版日期，简介，购买价格，租赁价格，备注

主键：**ISBN**

>管理员信息

属性：**工作号**，姓名，型别，电话，家庭住址，备注

主键：**工作号**

>派送员信息

属性：**派送员编号**，姓名，型别，电话，家庭住址，备注

主键：**派送员编号**

### 2.1 数据流程：

通过对系统的调查和可行性分析，画出系统的数据流程图：

#### 2.1.1 用户

用户对书店管理系统的要求有：

1. 能按各种方式（比如书名、编号、作者，类型）查询书店的藏书情况。
2. 能够方便地租赁图书、续租图书、归还图书、购买图书
3. 能够查询自己的基本资料、图书情况
4. 能够熟悉书店管理系统的使用。

读者进入系统工作的流程图为：

#### 2.1.2 书店管理员

他们对图书管理系统的要求有：

1. 能方便的对图书进行录入登记，注销陈旧的书籍。
2. 能够方便地对用户进行登记，或注销已经近两年未使用的用户信息（基本信息，租赁信息）。
3. 能够随时发布一些诸如租赁图书超期情况、店内书籍情况、租赁情况的信息，以便及时提醒租赁快要超期的用户及时归还或是续租。

书店管理员工作的流程图为:

#### 2.1.3 派送员

他们对图书管理系统的要求有：

1. 能够方便的获得用户的订单情况。（包括购买订单以及租赁订单）。
2. 能够从订单中浏览到用户的姓名，电话，住址。

## 3. 概念模型设计

>数据库需要表述的信息有以下几种：

1. 用户信息
2. 书籍信息
3. 管理员信息
4. 用户与书籍之间的关系(租赁关系及购买关系E-R图)
5. 管理员与书籍之间的关系（管理员_书籍E-R图）
6. 管理员与用户之间的关系（管理员_用户E-R图）

### 3.1 管理员与用户之间的关系

### 3.2 管理员与书刊之间的关系

### 3.3 用户与书籍之间的关系

### 3.4 派送员与用户之间的关系

## 4.逻辑设计

从理论‘E/R模型’到理论‘关系模型’的整理转换，通过E/R模型到关系模型的转化，可以得到如下关系模式：

>租赁关系

属性：**工作号**，**用户ID**，**ISBN**，是否续租，租赁日期，还书日期，备注。

主键：工作号，用户身份证号，**ISBN**

>管理员书籍关系

属性：**工作号**，**ISBN**，添加时间，是否在店。

主键：**工作号**，**ISBN**

>管理员用户关系

属性：**工作号**，**用户ID**，确认租还。

主键：**工作号**，**用户ID**

>订单信息

属性：**订单号**，**用户ID**，**ISBN**，**派送员编号**，用户姓名，书籍名称，派送员姓名，派送员电话，书籍是否有包装，用户电话，用户住址，备注。

主键：**订单号**，**派送员编号**

## 5. 数据库逻辑结构

### 5.1 出售图书信息表 *(BooksForSale)*

|字段名称|数据类型|是否可为空|
|:--------:|:-------:|:--------:|
|**ISBN**|varchar(20)|否|
|书籍名称*(Title)*|varchar(50)|否|
|作者*(Author)*|varchar(12)|否|
|类别*(Catergory)*|varchar(20)|否|
|出版社*(Pub_House)*|varchar(50)|是|
|出版日期*(Pub_Date)*|datetime|是|
|简介*(Intro)*|varchar(200)|是|
|购买价格*(PriceForSell)*|numeric(5,2)|否|
|备注*(Notes)*|varchar(200)|是|

### 5.2 租赁图书信息表 *(BooksForRent)*
|字段名称|数据类型|是否可为空|
|:--------:|:-------:|:--------:|
|**书籍ID** *(BookID)*|varchar(10)|否|
|ISBN|varchar(20)|否|
|租赁价格*(PriceForRent)*|int|否|
|是否可被租阅*(IsAvaliable)*|varchar(2)|否|

### 5.3 用户信息表 *(UserInfo)*

|字段名称|数据类型|是否可为空|
|:------:|:------:|:-------:|
|**用户ID** *(UserID)*|varchar(10)|否|
|用户姓名*(UserName)*|varchar(10)|否|
|密码*(Passwd)*|varchar(16)|否|
|住址*(Addr)*|varchar(100)|否|
|联系电话*(Tele)*|varchar(12)|是|
|注册时间*(SignUpTime)*|datetime|是|
|违章情况*(Violations)*|varchar(2)|是|
|备注*(Notes)*|varchar(100)|是|

### 5.4 管理员信息表 *(AdminInfo)*

|字段名称|数据类型|是否可为空|
|:------:|:------:|:-------:|
|**管理员ID** *(AdminID)*|varchar(12)|否|
|管理员密码*(AdminPasswd)*|varchar(16)|否|
|管理员姓名*(AdminName)*|varchar(12)|否|
|管理员电话*(AdminTele)*|varchar(12)|否|
|备注*(Notes)*|varchar(100)|是|

### 5.5 派送员信息表 *(CourierInfo)*

|字段名称|数据类型|是否可为空|
|:------:|:-----:|:-------:|
|**派送员ID** *(CourierID)*|varchar(12)|否|
|派送员密码*(CourierPasswd)*|varchar(16)|否|
|派送员姓名*(CourierName)*|varchar(12)|否|
|派送员电话*(CourierTele)*|varchar(12)|否|
|备注*(Notes)*|varchar(100)|是|

### 5.6 租赁情况表 *(RentingInfo)*

|字段名称|数据类型|是否可为空|
|:------:|:-----:|:------:|
|管理员ID *(AdminID)*|varchar(12)|否|
|ISBN|varchar(20)|否|
|用户ID*(UserID)*|varchar(10)|否|
|租赁日期*(RentingDate)*|datetime|否|
|还书日期*(DueDate)*|datetime|否|
|备注*(Notes)*|varchar(100)|是|

### 5.7 购买订单信息表 *(PurchasingOrders)*

|字段名称|数据类型|是否可为空|
|:-----:|:-----:|:-------:|
|**订单号** *(OrderID)*|varchar(20)|否|
|派送员ID*(CourierID)*|varchar(12)|否|
|用户ID*(UserID)*|varchar(10)|否|
|ISBN|varchar(20)|否|
|书籍名称*(Title)*|varchar(50)|否|
|购买价格*(PriceForSell)*|numeric(5,2)|否|
|购买日期*(PurchaseDate)*|datetime|否|
|用户姓名*(UserName)*|varchar(10)|否|
|住址*(Addr)*|varchar(100)|否|
|派送员电话*(CourierTele)*|varchar(12)|否|
|备注*(Notes)*|varchar(100)|是|

### 5.8 租赁订单信息表 *(RentingOrders)*
|字段名称|数据类型|是否可为空|
|:-----:|:-----:|:-------:|
|**订单号** *(OrderID)*|varchar(20)|否|
|派送员ID*(CourierID)*|varchar(12)|否|
|用户ID*(UserID)*|varchar(10)|否|
|书籍ID*(BookID)*|varchar(10)|否|
|ISBN|varchar(20)|否|
|书籍名称*(Title)*|varchar(50)|否
|租赁价格*(PriceForRent)*|int|否|
|租赁日期*(RentingDate)*|datetime|否|
|用户姓名*(UserName)*|varchar(10)|否|
|住址*(Addr)*|varchar(100)|否|
|派送员电话*(CourierTele)*|varchar(12)|否|
|备注*(Notes)*|varchar(100)|是|

### 5.9 书籍评价表 *(BookComments)*

|字段名称|数据类型|是否可为空|
|:------:|:-----:|:------:|
|**ISBN**|varchar(20)|否|
|书籍名称*(Title)*|varchar(50))|否|
|内容合理评分*(RationalityScore)*|int|是|
|学术性评分*(AcademicScore)*|int|是|
|语言简洁评分*(SimplicityScore)*|int|是|

## 6. 物理设计

    从理论‘关系模型’到实现/实施‘数据库建立’，物理文件的安排和建立索引

### 6.1 建立索引
>为了提高在表中搜索元组的速度，在实际实现的时候应该基于键码建立索引是各表中建立索引的表项：

1. 用户信息（用户ID）
2. 书籍信息（ISBN，书籍ID）
3. 管理员信息（工作号）
4. 派送员信息（派送员编号）
5. 租赁（工作号，读者学号，书籍ID）
6. 购买书籍订单（订单号）
7. 租赁书籍订单（订单号）
8. 管理员_书籍（工作号，ISBN）
9. 管理员_用户（工作号，用户ID）
10. 用户_派送员（用户ID，派送员编号）

### 6.2 用SQL实现设计
    实现该设计的环境为windows10-MySQL 5.7

```sql
create database BookStoreManagement;
```

#### 6.2.1  建立出售图书信息表

```sql
create table BooksForSale
  (
    ISBN varchar(20) not null primary key,
    Title varchar(50) not null,
    Author varchar(12) not null,
    Catergory varchar(20) not null,
    Pub_House varchar(50),
    Pub_Date datetime,
    Intro varchar(200),
    PriceForSell numeric(5,2) not null,
    Notes varchar(100),
  );
```

#### 6.2.2 建立租赁图书信息表

```sql
create table BooksForRent
  (
    BookID varchar(10) not null primary key,
    ISBN varchar(20) not null,
    IsAvaliable varchar(2) not null
    PriceForRent int not null,
    foreign key(ISBN) references BooksForSale
  );
```

#### 6.2.3 建立用户信息表

```sql
create table UserInfo
  (
    UserID varchar(10) not null primary key,
    UserName varchar(10) not null,
    Passwd varchar(16) not null,
    Addr varchar(100) not null,
    Tele varchar(12) not null,
    SignUpTime datetime,
    Violations varchar(2),
    Notes varchar(100)
  );
```

#### 6.2.4 建立管理员信息表

```sql
create table AdminInfo
  (
    AdminID varchar(12) not null primary key,
    AdminPasswd varchar(16) not null,
    AdminName varchar(12) not null,
    AdminTele varchar(12) not null,
    Notes varchar(100)
  );
```

#### 6.2.5 建立派送员信息表

```sql
create table CourierInfo
  (
    CourierID varchar(12) not null primary key,
    CourierPasswd varchar(16) not null,
    CourierName varchar(12) not null,
    CourierTele varchar(12) not null,
    Notes varchar(100)
  );
```

#### 6.2.6 建立租赁情况表

```sql
create table RentingInfo
  (
    AdminID varchar(12) not null primary key,
    ISBN varchar(20) not null,
    UserID varchar(10) not null,
    RentingDate datetime not null,
    DueDate datetime not null,
    Notes varchar(100)
    foreign key(AdminID) references AdminInfo,
    foreign key(ISBN) references BooksForSale,
    foreign key(UserID) references UserInfo
  );
```

#### 6.2.7 建立购买订单信息表

```sql
create table PurchasingOrders
  (
    OrderID varchar(20) not null,
    CourierID varchar(12) not null,
    UserID varchar(10) not null,
    ISBN varchar(20) not null,
    Title varchar(50) not null,
    PriceForSell numeric(5,2) not null,
    PurchaseDate datetime not null,
    UserName varchar(10) not null,
    Addr varchar(100) not null,
    CourierTele varchar(12) not null,
    Notes varchar(100),
    primary key(订单号),
    foreign key(CourierID) references CourierInfo,
    foreign key(UserID) references UserInfo,
    foreign key(ISBN) references BooksForSale
  );
```

#### 6.2.8 建立租赁信息订单表

```sql
create table RentingOrders
  (
    OrderID varchar(20) not null,
    CourierID varchar(12) not null,
    UserID varchar(10) not null,
    BookID varchar(10) not null,
    ISBN varchar(20) not null,
    Title varchar(50) not null,
    PriceForRent int not null,
    RentingDate datetime not null,
    UserName varchar(10) not null,
    Addr varchar(100) not null,
    CourierTele varchar(12) not null,
    Notes varchar(100),
    primary key(OrderID),
    foreign key(CourierID) references CourierInfo,
    foreign key(UserID) references UserInfo,
    foreign key(BookID) references BooksForRent,
    foreign key(ISBN) references BooksForSale
  );
```

#### 6.2.9 建立书籍评价表

```sql
create table BookComments
  (
    ISBN varchar(20) not null primary key,
    Title varchar(50) not null,
    RationalityScore int,
    AcademicScore int,
    SimplicityScore int,
    foreign key(ISBN) references BooksForSale
  );
```

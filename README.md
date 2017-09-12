# 面向对象的程序设计 ——  图书管理系统
---
## 一．需求分析：
针对图书馆的使用情况来看，图书管理系统存在三个主要需求:
1. 账号的注册，登陆与注销。
2. 读者如何借书与还书。
3. 管理员如何管理书籍。

根据以上需求，将设计一个图书管理系统。本系统旨在实现一个小型的图书管理系统，对于一个小型的图书馆或藏书室来说，实施本系统不仅可以减少工作人员数量，降低成本，而且可以大大提高工作效率，降低工作强度，方便读者借书查书及办理各种手续，更方便工作人员对图书进行更有效的管理。

---

## 二．程序的主要功能：
* 管理员功能：管理员可以注册其他管理员账号，修改密码，注销账号。可查找书籍，并且查看书籍信息。可增加，删除书籍。
* 读者功能：读者可以自主注册，修改密码，注销账号，查看账户信息。可查找书籍，并且查看书籍信息。可在线借阅，归还书籍。

---

## 三．程序运行平台：
>Visual Studio 2017

---

## 四．系统功能框架图：
![流程图](<div align=center>http://chuantu.biz/t6/46/1505204541x607756861.png</div>)

---

## 五．程序类说明：
本程序采用了面向对象的程序设计，系统面向2个对象：读者和管理员。
本程序以读者和管理2个对象为基本框架，设计了4个模块：
### 1.对象。包含了4个对象：
* 2个基类：*class Book* 和*class User*。
* 2个由基类派生出的派生类：*class Reader* 和*class Administrator*。

1. *class Book* 包含了2个功能函数：
* `void FindBook()`：查找书籍
* `void PrintBook(streampos pos)`：输出书籍信息

2. *class User* 包含了4个功能函数：
* `void Register(const string sign)`：注册账号
* `int Login(const string sign)`：登陆账号
* `void ChangePassword(const string sign)`：修改密码
* `void LogOff(const string sign)`：注销账号

3. *class Reader :public Book, public User* 包含了3个功能函数：
* `void ShowProfile()`：显示账户借阅书籍信息
* `void BorrowBook()`：借书
* `void ReturnBook()`：还书

4. *class Administrator :public Book, public User* 包含了2个功能函数：
* `void AddBook()`：新增书籍
* `void DeleteBook()`：删除书籍

### 2. 初始函数：
* `int main()`：主函数
* `void Initializate()`：初始化系统文件
* `int RegisterOrLogin()`：显示初始界面

### 3.对象功能函数：
* `void ReaderFunction(int n)`：显示读者界面
* `void AdministratorFunction()`：显示管理员界面

### 4.接口函数：
将需要多次调用的功能函数提取出来，使用包括统一接口，函数重载等方式来优化代码结构，以减少代码的冗余：
* `int IsLegal(string s)`；
* `streampos CheckAccount(string s, const string sign)`；
* `int CheckPassword(string s, const string sign, streampos pos)`；
* `streampos GetBook(long n)`；
* `streampos GetBook(int n, string s)`；
* `long ChangeBookNumber(long n)`；

---

## 六．程序说明文档：
### 文件存储格式（粗体表示变量）：

1. 用户和管理员账号（readers.bin 和 administrations.bin）：
* 可用：#**account**.**password***
* 不可用：* **account**.**password***

2. 书籍信息文件（books.bin）：
* **number of books**+**bookinfo**
* 其中**bookinfo**的格式为：
* 可用：#**serial number**@**ISBN**&**name**+**author**-**remainingnumber**
* 不可用：***serial number**@**ISBN**&**name**+**author**-**remainingnumber**

3. 用户信息文件（#**account**.bin）：
* **number of borrowing**#**serial number of book**

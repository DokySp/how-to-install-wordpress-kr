## 워드프레스를 위한 데이터베이스 생성하기

[원문](https://wordpress.org/support/article/creating-database-for-wordpress/)

여러분 자신의 웹서버에 워드프레스를 설치하는 경우, 아래의 방법들 중 한 가지를 따라서 워드프레스 데이터베이스와 user 계정을 생성하세요.


#### Plesk를 사용할 경우 **(번역X)**
> If your hosting provider supplies the Plesk hosting control panel and you want to install WordPress manually, follow the instructions below to create a database:
> 
> 1. Log in to Plesk.
> 1. Click Databases in the Custom Website area of your website on the Websites & Domains page:
> ![Plesk custom website databases](https://i1.wp.com/wordpress.org/support/files/2018/11/plesk-db.png?resize=768%2C558&ssl=1)
> 3. Click Add New Database, change database name if you want, create database user by providing credentials and click OK. You’re done!

#### cPanel을 사용할 경우 **(번역X)**
> If your hosting provider supplies the cPanel hosting control panel, you may follow these simple instructions to create your WordPress username and database. A more complete set of instructions for using cPanel to create the database and user can be found in Using cPanel.
> 
> 1. Log in to your cPanel.
> 1. Click MySQL Database Wizard icon under the Databases section.
> 1. In Step 1. Create a Database enter the database name and click Next Step.
> 1. In Step 2. Create Database Users enter the database user name and the password. Make sure to use a strong password. Click Create User.
> 1. In Step 3. Add User to Database click the All Privileges checkbox and click Next Step.
> 1. In Step 4. Complete the task note the database name and user. Write down the values of hostname, username, databasename, and the password you chose. (Note that hostname will usually be localhost.)

#### Lunarpages.com의 커스텀 cPanel을 사용할 경우(LPCP) **(번역X)**
> Lunarpages has developed their own version of cPanel.
> 
> 1. Log in to your account.
> 2. Go to Control Panel.
> 3. Click on the button on the left panel labeled ‘Go to LPCP’.
> 4. Go to MySQL Manager.
> 5. Add the user name and database name but leave the host name as the default IP number.
> 5. Note the IP address of the database on the right which is different from the default IP number of the host indicated in the above step.
> 5. When modifying the wp-config.php file, use the DB IP number, not ‘LOCALHOST’.
> 5. When modifying the wp-config.php file, be sure to use the full name of the database and user name, typically ‘accountname_nameyoucreated’.
> 5. Refer to http://wiki.lunarpages.com/Create_and_Delete_MySQL_Users_in_LPCP for more info.


#### phpMyAdmin을 사용할 경우

여러분의 웹서버에 [phpMyAdmin](https://wordpress.org/support/article/glossary/#phpmyadmin)이 설치되어있다면, 이 설명서를 따라 워드프레스를 위한 데이터베이스와 username을 생성할 수 있습니다. 참고로, 대부분의 리눅스 배포판에서 자동으로 PhpMyAdmin을 설치할 수 있습니다.

***참고:*** *이 설명서는 phpMyAdmin 4.4 기준으로 작성되었습니다. phpMyAdmin 설정 화면이 버전별로 살짝 다를 수 있습니다.*


1. 좌측 드롭다운 메뉴에 **워드프레스와 관련된 데이터베이스가 생성되지 않았다면**, 새로 데이터베이스를 생성합니다.
  1. 데이터베이스의 이름을 선택합니다. `wordpress` 혹은 `blog` 같은 이름이 좋습니다. 그러나 대부분의 호스팅 업체들이 여러분의 계정명과 언더바(_)로 시작하는 것을 요구할 것입니다. 따라서 여러분 컴퓨터에서 작업을 진행하더라도, 여러분의 서버가 호스팅 업체의 규칙을 따를 수 있도록 해서 생성한 데이터베이스가 별도의 수정 없이 호스팅 업체로 전환될 수 있도록 하게 하기 위해서 사용하는 호스팅 업체에서 데이터베이스 이름에 대한 요구사항을 직접 확인할 것을 권장합니다. **Create database** 칸에 데이터베이스 이름을 입력하고 여러분이 사용하는 최적의 언어와 인코딩 조합을 선택하세요. 대부분의 경우, "utf8\_"시리즈를 선택하는데, 여러분 언어에 최적화된 인코딩을 찾을 수 없다면 "utf8mb4\_general\_ci"를 선택하세요. ([해당 문서](https://make.wordpress.org/core/2015/04/02/the-utf8mb4-upgrade/) 참고)

  > **_각주:_** <br>
  > 한국어의 경우, "utf8mb4\_general\_ci"를 사용하면 됩니다. (이모지까지 지원한다네요!)

![phpMyAdmin language encoding drop down](https://i0.wp.com/wordpress.org/support/files/2018/11/phpMyAdmin_create_database_4.4.jpg?w=688&ssl=1)

2. 좌측 상단에 **phpMyAdmin** 아이콘을 클릭하여 메인페이지로 이동한 후에, **Users** 탭을 클릭합니다. 워드프레스와 연관된 user가 리스트에 없다면 새로 생성합니다: 
![phpMyAdmin Users Tab](https://i1.wp.com/wordpress.org/support/files/2018/11/users.jpg?resize=768%2C500&ssl=1)

  1. **Add user**를 클릭합니다.
  2. 워드프레스에서 사용할 username('`wordpress`'를 추천)을 **User name** 칸에 입력합니다. (드롭다운 메뉴에 **Use text field**가 체크되어있어야 합니다!)
  3. 안전한 비밀번호(영어 대소문자, 숫자, 특수기호 사용 권장)를 **Password** 칸에 입력합니다. (드롭다운 메뉴에 **Use text field**가 체크되어있어야 합니다!) 그리고 **Re-ypte** 칸에 입력한 비밀번호를 한 번 더 입력합니다.
  4. username과 비밀번호를 입력합니다.
  5. **Global privileges** 설정을 기본 옵션 그대로 둡니다.
  6. **Go** 버튼을 누릅니다.
  7. **User** 화면으로 돌아와 방금 생성한 계정에 있는 **Edit privileges** 아이콘을 클릭합니다.
  8. **Database-specific privileges** 섹션에서 **Add privileges to the following database** 드롭다운에 방금 생성한 데이터베이스를 선택한 후, **Go** 버튼을 누릅니다.
  9. 페이지와 선택한 데이터베이스의 권한이 새로 고침 됩니다. **Check All** 버튼을 눌러 모든 권한을 선택하고 **Go** 버튼을 누릅니다.
  10. 결과 페이지에서, 페이지 상단에 호스트 이름이 **Server:** 뒤에 잘 표시되는지 확인하세요. (아마 대부분 **localhost**일 것입니다.)
![phpMyAdmin03](https://i2.wp.com/wordpress.org/support/files/2018/11/phpMyAdmin_server_info_4.4.jpg?w=682&ssl=1)


#### CLI환경의 MySQL Client를 사용할 경우

쉘을 통해 MySQL에서 users와 databases를 생성할 수 있습니다. 아래 쉘스크립트를 쉘에 ~~(복붙)~~사용하면 빠르게 생성됩니당.

```shell
# <- 이 샾이 앞에 있으면 주석이란 뜻입니다.
# 그러니 주석을 쉘에 넣으면 안되겠죠..?
# $ 기호도 쉘을 표현한 기호이므로 아래 mysql -u 철수 -p만 복붙하시면 됩니당.
# mysql>도 MySQL 인터프리터(?) 표시이므로 그 뒤에만 복붙합니다.


# DBMS(MySQL) 접속
$ mysql -u 철수 -p 
# '철수'는 예시 관리자계정이름(username)입니다. (MySQL 계정 설정법은 아래에 있습니다!)
# 이 다음에 Enter password: 가 나오면 해당 계정 비밀번호를 입력합니다.


# Database 생성하기
mysql> CREATE DATABASE wordpress;
## 마찬가지로 wordpress도 예시의 DB 이름입니다. (밑에도 설명하겠지만, wordpress가 권장하는 DB이름입니다..)
# Query OK, 1 row affected (0.00 sec)
## 정상적으로 수행되었다면, 위와 같은 메시지가 뜹니다.


# Database 권한 부여
mysql> GRANT ALL PRIVILEGES ON wordpress.* TO "철수"@"hostname" IDENTIFIED BY "철수의 비밀번호";
## asdf 사용자에게 qwer DB의 읽기쓰기 권한을 주는 것입니다.
# Query OK, 0 row affected (0.00 sec)
## 정상적으로 수행되었다면, 위와 같은 메시지가 뜹니다.


# 권한 설정 Flush
mysql> FLUSH PRIVILEGES;
## 설정한 권한을 적용하는 겁니다.
# Query OK, 0 row affected (0.00 sec)
## 정상적으로 수행되었다면, 위와 같은 메시지가 뜹니다.]


# DBMS 접속 끊기
mysql> EXIT
## 뭐 더 설명이 필요할까요? ㅋ

```



- `root` 계정을 Wordpress DB 관리 계정으로 사용할 수도 있습니다만..  시스템 root 유저로 mysql 권한을 갖지 않도록 root 계정이 아닌 계정을 mysql admin 계정으로 사용하는 것이 안전합니다. (작업할 때, 루트로 작업하는 것을 최소화한다면 DB를 털릴 가능성을 줄일 수 있습니다.)
- `wordpress` 혹은 `blog`를 DATABASE 이름으로 설정하시길 권장합니다.
- *워드프레스 `username`*으로 `wordpress`를 설정하길 권장합니다...**만**, 이걸 보고 아마 전세계 대부분 사람들이 이름을 `wordpress`로 설정할 수 있다는 점을 유념하시길 바랍니다.
  - `hostname`은 거의 `localhost`일겁니다. 만약 호스트 이름이`localhost`가 아닌데 값을 모를 경우에는, 당신의 시스템 관리자와 함께 확인하십시오 당신이 당신 wordpress의 관지라가 아닌지를. 반대로 당신이 관리자라면, MySQL 접속 계정이 `root`가 아닌 일반 계정을 사용하고 있는지 확인해야 합니다.
- *비밀번호*는 반드시 복잡하고 유추하기 어려워야 합니다. (영어 대문자, 소문자, 숫자, 기호를 섞어 쓰기를 권장합니다.) 일반적인 단어를 안쓰도록 하기 위해 문장의 초성만 따서 비번을 설정하는 방법을 쓰면 좋습니다. ~~(초성놀이)~~


#### DirectAdmin을 사용하는 경우 **(번역X)**
> a. If you’re a regular User of a single-site webhosting account, you can log in normally. Then click MySQL Management. (If this is not readily visible, perhaps your host needs to modify your “package” to activate MySQL.) Then follow part “c” below.
> 
> b. Reseller accounts Admin accounts may need to click User Level. They must first log in as Reseller if the relevant domain is a Reseller’s primary domain… or log in as a User if the domain is not a Reseller’s primary domain. If it’s the Reseller’s primary domain, then when logged in as Reseller, simply click User Level. However if the relevant domain is not the Reseller’s primary domain, then you must log in as a User. Then click MySQL Management. (If not readily visible, perhaps you need to return to the Reseller or Admin level, and modify the “Manage user package” or “Manage Reseller package” to enable MySQL.)
> 
> c. In MySQL Management, click on the small words: Create new database. Here you are asked to submit two suffixes for the database and its username. For maximum security, use two different sets of 4-6 random characters. Then the password field has a Random button that generates an 8-character password. You may also add more characters to the password for maximum security. Click Create. The next screen will summarize the database, username, password and hostname. Be sure to copy and paste these into a text file for future reference.
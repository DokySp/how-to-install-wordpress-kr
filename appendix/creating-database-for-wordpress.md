## 워드프레스를 위한 데이터베이스 생성하기

[원문](https://wordpress.org/support/article/creating-database-for-wordpress/)

#### CLI환경의 MySQL Client를 사용할 경우

쉘을 통해 MySQL 또는 MariaDB에서 `users`와 `databases`를 생성할 수 있습니다. 아래 쉘스크립트를 쉘에 ~~(복붙)~~사용하면 빠르게 생성됩니당.

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


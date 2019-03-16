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

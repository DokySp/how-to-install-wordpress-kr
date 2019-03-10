# WordPress 설치하기

- 출처: [WordPress.org](https://codex.wordpress.org/Installing_WordPress)
- 한글작성자: 김도균
- 작성일: 2019월 2월 8일



## 목차

- [WordPress 설치 전 필요한 것들](#things-to-know-before-installing-wordpress)
- [가장 많이 쓰이는 5분 설치법](#famous-5-minute-installation)
- [상세한 설치법](#detailed-instructions)
- [NGINX 세팅하기](#configure-nginx)



## Things to Know Before Installing WordPress

#### WordPress 설치 전 필요한 것들

1. 서버 환경이 다음 조건을 만족하는지 확인
   - `PHP 7.3` 이상
   - `MySQL 5.6` 혹은 `MariaDB 10.0` 이상
   - HTTPS 지원
   - 웹 서버 프로그램: `nginx` 또는 `apache` 환경에서 가장 최적하게 동작함.
2. 최신버전 WordPress 다운로드

> https://wordpress.org/download/

3. 다운로드파일 압축해제 (`tar.gz` 혹은 `zip`파일)
4. 비밀키를 위한 안전한 비밀번호 생각하기 (`wp-config.php` 파일 편집 시 필요)



## Famous 5-Minute Installation

#### 가장 많이 쓰이는 5분 설치법

간단한 설명으로도 설치가 가능한 분들을 위한 퀵 버전 설명서입니다. 자세한 설명은 [상세한 설치법](#detailed-instructions)을 참고하세요.

**유닉스, 리눅스 기반 OS에서 파일 이름을 바꾸는게 익숙치 않으신 분들은 Step2를 반드시 하지 않으셔도 됩니다.** 설치프로그램이 자동으로 wp-config.php파일을 생성하므로 Step3를 그냥 넘어가셔도 됩니다.

0. (안한 사람들)WordPress 파일 압축 해제
1. `MySQL` (혹은 `MariaDB`)에 데이터베이스를 생성. 이 때 생성한 데이터베이스에 **읽기 및 쓰기 권한을 모두에게 풀 것.** ([MySQL 데이터베이스 생성 명령어](https://codex.wordpress.org/Installing_WordPress#Using_the_MySQL_Client))
2. *(Optional)* `wp-config-sample.php` 파일을 `wp-config.php`로 바꾸기. 그리고 나서 파일을 다음 설명에 맞추어 수정하고, Step1에서 생성한 데이터베이스 정보 기입.
3. WordPress파일을 원하는 위치에 옮기기.
   - 만약 루트 도메인에 워드프레스를 연결시킬 경우(https://www.example.com/), 모든 파일을 압축 해제 후 안의 내용물을 전부 루트 디렉토리에 넣을 것.
   - 만약 서브디렉토리에 넣을 경우(예시로 https://www.example.com/blog), blog 폴더를 생성하고, 모든 파일을 압축 해제 후 안의 내용물을 전부 blog 폴더에 넣을 것.
   - 만약 FTP프로그램을 사용하고, 강제로 알파벳을 소문자로 만들 경우, 소문자로 만드는 기능을 해제할 것!
4. ~~런~~ 홈페이지에 접속하여 설치를 계속할 것.

이게 끝이랍니다!



## Detailed Instructions

#### 상세한 설치법

### Step 1. 다운로드 및 압축 해제

WordPress패키지를 [여기](https://wordpress.org/download/)에서 다운로드 받은 후, 압축을 풉니다.

- 워드프레스를 원격 웹서버에 업로드할 경우엔, 작업용 컴퓨터에 워드프레스 패키지를 받은 후에 압축을 푸세요.

- FTP를 사용한다면, Step 2를 건너뛰세요. (파일 업로드는 나중에 다룹니다.)

- 만약 FTP가 아닌 쉘을 통해 웹서버에 엑세스하고, CLI환경에 익숙하신 분이라면, wget(혹은 lynx 또는 콘솔환경에서 쓰이는 웹브라우저)을 사용하십시오.

  - `wget https://wordpress.org/latest.tar.gz/`

  - 그리고 패키지를 다음 명령으로 압푹을 푸세요.

    `tar -xzvf latest.tar.gz`

    > 참고: tar **-z** 옵션은 gzip으로 압축된 파일을 풀어준다.



위 명령어대로 진행하면 다운로드 받은 압축파일이 해당 경로에 `wordpress`폴더로  풀립니다. 



### Step 2. DB 및 DB유저 생성

만약 호스팅 업체를 사용하고 있으시다면, 호스팅 업체에서 Wordpress 데이터베이스 세팅이 되어 있거나 자동으로 데이터베이스를 세팅할 수 있도록 할겁니다.(아니라면.. 흠...) 호스팅 업체의 홈페이지를 살펴보며, 데이터베이스 설정을 수동으로 진행해야 하는지를 확인해보십시오. 



만약 수동으로 데이터베이스를 생성해야 한다면, 다음 설명서를 따라 진행하십시오.

- [phpMyAdmin 엑세스하기](https://codex.wordpress.org/WordPress_Backups#Accessing_phpMyAdmin)
- [Plesk로 설정하기](https://codex.wordpress.org/Installing_WordPress#Using_Plesk)
- [cPannel로 설정하기](https://codex.wordpress.org/Installing_WordPress#Using_cPanel)
- [phpMyAdmin으로 설정하기](https://codex.wordpress.org/Installing_WordPress#Using_cPanel)

> 참고1: 위에 문서들은 GUI를 이용해서 DB 생성 및 사용자 설정을 하는 과정입니다. Wordpress에 글을 올리거나, 댓글을 달거나 등의 다양한 정보들을 관리하는 저장소를 생성한다고 생각하심 됩니다.
>
> 참고2: GUI로 생성하는 과정은 따로 번역하지 않겠습니다..ㅎㅎ ~~(절대 귀찮아서가 아닙ㄴ..)~~ 저것까지 번역하는건 Toooo Much 인듯 합니다...ㅎ



만약 Wordpress를 내 웹서버에 설치하는 경우, 다음 설명서 중 하나를 따라서 진행하십시오.

- phpMyAdmin이 설치되어 있는 경우, [phpMyAdmin 엑세스하기](https://codex.wordpress.org/WordPress_Backups#Accessing_phpMyAdmin)를 참고하세요. (원문)

- MySQL Client가 설치되어 있는 경우, [아래](#Using the MySQL Client) 설치법을 참고하면 됩니다. (번역해둠!)



만약 구축하려는 서버에서 오직 하나의 데이터베이스를 사용하고 있는데(!) 이미 사용하고 있다면(!!) 워드프레스를 그냥 안에 설치할 수 있습니다(!!!)

다만 DB Table끼리 구별 가능한 접두어(prefix)를 두어 기존 데이터를 덮어쓰지 않도록 방지할 수 있도록 하면 됩니다.

> 원문은 이렇게 되어 있는데.. 구체적인 방법은 모르겠고,, 여건이 된다면 추천하지는 않는 방법입니다.. (만에하나 작업하다 실수로 날리거나 덮어쓰면... Holy...)



#### Using the MySQL Client

쉘을 통해 MySQL 또는 MariaDB에서 `users`와 `databases`를 생성할 수 있습니다. 아래 쉘스크립트를 쉘에 사용~~(복붙)~~하면 빠르게 생성됩니당.

```shell
# <- 이 샾이 앞에 있으면 주석이란 뜻입니다.
# 그러니 주석을 쉘에 넣으면 안되겠죠..?
# $ 기호도 쉘을 표현한 기호이므로 아래 mysql -u 철수 -p만 복붙하시면 됩니당.
# mysql>도 MySQL 인터프리터(?) 표시이므로 그 뒤에만 복붙합니다.


# DBMS(MySQL) 접속
$ mysql -u 철수 -p 
# asdf는 예시 관리자계정이름입니다. (MySQL 계정 설정법은 아래에 있습니다!)
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





------

작성중입니다!!

## Configure Nginx

#### NGINX 세팅하기

```
server {
    listen       80;
    server_name  localhost;
 
    root   /usr/share/nginx/html;
    location / {
        index.php index  index.html index.htm;
        try_files $uri $uri/ =404;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
 
    location ~ \.php$ {
        try_files $uri =404; 
        fastcgi_pass   unix:/run/php/php7.2-fpm.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
 
    location ~ /\.ht {
        deny  all;
    }
}
```


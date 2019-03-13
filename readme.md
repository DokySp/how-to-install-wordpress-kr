# WordPress 설치하기

- 출처: [WordPress.ORG](https://codex.wordpress.org/Installing_WordPress)
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

ㅁㄴㅇㄹ



#### Using DirectAdmin

a. 귀찮앙



### Step 3: wp-config.php 설정하기

`wp-config.php`파일을 직접 생성하여 만들거나, 이번 단계를 건너 뛰고 [Step 5]()에서 WordPress 설치 스크립트가 스스로 설정하도록 하는 두 방법이 있습니다. (대신 어느 방법이나 Step 2에서 설정한 DB 관련 정보들을 알고 있어야 합니다.)



(설정파일과 비밀번호 보안을 위한 비밀키 생성에 대해 더 자세하고 구체적인 설명은 다음 링크를 참고하시면 됩니다. [Editing wp-config.php](https://codex.wordpress.org/Editing_wp-config.php))



Step 1에서 다운로드하고 압축을 푼 Wordpress 폴더 안에,  `wp-config-sample.php` 파일을 `wp-config.php` 로 이름을 바꾸시기 바랍니다. 그리고 파일을 연 후, 아래 [데이터베이스 정보들을 수정](https://codex.wordpress.org/Editing_wp-config.php#Configure_Database_Settings)합니다.

```shell
$ mv wp-config-sample.php wp-config.php
$ vim wp-config.php   # nano 같은 다른 편집기를 사용하셔도 됩니다.
```



```
 // ** MySQL settings - 웹호스팅 업체에서 다음 정보들을 확인할 수 있습니다. ** //
```

- DB_NAME 

  Step 2에서 만들었던 DB 이름을 작성합니다.

- DB_USER 

  Step 2에서 만들었던 `username`을 작성합니다.

- DB_PASSWORD 

  Step 2에서 만들었던 `username`에 대한 비밀번호를 적습니다.

- DB_HOST 

  Step 2에서 만들었던 `'username'@'localhost'`에서 @ 뒷 부분을 적습니다 (대부분은 `localhost`겠지만 아닐 수도 있습니다. [이것](https://codex.wordpress.org/Editing_wp-config.php#Possible_DB_HOST_values)들 중 하나일 수 있으니 참고 바랍니다). 포트, 소켓, 파이프가 필요한 경우, 콜론(`:`)을 붙인 후 관련 정보들을 기입하세요.

- DB_CHARSET 

  DB의 charset을 입력합니다. (한국어 포함) 굳이 바꾸실 필요는 없습니다([Editing wp-config.php](https://codex.wordpress.org/Editing_wp-config.php) 참조).

- DB_COLLATE 

  DB collation(정렬)은 일반적으로 빈칸으로 둡니다([Editing wp-config.php](https://codex.wordpress.org/Editing_wp-config.php) 참조).

섹션 라벨 밑 부분에 [secret key 값들을 입력](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys)합니다. (이건 필수는 아닌듯 합니다..)

```
  * Authentication Unique Keys.
```

모든 수정이 끝나면 `wp-config.php` 파일을 저장합니다.

```shell
# vim의 경우,
:wq
```





### Step 4: 파일 업로드하기

이제 Wordpress를 홈페이지 도메인에서 어디에 설치할지를 결정해야 합니다.

- **루트(최상위) 디렉토리**에 설치하는 경우. (ex> `https://www.myblog.com/`)

- **서브 디렉토리**에 설치하는 경우. (ex> `https://www.myblog.com/blog/`)

***참고:** 서버 컴퓨터에서 홈페이지 루트 디렉토리가 있는 위치는 서버 시스템 혹은 서비스 제공자에 따라 다릅니다. 이 위치를 모를 경우 호스팅 업체 혹은 시스템 관리자에게 확인을 해야 합니다.*

```shell
# ubuntu + nginx의 경우(둘 중 하나),
/usr/share/nginx/http
/var/www/html

# ubuntu + apache의 경우, 
/var/www/html
```



#### 루트(최상위) 디렉토리에 설치하는 경우

- If you need to upload your files to your web server, use an [FTP](https://codex.wordpress.org/Glossary#FTP) client to upload all the *contents* of the `wordpress` directory (but not the directory itself) into the root directory of your website.
- If your files are already on your web server, and you are using [shell](https://codex.wordpress.org/Glossary#Shell) access to install WordPress, move all of the *contents* of the `wordpress` directory (but not the directory itself) into the root directory of your website.

#### 서브 디렉토리에 설치하는 경우

- If you need to upload your files to your web server, rename the `wordpress` directory to your desired name, then use an [FTP](https://codex.wordpress.org/Glossary#FTP)client to upload the directory to your desired location within the root directory of your website.
- If your files are already on your web server, and you are using [shell](https://codex.wordpress.org/Glossary#Shell) access to install WordPress, move the `wordpress` directory to your desired location within the root directory of your website, and rename the directory to your desired name.

***Note:** If your FTP client has an option to convert file names to lower case, make sure it's disabled.*



### Step 5: 설치 스크립트 실행

Point a web browser to start the installation script.

- If you placed the WordPress files in the root directory, you should visit: `http://example.com/wp-admin/install.php`
- If you placed the WordPress files in a subdirectory called `blog`, for example, you should visit: `http://example.com/blog/wp-admin/install.php`



#### 설정파일 설치

If WordPress can't find the `wp-config.php` file, it will tell you and offer to try to create and edit the file itself. (You can also do this directly by loading `wp-admin/setup-config.php` in your web browser.) WordPress will ask you the database details and write them to a new `wp-config.php` file. If this works, you can go ahead with the installation; otherwise, go back and [create, edit, and upload the `wp-config.php` file yourself (step 3)](https://codex.wordpress.org/Installing_WordPress#Step_3:_Set_up_wp-config.php).

[![install-step3.png](https://codex.wordpress.org/images/thumb/5/5a/install-step3.png/600px-install-step3.png)](https://codex.wordpress.org/File:install-step3.png)



#### 설치 마무리

The following screenshots show how the installation progresses. Notice that in entering the details screen, you enter your site title, your desired user name, your choice of a password (twice), and your e-mail address. Also displayed is a check-box asking if you would like your blog to appear in search engines like Google and Technorati. Leave the box unchecked if you would like your blog to be visible to everyone, including search engines, and check the box if you want to block search engines, but allow normal visitors. Note all this information can be changed later in your [Administration Screens](https://codex.wordpress.org/Administration_Screens).

[![install-step5.png](https://codex.wordpress.org/images/thumb/1/1b/install-step5.png/600px-install-step5.png)](https://codex.wordpress.org/File:install-step5.png)

**Note: You should not use "admin" as a user id as shown above!**

If you successfully install the WordPress, login prompt will be displayed.



#### 설치 스크립트 문제해결

- 만약 설치 스크립트 동작 중 DB 관련 에러가 난다면:

  - [Step 2](https://codex.wordpress.org/Installing_WordPress#Step_2:_Create_the_Database_and_a_User)와 [Step 3](https://codex.wordpress.org/Installing_WordPress#Step_3:_Set_up_wp-config.php)로 되돌아간 후, `wp-config.php`파일에 모든 정보를 올바르게 적었는지 확인합니다.

  - **Step 3**에서 DB user에게 DB권한을 설정했는지 확인합니다.

  - DB 서버가 제대로 작동하고 있는지 확인합니다.

    ```shell
    $ sudo service mysql restart
    ```



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

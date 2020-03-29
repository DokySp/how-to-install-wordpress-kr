# WordPress 설치하기

- 출처: [wordpress.org](https://wordpress.org/support/article/how-to-install-wordpress/)
- 번역: 김도균([@DokySp](https://github.com/dokysp))
- 작성일: 2019월 2월 8일



## 목차

- [간단 설치법](#간단-설치법)
- [상세 설치법](#상세-설치법)
- [NGINX 세팅하기](./appendix/setting-nginx.md)


## 워드프레스 설치하기
워드프레스는 설치가 쉬운 것으로 잘 알려져 있습니다. 대부분의 상황에서, 워드프레스 블로그 설치는 괭장히 간단하며, 5분 안에 모두 설치를 하실 수 있습니다. [많은 웹 호스팅 업체]가 [워드프레스 자동 설치(Fantastico 등) 도구]를 지원합니다. 그러나, 워드프레스를 직접 설치하실 경우, 이 가이드가 도움이 될것입니다.

#### WordPress 설치 전 확인할 사항

워드프레스를 설치하기 전에, 몇 가지 진행하셔야 할 것들이 있습니다. [워드프레스 설치 전에](./appendix/before-you-install.md)문서를 참고하세요.
만약, 여러 개의 워드프레스 인스턴스가 필요한 경우, [여러 개 워드프레스 인스턴스 설치하기(영문)](https://wordpress.org/support/article/installing-multiple-blogs/)문서를 참고하세요.


## 간단 설치법

이미 워드프레스를 설치해본 경험이 있는 분들을 위한 간단 설치 설명서입니다. 자세한 설명은 [상세 설치법](#상세-설치법)을 참고하세요.

1. [WordPress 파일 다운로드](https://wordpress.org/download/) 및 압축을 풉니다.
2. [`MySQL`](https://wordpress.org/support/article/glossary/#mysql) (혹은 `MariaDB`)에 데이터베이스를 생성하세요. 이 때 생성한 데이터베이스에 **모든 사용자에게 읽기 및 쓰기 권한을 주도록 설정하세요.**
3. *(Optional)* `wp-config-sample.php` 파일을 `wp-config.php`로 바꾸세요. 그리고 나서 파일을 다음 설명에 맞추어 수정하고([wp-config.php 파일 수정하기(영문)](https://wordpress.org/support/article/editing-wp-config-php/) 문서 참고), Step1에서 생성한 데이터베이스 정보 기입.
참고: **유닉스, 리눅스 기반 OS에서 파일 이름을 바꾸는게 익숙치 않으신 분들은 Step3를 반드시 하지 않으셔도 됩니다.** 설치프로그램이 자동으로 wp-config.php파일을 생성하므로 Step3를 그냥 넘어가셔도 됩니다.
4. WordPress파일을 서버에 원하는 위치에 옮기도록 합니다.
   - 만약 루트 도메인에 워드프레스를 연결시킬 경우(ex> `https://www.example.com/`), 모든 파일을 압축 해제 후 안의 내용물을 전부 서버의 루트 디렉토리(ex>Apache의 경우, `/var/www/html`)에 넣을 것.
   - 만약 서브디렉토리에 넣을 경우(ex> `https://www.example.com/blog`), 서버의 루트 디렉토리에 blog 폴더를 생성하고, 모든 파일을 압축 해제 후 안의 내용물을 전부 blog 폴더에 넣을 것.
   - 만약 FTP프로그램이 강제로 알파벳을 소문자로 만들 경우, 이 기능을 해제하세요!
5. ~~런~~ 홈페이지에 접속하여 설치를 계속 진행하세요. 
   - 워드프레스를 서버의 루트 디렉토리에 설치한 경우, `https://example.com`로 접속!
   - 워드프레스를 서버의 서브 디렉토리(ex> `blog`)에 설치한 경우, `https://example.com/blog`로 접속!

이게 끝이랍니다! 이제 홈페이지로 접속하면 워드프레스가 설치되어있을 것입니다.


## 상세 설치법

### Step 1. 다운로드 및 압축 해제

WordPress패키지를 [여기](https://wordpress.org/download/)에서 다운로드 받은 후, 압축을 풉니다.

- 워드프레스를 원격 웹서버에 업로드할 경우엔, 서버 말고 평소 작업할 때 사용하는 컴퓨터에 워드프레스 패키지를 받은 후에 압축을 푸세요.
- FTP를 사용한다면, Step 2로 진행하세요. (파일 업로드는 나중에 다룹니다.)
- 만약 FTP가 아닌 쉘을 통해 웹서버에 바로 엑세스할 수 있고, CLI환경에 익숙하신 분이라면, 그리고 [FTP 사용](https://wordpress.org/support/article/glossary/#ftp)을 지양하고싶은 분이라면 `wget`(혹은 `lynx` 또는 콘솔환경을 지원하는 웹브라우저)을 사용하십시오.
  - `wget https://wordpress.org/latest.tar.gz/`
  - 파일을 다운로드한 후, 다음 명령으로 압축을 푸세요.
    `tar -xzvf latest.tar.gz`
    > 각주: <br>
    > tar **-z** 옵션은 gzip으로 압축된 파일을 풀어준다.

위 명령어대로 진행하면 다운로드 받은 압축파일이 해당 경로에 `wordpress`폴더로  풀립니다. 



### Step 2. DB 및 DB유저 생성

만약 호스팅 업체를 사용하고 있으시다면, 호스팅 업체에서 Wordpress 데이터베이스 세팅이 되어 있거나 자동으로 데이터베이스를 세팅할 수 있는 솔루션을 제공할것입니다.(아니라면.. 흠...) 호스팅 업체의 홈페이지를 살펴보며, 데이터베이스 설정을 수동으로 진행해야 하는지를 확인해보십시오. 

만약 수동으로 데이터베이스와 username을 생성해야 한다면, 아래의 [phpMyAdmin을 사용할 경우 데이터베이스를 생성하는 방법](#phpMyAdmin을-사용할-경우)을 따라 진행하시면 됩니다. Plesk, cPanel, mySQL과 같은 다른 툴을 사용하신다면, [워드프레스를 위한 데이터베이스 생성하기(영문)](./appendix/creating-database-for-wordpress.md)) 문서를 참고하세요.

> *각주:* 
> 1. 위에 문서들은 GUI를 이용해서 DB 생성 및 사용자 설정을 하는 과정입니다. Wordpress에 글을 올리거나, 댓글을 달거나 등의 다양한 정보들을 관리하는 저장소를 생성한다고 생각하심 됩니다.
>
> 2. 이전의 튜토리얼 본문에서 mySQL CLI를 사용하는 방법은 위의 데이터베이스 생성하기 문서로 이동하였으니 해당 문서를 참고해주십시오.


만약 구축하려는 서버에서 오직 하나의 데이터베이스를 사용하고 있는데(!) 이미 사용하고 있다면(!!) 워드프레스를 그냥 안에 설치할 수 있습니다(!!!). 다만 DB Table끼리 구별 가능한 접두어(prefix)를 두어 기존 데이터를 덮어쓰지 않도록 방지할 수 있도록 하면 됩니다.

> 원문은 이렇게 되어 있는데.. 여건이 된다면 추천하지는 않는 방법입니다.. (만에하나 테이블 데이터가 덮어쓰이거나 실수로 날리게 되면... Holy...)

#### phpMyAdmin을 사용할 경우

여러분의 웹서버에 [phpMyAdmin](https://wordpress.org/support/article/glossary/#phpmyadmin)이 설치되어있다면, 이 설명서를 따라 워드프레스를 위한 데이터베이스와 username을 생성할 수 있습니다. 참고로, 대부분의 리눅스 배포판에서 자동으로 PhpMyAdmin을 설치할 수 있습니다.

***참고:*** *이 설명서는 phpMyAdmin 4.4 기준으로 작성되었습니다. phpMyAdmin 설정 화면이 버전별로 살짝 다를 수 있습니다.*


_____
> 번역중입니다.


1. 좌측 드롭다운 메뉴에 **워드프레스와 관련된 데이터베이스가 생성되지 않았다면**, 새로 데이터베이스를 생성합니다.
  1. 데이터베이스의 이름을 선택합니다: ...
![phpMyAdmin language encoding drop down](https://i0.wp.com/wordpress.org/support/files/2018/11/phpMyAdmin_create_database_4.4.jpg?w=688&ssl=1)

2. 좌측 상단에 **phpMyAdmin** 아이콘을 클릭하여 메인페이지로 이동한 후에, **Users**탭을 클릭합니다. ...
![phpMyAdmin Users Tab](https://i1.wp.com/wordpress.org/support/files/2018/11/users.jpg?resize=768%2C500&ssl=1)

  1. ...
  2. ...

![phpMyAdmin03](https://i2.wp.com/wordpress.org/support/files/2018/11/phpMyAdmin_server_info_4.4.jpg?w=682&ssl=1)


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


# WordPress 설치하기
* 출처: [WordPress.org](https://codex.wordpress.org/Installing_WordPress)
* 한글작성자: 김도균
* 작성일: 2019월 2월 8일




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
     * 만약 루트 도메인에 워드프레스를 연결시킬 경우(https://www.example.com/), 모든 파일을 압축 해제 후 안의 내용물을 전부 루트 디렉토리에 넣을 것.
     * 만약 서브디렉토리에 넣을 경우(예시로 https://www.example.com/blog), blog 폴더를 생성하고, 모든 파일을 압축 해제 후 안의 내용물을 전부 blog 폴더에 넣을 것.
     * 만약 FTP프로그램을 사용하고, 강제로 알파벳을 소문자로 만들 경우, 소문자로 만드는 기능을 해제할 것!
 4. ~~런~~ 홈페이지에 접속하여 설치를 계속할 것.
 
이게 끝이랍니다!


## Detailed Instructions
#### 상세한 설치법
~~더 이상 자세한 설명은 생략한다~~

여기는 작성중입니다..


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


 


# WordPress 환경 구성 - Nginx

본 글은 제가 개인적으로 Wordpress 블로그 설치 시 사용하는 설치법을 정리한 글입니다. 따라서 구체적인 내용보다는 후에 편의를 위해 작성한 글이므로 모든 서버에 적용이 안될 수도 있으며 에러가 날 수도 있습니다.

추가로 본 글에서 사용하는 서버 환경은 `Google Cloud Platform`이며 이미지는 `Ubuntu 18.04`입니다.



본 글에선 다음과 같은 내용을 다룹니다.

- Wordpress 설치를 위한 환경 구성
- Wordpress를 위한 HTTPS 프로토콜 대응
- PHP와 nginx 연결



## Step 1. Nginx + PHP-fpm + MySQL 설치

먼저 서버 환경에 위의 세 개의 프로그램을 설치합니다.

```shell
$ sudo apt-get update
$ sudo apt-get install nginx mysql-server-5.7 php7.2-fpm
# sudo apt-get install php7.0-gd php7.0-curl php7.0-mbstring php7.0-xml php7.0-mcrypt
```



## Step 2. MySQL 사용자 생성





## Step 3. Certbot으로 https 프로토콜 대응

Certbot은 무료로 서버에 자동 갱신되는 인증서를 만들어주는 프로그램입니다.

```shell
# Certbot 설치
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot python-certbot-nginx 

# Certbot 시작
$ sudo certbot --nginx
```





## Step 4. Nginx에 PHP(fpm) 연동하기

Nginx에서 PHP를 사용하기 위해 nginx의 `default.conf`파일을 수정해주어야 합니다. 아래와 같이 수정하면 됩니다.

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
 	
 	// PHP 연동 코드
    location ~ \.php$ {
        try_files $uri =404; 
        fastcgi_pass   unix:/run/php/php7.2-fpm.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
 	
 	// PHP 연동 코드
    location ~ /\.ht {
        deny  all;
    }
}
```



## 마무리

이제 Wordpress를 설치하기 위한 환경을 모두 구성했습니다. 다시 [본문](<https://github.com/DokyoonKim/how-to-install-wordpress-kr>)으로 돌아가 Step 1 부터 시작하시면 됩니다.


# Schooloud 설치 방법

본 문서는 schooloud 서비스 배포 시 설치 후 실행 방법에 대해 기술합니다.<br>
클라우드 인프라 서비스를 위한 서버3대(Backend, proxy, openstack)와 dns 연결을 위한 nhn DNS plus 서비스가 필요합니다.<br>
라이선스는 각 레포지토리를 참고해주세요!

## 목차

- <a href="profile/INSTALL_BE.md">Backend-server</a>
- [Proxy-server](#Schooloud-Proxy-server)
- [Openstack-server](#Schooloud-Openstack-server)
- [Frontend-server](#Schooloud-Frontend-server)

## Schooloud-Backend-server

### 1. git clone

```
git clone https://github.com/schooloud/schooloud_back-end.git
```

### 2. ./deploy.sh 실행

```
./deployment/deploy.sh
```

### 3. 환경변수 설정

`schooloud_back-end/deployment/uwsgi.ini` 파일의 env를 사용자 환경에 맞게 설정합니다.<br><br>
**※주의※**<br>
서버의 IP주소와 APP_KEY 등 외부에 노출되지 않도록 주의하십시오. <br>
아래의 환경변수가 꼭 포함되어야 합니다.<br>

- PROXY_SERVER=${프록시 서버의 IP 주소}
- OPENSTACK_AUTH_URL=${오픈스택이 설치된 서버에서 오픈스택 인증 주소}
- OPENSTACK_ADMIN_PROJECT=${오픈스택이 설치된 서버에서 관리자 프로젝트 ID}
- APP_KEY=${NHN Cloud Dns plus 서비스 app key}
- FLASK_APP=schooloud
- PYTHONPATH=/home/ubuntu/schooloud_back/schooloud
- SCHOOLOUD_ENV=real <br><br>
  아래는 예시 입니다.<br>

```
env=PROXY_SERVER=110.165.16.219
env=FLASK_APP=schooloud
env=PYTHONPATH=/home/ubuntu/schooloud_back/schooloud
env=SCHOOLOUD_ENV=real
env=OPENSTACK_AUTH_URL=http://180.210.81.240/identity
env=OPENSTACK_ADMIN_PROJECT=832d84344c964a78b0c3c1a2d33c3683
```

### 4. 환경변수 적용

```
sudo cp /home/ubuntu/schooloud_back/deployment/schooloud_app_nginx /etc/nginx/sites-enabled/schooloud
sudo systemctl restart uwsgi
```

## Schooloud-Proxy-server

### 1. git clone

```
git clone https://github.com/schooloud/schooloud_proxy.git
```

### 2. Flask, nginx 설치

```
sudo apt install flask
sudo apt install nginx
```

### 3. nginx 설정파일 수정

```
sudo vi /etc/nginx/sites-enabled/default
```

아래와 같이 수정합니다.

```
location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri @app;
        }

        location @app {
                include uwsgi_params;
                uwsgi_pass unix:/home/ubuntu/schooloud_proxy/proxy.sock;
        }
```

### 4. uwsgi 실행

```
cd ~/schooloud_proxy
uwsgi --ini proxy.ini
```

## Schooloud-Openstack-server

### 1. devstack 설치

다음 [문서](https://openstack.dooray.com/share/pages/cNN00FoxQrSevSxU6RFCpA)를 참조하여 devstack을 설치합니다.

### 2. Wireguard 설정

다음 [문서](https://happyae.tistory.com/84)를 참조하여 proxy 서버와 openstack 서버를 연결합니다.

## Schooloud-Frontend-server

### 1. git clone

```
git clone https://github.com/schooloud/schooloud_front-end.git
```

### 2. myapp.conf 파일 수정

server_name의 schooloud.cloud를 자신의 domain name으로 수정합니다.

```
server {
  listen 80;
  server_name schooloud.cloud;
  location / {
    root   /schooloud_front-end/build;
    index  index.html index.htm;
    try_files $uri $uri/ /index.html;
  }
}
```

### 3. deploy.sh 실행

```
./deployment/deploy.sh
```

deploy.sh파일은 다음과 같습니다.</br>
개발 환경의 충돌을 막기 위해 도커를 사용하시거나 깨끗한 vm에서 실행하시기 바랍니다.

```
#1. apt update
sudo apt update

#2. nodejs 다운로드
sudo apt install -y nodejs

#3. npm 다운로드
sudo apt install -y npm

#nodejs를 관리하고 업그레이드하는 도구인 'n'을 전역적으로 설치
sudo npm install -g n

#4. nodejs 버전 업그레이드
sudo n lts

#nginx 설치
sudo apt install -y nginx

#nginx 설정
sudo rm /etc/nginx/sites-available/default
sudo rm /etc/nginx/sites-enabled/default
sudo cp -f /schooloud_front-end/deployment/myapp.conf /etc/nginx/sites-available/myapp.conf
sudo ln -s /etc/nginx/sites-available/myapp.conf /etc/nginx/sites-enabled/myapp.conf
sudo systemctl restart nginx
```

</br>
</br>
</br>

단순, local 환경에서의 실행을 원하신다면, 아래 절차를 따르세요.</br>
node가 깔려져있음을 가정합니다. node는 18.15.0 버전 이상을 사용합니다.

### 1. git clone

```
git clone https://github.com/schooloud/schooloud_front-end.git
```

### 2. dependency 설치

```
npm i
```

### 3. 개발 환경 실행

```
npm start
```

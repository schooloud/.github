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

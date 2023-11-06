## Schooloud Frontend-server

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

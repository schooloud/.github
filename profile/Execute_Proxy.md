## Schooloud Proxy-server

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

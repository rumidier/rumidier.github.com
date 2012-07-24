---
layout: post
title: "Don release"
date: 2012-07-23 18:49
comments: true
categories: Server
---

## Donnenwa Open

1. DNS 요구
2. Apache2 설정
3. supervisior 설정
4. 확인

### DNS 요구

도메인 네임을 받아 현진이(서버)에 연결해 주어야 하지만
브롬튼에 도메인이 정의가 되있기 때문에 SE님에게 요구하면 된다.(나만되는겨)

### Apache2 설정

```
$ ssh rumidier@bu….접속
$ cd /etc/apache2/
$ cd sites-available
$ vi user.site.kr (작성)
$ cd ../
$ cd sites-enable
$ ln -s 타킷-경로
$ ~/etc/init.d/apache2 restart
```    
### supervisior 설정

슈퍼 바이저는 서버가 죽었다 다시 살아 났을시 수동이 아닌 자동으로 서버를 뛰워주기 위해 필요한 기능이다.

돈내놔는 carton을 사용하고 plackup으로 뛰우며 플라넥스와는 다르게 worker의 갯수가 존재 하지 않는다. 포트 설정은 아파치에서 해준 포트를 명시 해준후 디렉토리와 유저, 환경 등록을 해주면 끝이 난다.
환경경로는 carton과 plackup 경로도 알아야 하는거 같다(이 부분은 설명이 더 필요)

```
$ cd /etc
$ vi supervisord.conf

[program:Donnenwa] 
command=/usr/local/bin/carton exec -Ilib -- /home/USER Donnenwa/local/bin/plackup -Ilib -a /home/USER/Donnenwa
app.psgi --host 127.0.0.1 --port You_port(ex:3000)  
directory=/home/User/Donnenwa 
user=USER 
environment=PATH=/usr/local/bin:/usr/bin:/bin,HOME=/home/USER
stdout_logfile=/home/USER/logs/stdout 
stderr_logfile=/home/USER/logs/stderr 

$ sudo supervisorctl
supervisor> status
….
supervisor> update
supervisor> exit
$ 서버 실행 확인 끝
```
   
### 더 물어 봐야 할것

1. supervisor의 셋팅을 무엇을 참조 하는가?
2. 도메인 등록은 어떻게 하는가?
3. apach2 설정은 어떻게 하는가?

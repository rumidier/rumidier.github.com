---
layout: post
title: "Don-Change-space"
date: 2012-07-24 14:20
comments: true
categories: Catalyst Perl
---

## Sil::Web::Don 변경

Sil::Schema는 Sil의 공용 스키마가 아닌데도 불구 하고 그렇게 보일수도 있는
상태 이다 이를 바꾸기 위해서
Sil::Don::Schema로 바꾼다. 이는 Sil의 Don만의 스키마라고
명시 해주는것과 같다.

변경전
```
lib
`-- Sil
    |-- Schema
    |   |-- Result
    |   |   |-- Charge.pm
    |   |   `-- User.pm
    |   `-- ResultBase.pm
    |-- Schema.pm
    `-- Web
        |-- Don
        |   |-- Controller
        |   |   |-- Deposit.pm
        |   |   |-- List.pm
        |   |   |-- Login.pm
        |   |   |-- Logout.pm
        |   |   `-- Root.pm
        |   |-- Model
        |   |   `-- DonDB.pm
        |   `-- View
        |       |-- Bootstrap.pm
        |       `-- Download
        |           `-- CSV.pm
        `-- Don.pm
```

 변경후
```
 lib
└── Sil
    └── Don
        ├── Schema
        │   ├── Result
        │   │   ├── Charge.pm
        │   │   └── User.pm
        │   └── ResultBase.pm
        ├── Schema.pm
        ├── Web
        │   ├── Controller
        │   │   ├── Deposit.pm
        │   │   ├── List.pm
        │   │   ├── Login.pm
        │   │   ├── Logout.pm
        │   │   └── Root.pm
        │   ├── Model
        │   │   └── DonDB.pm
        │   └── View
        │       ├── Bootstrap.pm
        │       └── Download
        │           └── CSV.pm
        └── Web.pm
```
 
## 경로명 변경

의존성이 걸려있는 모든 내역들을 grep 명령어로 찾아 아래와 같이 수정해 주었다.

변경전

```
Sil::Schema::Result::Charge
Sil::Schema::Result::User
Sil::Schema::ResultBase
Sil::Schema

Sil::Web::Don::Controller::Deposit
Sil::Web::Don::Controller::List
Sil::Web::Don::Controller::Login
Sil::Web::Don::Controller::Logout
Sil::Web::Don::Controller::Root
Sil::Web::Don::Model::DonDB
Sil::Web::Don::View::Bootstrap
Sil::Web::Don::View::Download::CS
Sil::Web::Don
```

변경후

``` 
Sil::Don::Schema::Result::Charge
Sil::Don::Schema::Result::User
Sil::Don::Schema::ResultBase
Sil::Don::Schema

Sil::Don::Web::Controller::Deposit
Sil::Don::Web::Controller::List
Sil::Don::Web::Controller::Login
Sil::Don::Web::Controller::Logout
Sil::Don::Web::Controller::Root
Sil::Don::Web::Model::DonDB
Sil::Don::Web::View::Bootstrap
Sil::Don::Web::View::Download::CS
Sil::Don::Web
```

## 변경후 문제점

내용 수정후 서버 실행이 app.psgi에서 모듈을 찾지 못한다고 하였다.
이유는 Sil_web_Don.conf 파일명을 수정 해주지 않았기에 발생한 문제였다.
경로명이 바뀌엇듯이 파일명도 교체 해주어야 한다.

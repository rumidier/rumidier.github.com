---
layout: post
title: "Catalyst-Login"
date: 2012-07-11 20:44
comments: true
categories: Catalyst perl
---

[Catalyst::Manual::Tutorial::05_Authentication](https://metacpan.org/module/Catalyst::Manual::Tutorial::05_Authentication)

## Load plugins

/lib/MyApp.pm

    $ vi ./lib/MyApp/Web/MyApp.pm

    # 아래에 다음과 같이 추가
    use Catalyst qw/
	-Debug
	ConfigLoader
	Static::Simple
	Unicode::Encoding

	StackTrace

	Authentication

	Session
	Session::Store::File
	Session::State::Cookie
    /;

MakeFile.PL

    $ vi Makefile.PL

    # 추가
    requires 'Catalyst::Plugin::Authentication';
    requires 'Catalyst::Plugin::Session';
    requires 'Catalyst::Plugin::Session::Store::File';
    requires 'Catalyst::Plugin::Session::State::Cookie';

    $ carton install

MyApp.conf

    $vi MyApp.conf

    # 추가
    <Plugin::Authentication>
	<default>
	    password_type clear
	    user_model    DB::User
	    class         SimpleDB
	</default>
    </Plugin::Authentication>

## Add Login and Logout Controllers

Controller 생성

    $ script/myapp_create.pl controller Login
    $ script/myapp_create.pl controller Logout

Login [Login.pm](https://gist.github.com/3089985)

    $ vi lib/MyApp/Controller/Login.pm

Logout [Logout.pm](https://gist.github.com/3090013)

    $ vi lib/MyApp/Controller/Logout.pm

## Add Valid User Check

Root [Root.pm](https://gist.github.com/3090343)

    $ vi lib/MyApp/Controller/Root.pm

## 추가 해야 할점

현재는 DB에 유저의 password가 암호화 되지 않음 문서상
다음 내용에 나오기 때문에 추가가 필요함

## CPAN

[DBIx::Class::Manual::DocMap](https://metacpan.org/module/DBIx::Class::Manual::DocMap)

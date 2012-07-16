---
layout: post
title: "Catalyst-signup"
date: 2012-07-11 22:55
comments: true
categories: Catalyst perl
---

Signup Controller [Login.pm](https://gist.github.com/3090526)

    $ vi lib/MyApp/Controller/Login.pm
    # 내용 추가

## :Private

forword 혹은 detach로만 접근이 가능 하며, URL로 부터 바로 접근이 불가능 합니다.

    sub signup :Path('/signup') :Args(0) {
	my ( $self, $c ) = @_;

	$c->detach('signup_POST') if $c->req->method eq 'POST';
    }

    sub signup_POST :Private {
	my ( $self, $c ) = @_;


## Validation - Empty Value

입력값중에 빈값이 있으면 안돼므로 빈값인지 확인 하여 빈값일시 메세지를
출력 할수 있게 작업한다.

    my $user_name = $c->req->param('user_name') || '';
    my $email     = $c->req->param('email')     || '';
    my $password  = $c->req->param('password')  || '';

    my @messages;
    push @messages, 'Input the user name'     unless $user_name;
    push @messages, 'Input the user email'    unless $email;
    push @messages, 'Input the user password' unless $password;

    if (@messages) {
        $c->flash(
            messages => @messages,
        );

        return $c->res->redirect($c->uri_for('/signup'));
    }

## Validation - DB Unique search

User table에 user_name과 email이 동일한 값이 있는지 확인 하여 동일한
값이 있을시 error_msg를 출력 할수 있게 한다.

    my $cond = {};
    $cond->{'me.user_name'} = "$user_name";
    my $name_search = $c->model('DonDB')->resultset('User')->search($cond);
    if ($name_search->count) {
        $c->flash(
            messages => 'Using ID again input the New ID',
        );

        return $c->res->redirect($c->uri_for('/signup'));
    }

    $cond = {} if $cond;
    $cond->{'me.email'} = "$email";
    my $email_search = $c->model('DonDB')->resultset('User')->search($cond);
    if ($email_search->count) {
        $c->flash(
            messages      => 'Using email again input the New email',
        );

        return $c->res->redirect($c->uri_for('/signup'));
    }

## 유저 등록

Validation이 통과 했다면 테이블에 등록 할수 있게 한다.
실패시 signup페이지로 다시 이동 하며 

    my $time    = strftime "%Y-%m-%d %H:%M:%S", localtime;
    my $created = $c->model('DonDB::User')->create({
        user_name  => $user_name,
        email      => $email,
        password   => $password,
        created_on => "$time",
        updated_on => "$time",
    });

    $c->res->redirect($c->req->uri) unless $created;

## 유저 등록 - 확인

등록후 이름과 패스워드를 확인하여 다음 페이지 혹은 tdpfjaptpwldhk 냐혀ㅔvpdlwlfmf ghcnfgksek.

    if ($c->authenticate({ user_name => $user_name, password => $password } )) {
        $c->res->redirect($c->uri_for($c->controller('List')->action_for('index')));
    } else {
        $c->stash(error_msg => "Bad username or password."); # maybe flash?
        $c->res->redirect($c->req->uri);
    }
}

Signup View.tt [signup.tt](https://gist.github.com/3090541)

    $ vi root/templates/default/src/login/signup.tt
    # 내용 추가

## jquery 미사용

현재 Validation은 컨트롤 단에서만 검사 한다
추가가 필요함

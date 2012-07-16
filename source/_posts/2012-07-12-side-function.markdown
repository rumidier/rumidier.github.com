---
layout: post
title: "Side-function"
date: 2012-07-12 14:03
comments: true
categories: Catalyst perl
---

## Action - approval, refuse

[approval](https://gist.github.com/3096325)

[refuse](https://gist.github.com/3096321)


Approval은 청구 목록에 대하여 승인 기능을
refuse는 청구 목렉에 대하여 거부 기능을 가지게 된다.

승인 기능은 두가지 상황에서 선택 할수 있게 된다.
/list/view/user_num과 전체 list상태, 대기 리스트 상태, 거부 리스트 상태
에서 활성화가 되고 action을 취할수 있게 한다.

거부 기능은 두가지 상황에서 선택 할수 있게 된다.
/list/view/user_num과 전체 list상태, 대기 리스트 상태, 승인 리스트 상태
에서 활성화가 되고 action 을 취할수 있게 한다.

/list/view/user_id

아래와 같이 id 값과 함께 전달 할수 있다.

    <a href="[% c.uri_for('/list/approval', charge.id) %]" class="btn btn-primary">승인</a>
    <a href="[% c.uri_for('/list/refuse', charge.id) %]" class="btn btn-primary">거부</a>

CaputreArgs(1) 옵션으로 $id 값(들)을 받을수 있게 된다.

    sub approval :Local :CaptureArgs(1) {
        my ( $self, $c, $id ) = @_;
        my @target_ids = split ',', $id;

    sub refuse :Local :CaptureArgs(1) {
	my ( $self, $c, $id ) = @_;
	my @target_ids = split ',', $id;



@target_id의 모든 값(들)을 status값이 2 or 3로 업데이트 한다.
업데이트는 검색을 한 값들을 대상으로 update를 하게 된다.

    $ vi root/templates/default/src/list

    # 승인
    my $approval = $c->model('MyApp_DB')->resultset('Charge')->search({ id => { -in
            => \@target_ids } })->update_all({ status => '2' });
    # 거부
    my $refuse = $c->model('MyApp_DB')->resultset('Charge')->search({ id => { -in
            => \@target_ids } })->update_all({ status => '3' });


flash기능으로 messages값을 전달하여 조건에 맞을시 메세지를 출력 시키도록 한다.(/list/index.tt 참고)
조건은 approval, refuse기능이 정상 작동 되었는지를 검사 하게 된다.

    if ($query_status) {
        $c->flash->{messages} = 'Success message.';
    }
    else {
        $c->flash->{messages} = 'No status Item.';
    }

템플릿에 쓰일 status값과 함께 전체 목록으로 redirect 시키도록 한다.

    $c->stash->{status} = '2'; #상태에 맞는 status값
    $c->res->redirect($c->uri_for('/list'));

## Action - delete

[delete](https://gist.github.com/3096329)

승인 기능은 두가지 상황에서 선택 할수 있게 된다.
/list/view/user_num과 전체 list상태, 대기, 거부, 수정 상태
 에서 활성화가 되고 action을 취할수 있게 한다.

    $ vi root/templates/default/src/list
    <a href="[% c.uri_for('/list/delete', charge.id) %]" class="btn btn-primary">삭제</a>

다른 기능과 같이 CaptureArgs(1)를 받는다.

    sub delete :Local :CaptureArgs(1) {
	my ( $self, $c, $id ) = @_;
	my @target_ids = split ',', $id;

다른 기능과 달리 update_all 이 아닌 delete_all를 통하여 내용을 삭제 한다.

    my $charge = $c->model('DonDB')->resultset('Charge')->search({ id => { -in => \@target_ids } })->delete_all;

## CPAN

[DBIx::Class::Manual::DocMap](https://metacpan.org/module/DBIx::Class::Manual::DocMap)

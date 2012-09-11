---
layout: post
title: "export_csv"
date: 2012-07-25 19:01
comments: true
categories: Cataylst Perl export_csv
---

목차

1. CSV 출력 준비
2. View 생성

### CSV 출력 준비

선택된 내역을 출력 하기 위한 버튼을 추가한다.

root/templates/bootstrap/src/deposit/index.tt


```
      <a class="btn btn-primary" id="do_export">출력</a>
```

선택된 내역 js처리

root/static/scripts/list.js


```
  $('#do_export').click(function() {
    var selected_charges = [];

    $('#charge_list tr').filter(':has(:checkbox:checked)').each(function(){
      if($(this).attr('id') !== undefined)
        selected_charges.push($(this).attr('id'))
    });

    location.href = '/deposit/export/' + selected_charges;
  });
```

Sil/Web/Don/Controller/Deposit.pm

선택된 승인 내역을 CSV로 출력하기 위하여
모듈 - [Catalyst::View::Download::CSV](https://metacpan.org/module/Catalyst::View::Download::CSV)을 사용 하였습니다.

```
sub export :Local CaptureArgs(1) {
    my ( $self, $c, $id ) = @_;
    my @target_ids = split ',', $id;
    
    my @charges;
    
    push @charges, ['제목', '청구자', '금액', '영수증날짜'];
    
    foreach my $charge($c->model('DonDB')->resultset('Charge')->search({id => { -in => \@target_ids }})->all) {
        push @charges, [ $charge->title, $charge->user->user_name, $charge->amount, $charge->usage_date];
    }

    if (@charges) {
        $c->stash->{'csv'} = { 'data' => [ @charges ] };
        $c->flash->{messages} = 'Success Exported.';

    } else {
        $c->flash->{messages} = 'Export Failed.';
    }
    $c->forward('Sil::Web::Don::View::Download::CSV');
}
```

## View 생성

View는 script_web_don_create view로 생성한다.

list/Sil/Web/Don/View/Download/CSV.pm을 생성 완료.


```
package Sil::Web::Don::View::Download::CSV;
use Moose;
use namespace::autoclean;

extends 'Catalyst::View::Download::CSV';

=head1 NAME

Sil::Web::Don::View::Download::CSV - Catalyst View

=head1 DESCRIPTION

Catalyst View.

=head1 AUTHOR

ja3ck

=head1 LICENSE

This library is free software. You can redistribute it and/or modify
it under the same terms as Perl itself.

=cut

__PACKAGE__->meta->make_immutable;

1;
```

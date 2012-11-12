---
layout: post
title: "month-split"
date: 2012-09-18 15:30
comments: true
categories: Perl catalyst bikeme
---

user의 아이디를 가지고 elapsed_at 의 내용을 가져 오게 된다
이 값은 2012-09-09 21:00:00 형식으로 되어 있으며
2012 와 09 를 기준으로 값을 따로 가지게 하여년도별 월 횟수를나타나게
해주었다 하지만 필요 없어 지움...

controll

    $cond = {} if %$cond;

    my $user_id;
    if ($id) {
        $user_id = $user_info->id;
    }
    else {
        $user_id = $c->user->id;
    }

    $cond->{'me.user_id'} = $user_id;

    my %attr            = ( 'order_by' => { -desc => 'me.elapsed_at' } );

    my $activity_search = $c->model('BikeMeDB')->resultset('Activity')->search($cond, \%attr);
    my $activities      = [ $activity_search->all ];
    my $activity_data   = {};

    for my $activity (@{ $activities }) {
        my $year;
        my $month;

        my $elapsed = $activity->elapsed_at;
        $year       = $activity->elapsed_at->year;
        $month      = $activity->elapsed_at->month;

        my @split_elapsed = split('-', $activity->elapsed_at, 3);

        $activity_data->{$split_elapsed[0]}{$split_elapsed[1]}++;
    }

    my $year  = $c->req->params->{year};
    my $month = $c->req->params->{month};

    my $max_year  = '00000';
    my $max_month = '00';

    if ($year && $month) {
        $max_year  = $year;
        $max_month = $month;
    }
    else {
        foreach my $year (keys %$activity_data) {
            if ($year gt $max_year) {
                $max_year = $year;
            }
            else {
                $max_month = '00';
                last;
            }

            foreach my $month (keys $activity_data->{$year}) {
                $max_month = $month if $month gt $max_month;
            }
        }
    }

    $cond = {} if %$cond;
    $cond->{'me.user_id'} = $user_id;
    $cond->{'me.elapsed_at'} = { 'like', "%"."$max_year"."-"."$max_month"."%" };

    $activity_search = $c->model('BikeMeDB')->resultset('Activity')->search($cond, \%attr);

view - 년-월

    [% FOEACH year IN activity_data.keys.reverse %]
        [% FOREACH month IN activity_data.$year.keys.sort.reverse %]
      <div class="btn">
        <a href="[% c.uri_for('/activities') %]?year=[% year %]&month=[% month %]" class="btn btn-primary">[% year %]-[% month %] ([% activity_data.$year.$month %])</a>
    </div>
        [% END %]
    [% END %]

---
layout: post
title: "git rebase"
date: 2012-05-14 12:11
comments: true
categories: git
---

브랜치를 나누기 쉬운 git-flow쓰지만 코드 확인이 불편 하다.
그래서 [형석님](http://aanoaa.github.com/) git - rabase를 사용해 본다.

다른 사람이 내게 pull-request를 날리게 되면 이게 잘돌아 가는지 확인이 
필요하다.

remote branch 확인 하는 방법

    $ git branch -a 또는 git branch -av

pull-request된 브랜치 명이 있다면 보이게 된다.

    remotes/origin/#1-test

remote 상태 확인 하러 가기

    $ git checkout "#1-test"

pull-request된 내용이 이상이 없을때는 github 홈페이지에서 허락을 하게 되면
master와 합쳐 지게 된다.
merge가 안된다는 명시를 하게 되면 현재 pull-request가 branch의 분기 시점이
현재 master와 차이(다른 커밋 메세지)가 포함 되어 있기 때문에
master 브랜치를 최신상태로 만들어 주고 rebase 해주어야 한다.

    $ git pull origin master

분기된 master이력이 최신으로 변경되었다면.

    $ git checkout "branch-name"
    $ git rebase master
    # conflict?
    # $ vim conflict.file -> 수정

conflict이 일어 났을시 bracnh명이 유지 될때와 유지 되지 않을때가 있다.

유지시

    $ git rebase --continue

(no branch)상태 

    $ git rebae --skip

conflict 처리 될때까지 반복

모든 문제의 해결을 했다면 

    $ git push origin "#1-test"

이제 github 홈페이지 에서 확인 절차를 밟으면 된다.
확인이 끝났다면 master branch에서

    (master) $ git pull

## pull-request를 보낼시

pull-request를 보낼때 또한 마스터의 가장 최근 이력을 기초로 한다.
가장 최신상태에서 

push를 해주고 github 홈페이지 에서 pull-request를 보내게 되면 마스터가
알아서 처리 해주게 된다.

    $ git push origin "#1-test"

## git 기본사항

모든 branch 확인 하는 방법

    $ git bracnh -a

remote 삭제 하는 방법

    $ git push origin :remote주소

brach 삭제 하는 방법

    $ git branch -d "branch name"

## remote 주소 변경하기

    $ git remote show origin # remote 상태 확인

push시 경로와 비밀번호 쓰라고 나오는 경우가 생겼는데
이런 경우 remote의 상태를 확인후 http://.....되있는 경우가 있다
이때는 주소를 http://가 아닌 ssh 주소로 해주면 나오지 않게 된다.

git 홈피에서 ssh 주소를 복사해오기

    $ git remote add aaa "ssh 주소 copy"
    $ git remote rm origin
    $ git remote show origin
    $ git remote rename aaa origin
    $ git remote show origin 으로 확인 및 푸쉬 해봄

## 마무리

merge된 branch 알아 보기
merge가 안된 branch는 표시 안되니 표시 된건
가차 없이 지워 버리자

    $ git br --merged

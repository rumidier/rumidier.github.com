---
layout: post
title: "Ubuntu SCP"
date: 2012-05-14 15:08
comments: true
categories:  ubuntu
---

서버파일 전송

    $ scp [option] [파일] [위치]
    <option>
    -r : 지정한 디렉토리 하위 디렉토리 및 파일까지 복사

예제

    $ scp rumi@rumidier.github.com:/home/meadow/workspace/filename.c .

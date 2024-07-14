---
layout: post
title: "StringBuilder와 StringBuffer"
date: 2023-12-04
---

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">

<link rel="stylesheet" href="{{ /assets/css/style.css | relative_url }}

<p>StringBuilder와 StringBuffer 모두 <u><b>문자열을 가변적으로 처리</b></u>하는 클래스이다.&nbsp;</p>
<p>&nbsp;</p>
<p><b>StringBuilder</b></p>
<p>- 내부 버퍼의 크기가 부족할 때마다 새로운 버퍼를 생성하고, 기존 내용을 복사한다. (ArrayList와 동일)&nbsp;</p>
<p>- <u><b>Thread unsafe</b></u>하기 때문에 멀티스레드 환경에서 동기화(Syncronized) 처리가 필요함&nbsp;</p>
<p>&nbsp;</p>
<p><b>StringBuffer</b></p>
<p>- StringBuilder와 동일하게 내부 버퍼를 사용하여 문자열을 가변적으로 다룸&nbsp;</p>
<p>- <u><b>Thread safe</b></u>한 클래스로 멀티스레드 환경에서도 안전하게 사용할 수 있다.&nbsp;</p>
<p>&nbsp;</p>
<p>단일 스레드 환경에서는 StringBuilder가 더 효율적임.&nbsp;</p>
<p>멀티쓰레드 환경에서는 StringBuffer가 더 효율적임&nbsp;</p>
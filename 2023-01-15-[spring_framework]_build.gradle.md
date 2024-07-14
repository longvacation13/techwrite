---
layout: post
title: "[spring framework] build.gradle"
date: 2023-01-15
---

<ul>
<li>라이브러리를 어느 서버 ( 상세하게는 mavenCentral() 이라고 부름 ) 에서 받아오는 역할을 하는 파일</li>
<li><u style="letter-spacing: 0px;">gradle이 의존관계를 모두 관리해줌</u></li>
<li>gradle이 의존관계를 관리하기 때문에 spring-boot-starter-web을 받아올때 tomcat, boot-test .. 등등 연관된 모든 라이브러리를 받아옴 &rarr; 최종적으로 spring-boot-core까지 받아옴</li>
<li>해당 파일에 라이브러리별 버전을 기입해 줄 수 있음</li>
<li>testImlementation : junit5 라는 테스트 라이브러리가 build.gradle 파일에 기본적으로 들어가 있음</li>
</ul>
<p style="text-align: center;"><b>(아래 dependencies 영역 참고)</b></p>
<pre id="code_1673791449262"><code>dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}</code></pre>
<p>* mavenCentral : 모든 라이브러리들이 들어가있는 오픈소스&nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
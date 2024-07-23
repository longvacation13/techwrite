# 비즈니스 로직과 도메인 로직이란 (1)

<blockquote>비즈니스 로직과 도메인로직이라는 말을 쓰는데 이 2가지는 차이점이 있다.&nbsp;</blockquote>
<table border="1" style="border-collapse: collapse; width: 100%; height: 235px;">
<tbody>
<tr style="height: 20px;">
<td style="width: 16.2791%; height: 20px;">종류</td>
<td style="width: 83.7209%; height: 20px;">설명</td>
</tr>
<tr style="height: 20px;">
<td style="width: 16.2791%; height: 20px;">도메인 로직&nbsp;</td>
<td style="width: 83.7209%; height: 20px;"><b>도메인 로직</b><span style="color: #333333; text-align: start;">이란<span>&nbsp;</span></span><span style="color: #006dd7;"><u><b>현실세계의 문제를 해결하기 위한 로직</b></u></span><span style="color: #333333; text-align: start;">을 말한다. 은행업무로 예를 들어보면<span>&nbsp;</span></span><span style="color: #006dd7;"><u><b>출금, 계좌개설, 계좌해지</b>&nbsp;</u></span>등이 있다.&nbsp;</td>
</tr>
<tr style="height: 195px;">
<td style="width: 16.2791%; height: 195px;">비즈니스 로직</td>
<td style="width: 83.7209%; height: 195px;"><span><b>비즈니스 로직</b>이란<span>&nbsp;</span><span style="color: #006dd7;"><u><b>도메인 로직을 해결하기 위한 로직</b></u></span>을 이야기한다.&nbsp;</span><br /><span>예를들어 도메인로직을 해결하기 위해<span>&nbsp;</span><span style="color: #006dd7;"><u><b>데이터베이스 연결하기, 백엔드서버 호출하기, 고객 데이터 저장하기, 캐시 데이터 저장하기</b></u></span><span>&nbsp;</span>등이 있다.&nbsp;<br /><br /></span>- 외부와의 네트워킹&nbsp;<br />- DB 접근 및 수정&nbsp;<br />- UI를 건드림 (예를들어 얼럿에 노출되는 메시지라던지)</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<blockquote>근데 업무 현장에서 도메인과 서비스 로직이 섞이는 경우가 자주 있다.&nbsp;</blockquote>
<p>예를들어 8000원을 USD 달러로 환전하고, 소수 3째자리까지 표시하는 프로그램을 만든다고 가정해보자.&nbsp;</p>
<p>이 프로그램의 역할을 도메인과 비즈니스 로직으로 분리해보면 다음과 같다.&nbsp;</p>
<p>① 미국 달러 기준으로 환전을 한다. = 도메인 로직&nbsp;</p>
<p>② 소수점 3째 자리까지 계산한다. = 비즈니스 로직</p>
<p>&nbsp;</p>
<p>이때 비즈니스 로직과 도메인 로직은 분리하는게 좋다.&nbsp;</p>
<p>왜 해야할까?&nbsp;</p>
<p>&nbsp;</p>
<p>다음과 같은 문제 때문이다.&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/9IOmF/btsIHbrgleK/uNQrCKNksx1xw9Co5FK8PK/img.png" /></span><figcaption>도메인 및 비즈니스 로직은 핵심 로직이기 때문에 테스트를 많이 해야하고 단위테스트를 위해 기능을 분리하는게 좋다.</figcaption>
</figure>
</p>
<p>&nbsp;</p>

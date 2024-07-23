# 비즈니스 로직과 도메인 로직이란 (2)

<p>앞에서 배운 도메인로직과 비즈니스 로직이라는 개념을 기반으로 은행 앱을 통해 대출을 받는다고 가정해 보자.&nbsp;</p>
<p>&nbsp;</p>
<p>크게 3가지 행동이 있다.&nbsp;</p>
<table border="1" style="border-collapse: collapse; width: 100%;">
<tbody>
<tr>
<td style="width: 16.6667%;">레이어</td>
<td style="width: 20.2714%;">Presentation&nbsp;</td>
<td style="width: 29.7286%;">Domain</td>
<td style="width: 33.3333%;">Data (repository)&nbsp;</td>
</tr>
<tr>
<td style="width: 16.6667%;">하는일</td>
<td style="width: 20.2714%;">대출하기 버튼</td>
<td style="width: 29.7286%;">대출을 받는다. (대출심사)<br />- 금리 확인<br />- 신용정보 확인<br />- 대출 실행&nbsp;</td>
<td style="width: 33.3333%;">대출정보를 저장</td>
</tr>
<tr>
<td style="width: 16.6667%;">변하기 쉽나?</td>
<td style="width: 20.2714%;">쉽게 변할수 있는 영역&nbsp;</td>
<td style="width: 29.7286%;">쉽게 변할 수 없는 영역&nbsp;</td>
<td style="width: 33.3333%;">쉽게 변할수 있는 영역&nbsp;<br />(서버가 될수도 로컬 DB가 될수도 있다.)</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/Z5qJh/btsIGzfaZbV/Q4BxBvodefCLJQhXATmlB1/img.png" /></span><figcaption>각 영역별 역할은 다음과 같다.</figcaption>
</figure>
</p>
<p>&nbsp;</p>
<ul>
<li>화면상(<b>UI</b>) 버튼이 별모양인지 세모모양인지 도메인 영역은 알 필요가 없다.&nbsp;</li>
<li>화면에서는(<b>UI</b>) 정보를 DB 서버에 저장하든, 로컬 서버에 저장하든 알 필요가 없다.&nbsp;</li>
<li>위 그림과 같이 레이어를 구성하면, 응집도는 높이고 결합도는 낮출수 있다.&nbsp;</li>
<li>이렇게 되면 controller는 controller를 사용할수도, viewmodel(<b>MVVM</b>)을 사용할수도, presenter(<b>MVP</b>)를 사용할수도 있다. (viewmodel과 presenter가 무엇인지에 대해서는 이 포스팅에서 조금 벗어나므로 다른 포스팅에서 다루는걸로..)</li>
<li>이 말은 각 레이어간 의존성을 낮출수 있다는 의미이다.&nbsp;</li>
</ul>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/ekGx7N/btsIGkP5ac8/TnscLzlkBOpw0AxrKTkNPK/img.png" /></span><figcaption>의존성은 바깥에서 안으로 흐르고, 각 영역별 의존성이 낮아짐으로 인해 레이어간 결합도가 낮게 만들수 있다.</figcaption>
</figure>
</p>

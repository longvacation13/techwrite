# 도커 redis 구축하기

<h2>1. 서론</h2>
<hr contenteditable="false" />
<p>도커에 대해 쉽게 알아보려면 우선 무역 방식의 변화를 설명해야 할거 같습니다.&nbsp;</p>
<table border="1" style="border-collapse: collapse; width: 100%;">
<tbody>
<tr>
<td style="width: 50%; text-align: center;">과거</td>
<td style="width: 50%; text-align: center;">현재</td>
</tr>
<tr>
<td style="width: 50%;"><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/bfKTwM/btrmpwYy2oG/Vqi9KoVZaCjHvwykwboGi1/img.png" /></span></figure>
</td>
<td style="width: 50%;"><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/dS4Aju/btrmwQuVraO/NXi9yva4moZ5WQnADfsyK0/img.png" /></span></figure>
<span><br /></span></td>
</tr>
<tr>
<td style="width: 50%;">규격화 되어 있지 않아 마구잡이식으로 적재</td>
<td style="width: 50%;">컨테이너라는 규격을 통해 대량 물류 운반이 가능해짐&nbsp;</td>
</tr>
</tbody>
</table>
<p>IT에서 언급되는 Docker 라는 기술이 위의 현재 모습과 같습니다.</p>
<p>&nbsp;</p>
<p>컨테이너를 통해 그 안에 필요한 프로그램(nodejs, jenkins, wordpress, redis 등등..) 을 넣고 사용하는 방식으로</p>
<p>image를(<b>=image란 redis, jenkins 등 프로그램의 압축파일</b>) 컨테이너에 올려서 안정적으로 관리하는게 현재 docker 라고 생각하시면 됩니다.&nbsp;</p>
<p>&nbsp;</p>
<p>도커 이전에는 아래와 같은 가상머신(VM)이 있었는데요. OS를 일정량 분할해야 했기 때문에 overhead 문제가 컸습니다.&nbsp; 도커의 경우 운영체제의 분할 없이 도커 엔진 위에 컨테이너를 올려서 사용하는 형태기 때문에 오버헤드 문제로 부터 훨씬 자유롭습니다.&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/N4RZ3/btrmrvd1qkV/AgxydaO8Jg5folG9emGUO1/img.png" /></span></figure>
</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="../assets/css/style.css">
</head>
<body>
<header>
    <h1>파이썬 아나콘다 연동(3) - flask uri redirect</h1>
    <p>Posted on 2021-11-07</p>
</header>
<main>
<p>uri 별로 페이지 redirect 처리를 해야하는데 테스트로 만든 index.html 페이지를 못찾는 현상이 생김&nbsp;</p>
<p>flask의 경우 html 페이지는 "<b>templates</b>"[s 꼭 필요함] 라는 폴더에 html 과 같은 정적 페이지 넣어놓는게 규칙으로 되어 있는것으로 보임 ( 절대경로로 찾으려 해도 못찾는 현상 있음 )&nbsp;</p>
<p>&nbsp;</p>
<p>폴더 계층구조로 보면 아래과 같은 형태로 되어있어야함&nbsp;</p>
<p>[project]&nbsp;</p>
<p>&nbsp;- [<b>templates](html 폴더)&nbsp;</b></p>
<p>&nbsp;- 기타..&nbsp;</p>
</main>
</body>
</html>
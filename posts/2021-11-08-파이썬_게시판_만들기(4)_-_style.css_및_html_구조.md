<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="../assets/css/style.css">
</head>
<body>
<header>
    <h1>파이썬 게시판 만들기(4) - style.css 및 html 구조</h1>
    <p>Posted on 2021-11-08</p>
</header>
<main>
<p>python flask 연동시 css 파일과 html 파일의 root directory가 정해져 있는 것으로 확인됨&nbsp;</p>
<p>&nbsp;</p>
<p>project&nbsp;</p>
<p>&nbsp;- template : html&nbsp;</p>
<p>&nbsp;- static/css : css&nbsp;</p>
<p>에 저장하고 css import시 아래와 같이 사용하면 적절하게 style 적용이 가능함.&nbsp;</p>
<pre class="html xml" id="code_1636378843553"><code>&lt;head&gt;
    &lt;link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}"&gt;
&lt;/head&gt;</code></pre>
<p>&nbsp;</p>
</main>
</body>
</html>
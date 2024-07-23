# 파이썬 게시판 만들기 (2) - sqlite3 DB 설치 및 연동 ( sqlite )

<p><a href="https://longvacation13.tistory.com/2" rel="noopener" target="_blank">2021.11.07 - [IT 개발/파이썬] - 파이썬 게시판 만들기(1) - 아나콘다 연동</a></p>
<figure contenteditable="false" id="og_1636378959138"><a href="https://longvacation13.tistory.com/2" rel="noopener" target="_blank">
<div class="og-image">&nbsp;</div>
<div class="og-text">
<p class="og-title">파이썬 게시판 만들기(1) - 아나콘다 연동</p>
<p class="og-desc">들어가기에 앞서.. 1. python vs anaconda ? Python은 pip 툴만을 포함하고 있다. 필요 패키지 및 라이브러리 등을 설치할 때 모두 수동으로 해줘야함 아나콘다는 Python 기본 패키지에 각종 수학/과학 라이</p>
<p class="og-host">longvacation13.tistory.com</p>
</div>
</a></figure>
<h2>모든 진행 내용은 아나콘다 가상환경 내에서 진행됩니다. 연동방법은 위 내용 참고.</h2>
<hr contenteditable="false" />
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>DB 설치를 위해서는 sqlite 설치가 필요함.&nbsp;</p>
<p>SQLite 설치는 아래 블로그 참조&nbsp;</p>
<p><a href="https://ddolcat.tistory.com/707" rel="noopener" target="_blank">https://ddolcat.tistory.com/707</a></p>
<figure contenteditable="false" id="og_1636292878581"><a href="https://ddolcat.tistory.com/707" rel="noopener" target="_blank">
<div class="og-image">&nbsp;</div>
<div class="og-text">
<p class="og-title">DB Browser for SQLite 다운로드 설치 및 기본 사용법</p>
<p class="og-desc">SQLite 데이터베이스에 접근 하기 위해 GUI 프로그램 중 DB Broswer for SQLite 프로그램의 설치 방법 및 사용방법에 대해 알아봅니다. SQLite 툴 중에 하나로 CRUD 작업, 인덱스 생성 등 많은 작업을 편하게</p>
<p class="og-host">ddolcat.tistory.com</p>
</div>
</a></figure>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>아나콘다 설치 후 가상환경에서 실행시 관련 모듈 설치할 필요 없음 ( default로 깔려있음 )&nbsp;</p>
<p>&nbsp;</p>
<p>sqlite import 및 테이블, 데이터 생성 코드는 아래 내용 참고.</p>
<p>사용자 임의의 파일명으로 생성 후, 가상환경에서 실행시키면 됨&nbsp;</p>
<pre class="python" id="code_1636293002808"><code># 참조 블로그 : https://dog-foot-story.tistory.com/71 
# 1.연결 객체 생성 
import sqlite3
from sqlite3.dbapi2 import Cursor
db = sqlite3.connect('test.db')
print(db)

# 2. 커서(쿼리문 전달 가능객체) 생성  
cursor = db.cursor()
print(cursor)

# 3. 테이블 생성 
# 초기화 ( 아래 작업이 없을 경우 계속 데이터 쌓이게 됨 )
cursor.execute("DROP TABLE IF EXISTS stInfo")
cursor.execute("CREATE TABLE stInfo(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, age INTEGER)")

# 4. 데이터 삽입    
# 4-1. 데이터 단건 삽입
cursor.execute("INSERT INTO stInfo(name, age) VALUES('홍길동', 20)")

# 4-2. 데이터 복수건 삽입 
cursor.executescript("""
    INSERT INTO stInfo(name, age) VALUES ('김길동','20');
    INSERT INTO stInfo(name, age) VALUES ('안길동','20');
    INSERT INTO stInfo(name, age) VALUES ('윤길동','20');
    INSERT INTO stInfo(name, age) VALUES ('이길동','20');
    INSERT INTO stInfo(name, age) VALUES ('신길동','20');
""")

# 5. 데이터 검색 
cursor.execute("SELECT * FROM stInfo")

# 5-1. 모든 행 읽기 
print(cursor.fetchall())

# 종료 
print('db test end')</code></pre>

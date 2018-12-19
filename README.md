# 181219 - Day3 (github page 만들기, Cloud9, Flask(경량화 웹 프레임워크), Python 연습문제)                                                                                                                   



# 1. github page 만들기



1. free bootstrap template 검색 ->  All Free Bootstrap Themes & Templates로 들어간다.

2. Bootstrap Themes 중 Resume 다운로드

3. github 페이지를 저장할 수있는 폴더를 git bash에서 명령어로 생성

   ```
   student@M70213 MINGW64 ~/Documents/week2/day3
   $ mkdir github_page
   ```

4. 다운받은 Resume Template 압축을 풀고 github_page로 복사하고 확인

   ```
   student@M70213 MINGW64 ~/Documents/week2/day3                                     
   $ cd github_page/                                                                                                                     
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page                           $ ls                                                                                css/  gulpfile.js  img/  index.html  js/  LICENSE  package.json  package-lock.json  README.md  scss/  vendor/  
   ```

5. github로 접속해서 New repository를 만든다.

6. New repository 이름을 wnsgur9648.github.io로 만든다.

7. 새로 만든 repository에 압축을 푼 파일들을 전부 업로드

   ```
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page                         
   $ git init                                                                         Initialized empty Git repository in C:/Users/student/Documents/week2/day3/github_page/.git/   
   
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git add .                                                                                                                           `
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git commit -m "first commit"              
   
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git remote add origin https://github.com/wnsgur9648/wnsgur9648.github.io.git                                                        
   student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git push -u origin master
   ```

> github에서 settings -> github pages로 간다. (자신의 도메인을 설정할 수도 있다.)



8. wnsgur9648.github.io로 들어가본다. 확인 완료

9. 로컬 컴퓨터에서 index.html을 vscode로 원하는대로 편집하고 저장하면서 확인

   -> 원하는 곳을 확인해보기 위해서 인터넷 창에서 요소검사를 해본다.

10. 수정한 부분을 재업로드 하기

    ```
    student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git add .                                                                         warning: LF will be replaced by CRLF in index.html.                                 The file will have its original line endings in your working directory                                                                
    student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git commit -m "my profile"                                                       [master 1fed2bd] my profile                                                         1 file changed, 17 insertions(+), 102 deletions(-)                                                                                   
    student@M70213 MINGW64 ~/Documents/week2/day3/github_page (master)                 $ git push                                                                         Enumerating objects: 5, done.                                                        Counting objects: 100% (5/5), done.                                                 Delta compression using up to 12 threads                                           Compressing objects: 100% (3/3), done.                                             Writing objects: 100% (3/3), 765 bytes | 765.00 KiB/s, done.                       Total 3 (delta 2), reused 0 (delta 0)                                               remote: Resolving deltas: 100% (2/2), completed with 2 local objects.               To https://github.com/wnsgur9648/wnsgur9648.github.io.git                           59773ff..1fed2bd  master -> master        
    ```



# 2. Cloud9



1. Cloud9에서 온 메일을 통해서 회원 가입을 한다. 이때 카드를 등록하라고 할 수도 있는데 그냥 등록하면 된다.
2. 회원 가입을 한 다음 Workspace를 만드는데 이름은 자기 마음대로 정하고 Template만 Blank로 선택을 하고 생성
3. [https://github.com/sspy/install_python](https://github.com/sspy/install_python)로 들어가서 해당 절차를 따라하면  자신의 Cloud9 Workspace에 설치할 수 있다.



- pyenv 설치

```
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```



- 환경변수 설정

```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
$ source ~/.bashrc -> 위의 설정한 내용들을 실제로 적용하는 것
$ reset -> 터미널창을 리셋한다.
$ pyenv -v -> 제대로나오면 설치됨
pyenv 1.2.8-5-gec9fb549

```



- 파이썬 설치

```
$ pyenv install 3.6.7 # pyenv를 통해서 python 3.6.7을 설치 
$ pyenv global 3.6.7 # 전역으로 버전 설정 -> 원래 설치되어 있는 버전을 업그레이드 시켜준다.
$ python -V # 파이썬 버전 확인
$ pyenv versions # 사용가능한 파이썬 버전 리스트 출력
```



- 파이썬 패키지 설치

```
$ pip install bs4
$ pip install requests
```



- 전 시간에 작성했던 파이썬 크롤링 코드가 Cloud9에서 작동하는지 확인

```python
import requests
import time
from bs4 import BeautifulSoup as bs
today = time.strftime("%a").lower()
# 1. 네이버 웹툰을 가져올 수 있는 주소를 파악하고 url 변수에 저장한다.
url = "https://comic.naver.com/webtoon/weekdayList.nhn?week={}".format(today)
# 2. 해당 주소로 요청을 보내 정보를 가져온다.
response = requests.get(url).text
# 3. 받은 정보를  bs를 이용하여 검색하기 좋게 만든다.
soup = bs(response, 'html.parser')
# 4. 네이버 웹툰 페이지로 가서 내가 원하는 정보가 어디 있는지 파악한다.
toons = []
li = soup.select('.img_list li')
for item in li:
  toon = {
    "title" : item.select('dt a')[0].text, #==item.select_one('dt a').text
    "url" : item.select('dt a')[0]["href"],
    "img_url" : item.select('.thumb img')[0]["src"]}
  toons.append(toon)
print(toons)
```





# 3. Flask(경량화 웹 프레임워크)



- Flask 설치

```
$ pip install flask
```



- Cloud9 Workspace에서 app.py를 만든다.

```
$ touch app.py
```

*app.py*

```python
#app.py
from flask import Flask

app = Flask(__name__)

@app.route('/index')
def index():
	print("hi")
	return "" #이 부분을 바꿔주면 화면에 글씨를 나타나게 할 수있다.
```



- 서버 작동

```
$ flask run --host 0.0.0.0 --port 8080
```

-> 서버 작동 후 http://ssafy-week2-wnsgur9648.c9users.io:8080/index로 들어가면 빈화면이 나온다.



- Flask 설정  (파일을 수정하고 적용 시킬려면 서버를 껐다 켜야 하는데 번거로움을 없애기 위해서 해당 설정을 넣는다. -> 수정하고 ctrl+s를 하면 자동으로  적용됨)

```
$ echo 'export FLASK_ENV=development' >> ~/.bashrc
$ source ~/.bashrc -> 이걸 안해주면 설정이 적용 안됨
$ flask run --host 0.0.0.0 --port 8080
- Environment: development
- Debug mode: on
- Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
- Restarting with stat
- Debugger is active!
- Debugger PIN: 172-321-668
- Detected change in '/home/ubuntu/workspace/day3/app.py', reloading
- Restarting with stat
- Debugger is active!
- Debugger PIN: 172-321-668
  10.240.1.30 - - [19/Dec/2018 04:32:23] "GET / HTTP/1.1" 404 -
  hi
  nice to meet you
  10.240.0.64 - - [19/Dec/2018 04:32:28] "GET /index HTTP/1.1" 200 -
```



- 네이버 웹툰 크롤링 코드 넣어서 크롤링한 정보 웹페이지에 나오게 하기

```python
from flask import Flask
import requests
import time
from bs4 import BeautifulSoup as bs

app = Flask(__name__)

@app.route('/index')
def index():
	print("hi")
	print("nice to meet you")
	return """
	<h1>유병재 잘생김</h1>
	<h3>Hello world</h3>
	<img src="~~~~~~"></img>
	"""

@app.route("/naverToon")
def naver_toon():
	today = time.strftime("%a").lower()
	# 1. 네이버 웹툰을 가져올 수 있는 주소를 파악하고 url 변수에 저장한다.
	url = "https://comic.naver.com/webtoon/weekdayList.nhn?week={}".format(today)
	
	# 2. 해당 주소로 요청을 보내 정보를 가져온다.
	response = requests.get(url).text
	
	# 3. 받은 정보를  bs를 이용하여 검색하기 좋게 만든다.
	soup = bs(response, 'html.parser')
	
	# 4. 네이버 웹툰 페이지로 가서 내가 원하는 정보가 어디 있는지 파악한다.
	toons = []
	li = soup.select('.img_list li')
	
	for item in li:
	  toon = { 
	    "title" : item.select('dt a')[0].text, #==item.select_one('dt a').text
	    "url" : item.select('dt a')[0]["href"], 
	    "img_url" : item.select('.thumb img')[0]["src"]}
	  toons.append(toon)
	  
	return "{}".format(toons)
```

 -> http://ssafy-week2-wnsgur9648.c9users.io:8080/naverToon으로 들어가면 크롤링한 정보가 나온다.





- html 파일 분리해서 저장

  -> return에 너무 긴 html 문서는 넣기 불편하므로 return자리에 html문서 자체 template을 넣어줄 수 있도록 해준다.



1. app.py안에 `from flask import Flask, render_template`를 넣어준다.

2. 파이썬 파일에서 해당  html 파일을 불러오기 위해서는 같은 경로상에 있는 template들이 모여있는 폴더에 html문서가 존재해야하고 해당 폴더의 이름은 templates로 정해져 있다. templates 폴더안에 자신이 rendering 하기 원하는 html 파일을 모두 넣어 놓는다.

3. `return render_template("naver_toon.html")`로 return하기를 원하는 html 파일을 보낸다.

```python
from flask import Flask, render_template
...
...
...	  
return render_template("naver_toon.html")
```



> html문서 내에서 특수 기호 없이 파이썬 코드가 동작하지 않는다.

- html문서 내에서 파이썬 코드를 동작시켜주는 2가지 방법이 있다.

  - {{ }} -> 우리 눈에 보이는것(변수 같은 것들을 담아준다.)

    ex) {{toon}}

  - {% %} -> 우리 눈에 보이지 않는 것(파이썬 문법들을 쓸 때 사용 ex) for, if...)

    ex) {% for i in range(5):%}

    ​      {% endfor %}



*naver_toon.html*

```html
<!DOCTYPE html>
<html>
    <head>     
    </head>
    <body>
        <h1>Naver Webtoon 모아보기</h1>
        {% for i in range(5) :%}
            {{t}}
        {% endfor%}
    </body>
</html>
```





- 원하는 인자를 넘겨주고 싶을 경우 `return render_template("naver_toon.html", t=toons)`

  html문서에서 넘겨받은 인자를 사용할 수 있다.



*naver_toon.html*

```html
<!DOCTYPE html>

<html>
    <head>
        
    </head>
    <body>
        <h1>Naver Webtoon 모아보기</h1>
        <table>
            <thead>
                <tr>
                    <th>썸네일</th>
                    <th>웹툰 제목</th>
                    <th>웹툰 링크</th>
                </tr>
            </thead>
            {%for i in t:%}
            <tbody>
                <tr>
                    <td><img src="{{i["img_url"]}}"></img></td>
                    <td>{{i["title"]}}</td>
                    <td><a href="{{i["url"]}}">클릭</a></td>
                </tr>
            </tbody>
            {% endfor %}
            
        </table>
    </body>
</html>
```





# 4. Python 연습문제



*test.py*

```python
#test.py
"""
파이썬 dictionary 활용 기초!
"""
import operator

# 1. 평균을 구하세요.
iu_score = {
    "수학": 80,
    "국어": 90,
    "음악": 100
}

# 답변 코드는 아래에 작성해주세요.
result=0
for i in iu_score.keys():
    result+=iu_score[i]

result/=len(iu_score)
print("{}".format(result))

#print(sum(list(iu_score.values()))/len(iu_score.values()))

# 2. 반 평균을 구하세요.
score = {
    "iu": {
        "수학": 80,
        "국어": 90,
        "음악": 100
    },
    "ui": {
        "수학": 80,
        "국어": 90,
        "음악": 100
    }
}
# 답변 코드는 아래에 작성해주세요.
result=0
cnt=0
for person in score.keys():
    for subject in score[person].keys():
        result+= score[person][subject]
        cnt+=1
result/=cnt

print("{}".format(result))

# 3. 도시별 최근 3일의 온도 평균은?
"""
출력 예시)
서울 : 값
대전 : 값
광주 : 값
부산 : 값
"""
# 3-1. 도시 중에 최근 3일 중에 가장 추웠던 곳, 가장 더웠던 곳은?
city = {
    "서울": [-6, -10, 5],
    "대전": [-3, -5, 2],
    "광주": [0, -2, 10],
    "부산": [2, -2, 9],
}

# 답변 코드는 아래에 작성해주세요.
ondo=0
for c in city.keys():
    for tem in city[c]:
        ondo+=tem
    ondo/=len(city[c])
    print("{} : {:.1f}".format(c, ondo))
    ondo=0

# 답변 코드는 아래에 작성해주세요.
first=True
max_tem=tem
max_city=c
min_tem=tem
min_city=c
 
for c in city:
    for tem in city[c]:
        if first :
            max_tem=tem
            max_city=c
            min_tem=tem
            min_city=c
            first=False

        else:
            if max_tem < tem:
                max_tem=tem
                max_city=c

            if min_tem > tem:
                min_tem=tem
                min_city=c 

print("가장 추웠던 곳 : {}, {}도".format(min_city, min_tem))
print("가장 더웠던 곳 : {}, {}도".format(max_city, max_tem))
          
# 4. 위에서 서울은 영상 2도였던 적이 있나요?
# 답변 코드는 아래에 작성해주세요.
# 1. cities 변수에서 서울부분만 추출해서 seoul변수에 저장한다.
# 1-1. flag 라고 하는 변수에 false 저장한다.
# 2. seoul 변수(list)를 순회하며 요소가 2와 같았던 적이 있는지 확인한다.
# 3. 2도 같았던 적이 있다면 flag 변수를 true로 바꿔준다.
# 4.flag변수에 따라 출력문을 작성한다.
if 2 in city["서울"]:
    print("서울은 영상 2도였던 적이 있습니다.")
else:
    print("서울은 영상 2도였던 적이 없습니다.")
```


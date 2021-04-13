# python 가상환경에서 django 프로젝트

## python 가상환경

### 가상환경 만들기

window

```shell
python -m venv venv
```

- python : 파이썬 관련 명령어 실행
- -m : 옵션 (명령어를 실행하기 위한 옵션)
- venv : 가상환경을 만드는 명령어
- venv : 가상환경이름 (현재는 venv라는 이름을 사용하고 있고, 특별한 이유가 없다면 venv로 편하게 작성하자)

macOS

```shell
python3 -m venv venv
```

### 가상환경 적용하기


window

```shell
source venv/Scripts/activate
```

- source : 코드 적용 명령어
- venv/Scripts/activate : 적용할 코드 경로

macOS

```shell
source venv/bin/activate
```


### 가상환경 해제하기

```shell
deactivate
```

- 그래도 동작이 이상하다? 터미널 종료!




### .gitignore

`.gitignore` 생성 및 `venv/` 추가

```text
venv/
```


### install django

```shell
pip install django
```



## django

### Start Project

Django 코드 전체는 `프로젝트(PROJECT)`라는 이름으로 관리합니다.

`django-admin startproject <PROJECTNAME>` 명령어를 통해 프로젝트의 시작을 알립니다.

```shell
django-admin startproject intro
```
- 예시에서는 `intro`라는 이름으로 프로젝트를 생성했습니다.

작성한 프로젝트 이름대로 폴더가 생성됩니다.

```text
# 프로젝트 구조
intro/
    intro/
    manage.py
```

아래와 같이 경로(`.` : 따로 폴더를 생성하지 않고 현재 경로에서 프로젝트를 시작하겠다는 의미)를 직접 지정할 수도 있습니다.

```shell
django-admin startproject intro .
```

- 예시에서는 `intro`라는 이름으로 프로젝트를 생성했습니다.

```text
# 프로젝트 구조
intro/
manage.py
```

- 반드시 두 가지 방법 모두 사용해보시면서, 차이점을 확인해주세요!


### Run Server

첫 번째 방식(경로 지정 없이)으로 프로젝트를 생성한 경우 `PROJECT` 생성 후에 `cd <PROJECTNAME>` 명령어로 해당 프로젝트로 이동합니다.

**반드시 `manage.py` 가 존재하는 경로에서 `python manage.py runserver` 명령어를 통해 서버를 실행합니다.**

**`ls` 명령어를 터미널에 입력해서 현재 경로에 `manage.py`가 있는지 꼭! 확인해주세요**

```shell
cd intro
python manage.py runserver
```

두 번째 방식(경로 지정)으로 프로젝트를 생성한 경우, 현재 경로에서 그대로 진행합니다.

**반드시 `manage.py` 가 존재하는 경로에서 `python manage.py runserver` 명령어를 통해 서버를 실행합니다.**

**`ls` 명령어를 터미널에 입력해서 현재 경로에 `manage.py`가 있는지 꼭! 확인해주세요**

```shell
python manage.py runserver
```

서버가 돌아가고 있어야지만 웹 브라우저를 통해 서비스를 이용할 수 있습니다.

귀여운 로켓을 확인해주세요!

- 서버 종료 : `ctrl + c`


### startapp

#### 앱 생성


Django 개발에서는 일반적으로 기능 단위 별로 코드를 관리하게되는데, 그 별개의 단위를 `APPLICATION`이라는 이름으로 부릅니다.

`python manage.py startapp <APPNAME>` 명령어를 통해 `APP`을 생성합니다.

**반드시 `manage.py` 가 존재하는 경로에서 `python manage.py runserver` 명령어를 통해 서버를 실행합니다.**

**`ls` 명령어를 터미널에 입력해서 현재 경로에 `manage.py`가 있는지 꼭! 확인해주세요**

```shell
python manage.py startapp pages
```

- 예시에서는`pages`라는 이름의 앱을 생성했습니다.


#### 앱 등록

- 반드시 생성 후에 등록!

(생성 전에 등록을 먼저 시도한다면 `아직은 없는 APP`이기 때문에 에러가 발생하면서 명령어가 정상적으로 동작하지 않습니다. 꼭 생성을 먼저해주세요!)

`<PROJECTNAME>/settings.py`의 `INSTALLED_APPS`에 생성한 앱을 추가해줍니다.

```python
# intro/settings.py

.
.
.

# Application definition

INSTALLED_APPS = [
    'pages',
    .
    .
]
```

### Develop APP

가장 기본이 되는 앱 기능을 구현합니다.

`urls.py`에서는 

어떤 url로 접근했을 때, `views.py`의 어떤 함수와 연결될지 결정하게 됩니다.

기본적으로는 `<PROJECTNAME>/urls.py`에서 처리하지만, 기능별로 `urls.py`을 따로 처리할 수도 있습니다.


**가장 기본이 되는 개발 순서는 다음과 같습니다.**

#### 1. `urls.py`

```python
# intro/urls.py
from django.contrib import admin
from django.urls import path
# 1. from 앱이름 import views 를 통해 python 코드를 불러오고,
from pages import views

urlpatterns = [
    path('admin/', admin.site.urls),
    # 2. url과 위에서 불러온 views의 특정 함수를 연결해줍니다.
    path('lotto/', views.lotto),
]
```

- 앞서 언급한대로, `views.py`의 특정 함수와 `url`을 연결 해줘야하는데, 예시의 `pages`앱에는 아직 `lotto`라는 함수가 없습니다. 바로 만들어주러 이동하겠습니다.

#### 2. `views.py`

> Q. APP 생성할 때는 생성 후 등록하라고 했는데, 함수는 상관없나요?
>
> A. 이왕이면, 생성 후에 등록하시는게 좋습니다. 다만 지금 설명의 흐름은 (브라우저를 통해) 유저가 우리의 서비스를 이용한다는 생각을 갖고, 해당 프로세스를 고려해여 진행하고 있습니다. 
>
> (유저가 브라우저에서 url로 접근한다 -> 우리의 서버에서는 어떤 일이 일어날까?)

`pages`앱으로 이동하여 함수 `lotto`를 생성해줍니다.

```python
# pages/views.py

from django.shortcuts import render
import random 

def lotto(request):
    numbers = range(1, 46)
    lotto = random.sample(numbers, 6)
    context = {
        'lotto': lotto,
    }
    return render(request, 'lotto.html', context)
```
- 예시에서는 `lotto.html`이라는 HTML 파일 하나를 랜더할 예정입니다. 이젠 해당 HTML 파일을 생성하러 이동 하겠습니다.
- 현재까지의 프로세스 : `url`로 접근한다 -> `lotto`라는 함수로 연결된다 -> `lotto`함수에서 `lotto.html`이라는 HTML파일을 랜더한다.

#### 3. templates

`pages`에 `templates`라는 폴더를 생성합니다.

**`templates`라는 폴더가 오타가 나지 않도록 주의합니다. 지금 다시 한번 확인합니다.**

- 현재 기본값으로 `templates`라는 폴더이름이 지정되어 있기 때문에, 폴더명을 틀리면 제대로 동작하지 않습니다.

그리고 `templates`폴더에 `lotto.html` HTML 파일을 생성합니다.

```HTML
<!-- lotto.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>로또 번호 생성</title>
</head>
<body>
  <h1>제 OOO회 로또 번호 추천</h1>
  <p>로또 번호는 {{ lotto }}입니다.</p>
</body>
</html>
```

웹 브라우저에서 `http://127.0.0.1:8000/lotto`로 이동해 확인합니다.

## 0818 수업 내용

### URL name

하드코딩을 없앤다!!!! url을 직접 수정하거나 관리하지않고, 별명을 통해 관리한다!

- 각각의 앱의  `urls.py` 

`app_name=앱이름`

`name=별명`



- url template tag 사용법

`action="{% url '앱이름:별명'%}"` (form 태그 기준)





### NAME SPACE

파일 구조가 다음과 같다

```text
articles/

	templates/

		index.html



pages/

	templates/

		index.html
```


`return render(request, 'index.html')` 이라고 했을 때, 어떤 걸 render하게 될까? 

- `INSTALLED_APPS` 에 등록된 순서로 찾게 된다.



어떻게 해결해야할까?

- templates 폴더 안에서 앱 이름으로 폴더를 하나 더 구성한다.

```text
pages/

	templates/

		pages/

			index.html
```

- `return render(request, 'pages/index.html')` 라고 수정한다.





### Template 상속

- 코드 재사용!!
- 동일하게 반복되는 코드를 한 파일에 작성을 한다.
- 그 파일을 상속해준다.



```python
# 프로젝트이름/settings.py

.
.
.
TEMPLATES = [
    {
        .
        'DIRS': [BASE_DIR / 'practice' / 'templates'],
        .
        .
        .
    },
]
```

```text
practice/

	manage.py

	practice/

		templates/

			base.html
```


- `base.html`

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  .
  .
  .
  {% block content %}
  {% endblock %}
  .
  .
  .
</body>
</html>
```



- `상속받는쪽.html`

```html
{% extends 'base.html' %}

{% block content %}
현재 페이지에서 보여줄 내용
{% endblock %}
```


https://docs.djangoproject.com/ko/3.0/misc/design-philosophies/
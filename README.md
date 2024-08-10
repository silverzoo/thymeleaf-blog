## 🍃 Thymeleaf 🍃 로 제작한 블로그
### 기본 문법과 표현식
#### 기본 문법

문서 최상단에 ‘`<html xmlns:th=”http://www.thymeleaf.org”>`‘ 코드를 넣어서 사용 가능하다.

<br>

#### 표현식

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| ${...} | 변수 표현식 | ${user} |
| *{...} | 선택 변수 표현식 | *{age} |
| #{...} | 메시지 표현식 | #{welcome.message} |
| @{...} | 링크 URL 표현식 | @{${product.imageUrl}} |
| ~{...} | 프래그먼트 표현식 | th:replace="~{fragments/header :: header}" |
| ${수식} | 계산 표현식 | ${user.age + 1} |

- **선택 변수 표현식**: `*{age}`

  부모 요소에서 변수 표현식으로 사용한 user 객체의 필드 age에 대한 값을 불러올 수 있다.
  즉, `${person.name}`과 같은 의미로 사용될 수 있다.

    ```html
    <div th:object="${person}">
        <p th:text="|이름 : *{name}|"></p>
        <p th:text="|이름 : ${person.name}|"></p>  <!--  위와 동일  -->
    </div>
    ```

- **메시지 표현식**: `#{welcome.message}`

  `messages.properties` 파일에서 아래와 같이 메시지를 설정할 수 있다. 이때, 메시지 표현식을 사용해 `welcome.message` 키의 값을 가져와 텍스트로 설정할 수 있다.

    ```
    welcome.message=Welcome to our website!
    ```

- **프래그먼트 표현식**: `th:replace="~{fragments/header :: header}"`

  ‘fragments’ 디렉토리에 위치한 ‘header.html’이라는 파일에서 `<header th:fragment="header"></header>` 처럼 ‘header’라는 이름의 HTML 조각인 프래그먼트를 불러와 사용할 수 있다.

<br>

#### 문법

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| th:text | 텍스트 값을 설정 | <p th:text="${message}"></p> |
| th:each | for-each 반복문 | <tr th:each="user : ${userList}"></tr> |
| th:if | if 조건문 | <div th:if="${condition}"></div> |
| th:unless | if not 조건문 | <div th:unless="${condition}"></div> |
| th:href | 링크 URL을 설정 | <a th:href="@{/path}"></a> |
| th:with | 로컬 변수를 선언 | <div th:with="localVar=${var}"></div> |
| th:object | 폼 객체를 설정 | <form th:object="${object}"></form> |

<br>

#### 템플릿 조각

재사용 가능한 HTML 조각을 정의하고 호출할 수 있다. 해당 표현식을 활용하여 footer나 header과 같이 공통적으로 들어가는 레이아웃 부분들을 호출할 수 있다.

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| th:insert | 기존 유지, 자식으로 삽입 | th:insert="~{fragments/header :: header}"> |
| th:replace | 완전히 교체 | th:replace="~{fragments/header :: header}"  |

- `th:insert`: HTML 요소의 자식으로 삽입한다. 기존 자식들은 그대로 유지가 된다.
- `th:replace`: HTML 요소를 전체적으로 교체한다. 기존 자식들은 프래그먼트로 완전히 교체된다.
- `layout.html 예시`:

  ‘title’과 ‘main’ 두 매개변수를 받는 프래그먼트를 정의한다. ‘content’에 ‘main’의 이름의 코드가 삽입된다.

    ```html
    <html xmlns:th="http://www.thymeleaf.org"
          th:fragment="layout(title, content)"
          class="bg-gradient-to-br from-gray-50 to-blue-50">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title th:replace="${title}">Elice Blog</title>
        <script src="https://cdn.tailwindcss.com"></script>
        <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
        <script src="https://cdn.jsdelivr.net/npm/feather-icons/dist/feather.min.js"></script>
        <style>
            body {
                font-family: 'Inter', sans-serif;
            }
        </style>
    </head>
    <body class="text-gray-800 leading-relaxed">
        <div th:replace="~{fragments/header :: header}"></div>
        <div th:replace="${content}"></div>
        <div th:replace="~{fragments/footer :: footer}"></div>
    
        <script>feather.replace()</script>
        <script src="/js/article.js"></script>
    </body>
    </html>
    ```

  실제 ‘content’의 내용은 아래의 문법을 사용한 html 파일들의 내용이 담긴다. 아래 코드는  ‘layout.html’ 파일의 ‘layout’ 프래그먼트를 사용하고, ‘title’과 ‘main’이라는 두 개의 매개변수를 전달한다는 의미이다.

    ```html
    <html xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)"
    th:replace="~{layout :: layout(~{::title}, ~{::main})}">
    <!-- Other HTML content here -->
    </html>
    ```
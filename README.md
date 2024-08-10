## 🍃 Thymeleaf 🍃 로 제작한 블로그
### 기본 문법과 표현식

#### 기본 문법

문서 최상단에 ‘`<html xmlns:th=”http://www.thymeleaf.org”>`‘ 코드를 넣어서 사용 가능하다.

<br>

#### 표현식

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| ${...} | 변수 표현식 |  |
| *{...} | 선택 변수 표현식 |  |
| #{...} | 메시지 표현식 |  |
| @{...} | 링크 URL 표현식 |  |
| ~{...} | 프래그먼트 표현식 |  |
| ${수식} | 계산 표현식 | ${user.age + 1} |

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

재사용 가능한 HTML 조각을 정의하고 호출할 수 있다.

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| th:insert |  |  |
| th:replace |  |  |
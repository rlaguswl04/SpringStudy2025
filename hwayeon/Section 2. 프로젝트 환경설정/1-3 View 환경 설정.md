# 1-3 View 환경 설정

**Welcome page 만들기**

- **index.html 파일 생성**
    
    src/main/ resources/static/index.html
    

`<!DOCTYPE HTML>`

`<html>`

`<head>`

    `<title>Hello</title>`

    `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">`

`</head>`

`<body>`

`Hello`

`<a href="/hello">hello</a>`

`</body>`

`</html>`

→ 서버 재실행 후, localhost:8080에 접속하면 Hello hello가 뜸

- **스프링 부트가 제공하는 Welcome Page 기능**
    - static/index.html을 올려두면 Welcome page 기능을 제공한다.
    - [spring.io](http://spring.io/) → project → spring boot → [Reference Doc.](https://docs.spring.io/spring-boot/index.html) → Documentation → Learning About Spring Boot Features → Welcome page 검색
    - [https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content](https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content)

![image.png](1-3%20View%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%2018749aa13a60801e99bdfa2dc6883c01/image.png)

![image.png](1-3%20View%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%2018749aa13a60801e99bdfa2dc6883c01/image%201.png)

→ 메뉴얼에서 검색하는 능력 필요

현재 만들어진 웰컴 페이지는 단순히 html 파일을 띄어준 정적 페이지이다. 동적 페이지를 만들기 위해 thymeleaf 템플릿 엔진을 사용 

- **thymeleaf 템플릿 엔진**
    - tjymeleaf 공식 사이트: [https://www.thymeleaf.org/](https://www.thymeleaf.org/)
    - 스프링 공식 튜토리얼: [https://spring.io/guides/gs/serving-web-content/](https://spring.io/guides/gs/serving-web-content/)
    - 스프링부트 메뉴얼: [https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-template-engines](https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-template-engines)
        
        → template engine 검색
        
        ![image.png](1-3%20View%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%2018749aa13a60801e99bdfa2dc6883c01/image%202.png)
        

**Controller(컨트롤러)**

- **Controller**

웹 애플리케이션의 첫 번째 진입점

- **controller 패키지 생성, Hellocontroller 클래스 생성 하여 코드 작성**main/java/hello.hello_spring/controller/Hellocontroller
    - @Controller
    - @GetMapping - 웹 애플리케이션에서 \hello라고 들어오면 이 메서드를 호출 해줌
    - model.addAttribute(attributeName, attributeValue)

`package hello.hello_spring.controller;`

`import org.springframework.stereotype.Controller;`

`import org.springframework.ui.Model;`

`import org.springframework.web.bind.annotation.GetMapping;`

`@Controller`

`public class HelloController {`

    `@GetMapping("hello")`

    `public String hello(Model model) {`

        `model.addAttribute("data", "hello!!");`

        `return "hello";`

    `}`

`}`

- **hello.html 파일 생성**
    
    resources/templates/hello.html
    

`<!DOCTYPE HTML>`

`<html xmlns:th="http://www.thymeleaf.org">  <!-- Thymeleaf 템플릿 엔진 선언, 선언시 Tymeleaf 문법 사용 가능-->`

`<head>`

    `<title>Hello</title>`

    `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />`

`</head>`

`<body>`

`<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>  <!-- Thymeleaf의 th-->`

`</body>`

`</html>`

`${data}`

→ model.addAttriute의 key 값으로 넣었던 data를 의미

value 값 hello!!로 치환 

- **thymeleaf 템플릿 엔진 동작 확인**

[http://localhost:8080/hello](http://localhost:8080/hello)

안녕하세요. hello!!

페이지 소스 보기 - controller에서 작성했던 hello!! 확인 가능

![image.png](1-3%20View%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%2018749aa13a60801e99bdfa2dc6883c01/image%203.png)

- **동작 환경 그림**

![image.png](1-3%20View%20%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%2018749aa13a60801e99bdfa2dc6883c01/image%204.png)

1. 웹 브라우저에 locolhost:8080/hello 검색 
2. 내장 톰켓 서버가 받아 /hello란 것이 왔음을 스프링에 던짐
3. helloController @GetMapping(”hello”) - http URL을 임의로 치면(Get 방식) hello가 URL에 매칭됨 
4. 그러면 helloController에 있는 @GetMapping(”hello”) public String hello(Model model) 메소드가 실행됨
5. 스프링이 model이란걸 만들어서 넣어준다. 그 모델에 .addAttribute를 한 것임. 그 다음 “hello”를 return, 여기서 hello는 resources/templates/hello.html에서 hello와 이름이 같음. 여기로 가서 렌더링 하라는 의미(Thymeleaf 템플릿 엔진 처리)
    
    → 컨트롤러에서 리턴 값으로 문자를 반환하면 뷰 리졸버(viewResolber)가 화면을 찾아서 처리한다.
    
    - 스프링 부트 템플릿 엔진 기본 viewName 매핑
    - resources::templates/ + (ViewName) + .html → ViewName이 hello로 바뀜

참고: spring-boot-devtools 라이브러리를 추가하면, html 파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경 가능

인텔리J 컴파일 방법: 메뉴 build → Recompile
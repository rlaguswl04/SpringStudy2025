# 2-2 MVC와 템플릿 엔진

**MVC(Model, View, Controller)**

- **MVC**

html을 그냥 주는게 아닌 서버에서 프로그래밍하여 동적으로 바꾸어서 내림, 가장 많이 하는 방식, 과거에는  JSP, PHP - 템플릿 엔진

과거  - model1 방식 : controller랑 view가 따로 분리 X, jsp를 이용하여 개발

현재 - MVC 스타일 주로 사용

→ View : 화면을 그리는데 모든 역량 집중 해야 함

Controller, Model : 비즈니스 로직과 관련이 있거나 내부적인 것을 처리하는데 집중 해야 함

- **Controller**

`package hello.hello_spring.controller;`

`import org.springframework.stereotype.Controller;`

`import org.springframework.ui.Model;`

`import org.springframework.web.bind.annotation.GetMapping;`

`import org.springframework.web.bind.annotation.RequestParam;`

`@Controller`

`public class HelloController {`

    `@GetMapping("hello")`

    `public String hello(Model model) {`

        `model.addAttribute("data", "hello!!");`

        `return "hello";`

    `}`

`// 추가`

    `@GetMapping("hello-mvc")`

    `public String helloMvc(@RequestParam("name") String name, Model model) {`

        `model.addAttribute("name", name);`

        `return "hello-template";`

    `}`

`}`

@RequestParam() - 외부에서 파라미터 받기, 외부에서 이름을 웹사이트에서 URL 파라미터로 바꿈

- **View**

resources/templates/hello-tamplate.html

`<html xmlns:th="http://www.thymeleaf.org">`

`<body>`

`<p th:text="'hello ' + ${name}">hello! empty</p>`

`</body>`

`</html>`

- **실행**

http://localhost:8080/hello-mvc

→ 에러

→ why? Required request parameter 'name' for method parameter type String is not present

파라미터 정보 보기 : Ctrl + P

@RequestParam() 파라미터 중 required의 default 값 true이므로 값 넣어 줘야 함, required = false 하면 값 안 넘겨줘도 됨

- **실행**

http://localhost:8080/hello-mvc?name=spring!

hello spring!

→ controller에서 `public String helloMvc(@RequestParam("name") String name, Model model)` name은 spring!으로 바뀜

`model.addAttribute("name", name);`의 name도 spring!으로 바뀌고 모델에 담김

return hello-template로 넘어가면 `${name}` name이 spring!으로 바뀜

model에서 값을 꺼냄, key 값이 name인 것에서 값(spring!)을 꺼내서 치환

- **MVC, 템플릿 엔진 이미지**

![image.png](2-2%20MVC%E1%84%8B%E1%85%AA%20%E1%84%90%E1%85%A6%E1%86%B7%E1%84%91%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BA%20%E1%84%8B%E1%85%A6%E1%86%AB%E1%84%8C%E1%85%B5%E1%86%AB%2018749aa13a6080ebabb5df48cc7ad477/image.png)

1. 웹 브러우저에 localhost:8080/hello-mvc 넘김
2. 내장 톰켓 서버가 hello-mvc 라는 것이 왔음을 스프링에게 던짐
3. 스프링은 helloController에 저 메소드가 매핑 돼있음을 확인하고 return hello-template, model(name:spring)
    
    → viewResolver가 동작(뷰를 찾아주고 템플릿에 연결 시켜줌)
    
4. 찾은 후 Thymeleaf 템플릿 엔진에게 처리 요청
5. 템플릿 엔진은 렌더링 후 변환한 HTML을 웹 브라우저에 반환

페이지 소스 보기

![image.png](2-2%20MVC%E1%84%8B%E1%85%AA%20%E1%84%90%E1%85%A6%E1%86%B7%E1%84%91%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BA%20%E1%84%8B%E1%85%A6%E1%86%AB%E1%84%8C%E1%85%B5%E1%86%AB%2018749aa13a6080ebabb5df48cc7ad477/image%201.png)
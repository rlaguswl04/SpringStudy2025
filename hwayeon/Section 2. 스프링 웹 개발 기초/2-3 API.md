# 2-3 API

**API**

객체를 json 방식으로 바꿔서 반환 ,view 없이 http body에 반환

정적 컨텐츠 방식을 제외하면 

1. MVC 방식 - html을 웹 브라우저에 넘겨줌
2. API 

→ html로 내리기 or API 방식으로 데이터를 바로 내리기

**@ResponseBody 문자 반환** : (HTTP에는 header부와 body부) 이 body부에 return 데이터를 직접 넣어줌

- **Controller에 추가**

`import org.springframework.web.bind.annotation.ResponseBody;`

`@Controller`

`public class HelloController {`

    `@GetMapping("hello-string")`

    `@ResponseBody`

    `public String helloString(@RequestParam("name") String name) {`

        `return "hello " + name;`

    `}`

`}`

@ResponseBody를 사용하면 뷰 리졸버(viewResolver)를 사용하지 않음

대신에 HTTP의 BODY에 문자 내용을 직접 반환(HTML BODY TAG를 말하는 것)

- **실행**

localhost:8080/hello-string?name=string!

hello string!

진짜는 지금부터!

**@ResponseBody 객체 반환**

- **Controller에 추가**

`@Controller`

`public class HelloController {`

    `@GetMapping("hello-api")`

    `@ResponseBody`

    `public Hello helloApi(@RequestParam("name") String name) {`

        `Hello hello = new Hello(); // 객체 생성`

        `hello.setName(name);`

        `return hello; // 문자가 아닌 객체 반환`

    `}`

    `static class Hello { // static 이용하면 클래스 안에서 클래스 사용 가능`

        `private String name;`

        `public String getName() {`

            `return name;`

        `}`

        `public void setName(String name) {`

            `this.name = name;`

        `}`

    `}`

`}` → javabean 규약, 프로퍼티 접근 방 : 메서드를 통해 접근

@ResponseBody를 사용하고, 객체를 반환하면 객체가 JSON으로 변환됨

- **실행**

http://localhost:8080/hello-api?name=spring!

![image.png](2-3%20API%2018749aa13a6080f58f5df3ad01dd6a97/image.png)

json으로 변환됨 - {key, value}로 이루어진 구조

과거에는 xml 방식 많이 사용- <HTML></HTML>

→ json 방식이 더 편리, 요즘에 많이 사용

문장 완성( (); ) 단축키 - Ctrl + Shift + Enter

**@ResponseBody 사용 원리**

- **@ResponseBody를 사용**

![image.png](2-3%20API%2018749aa13a6080f58f5df3ad01dd6a97/image%201.png)

1. 웹 브라우저에 localhost:8080/hello-api
2. 톰켓 내장 서버에서 hello-api가 왔음을 스프링에게 던짐
3. 스프링은 helloController에서 hello-api 확인, @ResponseBody라는 어노테이션이 붙어 있으므로 HTTP의 BODY에 문자 내용을 직접 반환, but 문자가 아닌 객체
4. return하면 HttpMessageConverter가 동작
    - 기본 문자 처리 : StringHttpMessageConverter가 동작
    - 기본 객체 처리 : MappingJackson2HttpMessageConverter가 동작 - json 방식으로 데이터를 만들어서 HTTP 응답에 반환한다.
    - byte 처리 등등 기타 여러 HttpMessageConvert가 기본으로 등록되어 있음
5. 나를 요청한 웹 브라우저에 반환

참고: 클라이언트의 HTTP Accept 헤더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해서 HttpMessageConverter가 선택된다. 더 자세한 내용은 스프링 MVC 강의에서 설명
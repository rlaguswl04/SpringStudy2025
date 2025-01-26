# ✔️Section 3 스프링 웹 개발 기초
- 정적 컨테츠
    - static은 그대로 반환됨
    - 관련 컨트롤러 없음 -> resources 가서 반환
- MVC: Model, View, Contreoller
    - 과거엔 뷰로 모든걸 다 했음 -> 지금은 MVC
    - view= 화면 관련된것만, controller = 나머지
- @GetMapping("~) 일때 locallhost.../~에 들어가면 원하는 내용이 나옴

### RequestParam

- 터미널에 오류 메시지 잘 읽어보기: ^p로 필요한거 보기
    - >~?name == spring! 이렇게 원하는 문자 웹에 띄울 수 있음

### API

- @ResponseBody -> html body 부분에 이 데이터 return 하겠다.
- html 조작 없이 보여줌 (소스코드 보기 해도 없음) ->BUT 이건 별로 안쓰고 데이터로 많이 씀
- ^shift enter : 자동 ); 편함
- json 방식 key:vlaue -> 객체 반환, responsebody면 json이 디폴트(원하면 xml가능)

getter, setter ->private인 name을 얘네를 통해서 외부에서 접근함. (=property 접근방식)

![image](https://github.com/user-attachments/assets/1960a715-b590-4aca-b08f-7ed9d1530613)

**@ResponseBody 사용 원리**

1. 문자면 api 응답에 바로 넣어서 주면 끝(JsonConverter)
2. 객체가 반환이 되면 루틴 = 디폴트대로 json방식으로 데이터 만들어서 api 응답에 반환하겠다.(StringConverter)

(converter 자료에 있는거 실무에서도 거의 그대로 씀)

**정리**

1. 정적 컨텐츠: 그냥 파일 그대로 내림
2. MVC와 템플릿 엔진: 템플릿 엔진을 모델뷰 방식으로 쪼개서 랜더링 된걸 전환
3. api: 객체 반환함

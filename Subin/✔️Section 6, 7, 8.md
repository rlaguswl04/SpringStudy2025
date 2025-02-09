**회원 웹 기능 - 등록**
---
Controller에 createForm @GetMapping으로 만들고





create @PostMapping으로 form 입력 받았을때 그 멤버 객체 만들고 -> setName으로 form에 멤버 만들어짐

 



join해서 멤버 가입으로 넘김 그리고 홈화면으로 돌림



@PostMapping은 데이터 등록할때 @GetMapping은 조회 할 때


**회원 웹 기능 - 조회**
---
@GetMapping으로 Model인 model 받아서 리스트에 넣기

addAttribute로 멤버 리스트를 멤버에 담아서 view로 넘김


**스프링 통합 테스트**
---
@SpringBootTest

@Transactional ->테스트 실행하고 데이터 롤백해줌

-단위단위 테스트가 좋은 테스트





**JdbcTemplate**
---
템플릿 레포지토리

**테스트 케이스 잘 짜는게 중요함

**JPA**
---
gradle jpa 의존성 추가

application에 관련 설정 추가

자동 테이블 생성해줌

코드에서 쿼리 짜줌

JPA에 @Transactional 필요함

**스프링데이터JPA**
---
JPA레포지토리 만들기

인터페이스만으로 구현 끝남

**AOP**
---
모든 메소드의 호출 시간을 측정하고 싶을때

메소드 하나마다 시간 측정 로직 짜면 유지보수 어려움 ->AOP 필요함

공통 관심사항 vs 핵심 관련 사항





"시간 측정 AOP 등록"

@Aspect가 필요함 AOP 사용 위해서

joinPoint마다 호출됨

프록시 사용됨

 
 

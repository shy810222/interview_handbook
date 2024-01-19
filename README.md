Interview Handbook
===============
- 인터뷰를 위한 예상문제를 기초부터 하나씩 정리
- 정리 중에 궁금한 것을 알아본 내용도 추가
- 나중에 내용이 많아지면 분리하고 주기적으로 정리



## 공통 질문
1. 프로세스와 스레드의 차이
    - 프로세스는 운영체제로부터 할당받은 작업의 단위
    - 스레드는 프로세스가 할당받은 자원을 이용하는 실행 흐름의 단위
3. wrapper 타입 설명
4. Stack, Que
    - Stack은 후입선출, Que는 선입선출
5. 프레임워크에 대해서
    - IOC(제어의 역전은 개발자의 코드가 제어를 하는 것이 아닌 제어를 받는 것을 말함) 개념이 적용된 기술이다.
    - 라이브러리는 개발자의 코드가 호출을 하고 프레임워크는 개발자의 코드를 가져다 쓰는 형태이다.

## Front End 질문
### Front End 공통질문
1. 브라우저 렌더링 순서
    - HTML 파싱
    - 파싱 중 javascript구문을 만나면 파싱 중단 후 javascript 파싱 및 실행(단, defer표시로 지연처리를 하면 중단하지 않고 파싱 완료 후 실행)
    - DOM Tree 구축
    - CSS 파싱
    - CSSOM Tree 구축
    - Render Tree 구축(여기서는 화면에 표시하지 않을 DOM요소는 제외)
    - Layout(Reflow)
    - Paint
2. Hoisting
    - var 변수와 함수 선언문을 함수 유효범위 최상단으로 올리는 것을 말한다.(let, const 제외)
    - 함수표현식은 javascript 엔진에 따라 다름
        ```javascript
        console.log(a); // 10
        console.log(b); // Uncaught ReferenceError: b is not defined
        console.log(c); // Uncaught ReferenceError: c is not defined
        console.log(df()); // 40
        console.log(ef()); // webkit: Uncaught ReferenceError: c is not defined, V8에서는 50
        
        var a = 10;
        let b = 20;
        const c = 30;
        
        function df() {
            return 40;
        }
        
        var ef = function() { // var로 선언할 경우 
            return 50;
        }
        ```
3. 클로저
    - 함수의 렉시컬 스코프를 기억하여 실행할 때도 해당 스코프에 접근할 수 있게 하는 것
    - 간단히 말하면 내부 함수가 외부 함수 변수에 접근할 수 있는 것
4. 실행 컨텍스트
    - 실행 컨텍스트는 스택
    - 전역 실행 컨텍스트와 함수 실행 컨텍스트 두 종류가 있음
    - 전역 실행 컨텍스트는 하나만 있으며 함수 실행 컨텍스트는 호출될 때마다 생성
5. 렉시컬 스코프
    - 함수를 선언할 때 상위 스코프가 결정되는 것
      ```javascript
      var a = 10;
      function print1(){
         var a = 20;
         print2();
      }

      function print2(){
         console.log(a);
      }
      
      print1(); // 10
      print2(); // 10
      ```
6. 스코프 체인
    - 상위 함수 스코프 및 전역 스코프 탐색을 위한 스코프 연결 목록
    - 실행 컨텍스트가 실행될 때 상위 함수 및 전역에 참조하는 변수를 찾기 위해 스코프 체인을 탐색
      ```javascript
      var v = "전역 변수";

      function a() {
         var v = "지역 변수1";
         function b() {
            var v = "지역 변수2";
            var z = "지역 변수3";
    	      function c() {
    	         console.log(v);
               console.log(v, z);
            }
            console.dir(c);
         }
      }
      ```
7. 이벤트 루프, 호출 스택(콜스택), 태스크큐, 마이크로태스크큐
    - 이벤트 루프: 브라우저의 동작 타이밍을 제어하는 관리자
    - 실행 우선순위: 마이크로태스크큐(Promis 콜백보다 Mutation Obsever 콜백이 먼저 실행), 태스크큐
    - 호출스택에 쌓인 순서대로 실행하며 이벤트 루프에 의해 비동기 콜백을 호출 스택으로 이동
8. Reflow, Repaint, Composite
    - Reflow는 DOM의 위치가 변경되면 발생
    - Repaint는 background같은 색깔 변경과 같은 경우 발생
    - Composite은 paint 단계에서 나뉜 여러 레이어를 합성해주면 GPU를 사용해 비용이 적게 든다. transform과 같은 속성이 대표적으로 composite만 발생시키는 속성
9. 이벤트 위임과 필요한 이유
    - 하위요소가 많고 공통의 이벤트가 있을 때 상위 요소에 이벤트를 추가하는 방법으로 event bubling에 의해 이벤트가 실행됨
    - 하나의 이벤트 핸들러만 필요하기에 최적화에 좋고 하위요소의 변동이 있을 때마다 이벤트 해제 및 바인딩 필요가 없음
10. this에 대한 설명
    - 호출이 될 때 값이 결정이 되며 호출방식에 따라 달라짐
    - new나 객체의 함수 호출은 해당 객체, apply, call, bind는 인수 객체, 그외는 use strict면 undefined 아니면 window
11. Browserslist
    - 빌드 시 지원 브라우저에 따라 폴리필의 내용이나 빌드 경과가 달라지는데 지원 브라우저를 선택하는 기능을 제공
    - .browserslistrc 파일 혹은 package.json에 정의하는 방법이 있으며 package.json에 정의하는 것을 공식 사이트는 권장
    

### React 질문

### Vue 질문


## Back End 질문
### Spring 질문
1. Bean 종류
   - 싱글톤 스코프: 스프링 컨테이너가 사라지기전까지 한개만 유지하며 별다른 설정이 없으면 싱글톤 스코프로 생성된다.
   - 프로토타입 스코프: DI가 발생할 때마다 새로운 객체가 생성되어 주입된다
   - 웹 스코프: Request, Session, Application, WebSocket 총 네개가 있으며 생명주기는 이름과 동일하다
2. 싱글톤 빈 생명주기
   - 스프링 컨테이너 생성 -> 빈 생성 -> DI 주입 -> 초기화 콜백 -> 사용 -> 소멸 전 콜랙 -> 스프링 종료
4. 프로토타입 빈 생명주기
   - 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존 관계 주입 -> 초기화 콜백 -> 사용 -> GC 수거
6. Component와 Bean 등록 차이점
   - Annotation의 위치가 다르다
   - Component는 ComponentScan에 의 해서 자동으로 등록된다
   - Bean 직접 등록을 해야하면 @Configuration에서 하는 것을 무조건 권장한다(CGLib로 프록시 패턴을 적용해 수동으로 등록하는 빈의 싱글톤 보장)
7. @Configuration proxyBeanMethods
   - proxyBeanMethods을 false로 설정할 경우 Configuration에서 등록하는 빈의 싱글톤을 보장하지 않는다
9. DI(의존성 주입)
   - 의존성 주입은 생성자, 필드, Setter 주입 세가지가 있고 생성자 주입을 가장 권장한다.
   - !왜 생성자 주입을 권장하는가? -> 생성자 주입을 해야 빈이 생성될 때 1번만 주입이 가능하여 객체의 불변성이 보장되고 단위 테스트가 쉽다.
10. AOP - Aspect Oriented Programming(관점 지향 프로그래밍)
    1. AOP 주요개념
       - Aspect: 관심사를 모듈화한 것
       - Target: Aspect를 적용하는 대상이 되는 객체
       - Advice: 실제 기능을 담은 구현체
       - JoinPoint: Advice가 적용될 시점이며 스프링 AOP는 프록시 방식을 사용해 항상 메서드 실행 시점이다
       - PointCut: JoinPoint 중에서 Advice가 적용될 위치를 선별하며 스프링 AOP는 메서드 실행 시점만 가능하다
    2. AOP 실행 시점 지정 Annotation
       - Before: 타겟 메소드가 호출되기 전에 어드바이스 수행
       - After: 결과(성공, 예외)와 관계없이 타겟 메소드가 완료되면 어드바이스 수행
       - AfterReturning: 타겟 메소드가 정상 수행 후 어드바이스 수행
       - AfterThrowing: 타겟 메소드가 예외를 던지면 어드바이스 수행
       - Around: 어드바이스가 타겟 메소드를 감싸서 호출 전과 후에 어디바이스를 수행
       - 동작 순서는 Around(타겟 실행 전) -> Before -> AfterThrowing -> AfterReturning -> After -> Around(타겟 실행 후)
    3. Pointcut 종류
       - execution: (접근제어자? 반환타입 선언타입?메서드이름(파리미터) 예외?)
       - within: 타입이 매칭되면 그 안의 모든 메서드가 매칭된다.
       - args, @target, @within: 단독으로 사용하면 안되고 주의가 필요함
       - @annottaion: 메서드에 해당 annotation이 있을 경우 매칭된다
       - bean: 스프링 빈 이름으로 매칭된다
    4. CGLib와 JDK 동적 프록시
       - 인터페이스가 없다면 CGLib로 프록시 생성
       - JDK 동적 프록시는 구체 클래스로 타입 캐스팅 불가능하다(MemberServiceImpl 프록시 생성 시 MemberService로는 타입캐스팅이 가능하나, MemberServiceImpl로는 타입캐스팅이 불가능)
       - CGLib는 구체 클래스로 타입 캐스팅 가능(MemberServiceImpl 프록시 생성 시 MemberService 및 MemberServiceImpl로 타입캐스팅 가능)
    5. Filter, Interceptor, AOP 순서 및 차이점
       - 순서는 Filter(pre) -> Interceptor(pre) -> AOP -> Interceptor(post) -> Filter(post)
       - Filter는 스프링이 아닌 WAS에서 지원하는 영역으로 스프링 빈을 사용할 수 없다.(해당 사항에 대해서 확인 필요!!)
       - Interceptor는 스프링 영역이나 요청이 Controller 전, 후, 그리고 view가 그려진 뒤에만 적용이 된다
       - AOP 스프링 빈의 메서드 레벨에 적용이 되며 서비스 로직, controller 등 다양한 위치에서 적용할 수 있다

### JPA(Java Persistence API) 질문
1. JPA란?
    - 자바에서 ORM(Object Relation Mapping) 기술 표준으로 사용되는 인터페이스 모음
    - JPA를 구현한 대표적인 오픈소스는 Hibernate
    - ORM은 객체를 테이블에 자동으로 영속화 해주는 것
2. JPA 장점
    - 반복되는 쿼리 안만들어도 된다
    - 수정하고자 하는 필드 데이터만 수정하는게 쉽다
    - 엔티티의 정보만으로도 DB를 볼 필요가 없음
    - 필드 변경이 발생할 경우 엔티티만 수정
    - 오타 등 컴파일 과정에서 오류 발견
    - DB 벤더 독립성(DB에 종속적이지 않음)
    - 영속성 상태일 때 1차 캐시를 사용하기 때문에 동일성을 보장하며 DB를 중복 조회하지 않는다
4. JPA 단점
    - 러닝커브가 높다
    - 다수 테이블 조인과 같이 복잡하고 무거운 쿼리 작성이 불편하다
    - 연관관계가 복잡할 경우 불편하다
    - OSIV를 사용할 경우 영속성 컨텍스트는 DB와 1:1로 연결되어 있어 커넥션 문제가 발생할 수 있다(확인 필요)
6. 영속성 컨텍스트란?
    - 엔티티를 영구 저장하는 환경 어플리케이션과 DB 사이에 객체를 보관하는 가상의 DB같은 역할
    - EntityManager는 엔티티를 저장 조회 등 영속성 컨텐스트에 엔티티를 보관 및 관리한다
    - 엔티티를 식별자 값으로 구분하기 때문에 반드시 식별자값이 있어야 한다
7. Entity 생명주기
    - 비영속 상태(new/transient): 영속성 컨텍스트와 관계가 없는 상태
    - 영속 상태(managed): 영속성 컨텍스트에 저장된 상태
    - 준영속 상태(detached): 영속성 컨텍스트에 저장되었다가 분리된 상태
    - 삭제 상태(removed): 삭제된 상태
9. open-in-view, open-session-in-view, open-entitymanager-in-view(OSIV)
    - 영속성 컨텍스트를 뷰까지 살아있으며 영속 상태를 유지한다
    - 동시 접속 트래필이 많은 경우 OSIV를 끄고 CQRS 패턴으로 커맨드와 쿼리를 분리하여 해결한다
    - CQRS 패턴: Command(등록 및 수정과 같은 비지니스 로직)와 Query(주로 화면을 그리기 위한 API)를 분리
    - 과거는 요청이 끝날 때 영속성 컨텍스트가 종료되어 엔티티를 언제든 변경할 수 있었으나 스프링 OSIV에서는 영속상태는 유지하되 트랜잭션 범위에서만 수정이 가능하도록 보완했다
    - LazyInitializationException: OSIV가 false일 때 Transaction이 종료되면 connection도 닫히기 때문에 이후에 LazyLoading을 하면 발생하는 에러
11. QueryDSL
    - JPA에서 복잡하거나 동적인 쿼리 구현의 한계를 해결하기 위해 사용한다
    - 코드로 SQL문을 작성하여 컴파일 시에 오류를 찾을 수 있고 공통 부분을 추출하여 재사용할 수 있다
    - JPQL을 만들어 주는 것이라 영속성 컨텍스트에서 먼저 찾는 것이 아닌 DB 조회 후 영속성 컨텍스트에 저장 시도 후 데이터가 있으면 영속성 컨텍스트 값을 반환
12. 동시성 문제 -> 두 번의 갱신 분실 문제(second lost updates problem)
    - A와 B가 거의 동시에 한 로우에 대해서 수정 작업을 할 경우 먼저 저장한 쪽의 데이터가 분실되는 것이다
    - 낙관적 락(Optimistic Lock)
        1. 대부분의 트랜잭션의 충돌이 발생하지 않을 것으로 보고 DB의 락을 사용하지 않고 Entity의 버전을 통해 동시성을 제어한다
        2. 어플리케이션 레벨에서 지원하는 락이다
        3. @Version: Entity의 버전을 관리할 수 있는 Annotation이며 사용 시 최초 커밋만 인정하게 할 수 있다
        4. LockModeType
            - NONE(default): 수정 시점에 버전 증가
            - OPTIMISTIC: 조회해도 버전을 체크한다. 트랜잭션 동안 변경되지 않음을 보장
            - OPTIMISTIC_FORCE_INCREMENT: 논리적인 변경(연관 관계의 엔티티가 변경)되었을 경우 버전을 증가하고 싶을때
    - 비관적 락
        1. DB의 락을 사용하여 동시성을 제어

### Java 질문
1. 인터페이스란 무엇인가?
   - 다른 클래스를 작성할 때 기본이 되는 틀이며 다른 클래스 사이의 중간 매개 역할을 담당한다.
   - 하나의 클래스만 상속받을 수 있는 java에 더 유연한 다형성을 지원하게 해준다.
2. ThreadLocal 사용 이유와 주의점
   - 여러 쓰레드에서 접근 가능한 변수나 데이터는 동시성 문제를 발생시키기에 해당 쓰레드에 저장소를 제공하는 ThreadLocal을 사용
   - 주의점은 ThreadLocal의 값을 제거하지 않을 경우 메모리 누수 및 쓰레드 재사용 시 의도치 않은 값이 나올 수 있으므로 사용 후 값 제거는 필수로 해야한다

### 기타 정리사항
1. 서버에서 클라이언트로 메세지 전송 방법
   1. polling
      - 주기적으로 서버에 요청을 날림
   2. long-polling
      - 요청을 보낸 후 서버에세 이벤트가 있을 때까지 연결을 잡고 있는 형태
   3. WebSocket
      - http기반의 소켓 통신으로 양방향 가능하나 웹소켓 서버가 필요
   4. Server-sent Events
      - html5 표준이며 서버에서 클라이언트로 단방향 전송




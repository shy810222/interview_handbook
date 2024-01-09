Interview Study
===============
인터뷰에서 필요할 것으로 예상되는 질문 정리하면서 복기

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
    5.Filter, Interceptor, AOP 순서 및 차이점
       - 순서는 Filter(pre) -> Interceptor(pre) -> AOP -> Interceptor(post) -> Filter(post)
       - Filter는 스프링이 아닌 WAS에서 지원하는 영역으로 스프링 빈을 사용할 수 없다.
       - Interceptor는 스프링 영역이나 요청이 Controller 전, 후, 그리고 view가 그려진 뒤에만 적용이 된다
       - AOP 스프링 빈의 메서드 레벨에 적용이 되며 서비스 로직, controller 등 다양한 위치에서 적용할 수 있다

### JPA 질문
1. 왜 사용하는가?
2. EntityManager와 영속성
3. open-in-view
아래의 내용은 추후 정리
4. 장점
    - 생산성 향상
    - 반복되는 쿼리 안만들어도 된다.
    - 수정하고자 하는 필드만 수정하는게 쉽다.
    - 유지보수 편의
    - 엔티티의 정보만으로도 DB를 볼 필요가 없음
    - 필드 변경이 발생할 경우 엔티티만 수정
    - 컴파일 과정에서 오류 발견
    - 오타 등
    - DB 벤더 독립성
    - 변경 감지 활용
5. 단점
    - 다수 테이블 조인 불편
    - 복잡한 연관관계 매핑
    - 잘못 사용할 경우 이슈
6. EntityManager 와 영속성
    - 영속상태란?
7. 인터셉터(리스너) 사용 경험
8. @Transaction 이 있을 때와 없을 때의 동작
9. LazyInitializationException (OSIV)
    - 서비스 메서드 종료(Transaction 종료) 시에 하이버네이트 session 도 함께 닫히기에 컨트롤러 등에서 entity 접근 시 발생하는 에러
10. Open Session In View 패턴
    - 전통방식
    - 서블릿 필터 시작시에 세션 열고 트랜잭션 시작
    - 뷰 렌더링 완료 후 트랜잭션 종료
    - 스프링
    - 필터 내에서 세션만 오픈
    - Lazy 로딩은 가능하지만 entity 변경은 적용되지 않음


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

브러우저리스트 공부
jpa더 공부




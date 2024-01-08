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
### JPA 질문

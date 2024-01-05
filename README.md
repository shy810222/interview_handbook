Interview Study
===============
인터뷰에서 필요할 것으로 예상되는 질문 정리하면서 복기

##공통 질문
1. 프로세스와 스레드의 차이
2. wrapper 타입 설명

## Front End 질문
1. 브라우저 렌더링 순서
   - HTML 파싱
   - 파싱 중 javascript구문을 만나면 파싱 중단 후 javascript 파싱 및 실행(단, defer표시로 지연처리를 하면 중단하지 않고 파싱 완료 후 실행)
   - DOM Tree 구축
   - CSS 파싱
   - CSSOM Tree 구축
   - Render Tree 구축(여기서는 화면에 표시하지 않을 DOM요소는 제외)
   - Layout(Reflow)
   - Paint
2. 호이스팅
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
4. 실행 컨텍스트
5. 렉시컬 스코프 및 스코프 체인
6. 이벤트 루프, 호출 스택(콜스택), 태스크큐, 마이크로태스크큐
   - 실행 우선순위: 마이크로태스크큐, 태스크큐
7. Reflow, Repaint, Composite



## Back End 질문
### Spring 질문
### JPA 질문

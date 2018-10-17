# 인사이트 자바스크립트(송형주, 고현준) 저서에서

- function statement 와 function expression (p.77)
    1. function statement
    ```
      // 일반적으로 세미콜론을 붙이지 않음

      function add(x, y) {
        return x + y;     
      }
    ```

    2. function expression
    ```
      // 세미콜론을 붙여줌
      
      var add = function (x, y) {
        return x + y;    
      };
    ```
    
    * 자바스크립트에서 함수는 일급 객체로서, 함수 또한 객체
    * 함수가 선언된 메모리 공간을 변수로 참조하는 것
    * function expression 은 함수의 이름을 지정해서 사용할 수도 있음.
      ```
        var factorialVar = function factorial(n) {
          if (n <= 1) {
            return 1;    
          }

          return n * factorial(n - 1);
        };
      ```
      * 위와 같이 함수의 이름을 지정할 수 있을 뿐 아니라 내부에서 함수명을 이용해 호출이 가능.
      * 단, 함수 외부에서 호출은 불가능.

- Function Hoisting 을 고려하여 function expression 을 사용할 것을 권고 (p.78)
    1. 더글라스 크락포드의 '자바스크립트 핵심가이드' 에서 함수 호이스팅을 지적하여 function expression 을 사용할 것을 권고함.
    2. 함수 호이스팅이란?
        ```
        add(2, 3);                  // 5
        
        function add(x, y) {
            return x + y;    
        }

        add(3, 4);                  // 7
        ```

        * function statement 방식으로 함수를 생성하면 함수가 호출되는 위치보다 아래에 있어도 호출됨.
        * 즉, function statement 형태로 정의한 함수의 유효 범위는 코드의 맨 처음부터 시작함.
        * 이것은 코드의 구조를 엉성하게 만들수 있다고 하여 function expression 사용을 권장함.

        ```
        add(2, 3);                      // uncaught type error

        var add = function (x, y) {
            return x + y;    
        }

        add(3, 4);                      // 7
        ```
- 함수도 객체다 (p.80)

    1. 함수도 객체이기때문에, 프로퍼티를 가질 수 있다.
        ```
        function add(x, y) {
            return x + y;    
        }

        add.result = add(3, 2);
        add.status = 'OK';

        console.log(add.result);    // 5
        console.log(add.status);    // 'OK'
        ```



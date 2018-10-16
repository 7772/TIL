# Today I Learned

## 인사이트 자바스크립트(송형주, 고현준) 저서에서

- function statement 와 function expression
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

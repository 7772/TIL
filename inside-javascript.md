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
- arguments 객체 (p.100)

    1. 실행된 함수의 내부에는 arguments 라는 유사배열객체가 있음.
    2. 다음과 같이 유용하게 사용이 가능.
        ```
        function sum() {
            var result = 0;
        
            for (var i = 0; i < arguments.length; i++) {
                result += arguments[i];    
            }   

            return result;
        }   

        console.log(sum(1, 2, 3));
        console.log(sum(1, 2, 3, 4, 5, 6));
        ```
    
        * 위와 같이 인자의 개수와는 상관없이 어떤 함수를 구현하고자 할때 유용하게 쓰임. 

- Inheritance (p.174)

    1. 프로토타입을 이용한 상속
        * 자바스크립트는 클래스 기반 상속을 지원하지 않는다.
        * 프로토타입을 이용하여 상속을 구현할 수 있다.
        ```
        function create_object(o) {
            function F() {}
            F.prototype = 0;
            return new F();    
        }
        ```
        * 위 코드는 인자로 들어오는 객체 o 를 상속받은 새로운 객체를 리턴하는 예제이다. (더글라스 크락포드)

        ```
        var person = {
            name: "landon",
            getName: function() {
                return this.name;    
            },
            setName: function(arg) {
                this.name = arg;    
            }    
        };

        function create_object(o) {
            function F() {}
            F.prototype = o;
            return new F();    
        }

        var student = create_object(person);
        console.log(student.getName());         // Landon
        student.setName("Eumji");
        console.log(student.getName());         // Eumji

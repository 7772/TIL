# Javascript

- Higher Order Function

    * 이 부분은 [Sukhjinder Arora 의 Medium Post](https://blog.bitsrc.io/understanding-higher-order-functions-in-javascript-75461803bad?_branch_match_id=576657172280289102) 을 참고했습니다.

    1. 먼저 이해해야할 것 
        - 자바스크립트에서 함수는 일급 객체로 취급된다.
            > 함수는 객체이고,  값으로써 함수의 인자가 될 수 있고 변수에 할당될 수도 있으며, 리턴값으로 반환 될 수도 있다.
            ```
            const square = function(x) {
                return x * x;    
            }

            square(5);  // prints 25

            const foo = square;

            foo(5);     // prints 25
            ```
            

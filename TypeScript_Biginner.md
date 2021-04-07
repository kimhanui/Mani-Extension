> 강의 링크 : https://www.youtube.com/watch?v=BwuLxPH8IDs

1. what is typescript?
- js의 superset
- lang이면서 tool -> ts쓰면 js로 컴파일된다.

2. Using typescript
- js는 무조건 html에서 가져온 값 string으로 읽음
  ㄴ 그래서 자료형 확인하는 로직이 붙음 -> TS는 안 쓰고 로직 가능

- tsc 명령어: ts-> js로 컴파일 하라는 뜻
- 'as HTMLInputElement'
    ```
    /* using-tes.ts */
    const button = document.querySelector("button");
    
    // ! as HTMLInputElement (input1.value 인식을 해결.)
    // input1,2는 반드시 null이 아닌 값을 갖는다.(Vanilla.js에선 안되는거)

    // (1)input1,2가 꼭 input이라고 보장할 수 없음
    // (2)HTML의 대부분 요소가 value 속성을 갖지 않음. (오류 뜬다.)
    // 이는 TS가 개발자로 하여금 타입을 더 명확히 작성하도록 함
    const input1 = document.getElementById("num1")! as HTMLInputElement;
    const input2 = document.getElementById("num2")! as HTMLInputElement;

    function add(num1, num2){
        return num1 + num2;
    }

    button.addEventListener("click", function() {
        console.log(add(input1.value, input2.value));
    }
    ```
- 'any' 타입: 파라미터에 마우스 호버시 자료형 볼 수 있음
    ㄴ 자료형 모른다는 뜻
    ㄴ 그대로 두기보단 `num1: number` 식으로 타입을 더 명확히 적어주는게 좋다.

- 'tsc using-ts.ts' : 컴파일 후 에러 발견
    ㄴ 컴파일하면 ts를 컴파일했으니 자동으로 `using-ts.js`가 생긴다. 확장자 `js`
    ```
    /* using-tes.ts */
    const button = document.querySelector("button");
    const input1 = document.getElementById("num1")! as HTMLInputElement;
    const input2 = document.getElementById("num2")! as HTMLInputElement;

    function add(num1: number, num2: number){
        return num1 + num2;
    }

    button.addEventListener("click", function() {
        console.log(add(input1.value, input2.value));
                        // ㄴ여기 에러
    }
    ```
    몇번 째 줄에 왜 났는지 자세히 알려준다..
    
    막 줄에 `+input1.value`, `+input2.value` 로 `+` 붙여줌 된다.
    숫자니까 `+` 붙인다는 뜻

- html파일에서 ts파일 부르기: `<script>`에 `using-ts.js`로 `js`타입으로 쓰기
    ㄴ 브라우저는 TS를 run할 수 없으므로

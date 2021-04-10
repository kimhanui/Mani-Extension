> 강의 링크 : https://www.youtube.com/watch?v=BwuLxPH8IDs

## What is typescript?
- js의 superset
- lang이면서 tool -> ts쓰면 js로 컴파일된다.

## TS 특징
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

## 컴파일하기
- `tsc app.ts -w`: 파일(`app.ts`)이 변경되는 걸 자동 감지 & 컴파일
- `tsc --init`: 현재 프로젝트 경로에서 한번만 실행한다. 
   - 프로젝트 관리해줌
   - `tsconfig.json` 생성. (어떻게 컴파일 할 건지 옵션 선택하는 파일)
       ```json
        "exclude": [
            "node_modules", // 와일드카드도 사용가능하다.
            ".vscode-test"
        ],
        "include": [
            // 여기에 컴파일 할 TS파일 작성해주면 그것'만' 컴파일한다.
            // 아예 비워두면 전체 TS파일 다 컴파일한다.
            // include - exclude 의 파일들을 컴파일한다고 생각하면 된다.
        ]
        ```
- `tsc`: 현재 경로에서 모든 ts 파일 컴파일함

## 자료형
  - number ( 1, 5.3, -10 )  
    - 모든 숫자. interger(정수)와 float(실수) 사이에 차이를 두지않는다.
  - string( 'Hi', "Hi", `Hi` )
    -  모든 text값.
    -  back quote 도 사용가능하다 (마지막 예시 값이 마크다운문법처리돼서 구별이 안됨..)
  - boolean ( `true, false` )  
    - 단지 딱 이 두 값. true, false
    - truthy or falsy 값은 없음!
      > JavaScript에서, 참 같은 값(Truthy)인 값이란 불리언을 기대하는 문맥에서 true로 평가되는 값입니다. 따로 거짓 같은 값으로 정의된 값이 아니면 모두 참 같은 값으로 평가됩니다. (예: false, 0, -0, 0n, "", null, undefined와 NaN 등)
      
      > 다음은 참 같은 값에 대한 예시입니다. JavaScript는 불리언 문맥에서 참 같은 값을 true로 변환하기 때문에 아래의 모든 if 블록을 실행합니다.
      ```
        if (true)
        if ({})
        if ([])
        if (42)
        if ("0")
        if ("false")
        if (new Date())
        if (-42)
        if (12n)
        if (3.14)
        if (-3.14)
        if (Infinity)
        if (-Infinity)
      ```

  - object ( `{age:30}`)
    - 모든 JS 객체이면서 좀 더 구체적인 type.
  - Array ( `[1, 2, 3]`)
    - 모든 JS 배열이면서 type은 유연할수도 엄격할 수도 있다.(element에 따라)
  - Tuple ( `[1,2]` )
    - TS에 의해 추가됨.
    - 고정된 길이의 배열.(배열과 차이점)
  - Enum ( `enum{ NEW, OLD }` )
    - TS에 의해 추가됨.
    - global한 상수 값
  - Any ( `*` )
    - 정해지지 않은 값
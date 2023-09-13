Typescript is Javascript with syntax for types.

-   자바스크립트를 기반으로 만들어진 언어.
    typescript is a strongly typed programming language.
    개발자의 실수로 부터 보호해주고 VScode와 함께 사용하면 더 나은 개발자 경험을 제공, 더욱 생산적인 개발자가 될 수 있음.

-   VScode + Typescript 조합은 매우 추천..! 둘다 마이크로소프트에서 만듦.

Why Typescript?
-> 타입 안정성. 코드에 버그가 엄청 줄고 런타임 에러가 줄고 생산성이 늘어난다.

타입스크립트는 자바스크립트로 변환해줘야 함. 브라우저가 타입스크립트를 이해하지 못하기 떄문.

---

Implicit(암묵적)과 Explicit(명시적) 표현 - 명시적 정의(변수 선언 시 타입 정의)

    - 명시적 선언
        let a: boolean = "x"  → 🚫 boolean 타입에 string타입 할당 불가

    - 변수만 생성(타입 추론)
        let b = "hello"  → b가 string 타입이라고 추론
        b = 1
        → 🚫 string 타입에 number타입 할당 불가 알림

-   암묵적 정의를 더 선호함. type checker가 타입을 추론해주기 때문.
-   단, 빈 배열을 변수로 선언할 경우에는 배열에 담길 타입을 명시적표현으로 써주는게 좋음.

---

Optional type - 선택적으로 값을 받아올 때 사용.

    const student : {
        name : string,
        age? : number // optional type
    } = {
        name : "sam"
    }

Alias type

-   코드 재사용을 높이기 위해 사용. 별명 타입을 만들어주는 것.
    type Student = { name: string, age?: number }
    -   Student라는 타입을 만들어서 재사용함.
        const Sam : Student = {
        name : "sam"
        }
        const Lucy : Student = {
        name : "lucy",
        age : 11
        }

함수의 리턴값 타입 지정하는 방법

    function classMate (name: string) {
        return ( // parameter에 타입 지정
            name
        )
    }
    function classMate = (name: string) : Student => (
        {name} // 화살표 함수 사용시 방법.
    )

    const sam = classMate("sam")

ReadOnly 속성

-   자바스크립트에는 없는 기능, 말 그대로 읽기전용이여서 선언 후 값 변경이 안됨.
    const numbers: readOnly number[] = [1, 2, 3, 4]
    numbers.push(1) -> 에러발생. 변경 불가..!! 값을 추가할 수 없음.
    \*map() 또는 filter() 는 할 수 있음. 값을 추가하거나 변경하는게 아니라 기존 값들에서 작업을 하기에 사용가능.

Tuple

-   array를 생성할 수 있되, 최소한의 길이를 가져야 하고, 특정 위치에 특정타입이 있어야 함.
    const student: [string, number, boolean] = ["sam", 11, true] >> 정해진 갯수의 요소를 가져야 하는 array를 지정할 수 있음. \*자바스크립트에는 없는 기능.
    student[0] = 12 → 🚫 string이 와야 함.

undefined, null, any

-   undefined, null은 자바스크립트에도 있는 타입
-   any : 타입스크립트로부터 빠져나오고 싶을 때 쓰는 타입.말 그대로 anything 아무거나 다 가능해져버림..
    \*\*타입스크립트를 쓰는 의미가 없어지니 사용자제..
    const a : any[] = [1, 2]
    const b : any = true
    a + b // 허용되어짐..! 오 쒯.

unknown, void, never

-   unknown : api로 부터 받아지는 값이 어떤 타입일지 모를 때 사용.
    unknown 타입을 쓴 후에 그 변수로 어떤 작업을 하려면, 그 변수의 타입을 먼저 확인한 후에 작업이 가능해짐.(typescript 보호를 받음)
    let a : unknown;
    let b = a + 1 // a 값을 모르기에 사용불가!

    if(typeof a === 'number'){
    let b = a + 1; // a의 타입을 확인 후에 작업은 가능!
    }
    if(typeof a === 'string'){
    let b = a.toUpperCase();
    }

-   void : 아무것도 return 하지 않는 함수에서 사용. 타입스크립트가 자동으로 인식함. 따로 타입선언 하지 않아도 됨.
-   never : 함수가 절대 return하지 않을 때 사용. 리턴값 없이 에러를 던질 때 사용.
    function hello(): never {
    throw new Error("xxx")
    } \* 타입이 두가지 일 수도 있는 상황에서 사용.
    function hello(name: string | number){
    name + 1 // 불가능, string일 수도 있으니까

                        if(typeof name === "string"){
                            name
                        } else if (typeof name === "number"){
                            name
                        } else {
                            name // type:never
                                 // 타입이 제대로 들어온다면, 이 부분코드는 작동하지 않음.
                        }
                    }

---

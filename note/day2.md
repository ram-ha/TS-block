Call Signatures

-   함수 위에 마우스를 올렸을 때 보여지는 힌트박스 내용처럼
    함수를 구현하기 전, 내가 타입을 만들고 함수가 어떻게 작동하는지 서술할 수 있음.
    함수 타입, 반환 타입, 인자의 타입 등등..

    type Add = (a:number, b:number) => number;
    const add:Add = (a, b) => a + b

Overloading(오버로딩)

-   함수가 여러개의 call signatures를 가지고 있을 때 발생
-   파라미터 타입이 다른 경우

    type Config = {
    path: string,
    state: object
    }
    type Push = {
    (path:string): void
    (config:Config): void
    }
    // Push 타입은 string과 object를 받을 수 있고 string일 때와 object일 때를 각각 처리할 수 있음
    // 패키지 혹은 라이브러리를 처음에 디자인할 때 이런식으로 많이 사용됨
    const push:Push = (config) => {
    if(typeof config === "string") {
    console.log("do something")
    } else {
    console.log(config.path)
    }
    }

Polymorphism(다형성)

-   여러가지 다른 구조들
-   concrete type : 기존부터 봤던 타입. number, string, boolean ...

    What is Generics(제네릭)?

    -   call signature를 작성할 때, 들어올 확실한 타입을 모를 때 사용
        타입스크립트에게 타입을 유추하도록 하는 것.
        기본적으로 placeholder를 사용해서 작성한 코드의 타입기준으로 바꿔줌.
    -   제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여
        하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법

    cf) any와 다를게 없지 않나? -> any로 선언된 타입은 끝까지 any타입을 유지하게 된다. - type A = (arr: any[]) => any
    const print : A = (arr) => arr[0]
    print([1,2,3]) // number 배열
    print.toUpperCase() ?????error!!

    -   number에는 toUpperCase라는 함수를 쓸 수 없음. 근데 any 타입은 any타입을 계속 유지하기 때문에 타입과 무관한 메서드도 사용할 수 있게 됨.
        매우 안좋은 방법..ㅎ 타입을 보장하려고 쓰는게 타입스크립트라는걸 잊지말자.

    \*\*추가설명 : number에 toUpperCase함수를 사용한다 했을 때..

    -   자바스크립트에서는 컴파일 과정에서는 문제없이 진행되고 런타임 과정에서 에러가 뜨는 상황이 발생한다. 말도 안되는걸...?
    -   타입스크립트에서 제네릭을 사용하면 자동으로 타입이 할당되고 타입스크립트가 number타입이네? 근데 string전용 함수를 왜 써? 안되지!! 하고 컴파일 이전에 에러로 알려준다.

---

항상 타입스크립트가 타입을 유추하도록 하는 것이 좋음.
type SuperPrint = <T>(a: T[]) => T
const superPrint: SuperPrint = (a) => a[0]

함수형태로 쓴다면?
function superPrint<T>(a: T[]){
return a[0]
}

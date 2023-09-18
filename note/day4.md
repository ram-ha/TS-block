타입의 모양 종류

type Player = { } // 오브젝트의 모양을 설명하는 것
type Player = string // type alias를 만드는 것
type Player = "1" | "2" // 타입을 특정된 값으로 만드는 것

---

타입과 인터페이스의 공통점

-   타입스크립트에게 오브젝트의 모양과 타입을 알려주는 것
-   둘다 추상클래스를 대신 할 수 있음.

    type PlayerA = {
    name: string
    }
    const playerA: PlayerA = {
    name: " ram"
    }
    /////
    interface PlayerB {
    name: string
    }
    const playerB: PlayerB = {
    name: "ram"
    }

타입스크립트 커뮤니티에서는 클래스나 오브젝트의 모양을 정의하고 싶으면 인터페이스를 쓰고
나머지 다른 모든 경우에서는 타입을 쓰라고 함.

-   이유 : 인터페이스를 상속시키는 방법이 직관적이기 때문

---

타입과 인터페이스의 차이점

-   타입은 새 property를 추가하기 위해 다시 선언 할 수 없지만, 인터페이스는 항상 상속이 가능함.
    인터페이스는 같은 변수명을 또 선언할 수 있지만, 타입은 불가능!

    interface Animal { name: string }
    interface Bear extends Animal { honey: boolean }
    type Animal = { name: string }
    type Bear = Animal & { honey: boolean }
    // 타입은 새 타입을 만들어서 &연산자를 사용해서 합집합(union) 가능

---

다형성, 제네릭, 클래스, 인터페이스 모두 합쳐보기

-   다형성은 다른 모양의 코드를 가질 수 있게 해주는 것
    다형성을 이룰 수 있는 방법은 제네릭을 사용하는 것
    제네릭은 concrete 타입이 아니라 placeholder타입이다.
    타입스크립트가 placeholder->concrete으로 바꿔줌

interface SStorage<T> {
[key:string]: T // key가 제한되지 않은 오브젝트를 정의함.

}

class LocalStorage<T> { // 제네릭을 클래스로 보내고 클래스는 제네릭을 인터페이스로 보낸 뒤, 인터페이스는 제네릭을 사용함.
private storage: SStorage<T> = {}
set(key:string, value:T){
this.storage[key] = value;
}
remove(key:string){
delete this.storage[key]
}
get(key:string): T { // 제네릭을 바탕으로 call signature 만들어줌. concrete type으로 바꿔줌
return this.storage[key]
}
clear(){
this.storage = {}
}
}

const stringsStorage = new LocalStorage<string>()
stringsStorage.get("kee")
stringsStorage.set("hello", "how are u")

const booleansStorage = new LocalStorage<boolean>()
booleansStorage.get("xxx")
booleansStorage.set("hello", true) // value 부분은 제네릭이 boolean으로 바뀜.

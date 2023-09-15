Abstract class

-   오직 다른 클래스가 상속받을 수만 있는 클래스, 다른 곳에서 직접적으로 추상클래스의 인스턴스를 만들진 못함.
-   클래스에게 어떻게 구현할지에 대해서는 말하지 않지만, 무엇을 구현해야 할 지는 알려줌.

    추상 메소드

    -   구현이 되어 있지 않은 (코드가 없는) 메소드
    -   추상 클래스를 상속받는 모든 것들이 구현을 해야하는 메소드
    -   메소드를 클래스 안에서 구현하지 않으면 만들 수 있음. (메소드는 클래스 안에 존재하는 함수)
        메소드의 call signature만 적어두면 만들 수 있음.

---

지금 까지 본 적 없는 Type 활용 : 메우 다재다능

type Team = "red" | "yellow" | "blue" // string 전체가 아닌 특정값들을 가짐. (타입 alias)
type Health = 1 | 5 | 10

type Player = {
nickname: string,
team: Team,
health: Health
}
-> concrete 타입의 특정 값을 쓸 수도 있음. 정해놓은 특정 값들만 사용해야 함.

const ram : Player = {
nickname: "ram",
team: "blue",
health: 5
}

type은 내가 원하는 모든 것이 될 수 있음.

---

Interfaces

-   오브젝트의 모양을 특정해주는 한가지 용도만을 가짐.
    type보다는 활용도가 제한적임.
-   타입스크립트에게 오브젝트의 모양을 알려줄 때 인터페이스를 사용하는 것을 추천.
    인터페이스 모양이 더 객체지향 프로그래밍처럼 보여서 이해하기 더 쉬움.

type Player = {
nickname: string,
team: Team,
health: Health
}
interface Player {
nickname: string,
team: Team,
health: Health
}

-   property들을 축적시킬 수 있음. (합체능력..!)
    같은 인터페이스의 다른 이름을 가진 property들을 합칠 수 있음.
    (type은 할 수 없는 기능)

interface User = {
name: string
}
interface User = {
age: number
}
interface User = {
weight: number
}

const ram : User = {
name: "ram",
age: 12,
weight: 30
}

---

// interface 방식
interface User {
name: string
}
interface Player extends User {

}
const ram : Player = {
name: "ram"
}

// type 방식
type User = {
name: string
}
type Player = User & {

}
const ram : Player = {
name: "ram"
}

---

추상클래스 + 인터페이스

abstract class User {
constructor(
protected firstName: string, // protected는 추상클래스로부터 상속받은 클래스들이 property에 접근가능함.
protected lastName: string
) {}
abstract sayHi(name: string): string
abstract fullName(): string
}
class Player extends User {
fullName(){
return `${this.firstName} ${lastName}`
}
sayHi(name:string){
return `Hello ${name}. My name is ${this.fullName()}`
}
}

표준화된 property와 메소드를 갖도록 해주는 설계도를 만들기 위해 추상클래스를 사용함.

추상화를 원할 때 클래스와 인터페이스를 사용할 때의 차이점

-   추상 클래스는 자바스크립트에서 클래스로 바뀜
-   인터페이스는 타입스크립트에만 존재함. 자바스크립트로 변환(컴파일)시 코드에 보여지지 않음.
    -> 파일사이즈를 줄이고 싶다면, 인터페이스를 사용하자!

interface User {
firstName: string,
lastName: string,
sayHi(name:string): string
fullName(): string
}
class Player implements User {
constructor(
private firstName: string, // 인터페이스를 상속할 때는 private, protected로 만들지 못함
public lastName: string // public만 가능
) {}
fullName(){
return `${this.firstName} ${lastName}`
}
sayHi(name:string){
return `Hello ${name}. My name is ${this.fullName()}`
}
}

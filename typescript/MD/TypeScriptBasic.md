# TypeScript

## 타입스크립트 란?
타입스크립트는 자바스크립트에 타입을 부여한 언어입니다. 자바스크립트의 확장된 언어라고 볼 수 있습니다. 타입스크립트는 자바스크립트와 달리 브라우저에서 실행하려면 파일을 한번 변환해주어야 합니다. 이 변환 과정을 **컴파일** 이라고 부릅니다.


## 타입스크립트 특징
- **컴파일 언어, 정적 타입 언어** <br>
자바스크립트는 동적 타입의 인터프리터 언어로 런타임에서 오류를 발견할 수 있습니다. 이에 반해 타입스크립트는 정적 타입의 컴파일 언어이며 타입스크립트 컴파일러 또는 바벨(Babel)을 통해 자바스크립트 코드로 변환됩니다. 코드 작성 단계에서 타입을 체크해 오류를 확인할 수 있고 미리 타입을 결정하기 때문에 실행 속도가 매우 빠르다는 장점이 있습니다. 하지만 코드 작성 시 매번 타입을 결정해야 하기 때문에 번거롭고 코드량이 증가하며 컴파일 시간이 오래 걸린다는 단점이 있습니다.

- **자바스크립트 슈퍼셋** <br>
타입스크립트는 자바스크립트의 슈퍼셋, 즉 자바스크립트 기본 문법에 타입스크립트의 문법을 추가한 언어입니다. 따라서 유효한 자바스크립트로 작성한 코드는 확장자를 .js에서 .ts로 변경하고 타입스크립트로 컴파일해 변환할 수 있습니다. 

- **객체 지향 프로그래밍 지원** <br>
타입스크립트는 ES6(ECMAScript 6)에서 새롭게 사용된 문법을 포함하고 있으며 클래스, 인터페이스, 상속, 모듈 등과 같은 객체 지향 프로그래밍 패턴을 제공합니다.

🤔바벨이란? <br>
바벨은 입력과 출력이 모두 자바스크립트 코드인 컴파일러입니다. 바벨은 최신 버전의 자바스크립트가 실행되지 않는 구 버전의 브라우저에서도 정상적으로 실행되도록 변환해줍니다

<Br>

## 타입스크립트 사용을 고려해야 하는 이유
- 높은 수준의 코드 탐색과 디버깅 <br>
타입스크립트는 코드에 목적을 명시하고 목적에 맞지 않는 타입의 변수나 함수들에서 에러를 발생시켜 버그를 사전에 제거합니다. 또한 코드 자동완성이나 실행 전 피드백을 제공하여 작업과 동시에 디버깅이 가능해 생산성을 높일 수 있습니다.

- 자바스크립트 호환 <br>
타입스크립트는 자바스크립트와 100% 호환됩니다. 따라서 프론트엔드 또는 백엔드 어디든 자바스크립트를 사용할 수 있는 곳이라면 타입스크립트도 쓸 수 있습니다. 타입스크립트는 앱과 웹을 구현하는 자바스크립트와 동일한 용도로 사용 가능하며 서버 단에서 개발이 이루어지는 복잡한 대형 프로젝트에서도 빛을 발합니다.

- 강력한 생태계 <br>
타입스크립트는 그리 오래되지 않은 언어임에도 불구하고 강력한 생태계를 가지고 있습니다. 대부분의 라이브러리들이 타입스크립트를 지원하며 스튜디오 코드를 비롯해 각종 에디터가 타입스크립트 관련 기능과 플러그인을 지원합니다.

<br>

## 프론트엔드 프레임워크와 타입스크립트
- 리액트(React) <br>
리액트와 타입스크립트의 호환성은 비교적 좋은 편입니다. 최근 들어 많은 개발자들이 리액트와 타입스크립트 조합을 선택하고 있습니다. 리액트 공식 홈페이지에서는 타입스크립트를 사용하기 위한 가이드를 제시하고 있습니다.

- 뷰(Vue.js) <br>
뷰 2.0에서는 타입스크립트를 사용할 수 있지만 몇몇 라이브러리의 도움을 받아야 하거나 구현 자체가 안 되는 문제도 다수 있었습니다. 최근 릴리즈된 뷰 3.0부터는 타입스크립트를 공식 지원합니다. 뷰 3.0 CLI는 타입스크립트 도구화 지원을 기본으로 제공합니다.

<br>

## 기본 타입 및 선언 방법
콜론(:)을 이용하여 자바스크립트 코드에 타입을 정의하는 방식을 타입 표기라고 합니다.

### String
문자열 타입 선언 방식
```js
let str: string = 'Hello World!';
```
<br>

### Numeber
숫자 타입 선언 방식
```js
let num: number = 10;
```
<br>

### Boolean
논리형 타입 선언 방식
```js
let isLoggedIn: boolean = false;
```
<br>

### Array
배열 선언 방식
```js
let arr: number[] = [1,2,3];
```
제네릭을 사용할 수 있다.
```js
let arr: Atrray<number> = [1,2,3];
```
<br>

### Object
TypeScript에서 JavaScript의 오브젝트처럼 사용하고 싶은 경우에는 {} 사용 <br>
interface이기 때문에 선언한 값은 전부 사용해야 함
```js
interface Myobj {
    foo: string;
    bar: number;
}

const a: Myobj = {
    foo: 'foo',
    bar: 3,
}
```

### Tuple
튜플은 배열의 길이가 고정되고 각 요소의 타입이 지정되어 있는 배열 형식
```js
let arr: [string, number] = ['hi', 10]
```
정의되지 않은 타입, 인덱스로 접근할 경우 오류
```js
arr[1].concat('!'); // Error, 'number' does not have 'concat'
arr[5] = 'hello'; // Error, Property '5' does not exist on type '[string, number]'
```


### Enum
이넘은 C, Java와 같은 다른 언어에서 흔하게 쓰이는 타입으로 특정 값(상수)들의 집합
```js
enum Avengers { Capt, IronMan, Thor }
let hero: Avengers = Avengers.Capt
```

인덱스 번호로 접근 가능
```js
enum Avengers { Capt, IronMan, Thor }
let hero: Avengers = Avengers[0]; // Capt
```

이넘의 인덱스를 사용자 편의로 변경 가능
```js
enum Avengers { Capt = 2, IronMan, Thor }
let hero: Avengers = Avengers[2]; // Capt
let hero: Avengers = Avengers[4]; // Thor
```

### any
모든 타입에 대해서 허용한다는 의미
```js
let str: any = 'hi';
let num: any = 10;
let arr: any = ['a', 2, true];
```

### void
반환 값이 없는 함수의 반환 타입 return이 없거나 return이 있더라도 반환하는 값이 없으면 함수의 반환 타입을 void로 지정
```js
function printSomething(): void {
    console.log('sth');
}

function returnNothing(): void {
    return;
}
```

### Never
함수의 끝에 절대 도달하지 않는다는 의미를 지닌 타입
```js
function neverEnd(): never {
    while(true) {

    }
}
```

### unknown
어떤 타입인지 모르는 변수는 타입스크립트에서 unknown 이라는 타입을 사용할 수 있다
```js
let a:unknown;

// let b = a + 1 // 에러 타입이 언노운이기 떄문에
if(typeof a === 'number') {
    let b = a + 1
}
if(typeof a === "string"){
    let b = a.toUpperCase();
}
```

## 변수명 + ?
변수명 뒤에 물음표를 붙이면 타입이 undefined 도 같이 붙는다 <br>
**age?:number** 를 붙이게 되면 타입은 number | undefined 가 된다
```js
const player : {
    name: string,
    age?:number
} = {
    name: "deepjun"
}
```

# 함수

### Call Signatures
미리 타입을 만들고 함수가 어떻게 작동하는지 서술해둘 수 있다
```js
type Add = (a:number, b:number) => number;

const add:Add = (a,b) => a+b
```

### Overloading
오버로딩은 서로다른 함수가 여러개의 call signatures를 가지고 있을 때 발생시킨다 <br>
```js
type Add = {
    (a:number, b:number) : number
    (a:number, b:string) : number
}

const add:Add = (a,b) => {
    if(typeof b === "string") return a;
    return a + b
}
```
```js
type Add = {
    (a:number, b:number) : number
    (a:number, b:number, c:number) : number
}

const add:Add = (a,b,c?:number) => {
    if(c) return a + b + c
    return a + b
}

add(1, 2)
add(1, 2, 3)
```
```js
type Config = {
    path: string,
    state: object
}
type Push = {
    (path:string):void
    (config: Config):void
}

const push:Push = (config) => {
    if(typeof config === "string") console.log(config)
    else{
        console.log(config.path, config.state)
    } 
}
```

### 다형성
<br>
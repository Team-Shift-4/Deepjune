### computer programming language paradigm
---
> ♣︎ 저급언어(Low-level language), 고급언어(High-level language)
- 저급언어(Low-level language))
  - 기계 중심적 언어
  - 프로그래밍하기 어렵다
  - 에러 발생기 수정이 힘들다
  - 다른 기계와 호환하기 어렵다
  - 수행 시간이 빠르다
  - 종류 : 기계어, 어셈블리어
  - 바로 cpu가 사용가능하기 때문에 번역기가 필요없음
  - cpu가 이해하는 언어(저급언어)는 computer instruction
    - 이것은 operation(명령코드)코드와 operand(피연산자)코드로 구성된다
    - opreation코드는 기계어의 일부이며 수행할 명령어를 나타내는 부호를 만한다.
<br>

- 고급언어(High-level language)
  - 자연어
    - 사용자가 중심이 되는 언어
    - 이 세상에 이루어진 언어(영어나 한국어)
    - 이런 언어를 cou가 이해할 수 없기때문에 번역기(하나의 소프트웨어)가 필요
      - 컴파일러, 인터프리터
<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/Low%20High%20Language.png" width="550px" height="200px"></p>
<br>

<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/저급고급객체.png" width="550px" height="200px"></p>
- 비구조적 언어
  - 저급언어
  - 수많은 분기문과 GOTO문으로 구성
    - GOTO문은 프로그램이 실행하는 부분이 일정하지가 않고 전역을 왔다갔다한다 -> 스파게티 코드라고도 함.
<br>

- 구조적 언어
  - 고급언어 : c언어(절차지향언어)
    - 주석, 변수, 상수로 구성
    - 흐름제어문(Flow control)
      - GOTO문을 사용하지 않고 코드가 실행되는 순서를 제어하는 것.
        - 위에서 아래로 한 줄씩 실행
        - 선택과 반복을 통해 알고리즘 구성
        - 객체지향적 언어에선 프로그램의 작성단위가 클래스지만 흐름 제어문은 함수이다
        - 하나의 프로그램을 만드는데 함수를 써서 다음에 이 코드가 필요하면 재활용 가능
<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/흐름제어문.png" width="550px" height="500px"></p>
<br>

- 객체지향적 언어
- 자바, 파이썬 ,자바스크립트
- A함수가 B함수를 호출하고 B함수가 C함수를 호출할 경우 A함수만 호출하기는 어렵다. 그래서 나온게 객체지향언어.
- 구조적 언어와 다른점
    - 객체지향적 언어는 컴파일러가 돌아가기 전에 먼저 돌아가는것이 pre prosessor인데 실행할 코드와 실행하지 않을 코드(주석)를 구분
    - 객체지향적 언어는 구조적언어를 안고가는데 거기에 객체지향적 언어의 요소를 추가한 것이다.
<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/구성체계.png" width="550px" height="300px"></p>

- Declare
  - 변수를 선언(변수 공간을 확보)

- Data types
  - 변수의 자료형
    - 메모리 공간을 확보하기 위함
    - 자료형에 비해 값이 너무 작아져버리면 overflow발생

- Scope(자료형의 범위)
- Lifecycle(생명주기,태어나서 죽을때까지)
  - 클래스에서 변수가 선언될 때 태어났다가 클래스가 닫히면 죽음

- Operator
  - 변수가 태어나면 연산을 진행해야 하는데 이 때 operator가 필요함
  - type of operator
    - 연산자를 기능별로 분류
      - 산술연산
      - 논리연산
      - 비교연산
      - boolean연산
      - 대입연산
      - 복합연산자
      - 단항연산
      - 비트연산자
      - 삼항연산자
    
- Operator orecedence
  - 연산자 우선순위
    
- Data type consensus in binary operation
  - 바이너리 연산의 데이터 유형 합의
      - 문자열 + 숫자 결과  문자열로 형 변환
        

- Flow control
  - default
    - 위에서 아래로 실행
  - Selection
    - 이 언어에서 어떤 선택문이 존재하는가
  - Loop
    - 이 언어에서 어떤 반복문이 존재하는가
    

- Function
  - Declare
    - 이 언어에서 함수를 어떻게 선언하는지
  - overloading
    - 이 함수에서 오버로딩을 지원하는지
<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/언어를%20처음%20배울때%20이것만%20알면%20끝.png" width="600px" height="500px"></p>

- OOP중 핵심적인 내용
상속 : class a ~ class f가 있다고 하자 만일 class a에서 작성했었던 코드를 class b~ f까지 적용해야 한다면 코드를 일일이 다 입력해야 할 것이다. 하지만 상속을 사용하면 곧바로 class a에 있는 코드를 바로 적용 할 수 있다.
<p align="center"><img src="./img/Computer%20Programming%20Language%20Paradigm/객체지향.png" width="550px" height="500px"></p>
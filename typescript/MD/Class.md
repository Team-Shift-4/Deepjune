# 클래스
객체지향 프로그래밍
```js
//abstract Class 추상 클래스
//abstract Class : 다른 클래스가 상송받을 수 있는 class
//abstract 를 사용하면 상속받을 class에 'extends' 를 꼭 추가
abstract class User{
constructor(
private firstName:string,
private lastName:string,
public nickname:string
){}
}

class Player extends User{

}

//new User는 사용할 수 없다 -> 상속만 가능
const seung = new Player("Jeong","deep","deepjun");

//private한 것들은 대입이 되지 않는다. public 만 가능!
seung.firstName = "Jeong";


//접근 지정자

//private - 선언한 클래스 안에서만!
//protected - 선언한 클래스 안, 상속받은 클래스 안
//public - 다 가능

abstract class User{
constructor(
protected firstName:string,
protected lastName:string,
protected nickname:string
){}

abstract getNickName():void
getFullName(){
return `${this.firstName} ${this.lastName}`
}
}

class Player extends User{
getNickName(){
console.log(this.nickname)
}
}

const seung = new Player("Jeong","deep","deepjun");
seung.getFullName();
```
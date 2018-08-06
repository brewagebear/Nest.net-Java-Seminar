6.5 생성자(constructor)
=========================
생성자란?
-----------
  - 인스턴스가 생성될 때마다 호출되는 ‘인스턴스 초기화 메서드’ 
  - 몇가지 조건을 제외하고는 메서드와 같다.  
  - 인스턴스 변수의 초기화 또는 인스턴스 생성시 수행할 작업에 사용 
  - 모든 클래스에는 반드시 하나 이상의 생성자가 있어야 한다.
  * * * 
  - 인스턴스 초기화 – 인스턴스 변수에 적절한 값을 저장하는 것.
* * *

*생성자의 조건*
--------------
>1. 생성자의 이름은 클래스의 이름과 같아야 한다.
>2. 생성자는 리턴값이 없다. (하지만 void를 쓰지 않는다.)

* * *
기본 생성자란?
-------------
1. 매개변수가 없는 생성자 
2. 클래스에 생성자가 하나도 없으면 컴파일러가 기본 생성자를 추가한다. 
    (생성자가 하나라도 있으면 컴파일러는 기본 생성자를 추가하지 않는다.) 

<pre><code> 클래스이름() { } 
 Card() { } // 컴파일러에 의해 추가된 Card클래스의 기본생성자. 내용이 없다. </code></pre>
**“모든 클래스에는 반드시 하나 이상의 생성자가 있어야 한다.”**

<pre><code>class Data1 {
    int value;
    Data1() {} // 기본생성자 
    }</code></pre>

**매개변수가 있는 생성자**
-----
<pre><code>Car c = new Car();
c.color = "white";
c.gearType = "auto"
c.door = 4;  
************************************
Car c = new Car("white","auto",4);
</code></pre>
**생성자에서 다른 생성자 호출하기- This()**

* this() – 생성자, 같은 클래스의 다른 생성자를 호출할 때 사용,
다른 생성자 호출은 생성자의 첫 문장에서만 가능

<pre><code>Car (){
c.color = "white";
c.gearType = "auto"
c.door = 4; 
} 
* 코드의 재사용성을 높인 코드
Car (){ 
    //Card("white","auto",4);
    this("white","auto",4);
}
</code></pre>

**참조변수 this**
-----
*this – 인스턴스 자신을 가리키는 참조변수. 인스턴스의 주소가 저장되어있음 

모든 인스턴스 메서드에 지역변수로 숨겨진 채로 존재
<pre><code>Car (String c, String g, int d){
    color = c;
    gearType = g;
    door = d; 
} 
* 인스턴스변수와 지역변수를 구별하기 위해 참조변수 this사용 
Car (String color, String gearType, int door){
    this.color = color;
    this.gearType = gearType;
    this.door = door; 
} 
</code></pre>

**생성자를 이용한 인스턴스의 복사**
-----

 * 인스턴스간의 차이는 인스턴스변수의 값 뿐 나머지는 동일하다. 
 * 생성자에서 참조변수를 매개변수로 받아서 인스턴스변수들의 값을 복사한다. 
 * 똑같은 속성값을 갖는 독립적인 인스턴스가 하나 더 만들어진다. 

모든 인스턴스 메서드에 지역변수로 숨겨진 채로 존재
<pre><code>Car (Car c){ // 인스턴스의 복사를 위한 생성자.
    color = c.color;
    gearType = gearType;
    door = c.door; 
} 
************************************
Car (Car c){
    this(c.color, c.gearType, c.door);
} 
</code></pre>


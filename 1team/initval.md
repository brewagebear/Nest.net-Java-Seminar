6.변수의 초기화
======
변수의 초기화
----
* 변수를 선언하고 처음으로 값을 저장하는 것 
* 멤버변수(인스턴스변수,클래스변수)와 배열은 각 타입의 기본값으로 자동초기화되므로 초기화를 생략할 수 있다. 
* 지역변수는 사용전에 꼭!!! 초기화를 해주어야한다. 
* * *
멤버변수의 초기화
-----
* 멤버변수의 초기화 방법
1. 명시적 초기화
<pre>
class Car {
    int door = 4;     ->기본형 변수의 초기화.
    Engine e = new Engine();  ->참조형 변수의 초기화.
    //...
}
</pre>
2. 생성자
<pre>
Car(String color,String gearType,int door){
    this.color=color;
    this.gearType=gearType;
    this.door=door;
}
</pre>
3. 초기화 블럭
* 인스턴스 초기화 블럭: {}
* 클래스 초기화 블럭: static {}
* * *
초기화 블럭
-----
* 클래스 초기화 블럭 - 클래스변수의 복잡한 초기화에 사용되며, 클래스가 로딩될 때 실행된다
* 인스턴스 초기화 블럭 – 생성자에서 공통적으로 수행되는 작업에 사용되며 인스턴스가 생성될 때 마다 (생성자보다 먼저)실행된다. 
<pre>
class InitBlock {
    static{/* 클래스 초기화 블럭*/}
    {/*인스턴스 초기화 블럭*/}
}
</pre>
* * *
멤버변수의 초기화 시기와 순서
----
* 클래스변수 초기화 시점 : 클래스가 처음 로딩될 때 단 한번 
* 인스턴스변수 초기화 시점 : 인스턴스가 생성될 때 마다 
<pre>
class InitTest {
    static int cv = 1; //명시적 초기화
    int iv = 1; //명시적 초기화
    static {cv = 2;} //클래스 초기화 블럭
    {iv=2;} //인스턴스 초기화 블럭
    InitTest() { //생성자
        iv=3
    }
}
</pre>
>클래스 초기화
1. cv==0(기본값)
2. cv==1(명시적 초기화)
3. cv==2(클래스 초기화블럭)
> 인스턴스 초기화
4. cv==2,iv==0 (기본값)
5. cv==2,iv==1 (명시적 초기화)
6. cv==2,iv==2 (인스턴스 초기화 블럭)
7. cv==2,iv==3(생성자)

멤버변수의 초기화 시기와 순서 예제
-----

<pre>
class Product {
    static int count = 0; // 생성된 인스턴스의 수를 저장하기 위한 변수
    int serialNo; // 인스턴스 고유의 번호

    { // 인스턴스 초기화 블럭 : 모든 생성자에서 공통적으로 수행될 코드
    ++count;
    serialNo = count;
    }
    public Product() {}
}
class ProductTest {
    public static void main(String args[]) {
        product p1 = new Product();
        product p2 = new Product();
        product p3 = new Product();

        System.out.println("p1의 제품번호(serial no)는 " + p1.serialNo);
        System.out.println("p2의 제품번호(serial no)는 " + p2.serialNo);
        System.out.println("p3의 제품번호(serial no)는 " + p3.serialNo);
        System.out.println("생산된 제품의 수는 모두 "+Product.count+"개 입니다.");
    }
}
</pre>

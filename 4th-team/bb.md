# Abstract class (추상 클래스)

####추상화란?
>객체들의 공통된 속성(property)와 행위(method)를 뽑아내는 작업
결론적으로 공통적인 성질 또는 특징을 뽑아내는 작업을 의미

### 예시)
--------------------------------------
<pre>
<code>
public abstract class KakaoFriends {

    private String name;
    private int age;

    public KakaoFriends(){

    }

    public KakaoFriends(String name, int age){
        this.name = name;
        this.age = age;
    }

    abstract public void move();

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
</code>
</pre>
--------------------------------------
>+ abstract 키워드를 사용하여 추상클래스라는 것을 명시할 수 있습니다.
>+ 추상클래스는 자기 스스로 인스턴스를 생성하지 못합니다.
>+ 그리고 추상클래스는 abstract메서드를 선언 할 수도 있고 안 할 수도 있습니다.
>+ 상속받아서 재구현해야 하므로 private 접근지정자를 사용 못합니다.

### 예시)
--------------------------------------
<pre>
<code>
public class Ryan extends KakaoFriends {

    public Ryan(String name, int age) {
        super(name, age);
    }

    @Override
    public void move() {
        System.out.println("라이언은 늠름하게 움직입니다.");
    }
}
</code>
</pre>

<pre>
<code>
public class Apech extends KakaoFriends {

    public Apech(String name, int age) {
        super(name, age);
    }

    @Override
    public void move() {
        System.out.println("어피치는 통통 튀는 매력으로 움직입니다.");
    }
}
</code>
</pre>
Ryan is a KakaoFriends
Apech is a KakaoFriends

--------------------------------------

#interface
### 예시)
--------------------------------------
<pre>
<code>
public interface ServiceInterface {

    public static final int MAX_NUM = 100; //상수 필드

    public void getMemberInformation();
    public void setMemberInformation();
    abstract public void test();
    public default void print(){
        System.out.println("디폴트 메소드");
    }
    public default void print2(){}

    public static void staticPrint() {
        System.out.println("인터페이스도 정적메서드를 가질 수 있다.");
    }

}
</code>
</pre>
인터페이스는 
- 상수 필드
- 추상메서드
- default 메서드
- 정적 메서드
이 4가지를 정의할 수가 있다.(Java 8 기준. 이전에는 추상메서드만 선언가능)
--------------------------------------
### 예시)
--------------------------------------
<pre>
<code>
public class HRService implements ServiceInterface {

    @Override
    public void getMemberInformation() {
        System.out.println("인사정보 조회");
    }

    @Override
    public void setMemberInformation() {
        System.out.println("인사정보 추가");
    }

    @Override
    public void test() {

    }
}
</code>
</pre>

<pre>
<code>
public class ShoppingService implements ServiceInterface {
    @Override
    public void getMemberInformation() {
        System.out.println("쇼핑몰 회원정보 조회");
    }

    @Override
    public void setMemberInformation() {
        System.out.println("쇼핑몰 회원정보 추가");
    }

    @Override
    public void test() {

    }
</code>
</pre>
class 라는 키워드 대신, interface 라는 키워드를 사용해서 정의합니다.
interface는 추상메서드들만 정의가 가능(자바 8 오면서 조금 변했지만)
구현 시, implement 라는 키워드를 이용해서 상속받아 구현합니다.

--------------------------------------

#abstact class vs interface
###차이점
>추상클래스는 extends(확장 : 상속) 키워드를 통해, 기능을 확장하고 이용하는데 목적이 있습니다.(계층구조로 명확히 표현할 때도 좋음)

>인터페이스는 implement(구현) 키워드를 통해, 구현클래스 또는 서브클래스에게 구현을 강제하는데 목적이 있습니다.
구현을 강제함으로써, 구현클래스의 인스턴스는 같은 동작 또는 독립된 동작을 보장받을 수 있습니다.(디자인을 구성하는 요소들이 자주 바뀔때 사용하면 좋다. 비행기들 마다, 디자인된 요소들은 같지만 요소들이 각각 조금씩 다르고 변경이 심할 때.)

>그리고, 자바에서는 단일 상속만 가능하지만. 인터페이스를 이용하면 다중으로 상속을 할 수 있습니다.

### 예시)
--------------------------------------
<pre>
<code>
public class MyVehicle extends Car, AirPlane {
}

public class AirPlane {

    public void drive(){
        System.out.println("슈우우우웅");
    }
}

public class Car {

    public void drive(){
        System.out.println("부릉부릉");
    }
}
</code>
</pre>
저런식으로, 다중상속을 받으면. 누구의 drive()를 호출해야 할까요?
다중상속의 모호성 때문에, 자바에서는 기본적으로 단일상속만을 지원합니다.

반면에 인터페이스는 아래와 같이. 다중상속을 받아서 구현을 하지만, 에러없이 잘 구현해서 구현클래스의 동작을 보장을 해줍니다. 이런 모습 때문에, 다중상속에 문제점을 해결하기 위해 존재하는거 아니냐라는 오해를 사기도 합니다.

<pre>
<code>
public class ShoppingService2 implements ServiceInterface, ServiceInterface2 {
    @Override
    public void getMemberInformation() {

    }

    @Override
    public void setMemberInformation() {

    }

    @Override
    public void test() {

    }
}

public interface ServiceInterface {

    public static final int MAX_NUM = 100; //상수 필드

    public void getMemberInformation();
    public void setMemberInformation();
    abstract public void test();
    public default void print(){
        System.out.println("디폴트 메소드");
    }
    public default void print2(){}

    public static void staticPrint() {
        System.out.println("인터페이스도 정적메서드를 가질 수 있다.");
    }

}

public interface ServiceInterface2 {

    public void getMemberInformation();
    public void setMemberInformation();
}
</code>
</pre>

--------------------------------------

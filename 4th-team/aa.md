# Java Inner Class (내부 클래스)

>자바 이너 클래스 혹은 중첩 클래스는 하나의 클래스로, **클래스나 인터페이스 내부**에 선언되는 클래스 입니다. **가독성**과 **유지보수**에 유리합니다. 외부클래스의 **모든 멤버에 접근** 가능합니다.


### 1. Syntax
--------------------------------------
<pre>
<code>
>class Java_Outer_class{
    //code
class Java_Inner_class{
    //code
}
}
</code>
</pre>
--------------------------------------

### 2. 장점

>1) 외부클래스의 모든 멤버 (데이터, 메소드 등)에 접근할 수 있다.
>2) 외부클래스 내부에 있기 때문에 가독성이 좋고, 유지보수에 유리하다.
>3) 코드 최적화 유리

### 3. 이너클래스 vs 중첩클래스

이너클래스는 중첩클래스의 한 부분입니다.
중첩 클래스 중 정적 중첩 클래스가 이너클래스입니다.

#####중첩 클래스의 2가지 타입
>1) 정적 중첩 클래스 (이너 클래스)
>* 멤버 이너 클래스
>* 익명 이너 클래스
>* 지역 이너 클래스
>2) 동적 중첩 클래스

### 4. 정적 중첩 클래스 (이너 클래스)

정적 중첩 클래스는 클래스 내에서 만들어 지고, 외부 메소드는 멤버 이너 클래스라고 불립니다.

######syntax :
--------------------------------------
<pre>
<code>
>class outer{
    //code
class inner{
    //code
}
}
</code>
</pre>
--------------------------------------

### 5. Member inner class

아래 예에서는,
외부 클래스의 개인적 데이터 멤버로 접속할 수 있는, 멤버 이너클래스로 msg() 메소드를 만들 수 있습니다.

--------------------------------------
<pre>
<code>
class TestMemberOuter1{

 private int data=30;

 class Inner{

  void msg(){System.out.println("data is "+data);}

}

 public static void main(String args[]){

  TestMemberOuter1 obj=new TestMemberOuter1();

  TestMemberOuter1.Inner in=obj.new Inner();

  in.msg();

 }

} 
</code>
</pre>
output
data is 30

--------------------------------------

### 6. Anoymous inner class
이 클래스는 이름이 없습니다.
인터페이스나 클래스의 메소드를 오버라이딩 해야한다면, 이 클래스가 사용될 수 있습니다.
클래스로 만드는 방법 인터페이스로 만드는 방법 두가지가 있습니다.

#####예시)

1) 클래스 사용
--------------------------------------
<pre>
<code>
abstract class Person{

   abstract void eat();

 }

class TestAnonymousInner{

 public static void main(String args[]){

  Person p=new Person(){

  void eat(){System.out.println("nice fruits");}

  };

  p.eat();

 }

}
</code>
</pre>
output
nice fruits

--------------------------------------

2) 인터페이스 사용
--------------------------------------
<pre>
<code>
interface Eatable{

  void eat();

}

class TestAnnonymousInner1{

  public static void main(String args[]){

  Eatable e=new Eatable(){

    public void eat(){System.out.println("nice fruits");}

 };

 e.eat();

 }

}
</code>
</pre>
output
nice fruits

--------------------------------------
###7. Local inner class
메소드 안에서 생성되는 클래스를 지역 이너 클래스라 부릅니다.
만약 지역 이너 클래스를 불러오고 싶다면, 메소드 안에 클래스를 만들어야 합니다.
#####예시)

--------------------------------------
<pre>
<code>
public class localInner1{

    private int data=30; // 인스턴스 변수

    void display(){

      class Local{

        void msg(){System.out.println(data);}

     }

    Local l=new Local();

     l.msg();

     }

     public static void main(String args[]){

       localInner1 obj=new localInner1();

        obj.display();

   }

}
</code>
</pre>
output
30

--------------------------------------

###중첩 인터페이스도 있습니다 !!!!!!!!
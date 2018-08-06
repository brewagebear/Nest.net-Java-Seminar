6.4 오버로딩(overloading)
=========================
오버로딩이란
-----------
->하나의 클래스에 같은 이름의 메서드를 여러개 정의하는 것을 오버로딩이라고 한다.
* * *
**오버로딩의 조건**
--------------
>1. 매서드의 이름이 같아야 한다.
>2. 매개변수의 개수 또는 타입이 달라야 한다.
>3. 매개변수는 같고 리턴타입이 다른 경우는 오버로딩이 성립되지 않는다.(이 경우 중복 정의로 간주되어 컴파일 시에 에러가 발생한다.)
* * *
오버로딩의 예
-------------
1. System.out.println메서드
* 다양하게 오버로딩된 메서드를 제공함으로써 모든 변수를 출력할 수 있도록 설계
<pre><code>void println()
void println(boolean x)
void println(char x)
void println(char[] x)
void println(double x)
void println(float x)
void println(int x)
void println(long x)
void println(Object x)
void println(String x)</code></pre>

2. 매개변수의 이름이 다른 것은 오버로딩이 아니다.
* 매개변수의 이름만 다른경우,아무의미가 없는 문장
<pre><code>int add(int a,int b) { return a+b; }
int add(int x,int y) { return x+y; }</code></pre>

3. 리턴타입은 오버로딩의 성립조건이 아니다.
* 리턴타입만 다른경우 어떤 메서드가 호출된 것인지 결정할 수 없기 때문에 오버로딩으로 간주되지 않는다.
<pre><code>int add(int a,int b) { return a+b; }
long add(int a,int b) { return (long)(a+b); }</code></pre>

4. 매개변수의 타입이 다르므로 오버로딩이 성립한다.
* 서로 순서가 다른 경우,호출 시 매개변수의 값에 의해 호출될 메서드가 구분될 수 있으므로 오버로딩으로 간주된다.
<pre><code>long add(int a,long b) { return a+b; }
long add(long a,int b) { return a+b; }</code></pre>
5. 매개변수는 다르지만 같은 의미의 기능 수행
<pre><code>
int add(int a,int b) { return a+b; }
long add(long a,long b) { return a+b; }
int add(int[] a){
    int result=0;
    for(int i=0;i < a.length;i++){
    	result+=a[i];
    }
    return result;
}
 </code></pre>
* * *
가변인자와 오버로딩
-----
* 기존에 메서드의 매개변수 개수는 고정적이었으나 JDK1.5부터 동적으로 지정해 줄 수 있게 되었으며, 이 기능을 가변인자라고 한다.
* 가변인자는 '타입... 변수명'과 같은 형식으로 선언한다.
<pre>
String concatenate(String s1,String s2) {...}
String concatenate(String s1,String s2,String s3) {...}
String concatenate(String s1,String s2,String s3,String s4) {...}
</pre>
<pre>
String concatenate(String... str) {...}
</pre>
>이 메서드를 호출할 때는 인자가 아예 없어도 되고 배열도 인자가 될 수 있다.

가변인자를 사용한 메서드를 오버로딩 할 때 문제점
----
* 가능하면 가변인자를 사용한 메서드는 오버로딩 하지 않는 것이 좋다.
<pre>
static String concatenate(String delim,String... args) {...}
static String concatenate(String... args) {...}
</pre>

>concatenate(s1,s2,s3)와 같이 호출시에 두 메서드중 무엇을 호출했는지 구별되지 못해서 오류가 발생한다.

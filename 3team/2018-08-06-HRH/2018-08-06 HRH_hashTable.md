## 해쉬테이블
### 해쉬테이블이란?
>해쉬테이블 : 키(key) 와  값(value) 로 이루어진 한 쌍으로 데이터를 저장한다.  


### 사용법
1) 선언

>Hashtable<Integer, String> ht = new Hashtable<> (); //key: Integer 타입, value: String 타입으로 저장

2) 메소드
* put(key, value) 

    해당하는 키(key)에 값(value)을 집어넣는 메소드
<pre><code>
ht.put(new Integer(1), "안녕하세요"); //key: 1, value: 안녕하세요
ht.put(2, "감사해요"); //key: 2, value: 감사해요
ht.put(3, "잘있어요"); //key: 3, value: 잘있어요
</pre></code>  

* get(key)  

    키(key) 값에 해당하는 값(value)을 찾아서 반환해준다
<pre><code>
String a = ht.get(2); 
//a.equals("감사해요")
</pre></code>  

* containsKey(key)  

    키(key)가 있는지 없는지 확인하는 메소드  
    반환형은 Boolean  

* containsValue(value)  

    값(value)가 있는지 없는지 확인하는 메소드  
    반환형은 Boolean  

* clear()  

    해쉬테이블내 모든 키(key) 와 값(value) 를 지운다.  

  
  
### HashMap 과의 차이점
>단일 쓰레드에는 HashMap, 멀티 쓰레드에는 HashTable 을 쓴다. jdk 1.8 이후에서는 HashTable 보다 ConcurrentHashMap 사용을 권장한다.  
HashTable 은 Key 와 Value 에 null값을 허용하지 않는다.

* 참고 사이트  
https://sthwin.blog.me/220825616965


  

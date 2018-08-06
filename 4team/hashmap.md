# HashMap   

### 해쉬맵이란?
>HashMap은 Map을 구현한다. Key와 value를 묶어 하나의 entry로 저장한다는 특징을 갖는다. 그리고 hashing을 사용하기 때문에 많은양의 데이터를 검색하는데 뛰어난 성능을 보인다.

> + Map 인터페이스의 한 종류로 ( "Key", value) 로 이뤄져 있다.
> + key 값을 중복이 불가능 하고 value는 중복이 가능. value에 null값도 사용 가능하다.
> + 멀티쓰레드에서 동시에 HashMap을 건드려 Key - value값을 사용하면 문제가 될 수 있다. 멀티쓰레드에서는 HashTable을 쓴다
--------------------------------------

| 생성자 / 메서드 | 설명 및 예시 |
|:--------:|:--------:|
| HashMap() | - HashMap 객체를 생성 <br/>ex) HashMap<String , Integer> map = new HashMap<String , Integer>(); <br/>Map<String, Integer> map = new HashMap<String, integer>();|
|HashMap(int initlalCapacity)|- 지정된 값을 초기 용량으로 하는 HashMap객체를 생성한다.|
|HashMap(int initlalCapacity, float loadFactory)|- 지정된 값을 초기용량과 load factory의 HashMap 객체를 생성한다.| 
|HashMap(Map m) |- 주어진 Map에 저장된 모든 요소를 포함하는 HashMap을 생성한다. |
|void clear()|- HashMap에 저장된 모든 객체를 제거한다.<br/>ex) map.clear();|
|Object clone()|- 현재 HashMap을 복제하여 반환한다.<br/>ex) newmap = (HashMap)map.clone();|
|Object put(Object Key, Object Value)|- HashMap에 키와 값을 저장.<br/>ex) map.put("A", "aaa");<br/>map.put("B", "bbb");<br/>map.put("C", "ccc");|
|boolean containsKey(Object Key)|- HashMap에 지정된 키(Key)가 포함되어 있는지 알려준다.|
|boolean containsValue(Object Value)|- HashMap에 지정된 값(Value)가 포함되어 있는지 알려준다.|
|Set entrySet()|- HashMap에 저장된 Key - Value갑슬 엔트리(키와 값을 결합)의 형태로 Set에 저장하여 반환<br/>ex) map.put("A", 1);<br/>map.put("B", 2);<br/>map.put("C", 3);<br/>Set set = map.entrySet();<br/>System.out.println("set values are" + set);<br/>(result) set values : [A=1,B=2,C=3]<br/>
|Object get(Object Key)|- 지정된 Key 의 값을 반환한다.<br/>ex) map.put("A", 1);<br/>map.put("B", 2);<br/>map.put("C", 3);<br/>String val = (String)map.get("B");<br/>System.out.println("Value for key B is: " + val);<br/>(result)<br/> Value for key B is 2<br/>|
|Set keySet()|- HashMap에 저장된 모든 키가 저장된 Set을 반환한다.<br/>ex) map.put("A", 1);<br/>map.put("B", 2);<br/>map.put("C", 3);<br/>Set keyset = map.keySet();<br/>System.out.println("Key set values are" + keyset);<br/>(result) Key set values are [A,B,C]<br/>|
|void putAll(Map m)|- Map에 해당하는 모든 요소를 HashMap에 저장한다.|
|Object remove(Object Key)|- HashMap에서 지정된 키로 지정된 값을 제거한다.<br/>ex) map.remove("key");|
|int size()|- HashMap에 저장된 요소의 개수를 반환한다.|
|Collection values()|- HashMap에 저장된 모든 값을 컬렉션 형태로 반환한다.|

<pre>
<code>
import java.util.HashMap;

import java.util.Iterator;

import java.util.Map;

import java.util.Set;

 

pubilc class HashMapDemo

{

 public static void main(String[] args) 

 {

  HashMap<String, Integer> fruitMap = new HashMap();

  fruitMap.put("사과", 1000);

  fruitMap.put("배", 2000);

  fruitMap.put("자두", 3000);

  fruitMap.put("수박", 4000);

 

  // get() --> Key에 해당하는 Value를 출력한다.

  System.out.println( fruitMap.get("자두") );   // 3000

 

        // values() --> 저장된 모든 값 출력

  System.out.println( fruitMap.values() ); // [1000, 2000, 3000, 4000]

 

  // HashMap에 넣은 Key와 Value를 Set에 넣고 iterator에 값으로 Set정보를 담에 준다.

  // Interator itr = fruitMap.entrySet().interator(); 와 같다.

  Set<Entry<String, Integer>> set = fruitMap.entrySet();

  Interator<Entry<String, Integer>> itr = set.interator();

  while (itr.hasNext())

  {

   Map.Entry<String, Integer> e = (Map.Entry<String, Integer>)itr.next();

   System.out.println("이름 : " + e.getKey() + ", 가격 : " + e.getValue() + "원");

  }

}
</code>
</pre>
--------------------------------------
>output
이름 : 사과, 가격 : 1000원
이름 : 배, 가격 : 2000원
이름 : 자두, 가격 : 3000원
이름 : 수박, 가격 :  4000원

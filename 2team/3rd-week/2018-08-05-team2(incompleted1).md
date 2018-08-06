셋(Set) : 데이터 집합의 한 종류
========
## - 저장순서 유지X 
## - 데이터 중복 허용X 

<img src=".\SetEdit.PNG" alt="셋 상속도" width = 400>

--------------
--------------
해시셋(HashSet)
==============




--------------
--------------

소트셋(SortedSet)
==============
>교재에는 SortedSet, NavigableSet과 관련된 내용이 빠져있습니다. 대신 JAVA API 문서를 참고해주세요.  
https://docs.oracle.com/javase/10/docs/api/java/util/SortedSet.html

## 저장된 원소에 대한 **전순서** 배열을 지원하는 Set의 **확장 인터페이스**
### 임의의 두 **원소를 비교하여 규칙에 따라 순서** 지정
### Iterator은 항상 **오름차순**으로만 이동

-------------------

### SortedSet의 메서드
<img src=".\SortedSet methods.PNG" alt="소트셋 메서드" width = 1100>

>Spliterator는 Iterator과 비슷하게 객체를 탐색하고 분할하기 위한 인터페이스로, 병렬 작업에 보다 특화되었다.

### 규칙
- Comparable : 통념적인 순서 (1-2-3-4-... / A-B-C-D) (natural order)
- Comparator : 사용자가 정한 특정한 규칙
>Comparator 인터페이스는 SortedSet 생성 시에 제공된다.

### SortedSet을 구현한 클래스의 생성자 규칙
1. 매개변수 X (빈 SortedSet)
2. Comparator 매개변수 1개 (특정 규칙있는 빈 SortedSet)
3. Collection 매개변수 1개 (Collection과 같은 원소의 SortedSet, 통념적인 순서)
4. SortedSet 매개변수 1개 (SortedSet과 같은 원소, 순서의 SortedSet)

----------------------
-----------------------

네비게이블셋(NavigableSet)
==============

## SortedSet에 **검색 목표에 가장 근접한 결과** 확인 기능을 추가한 **인터페이스**
### SortedSet과 달리 **오름차순, 내림차순** 접근 모두 가능

>단, 오름차순 탐색속도가 더 빠르다.

### NavigableSet의 메서드
<img src=".\NavigableSet methods.png" alt="네비게이블셋 메서드" width = 1100>

### 반환값이 null일 경우 모호해지므로 null 추가를 허용하지 않는 것을 권장
>본질적으로 Comparable은 null 값을 허용하지 않는다.

--------------

### TreeSet **클래스**와 ConcurrentSkipListSet **클래스**는 NavigableSet **인터페이스**를 상속받은 것  
  
   
## 즉, SortedSet과 NavigableSet 모두 **인터페이스**이므로 단독적으로 사용불가

-------------
--------------

ConcurrentSkipListSet
=========

## **NavigableSet 인터페이스를 상속받은 클래스**의 한 종류
> Java SE 10 API 문서 기준 NavigableSet을 상속받은 클래스에는 ConcurrentSkipListSet과 TreeSet 두 종류가 있다.

### NavigableSet에 **쓰레드 안정성과 함수의 원자성을 보장**하고 **확장성**을 추가한 클래스
> A scalable concurrent NavigableSet implementation based on a ConcurrentSkipListMap. (Java SE 10 API 문서)

### 원소의 보다 빠른 검색을 위해 **skip list 자료구조**를 적용
<img src=".\skip_list.png" alt="네비게이블셋 메서드" width = 500>

### ConcurrentSkipListSet 생성자
<img src=".\concurrent-constructor.PNG" alt="ConcurrentSkipListSet생성자" width = 1100>


### NavigableSet과 마찬가지로 **오름차순, 내림차순** 접근 모두 가능
> 단, 오름차순 탐색속도가 더 빠르다.

### ConcurrentSkipListSet을 이용한 샘플 코드 - 1

```java
import java.util.Iterator;
import java.util.NavigableSet;
import java.util.concurrent.ConcurrentSkipListSet;

public class ConcurrentSkipListSetDemo {

    public static void main(String[] args) {
        NavigableSet<String> citySet = new ConcurrentSkipListSet<String>();
        citySet.add("Seoul");
        citySet.add("Cheongju");
        citySet.add("Seongnam");
        citySet.add("Jeonju");
        citySet.add("Busan");

        
        System.out.println("---- Traversing the set----");
        Iterator<String> itr = citySet.iterator();
        while(itr.hasNext()){
            System.out.println("Value -  " + itr.next());
        }
    }
}
```

### 출력 결과

    ---- Traversing the set----  
    Value - Busan  
    Value - Cheongju  
    Value - Jeonju  
    Value - Seongnam  
    Value - Seoul  

> 별도의 Comparator을 제시하지 않았기 때문에 원소를 추가하면 자동으로 알파벳순으로 정렬한다. (통념적 순서)

### ConcurrentSkipListSet을 이용한 샘플 코드 - 2

```java
import java.util.Iterator;
import java.util.NavigableSet;
import java.util.Set;
import java.util.concurrent.ConcurrentSkipListSet;

public class CSSDemo {
    public static void main(String[] args) {
        NavigableSet<String> citySet = new ConcurrentSkipListSet<String>();
        citySet.add("Seoul");
        citySet.add("Cheongju");
        citySet.add("Seongnam");
        citySet.add("Jeonju");
        citySet.add("Busan");
        
        System.out.println("---- Traversing the set-----");
        Iterator<String> itr = citySet.iterator();
        while(itr.hasNext()){
            System.out.println("Value -  " + itr.next());
        }

        System.out.println("---- Higher & Lower-----");
        
        System.out.println("Higher - " + citySet.higher("B"));
        
        System.out.println("Lower - " + citySet.lower("Seongnam"));
        
        System.out.println("---- Tail Set -----");
        
        Set<String> set = citySet.tailSet("Cheongju");
        
        itr = set.iterator();
        while(itr.hasNext()){
            System.out.println("Value -  " + itr.next());
        }
    }
}
```

### 출력 결과

    ---- Traversing the set-----  
    Value - Busan  
    Value - Cheongju  
    Value - Jeonju  
    Value - Seongnam  
    Value - Seoul  
    ---- Higher & Lower ----
    Higher - Busan
    Lower - Jeonju
    --- Tail Set ----
    Value - Cheongju  
    Value - Jeonju  
    Value - Seongnam  
    Value - Seoul

> Higher : 지정된 원소 또는 입력된 데이터 바로 윗값의 원소를 반환한다. 입력된 데이터가 B이므로 사전적 순서 상 Busan이 반환된다.  
> Lower : 지정된 원소 또는 입력된 데이터 바로 아랫값의 원소를 반환한다. 지정된 원소가 Seongnam이므로 사전적 순서 상 Jeonju가 반환된다.  
> tailSet : 매개변수가 Set의 원소 하나이므로 SortedSet의 메서드임을 알 수 있다. 지정된 원소 Cheongju 이상의 값을 갖는 원소들이 반환된다.


참고한 사이트  
https://docs.oracle.com/javase/10/docs/api/overview-summary.html  
https://netjs.blogspot.com/
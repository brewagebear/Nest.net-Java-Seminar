13.7 데몬 쓰레드 (Daemon Thread)
====

일반 쓰레드의 작업을 돕는 보조적인 역할을 하는 쓰레드
----

### 1. 일반 쓰레드가 모두 종료되면 자동으로 종료됨
### 2. 실행 후 대기하다가 특정 조건이 만족될 때만 작업 수행

실행방법
----

### 쓰레드 생성 후 실행하기 전 setDaemon(true) 호출

```java
boolean isDaemon() // 데몬 쓰레드 여부 확인
void setDaemon(boolean on) // 데몬 쓰레드로 변경
```


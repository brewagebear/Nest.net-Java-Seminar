#표준입출력과 FILE

####입출력
>컴퓨터 내부 또는 외부의 장치와 프로그램간의 데이터를 주고받는 것
####stream
>자바에서 입출력을 수행하기 위해 두 대상을 연결하고 데이터를 운반하는데 사용되는 연결통로
먼저 보낸 데이터를 먼저 받게 되어 있으며 중간에 건너뜀 없이 연속적으로 데이터를 주고 받는다.
####byte기반 stream
>스트림은 바이트단위로 데이터를 전송하며 입출력 대상에 따라 다음과 같은 입출력스트림이 있다.
File - FileInputStream - FileOutputStream
Memory(Byte배열) - ByteArrayInputStream - ByteArrayOutputStream
Process - PipedInputStream - PipedOutputStream
Audio - AudioInputStream - AudioOutputStream
이들은 모두 InputStream 또는 OutputStream의 자손들이며, 각각 읽고 쓰는데 필요한 추상메서드를 자신에 맞게 구현해 놓았다. 자바에서는 java.io패키지를 통해서 많은 종류의 입출력관련 클래스들을 제공한다.
InputStream의 read()와 OutputStream의 write(int b)는 입출력의 대상에 따라 읽고 쓰는 방법이 다를 것이기 때문에 각 상황에 알맞게 구현하라는 의미에서 추상메서드로 정의되어 있다.
####보조stream
>실제 데이터를 주고받는 스트림이 아니기 때문에 데이터를 입출력할 수 있는 기능은 없지만, 스트림의 기능을 향상시키거나 새로운 기능을 추가할 수 있다.

예를 들어 test.txt라는 파일을 읽기위해 FileInputStream을 사용할 때, 입력 성능을 향상시키기 위해 버퍼를 사용하는 보조스트림인 BufferedInputStream을 사용하는 코드는 다음과 같다.

<pre>
<code>
// 먼저 기반스트림을 생성한다.
FileInputStream fis = new FileInpustSrndtream("test.txt");

// 기반스트림을 이용해서 보조스트림을 생성한다.
BufferedInputStream bis = new BufferedInputStream(fis);
bis.read(); // 보조스트림인 BufferedInputStream으로부터 데이터를 읽는다.
</code>
</pre>

| 입력 | 출력 | 설명 |
|:--------|:--------|:--------|
| FilterInputStream | FilterOutputStream | 필터를 이용한 입출력 처리 |BufferedInputStream0|BufferedOutputStream|버퍼를 이용한 입출력 성능향상
| DataInputStream | DataOutputStream | int, float와 같은 기본형 단위(primitive type)로 데이터를 처리하는 기능 |
|SequenceInputStream|없음|두 개의 스트림을 하나로 연결
|LineNumberInputStream|	없음|읽어 온 데이터의 라인 번호를 카운트(JDK1.1부터 LineNumberReader로 대체)
|ObjectInputStream|	ObjectOutputStream|데이터를 객체 단위로 읽고 쓰는데 사용. 주로 파일을 이용하며 객체 직렬화와 관련 있음
|없음|PrintStream|버퍼를 이용하며, 추가적인 print관련 기능(print, printf, println메서드)
|PushbackInputStream|없음|버퍼를 이용해서 읽어 온 데이터를 다시 되돌리는 기능(unread, push back to buffer)

####문자기반stream
java에서는 한 문자를 의미하는 char형이 1byte가 아니라 2byte이기 때문에 바이트기반의 스트림으로 2byte인 문자를 처리하는 데는 어려움이 있다. 이 점을 보완하기 위해서 문자기반의 스트림이 제공된다. 문자데이터를 입출력할 때는 바이트기반 스트림 대신 문자기반 스트림을 사용하자.

바이트기반 스트림과 문자기반 스트림의 읽기 쓰기에 사용되는 메서드를 비교하면 byte배열 대신 char배열을 사용한다는 것과 추상메서드로 선언된 메서드의 종류가 다르다.
보조스트림 역시 문자기반 보조스트림이 존재하며 사용목적과 방식은 바이트 기반과 다르지 않다.

##표준입출력
--------------------------------------

JAVA에서는 SYSTEM 클래스를 통해 기본적인 스크린과 키보드를 통한 입출력 방법을 제시합니다. 이것을 표준 입출력 이라고 합니다. System 클래스 안에는 in, out , err 과같은 멤버 변수 가 있습니다. 순서대로 입력,출력,에러를 뜻합니다.

--------------------------------------

###in

System.in 의 변수타입이 InputStream입니다. 여기서 InputStream이 추상클래스입니다. 추상클래스는 객체를 생성할 수 없지만 형변환을 통하여 객체를 생성한 것입니다. 무엇인가를 키보드를 통해 입력하려고 할때 사용되는 것이 바로  'System.in'입니다. 자료형이 InputStream이기 때문에 바이트 단위로만 입출력이 허용됩니다. 한글은 두 바이트가 합쳐져야 의미를 가집니다. 그래서 System.in을 통하여 읽을 때는 영문과 한글의 처리를 구분해야 합니다.

--------------------------------------

###out
out도 역시 마찬가지로 OutputStream 클래스의 객체이지만 , 추상클래스는 객체가 될수 없기때문에 PrintStream 이라는 후손 클래스를 이용하여 객체를 생성하고 그것을 우리가 씁니다.

write()는 byte나 ASCII CODE를 출력할 때 쓰입니다. 그리고 write()는 print()와 달리 모니터에 바로 출력을 하는 것이 아니라 jvm buffer에 쌓아 두었다가 출력을 하는 방식이기 때문에 flush()를 써주어야 출력이 됩니다.
print()
println()
printf()

--------------------------------------

###err

out과 비슷 합니다. 표시 개념이 다르다고 볼 수 있습니다. 에러가 발생했을때 알려줘야 할 내용을 표시하고자 한다면 System.err 을 쓰면 되고 일반적인 데이터를 출력하고자한다면 System.out을 쓰면되는 겁니다. eclipse는 err로 출력되는 데이터를 빨간색으로 표시해줍니다.

--------------------------------------

##표준입출력의 대상변경

###setOut(), setErr(), setIn()

InputStream으로 System.in, OutputStream으로 System.out, System.err의 읽기/쓰기를 새로우 스트림으로 변경할 수 있다.

<pre>
<code>
OutputStream output = new FileOutputStream("system.out.txt");
PrintStream printOut = new PrintStream(output);

System.setOut(printOut);
</code>
</pre>

##RandomAccessFile

>입력과 출력을 하나의 클래스로 파일에 대한 입력/출력을 모두 할 수 있게 설계된 클래스. 가장 큰 장점은 파일의 어느 위치에나 읽기/쓰기가 가능하다는 점이다.


#####RandomAccessFile 생성
<pre>
<code>
RandomAccessFile file = new RandomAccessFile("file.txt", "rw");
</code>
</pre>
생성자의 두번쨰 'rw'는 RandomAccessFile의 mode 값이다. rw는 Read/Write를 뜻한다.

#####RandomAccessFile 이동
<pre>
<code>
RandomAccessFile file = new RandomAccessFile("file.txt", "rw");

//단위 : Byte
file.seek(200);

long pointer = file.getFilePointer();

file.close();
</code>
</pre>

#####RandomAccessFile 읽기/쓰기
<pre>
<code>
//읽기 사용법
RandomAccessFile file = new RandomAccessFile("file.txt", "rw");

int aByte = file.read();

file.close();
</code>
</pre>
<pre>
<code>
//쓰기 사용법
RandomAccessFile file = new RandomAccessFile("file.txt", "rw");

file.write("Hello World".getBytes());

file.close();
</code>
</pre>

##File
>File 클래스로 통해 파일과 디렉토리를 다룰 수 있도록 제공한다

File클래스는 파일과 파일의 메타데이터의 접근하는 기능만 제공한다. 만약 파일의 내용을 읽기/쓰기 기능을 원한다면 file Stream을 이용해야한다.

#####File 초기화
<pre>
<code>
File file = new File("input-file.txt");
</code>
</pre>
#####존재여부 확인
File 객체 생성시 실제 파일이 없어도 예외가 나지 않고 정상적으로 생성된다.
<pre>
<code>
boolean fileExists = file.exists();
</code>
</pre>
#####디렉토리 생성
mkdir() / mkdirs()
<pre>
<code>
File file = new File("c:\\users\\javastudy\\newdir");

boolean dirCreated = file.mkdir();
</code>
</pre>
#####파일 길이
<pre>
<code>
long length = file.length();
</code>
</pre>
#####Rename
<pre>
<code>
boolean success = file.renameTo(new File("c:\\data\\new-file.txt"));
</code>
</pre>
#####파일삭제
<pre>
<code>
boolean success = file.delete();
</code>
</pre>
#####디렉토리 확인
<pre>
<code>
boolean isDirectory = file.isDirectory();
</code>
</pre>
#####파일 리스트
list() / listFiles()
<pre>
<code>
File file = new File("c:\\data");

String[] fileNames = file.list();

File[]   files = file.listFiles();
</code>
</pre>

##직렬화(Serialization)
>자바 직렬화란 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 데이터 변환하는 기술과 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역직렬화)을 아울러서 이야기합니다.
시스템적으로 이야기하자면 JVM(Java Virtual Machine 이하 JVM)의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 바이트 형태로 변환하는 기술과 직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태를 같이 이야기합니다.

자바 오브젝트를 쓰고(Serialization) 읽기(Deserializetion) 하기 위해선 Serializable 인터페이스를 구현(선언)해야한다.
##ObjectInputStream과 ObjectOutputStream
ObjectInputStream/ObjectOutputStream은 raw 한 byte를 읽는거 대신, InputStream/OutputStream을 통해 자바 오브젝트를 읽을 수 있도록 해준다.
###직렬화
<pre>
<code>
    Member member = new Member("김배민", "deliverykim@baemin.com", 25);
    byte[] serializedMember;
    try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
        try (ObjectOutputStream oos = new ObjectOutputStream(baos)) {
            oos.writeObject(member);
            // serializedMember -> 직렬화된 member 객체 
            serializedMember = baos.toByteArray();
        }
    }
    // 바이트 배열로 생성된 직렬화 데이터를 base64로 변환
    System.out.println(Base64.getEncoder().encodeToString(serializedMember));
}
</code>
</pre>
위 예제에서 객체를 직렬 화하여 바이트 배열(byte []) 형태로 변환하였습니다.


###역직렬화
<pre>
<code>
    // 직렬화 예제에서 생성된 base64 데이터 
    String base64Member = "...생략";
    byte[] serializedMember = Base64.getDecoder().decode(base64Member);
    try (ByteArrayInputStream bais = new ByteArrayInputStream(serializedMember)) {
        try (ObjectInputStream ois = new ObjectInputStream(bais)) {
            // 역직렬화된 Member 객체를 읽어온다.
            Object objectMember = ois.readObject();
            Member member = (Member) objectMember;
            System.out.println(member);
        }
    }
</code>
</pre>
###직렬화가 가능한 클래스 만들기 - Serializable, transient
>직렬화가 가능한 클래스를 만드는 방법은 Serializable 인터페이스를 원하는 클래스에 구현(선언)하면 된다.
<pre>
<code>
class UserInfo implements Serializable {
  String name;
  transient String password;
  int age;
}
</code>
</pre>
###직렬화가능한 클래스의 버전관리
####serialVersionUID
>직렬화된 객체를 역직렬화할 떄는 직렬화 했을 떄와 같은 클래스를 사용해야한다. 하지만 클래스의 내용이 변경된 경우 역직렬화에 실패한다.
<pre>
<code>
public static class Person implements Serializable {

    private static final long serialVersionUID = 1234L;

    public String name = null;
    public int    age  =   0;
    //public String address = "";
}
</code>
</pre>
static 변수나 transient가 붙은 인스턴스변수는 직렬화에 영향을 미치지 않는다.


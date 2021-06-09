# Java IO

## 스트림(Stream)

데이터를 운반하는데 사용되는 연결통로이다.  

스트림은 연속적인 데이터의 흐름을 물에 비유해서 붙여진 이름인데 여러 가지로 유사한 점이 많다.  
물이 한쪽 방향으로만 흐르듯이 스트림도 단방향 통신만 가능하며 따라서 입력과 출력을 동시에 처리할 수 없다.
그래서 입력 스트림(input stream)과 출력 스트림(output stream)이 필요하다.  

스트림은 먼저 보낸 데이터를 먼저 받게 되어 있으며 중간에 건너뜀 없이 연속적으로 데이터를 주고 받는다.  
큐(queue)와 같은 FIFO(First In First Out)구조로 되어 있다고 생각하면 된다.

### 보조스트림

스트림의 기능을 보완하기 위한 보조스트림이 존재한다.  
보조스트림은 실제 데이터를 주고받는 스트림이 아니기 때문에 데이터를 입출력할 수는 없지만, 스트림의 기능을 향상시키거나 새로운 기능을 추가할 수 있다.  

예를 들어, 텍스트 파일을 읽기 위해 FileInputStream 을 사용할 때, 입력 성능을 향상시키기 위해 버퍼를 사용하는 보조스트림인 BufferedInputStream 을 사용한다.  
버퍼를 사용한 입출력과 사용하지 않은 입출력간의 성능 차이는 상당하기 때문에 대부분의 경우에 버퍼를 이용한 보조스트림을 사용한다고 한다.  
-> 실제 테스트하여 시간 비교를 해보자

#### 버퍼 (Buffer)

버퍼는 두 장치간 또는 장치와 애플리케이션간에 전송되는 데이터를 임시 저장하는 메모리 영역이다.  
버퍼를 사용하면 OS 레벨에 있는 시스템 콜의 횟수 자체를 줄이기 때문에 성능이 빨라지는 것이다.

## Byte Stream

바이트 단위로 데이터를 전송하는 스트림이다.  
즉, 입출력의 단위가 1 byte 이다.

### InputStream 과 OutputStream

모든 바이트기반 io 클래스의 상위 클래스이다.

#### InputStream

##### void close()

스트림을 닫음으로써 사용하고 있던 자원을 반환한다.

##### void mark(int readlimit)

현재 위치를 표시해 놓는다. 후에 reset() 에 의해서 표시해 놓은 위치로 다시 돌아갈 수 있다.  
readlimit 은 되돌아갈 수 있는 byte 의 수이다.

##### boolean markSupported()

mark() 와 reset() 지원여부를 알려준다.  
mark() 와 reset() 기능을 지원하는 것은 선택적이므로, 사용하기 전에 해당 메서드를 호출해서 지원여부를 확인해야 한다.

##### abstract int read()

1 byte 를 읽어 온다. 더 이상 읽어 올 데이터가 없으면 -1 을 반환한다.  
abstract 메서드라서 InputStream 의 하위 클래스들은 자신들의 상황에 알맞게 구현해야한다.

##### int read(byte[] b)

배열 b 의 크기만큼 읽어서 배열을 채우고 읽어 온 데이터의 수를 반환한다.  
반환하는 값은 항상 배열의 크기보가 작거나 같다.

##### int read(byte[] b, int off, int len)

최대 len 개의 byte 를 읽어서, 배열 b 의 지정된 위치(pff)부터 저장한다.  
실제로 읽어 올 수 있는 데이터가 len 개보다 적을 수 있다.

##### void reset()

스트림에서의 위치를 마지막으로 mark() 이 호출되었던 위치로 되돌린다.

##### long skip(long n)

스트림에서 주어진 길이(n) 만큼을 건너뛴다.

#### OutputStream

##### void close()

입력소스를 닫음으로써 사용하고 있던 자원을 반환한다.

##### void flush()

스트림의 버퍼에 있는 모든 내용을 출력소스에 쓴다.

##### abstract void write(int b)

주어진 값을 출력소스에 쓴다.

##### void write(byte[] b)

주어진 배열 b 에 저장된 모든 내용을 출력소스에 쓴다.

##### void write(byte[] b, int off, int len)

주어진 배열 b 에 저장된 내용 중에서 off 번째부터 len 개 만큼만을 읽어서 출력소스에 쓴다.

## Character Stream

문자 데이터를 다루는데 사용된다는 것을 제외하면 바이트 스트림의 사용방법가 유사하다.  
문자 데이터를 다루기 때문에 입출력의 단위는 2 byte 가 된다.

다만, 문자 스트림이 단순히 2 byte 로 스트림을 처리하는 것만을 의미하지는 않는다.  
문자 스트림은 여러 종류의 인코딩과 자바에서 사용하는 유니코드간의 변환을 자동적으로 처리해준다.

#### Reader 와 Writer

바이트 스트림의 InputStream 과 OutputStream 과 같은 역할을 하는 것이 Reader 와 Writer 이다.  
byte 배열 대신 char 배열을 사용한다는 것 외에는 InputStream/OutputStream 메서드와 다르지 않다.

Reader 는 특정 인코딩을 읽어서 유니코드로 변환하고 Writer 는 유니코드를 특정 인코딩으로 변환하여 저장한다.

## 표준 입출력

표준 입출력은 콘솔을 통한 데이터 입력과 콘솔로의 데이터 출력을 의미한다.  
Java 에서는 표준 입출력을 위해 3가지 입출력 스트림 System.in, System.out, System.err 을 제공한다.

#### System.in

콘솔로부터 데이터를 입력받는데 사용한다.

#### System.out 과 System.err

콘솔로 데이터를 출력하는데 사용한다.

<hr>

#### References

> 웹 문서
> - [geeksforgeeks | Java IO : Input-output in Java with Examples](https://www.geeksforgeeks.org/java-io-input-output-in-java-with-examples/)
> - [geeksforgeeks | Java.io.InputStream Class in Java](https://www.geeksforgeeks.org/java-io-inputstream-class-in-java/)
> - [geeksforgeeks | Java.io.OutputStream class in Java](https://www.geeksforgeeks.org/java-io-outputstream-class-java/)
> - [geeksforgeeks | Introduction to Java NIO with Examples](https://www.geeksforgeeks.org/introduction-to-java-nio-with-examples/)
> - [geeksforgeeks | Difference between Java IO and Java NIO](https://www.geeksforgeeks.org/difference-between-java-io-and-java-nio/)
> - [baeldung | How to Read a File in Java](https://www.baeldung.com/reading-file-in-java)
> - [baeldung | Java – Write to File](https://www.baeldung.com/java-write-to-file)
> 
> 도서
> - Java의 정석(2nd Edition) 중 14장 입출력(I/O)'
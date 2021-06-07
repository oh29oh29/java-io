# Java IO

## 스트림(stream)

데이터를 운반하는데 사용되는 연결통로이다.  

스트림은 연속적인 데이터의 흐름을 물에 비유해서 붙여진 이름인데 여러 가지로 유사한 점이 많다.  
물이 한쪽 방향으로만 흐르듯이 스트림도 단방향 통신만 가능하며 따라서 입력과 출력을 동시에 처리할 수 없다.
그래서 입력 스트림(input stream)과 출력 스트림(output stream)이 필요하다.  

스트림은 먼저 보낸 데이터를 먼저 받게 되어 있으며 중간에 건너뜀 없이 연속적으로 데이터를 주고 받는다.  
큐(queue)와 같은 FIFO(First In First Out)구조로 되어 있다고 생각하면 된다.

#### 보조스트림

스트림의 기능을 보완하기 위한 보조스트림이 존재한다.  
보조스트림은 실제 데이터를 주고받는 스트림이 아니기 때문에 데이터를 입출력할 수는 없지만, 스트림의 기능을 향상시키거나 새로운 기능을 추가할 수 있다.  

예를 들어, 텍스트 파일을 읽기 위해 FileInputStream 을 사용할 때, 입력 성능을 향상시키기 위해 버퍼를 사용하는 보조스트림인 BufferedInputStream 을 사용한다.  
버퍼를 사용한 입출력과 사용하지 않은 입출력간의 성능 차이는 상당하기 때문에 대부분의 경우에 버퍼를 이용한 보조스트림을 사용한다고 한다.  
-> 실제 테스트하여 시간 비교를 해보자

## InputStream 과 OutputStream

#### InputStream

모든 바이트기반 io 클래스의 상위 클래스이다.

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
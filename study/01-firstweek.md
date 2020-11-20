# 1주차 과제: JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가.#1

# 목표

자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.

## 학습할 것

[1.   JVM이란 무엇인가](#jvm)   
[2.   컴파일 하는 방법](#compile)   
[3.   실행하는 방법](#howtorun)  
[4.   바이트코드란 무엇인가](#bytecode)   
[5.   JIT 컴파일러란 무엇이며 어떻게 동작하는지](#jitcompiler)  
[6.   JVM 구성 요소](#componentsofjvm)  
[7.   JDK와 JRE의 차이](#jdkjre)   
---


### <div id="jvm"> 1.JVM이란 무엇인가 </div>

![jvm](/images/firstweek/jvm.jpeg "jvm과 컴파일")


>출처 : 이것이 자바다 - 신용권 지음

  - `JVM(Java Virtual Machine)`은  
    `운영체제를 대신해서 자바 프로그램을 실행하는 가상의 운영체제 역할`을 한다.   
     운영체제별로 프로그램을 실행하고 관리하는 방법이 다르기 때문에,   
     `운영체제와 자바 프로그램을 중계`하는 `JVM(Java Virtual Machine)`을 두어   
     자바 프로그램이 `여러 운영체제에서 동일한 실행결과`가 나오도록 설계한 것이다.   
     `자바 프로그램은 완전한 기계어가 아닌, 중간 단계의 바이트 코드`이기 때문에   
     이것을 실행할 수 있는 JVM(Java Virtual Machine)이 필요하다.  

>좀더 쉽게 예를 들자면 다른 모르는 언어들을 한국어로 바꿔주는 `통역사`의 역할이랄까?  

---

### <div id="compile"> 2.컴파일 하는 방법 </div>  

### <div id="howtorun"> 3.실행 방법 </div>

---
[위의 사진을 보며 이해 해 보자.](#jvm)  

helloword.java 라는 소스파일이 있다고 가정하고  컴파일을 한다고 가정해 보면  
helloword.java를  
자바컴파일러(javac.exe)를 통해   
helloword.class 의 바이트 코드 파일로 변경(컴파일)한다.   
그리고 변경된(컴파일된) 바이트코드파일 (helloword.class)을  
jvm(java.exe)으로 구동하여 각각의 운영 체제에 맞게 실행가능 해 진다.

`컴파일 및 실행 방법`을 실습을 해보자  (맥 기준 입니다.)  
저장경로는 편의상 바탕화면(desketop)  
hello word test 폴더에 소스파일을 저장 하였습니다.   
`텍스트 편집기`을 열어  아래 소스코드를 작성하고  `HelloWorld.java`  확장자까지 붙여 저장을 하자.    


<div id = "code"> HelloWorld.java 파일의 소스코드 </div>

>```java
>public class HelloWorld {
>public static void main(String[] args) {
>System.out.println("헬로 월드");
>    }
>}
>```
  
아래 사진은 [2.컴파일 하는 방법](#compile)와 [3.실행 방법](#howtorun) 의 과정을 담은 예제이다.  
사진의 1. 2. 3. 을 천천히 살펴보자.

<div id="Compilationprocess"> </div>  

![Compilationprocess](/images/firstweek/Compilationprocess.jpeg "컴파일과 실행 과정")

---
### <div id="bytecode"> 4.바이트코드란 무엇인가 </div>

- `바이트코드(Bytecode)는 고급 언어로 작성된 소스 코드를 가상머신이 이해할 수 있는 중간 코드로 컴파일한 것을 말한다.`  
- 바이트코드는 기계어는 아니지만 `가상 머신에 의해 기계어로 손쉽게 변환할 수 있는 코드`이다. 
 `가상머신은 이 바이트코드를 각각의 하드웨어 아키텍처에` 맞는 `기계어`로 `다시 컴파일`한다.  
 어셈블리어에 가까운 형태를 띄고 있으며 어떨 때는 가상머신용 오브젝트 코드까지 바이트코드라고 부르기도 한다.
       
  >출처 나무위키
  

[위의 사진](#jvm)과 
[예제](#Compilationprocess) 을 참고해 보자.  

[1. jvm](#jvm) 의 설명에 `자바 프로그램은 완전한 기계어가 아닌, 중간 단계의 바이트 코드` 라는 설명이 있다.    

 아래는 자바 바이트코드이다.  
 [위의 코드 HelloWord.java](#code)를 `자바 바이트코드로 컴파일한 결과(HelloWorld.class)`이다.  

``` java
public class HelloWorld {

  // compiled from: HelloWorld.java

  // access flags 0x1
  public <init>()V
   L0
    LINENUMBER 1 L0
    ALOAD 0
    INVOKESPECIAL java/lang/Object.<init> ()V
    RETURN
   L1
    LOCALVARIABLE this LHelloWorld; L0 L1 0
    MAXSTACK = 1
    MAXLOCALS = 1

  // access flags 0x9
  public static main([Ljava/lang/String;)V
   L0
    LINENUMBER 3 L0
    GETSTATIC java/lang/System.out : Ljava/io/PrintStream;
    LDC "\ud5ec\ub85c \uc6d4\ub4dc"
    INVOKEVIRTUAL java/io/PrintStream.println (Ljava/lang/String;)V
   L1
    LINENUMBER 4 L1
    RETURN
   L2
    LOCALVARIABLE args [Ljava/lang/String; L0 L2 0
    MAXSTACK = 2
    MAXLOCALS = 1
}

```
-----  
   
### <div id="jitcompiler"> 5.JIT 컴파일러란 무엇이며 어떻게 동작하는지 </div>
- JIT 컴파일(just-in-time compilation) 은 프로그램을 `실제 실행하는 시점에 기계어로 번역하는 컴파일 기법`이다.
- 전통적인 입장에서 컴퓨터 프로그램을 만드는 방법은 두 가지가 있는데, `인터프리트 방식과 정적 컴파일 방식`으로 나눌 수 있다. 이 중 `인터프리트 방식은 실행 중 프로그래밍 언어를 읽어가면서 해당 기능에 대응하는 기계어 코드를 실행`하며, 반면 `정적 컴파일은 실행하기 전에 프로그램 코드를 기계어`로 번역한다.
 
 - JIT 컴파일러는 `두 가지의 방식을 혼합한 방식`으로 생각할 수 있는데, `실행 시점에서 인터프리트 방식으로 기계어 코드를 생성`하면서 `그 코드를 캐싱`하여, 같은 함수가 여러 번 불릴 때 `매번 기계어 코드를 생성하는 것을 방지`한다.
 
 최근의 자바 가상 머신과 .NET, V8(node.js)에서는 JIT 컴파일을 지원한다.  
 즉, `자바 컴파일러가 자바 프로그램 코드를 바이트코드로 변환`한 다음,   
 `실제 바이트코드를 실행하는 시점에서 자바 가상 머신이 바이트코드를 JIT 컴파일을 통해 기계어로 변환`한다.


### <div id="componentsofjvm"> 6.JVM 구성 요소</div>

![jvmcomponents](/images/firstweek/jvmcomponents.jpg "jvm의 구성 요소")
>사진 출처 https://www.edureka.co/blog/java-architecture/#whatisjavaarchitecture

__JVM의 구조는 크게__    
- __클래스로더(Class Loader),__   
- __실행 엔진(Execution Engine),__    
- __데이터 영역(Runtime Data Area),__    
- __Garbage Collector__ 로 구분  
  1. 클래스 로더 :  
  자바에서 소스를 작성하면 Person.java 처럼 .java파일이 생성된다.  
  .java 소스를 자바컴파일러가 컴파일하면 Person.class 같은 .class파일(바이트코드)이 생성된다.  
  `이렇게 생성된 클래스파일들을 엮어서 JVM이 운영체제로부터 할당받은 메모리영역인 Runtime Data Area로 적재하는 역할을 Class Loader가 한다. `(자바 애플리케이션이 실행중일 때 이런 작업이 수행된다.)  
  Java 프로그램을 실행할 때마다 클래스 로더가 먼저로드.  
    
  2. 실행 엔진(Execution Engine) :  
    Class Loader에 의해 메모리에 적재된 `클래스(바이트 코드)들을 기계어로 변경해 명령어 단위로 실행`하는 역할을 한다.  
 명령어를 하나 하나 실행하는 인터프리터(Interpreter)방식이 있고  
 JIT(Just-In-Time) 컴파일러를 이용하는 방식이 있다.  
 JIT 컴파일러는 적절한 시간에 전체 바이트 코드를 네이티브 코드로 변경해서 Execution Engine이 네이티브로 컴파일된 코드를 실행하는 것으로 성능을 높이는 방식이다.
  
  3. Garbage collector :   
   Garbage Collector(GC)는 Heap 메모리 영역에 생성(적재)된 객체들 중에 참조되지 않는 객체들을 탐색 후 제거하는 역할을 한다.

  4. 데이터영역 (메모리영역, Runtime Data Area)  
  - JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역이다.  
 이 영역은 크게 `Method Area, Heap Area, Stack Area, PC Register, Native Method Stack`로 나눌 수 있다.
    
      
    
  ![runtimedataarea](/images/firstweek/runtimedataarea.png "데이터영역")  
    __1. Method area (메소드 영역)__  
    클래스 멤버 변수의 이름, 데이터 타입, 접근 제어자 정보같은 필드 정보와 메소드의 이름,   
    리턴 타입, 파라미터, 접근 제어자 정보같은 메소드 정보, Type정보(Interface인지 class인지),  
    Constant Pool(상수 풀 : 문자 상수, 타입, 필드, 객체 참조가 저장됨), static 변수, final class 변수등이 생성되는 영역이다.    
    __2. Heap area (힙 영역)__  
    new 키워드로 생성된 객체와 배열이 생성되는 영역이다.  
    메소드 영역에 로드된 클래스만 생성이 가능하고  
    Garbage Collector가 참조되지 않는 메모리를 확인하고 제거하는 영역이다.  
    __3. Stack area (스택 영역)__  
    지역 변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값등이 생성되는 영역이다.  
    int a = 10; 이라는 소스를 작성했다면  
    정수값이 할당될 수 있는 메모리공간을 a라고 잡아두고 그 메모리 영역에 값이 10이 들어간다.  
    즉, 스택에 메모리에 이름이 a라고 붙여주고 값이 10인 메모리 공간을 만든다.  
   클래스 Person p = new Person(); 이라는 소스를 작성했다면  
   Person p는 스택 영역에 생성되고 new로 생성된 Person 클래스의 인스턴스는  
   힙 영역에 생성된다.  
  그리고 스택영역에 생성된 p의 값으로 힙 영역의 주소값을 가지고 있다.  
  즉, 스택 영역에 생성된 p가 힙 영역에 생성된 객체를 가리키고(참조하고) 있는 것이다.  
   메소드를 호출할 때마다 개별적으로 스택이 생성된다.  
   __4. PC Register (PC 레지스터)__
   Thread(쓰레드)가 생성될 때마다 생성되는 영역으로 Program Counter  
   즉, 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역이다. (*CPU의 레지스터와 다름)  
   이것을 이용해서 쓰레드를 돌아가면서 수행할 수 있게 한다.  
    __5. Native method stack__  
    자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역이다.  
    보통 C/C++등의 코드를 수행하기 위한 스택이다. (JNI)  
    쓰레드가 생성되었을 때 기준으로  
     1,2번인 메소드 영역과 힙 영역을 모든 쓰레드가 공유하고,  
     3,4,5번인 스택 영역과 PC 레지스터, Native method stack은  
     각각의 쓰레드마다 생성되고 공유되지 않는다.
    >
   >jvm의 사진, 설명, 자세한 사항은 출처 https://jeong-pro.tistory.com/148  
   
    

### <div id="jdkjre"> 7.JDK와 JRE의 차이</div>
 - JDK : `Java Development Kit`의 약자 이며 `JRE를 포함 + @` 이다.
   - JDK 는 Java 애플리케이션 및 애플릿을 개발하는 데 사용되는 소프트웨어 개발 환경.  
   여기에는 JRE 및 여러 개발 도구, 인터프리터 / 로더 (java), 컴파일러 (javac), 아카이버 (jar), 문서 생성기 (javadoc)가 다른 도구와 함께 포함되어 있습니다.
   
 - JRE : `Java Runtime Environment`의 약자
   - JRE 소프트웨어는 Java 프로그램을 실행할 수있는 런타임 환경을 구축.  
   JRE는 Java 코드를 가져 와서 필요한 라이브러리와 결합한 후 JVM을 시작하여 실행하는 온 디스크 시스템입니다. JRE에는 Java 프로그램을 실행하는 데 필요한 라이브러리와 소프트웨어가 포함되어 있습니다. 
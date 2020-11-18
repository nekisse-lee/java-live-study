# 1주차 과제: JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가.#1

# 목표

자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.[^1]

## 학습할 것

[1.   JVM이란 무엇인가](#jvm)   
[2.   컴파일 하는 방법](#compile)   
[3.   실행하는 방법](#howtorun)  
[4.   바이트코드란 무엇인가](#bytecode)   
[5.   JIT 컴파일러란 무엇이며 어떻게 동작하는지]   
[6.   JVM 구성 요소]   

[7.   JDK와 JRE의 차이]   
---


### <div id="jvm"> 1.JVM이란 무엇인가 </div>

![jvm](/images/firstweek/jvm.jpeg "jvm과 컴파일")


>출처 : 이것이 자바다 - 신용권 지음

   `JVM(Java Virtual Machine)`은  
    `운영체제를 대신해서 자바 프로그램을 실행하는 가상의 운영체제 역할`을 한다.   
     운영체제별로 프로그램을 실행하고 관리하는 방법이 다르기 때문에,   
     운영체제와 자바 프로그램을 중계하는 JVM(Java Virtual Machine)을 두어   
     자바 프로그램이 `여러 운영체제에서 동일한 실행결과`가 나오도록 설계한 것이다.   
     `자바 프로그램은 완전한 기계어가 아닌, 중간 단계의 바이트 코드`이기 때문에   
     이것을 실행할 수 있는 JVM(Java Virtual Machine)이 필요하다.  

>좀더 쉽게 예를 들자면 다른 모르는 언어들을 한국어로 바꿔주는 `통역사`의 역할이랄까?

### <div id="compile"> 2.컴파일 하는 방법 </div>
### <div id="howtorun"> 3.실행 방법 </div>

[위의 사진을 보며 이해 해 보자.](#jvm)  

helloword.java 라는 소스파일이 있다고 가정하고  컴파일을 한다고 가정해 보면  
helloword.java를  
컴파일러(javac.exe)를 통해   
helloword.class 의 바이트 코드 파일로 변경(컴파일)한다.   
그리고 변경된(컴파일된) 바이트코드파일 (helloword.class)을  
jvm(java.exe)으로 구동하여 각각의 운영 체제에 맞게 실행가능 해 진다.

`컴파일 및 실행 방법`을 실습을 해보자  (맥 기준 입니다.)  
저장경로는 편의상 바탕화면(desketop)  
hello word test 폴더에 소스파일을 저장 하였습니다.   
`텍스트 편집기`을 열어  아래 소스코드를 작성하고  `HelloWorld.java`  확장자까지 붙여 저장을 하자.    


>HelloWorld.java 파일의 소스코드
>
>```java
>public class HelloWorld {
>public static void main(String[] args) {
>System.out.println("헬로 월드");
>    }
>}
>```
  




![Compilationprocess](/images/firstweek/Compilationprocess.jpeg "컴파일과 실행 과정")






### <div id="bytecode"> 4.바이트코드란 무엇인가 </div>

[위의 사진](#jvm)  
[예제](#Compilationprocess) 을 참고해 보자.  
 
[^1] 각주테스트

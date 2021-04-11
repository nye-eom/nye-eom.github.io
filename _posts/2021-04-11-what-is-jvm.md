---
layout: post
title: "JVM 이란?"
author: nyeom
tags: [Java]
---

JVM(Java Virtual Machine)이란, 자바 가상머신의 약자를 줄여 부르는 용어로 스택기반의 가상머신이다. ClassLoader, Execution Engine, Runtime Data 영역으로 구성되어있다.

### ClassLoader
![image](https://www.cubrid.org/layouts/layout_master/img/b94d4a812724c780250e0aa47711e40e.png)\
 JVM으로 클래스를 로드하고 링크를 통해 배치하는 작업을 수행하는 모듈이다. Runtime시에 동적으로 클래스를 로드한다. jar파일 내 저장된 클래스들을 JVM위에 탑재하고 사용하지 않는 클래스들을 메모리에서 삭제한다.

### Execution Engine

 클래스로더가 JVM 내의 런타임 데이터 영역에 바이트 코드를 배치시키면 실행엔진에 의해 코드가 실행된다. 바이트코드를 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경한다. 실행방식에는 두가지방식(인터프리터, JIT)이 있다.
 
 - Interpreter?

 바이트 코드를 명령어 단위로 읽어서 실행한다. 한줄씩 실행하기에 느리다는 단점을 가진다.

 - JIT(Just In Time)

인터프리터 방식의 단점을 보완하기 위해 도입된 JIT 컴파일러이다. 인터프리터 방식으로 실행하다가 적절한 시점에 바이트코드 전체를 컴파일하여 네이티브코드로 변경 후 더이상 인터프리터 하지 않고 네이티브 코드로 직접 실행하는 방식이다. 네이티브코드는 캐시에 보관되어 한번 컴파일된 코드는 빠르게 수행하게 된다. 처음 컴파일을 하는 시점에서는 인터프리터 방식보다 오래 걸리지만 캐시에 보관된 이후에는 성능이 낫다. JIT 컴파일러를 사용하는 JVM들은 내부적으로 해당 메서드가 얼마나 수행되는지 체크하고 일정정도가 넘을때에만 컴파일을 수행한다. 

### Runtime Data Area
![image](https://www.programcreek.com/wp-content/uploads/2013/04/JVM-runtime-data-area.jpg)\
프로그램이 실행되면서 JVM은 OS로 부터 프로그램이 필요로 하는 메모리를 할당받은 영역이다. JavaCompiler(.javac)가 자바소스(.java)를 읽어드려 바이트코드(.class)로 변환시키면 ClassLoader를 통해 .class 파일을 JVM으로 로딩한다. 로딩된 .class파일들이 Execution Engine을 통해 해석되고 해석된 바이트코드는 Runtime Data Area에 배치되어 실질적인 수행이 이루어지게 된다.

메모리 효율성을 위해 메모리 구조를 알아야하는데 한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위해서 어떻게 메모리를 관리할지에 따라 프로그램의 성능이 좌우되며 JVM은 할당받은 메모리를 용도에 따라 여러 영역(Thread, Heap, Method Area)으로 나누어서 관리한다.

- Thread

쓰레드가 어떤 부분을 어떤 명령으로 실행해야하는지에 대한 기록을 하며 현재 수행중인 JVM 명령의 주소를 갖는다.

JVM 스택 영역은 프로그램 실행과정에서 임시 할당 되었다가 메소드를 빠져나가면 바로 소멸되는 데이터를 저장하기 위한 영역이다. 각종 형태의 변수, 임시데이터, 스레드, 메소드 정보를 저장한다.

메소드 호출시마다 각각의 스택프레임이 생성된다. 메서드 수행이 끝나면 프레임 별로 삭제한다.

메소드 안에서 사용되는 로컬변수를 저장하며 호출된 메서드의 매개변수, 지역변수 및 연산시 일어나는 값들을 임시로 저장한다. Last In Firtst Out(LIFO)

네이티브 메소드 스택은 실제 실행할수 있는 기계어로 작성된 프로그램을 실행하는 영역이다.

자바 네이티브 인터페이스를 통해 바이트 코드로 전환하여 저장하게 된다. 커널이 스택을 잡아 독자적으로 프로그램을 실행시키는 영역이다.

- Heap
![image](https://www.journaldev.com/wp-content/uploads/2014/05/Java-Memory-Model.png)\
객체를 저장하는 가상메모리 공간으로 NEW 연산자로 생성된 객체와 배열을 저장한다. Heap 영역이 가비지콜렉션의 대상이 된다. 

Permanent Generation, NEW/YOUNG 영역, Old 영역으로 구성된다.

Permanent Generation 는 생성된 객체들의 정보의 주소값이 저장된 공간이다.

클래스로더에 의해 로드되는 클래스, 메소드 등에 대한 메타정보가 저장되는 영역이다.

Reflection을 사용해 동적으로 클래스가 로딩되는 경우에 사용된다.

NEW/YOUNG 영역은 Eden과 Survivor 0/1로 구성된다.

Eden은 새롭게 생성된 객체가 할당되는 영역으로 대부분의 객체는 unreachable 상태가 되기 때문에 많은 객체가 Young 영역에서 생성되었다가 사라진다. 

Eden 영역에서 GC가 한번 발생한 후 살아남아 있는 객체는 Survivor 0/1 영역 중 하나로 이동된다.

이 과정을 반복하다 계속해서 살아남아 있는 객체는 일정시간 참조되고 있다는 뜻으로 Old 영역으로 이동시킨다. 해당 영역에 대한 GC를 Minor GC라 부른다. Minor GC는 Eden 영역이 꽉찼을 때 발생하게 된다. 

Survivor 0/1은 Eden에서 참조되는 객체들이 저장되는 공간이다. 최소 1번의 GC 이상 살아남은 객체가 존재하는 영역이다. Eden에서 하나의 Survivor 영역으로 살아남은 객체가 이동되고 한 영역이 가득차게 되면 다른 survivor영역으로 이동시킨다. 단, 1개의 survivor영역은 반드시 빈 상태가 된다. 

Old 영역은 Eden 영역에 NEW 영역 내 Eden 영역에 객체가 가득차게 되면 GC를 발생시켜 Eden 영역에 있는 값들을 Survivor 1영역에 복사하고 이 영역을 제외한 나머지 영역의 객체를 삭제한다.

인스턴스는 소멸방법과 소명시점이 지역변수와 다르기에 힙이라는 별도의 영역에 할당된다. 

Young 영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역이다. 복사되는 과정에서 Young영역보다 크게 할당되며 해당영역에 대한 GC를 Major GC라 부른다. 

Major GC는 Old 영역에 있는 모든 객체들을 검사하여 참조되지 않은 객체들을 한꺼번에 삭제한다.

시간이 오래걸리고 실행중 프로세스가 정지되는데 이를 ‘Stop the world’라고 한다. Major GC가 발생하면 GC를 실행하는 스레드를 제외한 나머지 스레드는 작업이 중단되고 GC가 완료되면 작업을 재개한다.

- Method Area(=Class Area, Static Area)

클래스 정보를 처음 메모리 공간에 올릴때 초기화되는 대상을 저장하기 위한 공간.

Runtime Constance Pool이라는 별도의 관리 영역도 함께 존재한다. 

상수 자료형을 저장하여 참조하고 중복을 막는 역할을 수행한다.

클래스 데이터를 위한 공간으로 Field Information, Method Information, Type Information을 관리한다.

Field Information : 멤버변수의 이름,데이터타입,접근제어자정보

Method Information : 메소드이름, 리턴타입, 매개변수, 접근제어자정보

Type Information : 클래스인지 interface인지 여부 저장, type 속성, 이름, super class 이름


### JVM 옵션
```yml
---
#Server 포트 설정
-Dserver.port=9001

#초기 Heap 크기(init, default 64m)
-Xms256m

#최대 Heap 크기(Max, default 256m)
-Xmx2048m

#JIT 컴파일러를 위한 옵션으로 컴파일코드 캐시 최대 사이즈 지정
-XX:ReservedCodeCacheSize=240m

#최소 new size(객체가 생성되어 저장되는 초기공간 사이즈로 Eden+Survivor 영역)
-XX:NewSize

#최대 new size(객체가 생성되어 저장되는 초기공간 사이즈로 Eden+Survivor 영역)
-XX:MaxNewSize

#New/Survivor 영역 비율(n으로 지정시 Eden : Survivor = 1:n)
-XX:SurvivorRatio

```Young 영역과 Old 영역의 비율(n으로 지정시 Young:Old=1:n)
-XX:NewRatio

```인코딩 설정
-Dfile.encoding=UTF-8
---
```
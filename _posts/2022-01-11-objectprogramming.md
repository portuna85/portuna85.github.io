---
layout: single
title: "객체지향 프로그래밍 1"
---

## 클래스 : 객체를 정의 해 놓은것 객체를 생성하는대 사용
## 객체 : 실제로 존재하는 것 사물 또는 개념 용도는 속성과 기능에 따라 다름
### 클래스는 tv설계도 객체는 tv
### 클래스 - 데이터와 함수의 결합.
    구조체 : 타입에 관련없이 서로 관련된 데이터들을 저장할 수 있는 공간
    클래스 : 구조체 + 함수 
## 객체와 인스턴스
### 객체는 인스턴스를 포함하는 일반적인 의미
## 객체의 구성 요소 - 속성과 기능
### - 속성은 변수 기능은 메서드
```java
public class Car {
    // 속성
    public String model;    // 차량 모델
    public String color;    // 차량 색상 
    public int maxSpeed;    // 최고속도
  
    // 기능
    public void turnON() {      // 시동 ON
        System.out.println("시동을 켭니다.");
    }
    
    public void ride() {        // 주행
        System.out.println("차량이 달립니다.");
    }
    
    public void turnOff() {     // 시동 OFF
        System.out.println("시동을 끕니다.");
    }
}
```
## 변수와 메소드
### 변수
  - 변수의 선언위치가 변수의 종류와 범위(scope)를 결정한다.
## 선언 위치에 따른 변수의 종류
### 인스턴스 변수(instance variable)  (클래스 영역)
  - 인스턴스 생성 후 "**참조변수.인스턴스변수명**"으로 접근
  - 인스턴스 생성할 때 생성, 참조 변수 없을시 gc가 자동 제거함

## 클래스 변수(class variable, static variable) (클래스영역)
  - 인스턴스 생성없이, "**클래스이름.클래스변수명**" 으로 접근 

## 지역 변수(local variable)              (메소드 영역)
  - 메소드 내에 선언, 메소드 종료시 함께 소멸
```java
public class Variables {        // 클래스영역 시작
    int iv;                     // 인스턴스변수
    static int cv;              // 클래스변수(static 변수, 공유변수)

    void method() {             // 메소드영역 시작
        int lv = 0;             // 지역변수(로컬변수)
    }                           // 메소드영역 끝
}
```
## 메소드
  - 작업을 실행하기 위한 명령문
  - 반복되는 코드 축소 관리 용이
  - 한개의 메소드는 한기능만 수행하도록 작성
  - 메서드는 클래스 영역 안에서만 정의 가능
## return문
  메소드 정상종료되는 경우
  - 블럭{}이 끝까지 수행 했을때.
  - 블럭{}안 수행 도중 return문을 만났을 때.
  - 반환 값이 없는 경우 return;만 작성하거나 생략가능
  - 있는경우 return 반환 값; 타입 일치해야만 함.
```java
public class plus {
  public int add(int x, int y) {        // return Type는 int타입
    int result = x + y;
    return result;                      // int타입으로 반환.
  }
}
```
# 메소드

## 인스턴스 메소드(instance method)
  - 반드시 객체 생성해야만 호출 가능
  - 참조변수.메소드 이름();
  - 메소드 내 인스턴스변수 사용가능

## 클래스 메소드(class method, static method)일 경우
  - 클래스명.메소드 이름(); 객체생성 없어도 됨
  - 인스턴스변수나 인스턴스메서드 관련없는 작업 수행
  - 메서드 내 인스턴스 변수 사용 안한다면 static 붙이는게 관례

```java
public class MyMath {
  public long a, b;

  public long add() {     // 인스턴스 메소드
    return a + b;
  }

  public static long add(long a, long b) {     // 클래스매소드(static 메소드)
    return a + b;
  }

  public static void main(String[] args) {
    MyMath.add(3L, 5L);                         // 클래스 메소드 호출

    MyMath myMath = new MyMath();               // 객체 생성(인스턴스 생성) 후 참조 변수 대입
    myMath.a = 3L;
    myMath.b = 5L;
    myMath.add();                             // 인스턴스메소드 호출
  }
}
```
```java
public class CallClass {
  public void instanceMethod() {                // 인스턴스 메소드
  }

  public static void staticMethod() {           // 클래스 메소드(static 메소드)
  }

  public void instanceMethod2() {                    // 인스턴스메소드에서
    instanceMethod();                           // 다른 인스턴스메소드 호출한다
    staticMethod();                             // 클래스 메소드(static 메소드) 호출한다.
  }
  
  public static void staticMethod2() {
      instanceMethod();                         // 에러남. 인스턴스메서드 호출 불가
      staticMethod();                           // static 메소드 호출 가능
  }
}
```

# JVM 메모리 구조
## 메소드 영역(Method Area)
  - JVM 실행시 생성 
  - 모든 스레드 공유
  - 클래스, 메소드, 인터페이스
  - 클래스변수(class variable, static variable)
## 스택 영역(Stack Area) Call Stack 라고도 부름
  - 메소드 호출시 수행에 필요한 메모리 할당.
  - 메소드의 파라메타, 지역변수(local variable), 반환값(return 값;) 임시 저장
  - 수행 종료하면 메모리 반환.
  - 메소드 실행 순으로 쌓이고 제일 위 메소드 순으로 프레임 제거.
## 힙 영역(Heap Area)
  - new 생성자로 생성된 객체, 배열이 생성되는 곳
  - JVM이 Garbage Collecor를 실행시켜 쓰레기 객체 자동으로 제거.

## 기본형 매개변수, 참조형 매개변수
### 기본형 매개변수
  - 변수의 값을 읽기만 할 수 있다.(Read Only)
### 참조형 매개변수
  - 변수의 값을 읽고 변경할 수 있다.(Read & Write)

```java
class PrimitiveParam {
  public static void main(String[] args) {
    Data d = new Data();
    d.x = 20;
    changePrimitive(d.x);
    System.out.println("기본형 매개변수데이터를 바꿀경우");
    System.out.println("(main) x =  " + d.x);
    System.out.println("x값을 바꾼후 x : " + d.x);
    System.out.println();
    System.out.println("참조형 매개변수데이터를 바꿀경우");
    changeReference(d);
    System.out.println("(main) x =  " + d.x);
    System.out.println("x값을 바꾼후 x : " + d.x);
  }

  static void changePrimitive(int x) {           // 기본형 매개변수
    x = 100;
    System.out.println("기본형매개변수 메소드 출력 : " + x);
  }

  static void changeReference(Data d) {          // 참조형 매개변수
    d.x = 100;
    System.out.println("참조형매개변수 메소드 출력 :" + d.x);
  }
}
class Data {
  public int x;

  public Data() {
  }
}
```
## 재귀호출
  - 매서드 내에서 자기자신을 반복적으로 호출하는 것
  - 이해하기 쉽고 간결한 코드를 작성할수 있다.
  - 팩토리얼, 제곱, 폴더목록표치 등
```java
/*
  5! = 5 X 4 X 3 X 2 X 1
 */
public class Factorial {
  public static void main(String[] args) {
    int result = factorial(5);
    System.out.println(result);
  }

  static int factorial(int a) {             // 펙토리얼 메소드
    int result = 0;
    if (a == 1) {
      result = 1;
    } else {
      result = a * factorial(a - 1);
    }
    return result;
  }
}
```
## 오버로딩(Overloding)
  - 하나의 클래스에 동일이름의 메소드를 여러개 정의 하는 것.
### 오버로딩 조건
  - 메소드 이름 같아야 한다.
  - 매개변수의 갯수 또는 타입이 달라야한다.
  - 매개변수 개수, 타입이 동일한경우 already defined에러발생
  ```java
class MethodOverloding {
  public int add() {
    return 0;
  }

  public int add(int x, int y) {
    int resutl = x + y;
    return resutl;
  }

  public int add(double x, int y) {
    int resutl = x + y;
    return resutl;
  }

  public int add(int x, double y) {
    int resutl = x + y;
    return resutl;
  }

  public int add(int x, int y, int z) {
    int resutl = x + y + z;
    return resutl;
  }

  public float average(int x, int y) {
    float result = ((x + y) / 2.0f);
    return result;
  }

  public float average(int x, int y, int z) {
    float result = ((x + y + z) / 3.0f);
    return result;
  }
}
```
## 생성자(constructor)
  - 메소드와 비슷해 보이지만 아님
  - 인스턴스가 생성될 때마다 호룿로든 '인스턴스 초기화 매소드'
  - 인스턴스 변수 초기화 인스턴스 생성시 수행 할 작업에 사용
  - 모든 클래스엔 반드시 하나이상의 생성자 있어야함.(생성자 없는경우 컴파일시 기본생성자 자동 생성)
  - 생성자 이름은 클래스 이름과 동일해야함
  - 생성자는 리턴값 자체가 없음 (void 안들어감.)
 

### 생성자에서 다른생성자 호출 (this()를 사용)
  - 생성자, 같은 클래스의 다른 생성자를 호출할때 사용
  - 다른 생성자 호출은 생성자의 첫 문장에서 사용가능
### 참조변수 this
  - 인스턴스 자신을 가리키는 참조변수. 인스턴스의 주소가 저장
  - 모든 인스턴스 매소드 지역변수로 숨겨진 채로 존재
### 생성자를 이용한 인스턴스의 복사
```java
public class Car {
  public String color;
  public String name;
  public String gearType;
  public int door;

  public Car() {
    this("RED", "SONATA", "auto", 4);
  }
  // 인스턴스 변수와 지역변수를 구별하기위해 참조변수 this를 사용.
  public Car(String color, String name, String gearType, int door) {
    this.color = color;
    this.name = name;
    this.gearType = gearType;
    this.door = door;
  }

  public Car(Car c) {        // 인스턴스 복사를 위한 생성자.
    color  = c.color;
    name = c.name;
    gearType = c.gearType;
    door = c.door;
  }

  public static void main(String[] args) {
    Car car1 = new Car();
    Car car2 = new Car(car1);      // Car(Car car1)를 호출
  }
}
```






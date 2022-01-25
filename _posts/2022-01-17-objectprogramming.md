---
layout: single
title: "객체지향 프로그래밍 2"
---
## 상속
### 상속관계
  - 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것.
  - 두 클래스를 부모클래스와 자식클래스로 관계 지어주는 것.
  - 자식클래스는 부모클래스의 모든 멤버를 상속받는다.(생성자, 초기화 블럭 제외)
  - 자식클래스의 멤버수는 부모클래스보다 같거나 많다.
  - 공통부분은 부모클래스에서 관리하고 개별부분은 자식클래스에서 관리한다.
  - 부모클래스의 변경은 자식클래스에 영향을 미치지만, 자식클래스의 변경은 부모클래스에 영향이 없다.

### 포함관계
  - 한 클래스의 멤버변수로 다른 클래스를 선언 하는 관계
  - 작은 단위의 클래스를 먼저 만들고, 이 클래스들을 조합해 커다란 클래스를 만든다.

### 클래스간 관계 결정 (상속 또는 포함)
  - 가능한 많은 관계를 맺어주어 재사용성을 높이고 관리하기 쉽게 한다.
  - 상속관계 : 원(Circle)은 도형(Shape)이다.
  - 포함관계 : 원(Circle)은 점(Point)를 가지고 있다.

```java
public class Shape {}
class Circle extends Shape {}               // 상속관계

class Point {                               // 포함관계
    public int x;
    public int y;
}

class Circle {
    Point p = new Point();
    public int z;
}
```

### 단일상속(single inheritance)
  - 자바는 단일상속만 허용
  - 비중이 높은 클래스 하나만 상속관계로, 나머지는 포함관계로 한다.


```java
public class Tv {
  public boolean power;
  public int channel;

  public boolean powerOn() {
    System.out.println("TV 전원On");
    return true;
  }

  public boolean powerOff() {
    System.out.println("TV 전원Off");
    return false;
  }

  public void channelUp() {
    ++channel;
  }

  public  void channelDown() {
    --channel;
  }
}

class DVD {
  public boolean power;
  public int counter = 0;

  public boolean powerOn() {
    System.out.println("DVD 전원On");
    return true;
  }

  public boolean powerOff() {
    System.out.println("DVD 전원Off");
    return false;
  }

  public void playDVD() {
    counter++;
  }

  public void stopDVD() {
    counter--;
  }

  public int endDVD() {
    return 0;
  }
}

class SmartTv extends Tv {
  DVD dvd = new DVD();

  public boolean powerOn() {
    return dvd.powerOn();
  }

  public void play() {
    dvd.playDVD();
  }

  public boolean powerOff() {
    return dvd.powerOff();
  }
}
```

### Object클래스 - 모든 클래스의 최상위부모 클래스
  - 상속 없는 클래스는 자동적으로 Object클래스를 받는다.
  - 상속 계층도의 최상위에는 Object클래스가 위치한다.

### 오버라이딩(Overriding)
  - 부모클래스에서 상속받은 메서드의 내용을 자식클래스에 맞게 변경하는 것
  - 조건
  1. 선언부가 같아야함(이름, 매개변수, 리턴타입)
  2. 부모클래스의 메소드접근제어자가 좁은 범위로 변경 불가
  3. 부모클래스의 메소드보다 많은 예외를 선언 불가
  - 오버로딩(Overloding) - 기존에 없는 메소드를 정의 하는것.
  - 오버라이딩(Overriding) - 상속 받은 메소드의 내용을 변경 하는 것
  
```java
public class Tv {
  public void channelUp() {}
}

class SmartTv extends Tv{
  @Override
  public void channelUp() {}          // 오버라이딩
  public void channelUp(int i) {}     // 오버로딩

  public void channelDown() {}        // 새로운 메소드
  public void channelDown(int i) {}   // 오버로딩
  public void channelDown() {}        // 메소드 중복정의
}
```

### this, super 참조변수
  - this : 인스턴스 자신을 가리키는 참조변수. 인스턴스 주소저장
  - super : this와 동일. 다만 부모의 멤버와 자신의 멤버를 구별하는 데 사용

### super() 생성자
  - 자식클래스의 인스턴스를 생성하면, 자식의 멤버와 부모으 멤버가 합쳐진 하나의 인스턴스 생성
  - 부모의 멤버들도 초기화 하여야 됨으로 자식 생성자 첫 문장에 부모 생성자 호출
  - Object클래스를 제외한 클래스는 첫 줄에 부모 생성자 호출을 해야한다.


```java
public class TvExam {
  public static void main(String[] args) {
    SmartTv tv = new SmartTv();

    tv.print();
  }
}

class Tv {
  public int channel = 1;
}

class SmartTv extends Tv {
  public int channel = 20;

  public void print() {
    System.out.println("channel = " + channel);                 // channel = 20
    System.out.println("this.channel = " + this.channel);       // this.channel =20
    System.out.println("super.channel = " + super.channel);     // super.channel = 1
  }
}
```

```java
public class TvExam {
    public static void main(String[] args) {
        SmartTv tv = new SmartTv();

        tv.print();
    }
}

class Tv {
    public int channel = 1;
}

class SmartTv extends Tv {
    public void print() {
        System.out.println("channel = " + channel);                 // channel = 1
        System.out.println("this.channel = " + this.channel);       // this.channel = 1
        System.out.println("super.channel = " + super.channel);     // super.channel = 1
    }
}
```

## 제어자(modifier)
  - 제어자는 크게 접근제어자, 그 외 제어자로 나뉨
  - 접근제어자는 하나만, 그 외 제어자는 조합해서 사용 가능

### static
  - 사용 가능한 곳 : 멤버면수, 메서드, 초기화블럭

#### static 멤버변수
  - 클래스변수는 인스턴스를 생성하지 않고도 사용 가능.
  - 클래스가 메모리에 로드될때(JVM실행시) 생성

#### static 메소드
  - 인스턴스 생성하지 않고도 호츨 가능
  - static메서드 내에서는 인스턴스멤버를 직접 사용 불가.

### final
  - 사용 가능한 곳 : 클래스, 메소드, 멤버변수, 지역변수

#### final 클래스
  - 변경 불가 클래스, 확장불가 클래스
  - 다른 클래스의 조상 불가

#### final 메소드
  - 변경 불가 메소드
  - 오버라이딩 통해 재정의 불가

#### final 멤버변수, final 지역변수
  - 값을 변경할 수 없는 상수

### abstract
  - 사용 가능 한 곳 : 클래스, 메소드

#### abstract 클래스
  - 클래서내에서 추상메서드가 선언되었음을 의미

#### abstract 메소드
  - 선언부만 작성하고 구현부는 작성하지 않은 추상메서드임을 알림.

### 접근제어자(access modifier)
  - 사용 가능한 곳 : 클래스, 멤버변수, 메소드, 생성자
  - private : 같은 클래스 내에서만 접근 가능
  - default : 같은 패키지 내에서만 접근 가능
  - protected : 같은 패키지, 다른 패키지의 자식 클래스에서 접근 가능.
  - public : 접근제한 없음.

#### 접근제어자를 사용하는 이유 - 캡슐화
  - 외부로부터 데이터를 보호하기 위해
  - 내부적으로만 사용되는 부분을 감추기 위해

## 다형성(polymorphism)
  - 하나의 참조변수로 여러 타입 객체를 참조 할수 있다.
  - 부모 타입의 참조변수로 자식타입의 객체를 다룰 수 있다. 단 자식타입인스턴스에만 있는 인스턴스멤버 사용불가
  - 부모타입으로 자식타입 인스턴스를 참조 가능
  - 하지만 자식타입으로 부모타입 인스턴스 참조 불가.(인스턴스 맴버 갯수 차이 때문.)

### 참조변수 형변환
  - 상속관계에 있는 타입간 형변환 가능
  - 자식 타입에서 부모타입 형변환할때 형변환 생략 가능

```java
public class Tv {
    public boolean power;
    public int channel;
    
    public boolean powerOn() {
        return true;
    }
    public void channelUp() {
        ++channel;
    }
    public void channelDown() {
        --channel;
    }
}
class CaptionTv extends Tv {
    public String text;
    public void caption() {}
}
public class TvExam {
  public static void main(String[] args) {
    Tv t1 = new Tv();
    Caption c1 = new Caption();
    Tv t2 = new Caption();
    Caption c2 = new Tv();               // 불가능
    
    Tv tv3 = null;
    Caption c3 = new Caption();
    Caption c4 = null;
    tv3 = c3;                           // tv3 = (Car) c3; 부모 <- 자식 
    c4 = (Caption) tv3;                 // 자식 <- 부모
  }
}
```

## instanceof 연산자
  - 참조변수가 참조하는 인스턴스의 실제 타입 체크할때 사용
  - 이항연산자며 왼쪽에는 참조변수, 오른쪽에는 타입. ex. if( car instanceof Car )
  - 연산결과가 true면, 해당 타입으로 형변환 가능


## 추상클래스(abstract class)
  - 클래스가 설계도라면 추상클래스는 '미완성 설계도'
  - 추상메소드(미완성 메소드)를 포함한 클래스
  - 완성된 설계도가 아니므로 인스턴스 생성 불가
  - 다른 클래스 작성하는데 도움을 줄 목적으로 작성
  - 다른 클래스에서 추상 클래스를 extends 해서 사용하거나,  추상클래스 자체를 익명 클래스로 생성해서 사용 가능

### 추상메소드(abstract method)
  - 선언부만 있고 구현부가 없는 메소드
  - 추상클래스를 상속받는 자식클래스에서 추상 메소드를 완성해야한다.


```java
public class MoveEx {
  public static void main(String[] args) {
    Unit[] group = {new Marine(), new Tank(), new Marine()};
    
    for (int i = 0; i < group.length; i++) {
      group[i].go();
      group[i].stop();
    }
  }
}

// 추상클래스 작성
abstract class Unit {                           // 추상 클래스
  public int x, y;

  abstract void move(int x, int y);             // 추상 메소드

  public void go() {}                           // 메소드

  public void stop() {                          // 메소드
    System.out.println("멈춰!");
  }
}

class Marine extends Unit {                     // 추상 클래스 상속 받아 추상메소드 작성
  public void move(int x, int y) {
    System.out.println("Marin [x : " + x + ", y : " + y + "]");
  }

  public void go(int x, int y){
    System.out.println("Marin [x : " + x + ", y : " + y + ']');
  }

  public void stimPack() {
    System.out.println("스팀팩 사용");
  }
}

class Tank extends Unit {                       // 추상 클래스 상속 받아 추상메소드 작성
  public void move(int x, int y) {
    System.out.println("Tank [x : " + x + ", y : " + y + "]");
  }

  public void go(int x, int y){
    System.out.println("Tank [x : " + x + ", y : " + y + ']');
  }

  public void changeMode() {
    System.out.println("모드 변경");
  }
}

class DropShip extends Unit {                   // 추상 클래스 상속 받아 추상메소드 작성
  public void move(int x, int y) {
    System.out.println("DropShip [x : " + x + ", y : " + y + "]");
  }

  public void go(int x, int y){
    System.out.println("DropShip [x : " + x + ", y : " + y + ']');
  }

  public void load() {
    System.out.println("유닛 태움");
  }

  public void unLoad() {
    System.out.println("유닛 내림");
  }
}
```

## 인터페이스(interface)
  - 실제 구현된 것이 전혀 없는 기본 설계도.(알맹이 없는 껍데기)
  - 추상 메소드 모음
  - 추상메소드와 상수만 멤버로 가짐
  - 인스턴스 생성할수 없고, 클래서 작성에 도움을 줄 목적으로 사용
  - 미리 정해진 규칙에 맞게 작성하도록 하는데 사용됨
  - 인터페이스도 클래스처럼 상속 가능 (클래스와 반대로 다중상속 가능)
  - 클래스의 Object클래스와 같은 최고 조상이 없다.
  - 서로 관계없는 클래스들에게 관계를 맺을수 있다.

## 인터페이스 작성
  - 인터페이스를 구현하는 것은 클래스가 상속받는것과 비슷
  - extends대신 implements를 사용

```java
public class Repair {
    public static void main(String[] args) {
        Tank tank = new Tank();
        Marine marine = new Marine();
        SCV scv = new SCV();
        
        scv.repair(tank);
    }
}

interface Repairable {}
interface Movable {
  public void move(int x, int y);                                   // 인터페이스에 정의된 메소드
}
interface Attackable {
  public int attack(Unit u);                                        // 인터페이스에 정의된 메소드
}
interface Fightable extends Movable, Attackable, Repairable {}      // 다중 상속 허용.

class Unit {
    int hitPoint;
    final int MAX_HP;

    Unit(int hp) {
        this.MAX_HP = hp;
    }
}

class GroundUnit extends Unit {
    GroundUnit(int hp) {
        super(hp);
    }
}

class AirUnit extends Unit {
    AirUnit(int hp) {
        super(hp);
    }
}

class Tank extends GroundUnit implements Repairable {           // Tank클래스에 GroundUnit 상속 Repairable 구현
    Tank() {
        super(250);
        super.hitPoint = super.MAX_HP;
    }
    
    @Override
    public String toString() {
        return "Tank{}";
    }
}

class Marine extends GroundUnit {
    Marine() {
        super(40);
        super.hitPoint = super.MAX_HP;
    }
}

class SCV extends GroundUnit implements Repairable {                // SCV클래스에 GroundUnit 상속 Repairable 구현
    SCV() {
        super(60);
        super.hitPoint = super.MAX_HP;
    }

    void repair(Repairable r) {}
}
```

## 내부클래스(inner class)
  - 클래스 안에 선언된 클래스
  - 특정 클래스 안에서만 주로 사용되는 클래스를 내부클래스로 선언
  - 내부 클래스에서 외부 클래스의 멤버를 쉽게 접근 가능
  - 코드의 복잡성을 줄일수 있다

### 종류와 특징
  - 내부 클래스의 종류는 변수 선언위치와 특징이 동일 함.
  - 인스턴스클래스 : 인스턴스변수처럼 맴버변수 선언위치에 선언, 인스턴스맴버처럼 사용.
  - 스태틱클래스 : 스태틱변수처럼 맴버변수 선언위치에 선언, 스태틱멤버처럼 사용.
  - 지역클래스 : 메서드나 초기화 블럭안에 선언, 선언된 영역 내부에서만 사용.
  - 익명클래스 : 이름 없는 일회용 클래스, 생성과 선언을 동시에 하나의 객체만 생성가능

```java
public class Main {
  public static void main(String[] args) {
    CarFactory car = new CarFactory() {
      @Override
      public void make() {

      }

      @Override
      public int destory() {
        System.out.println("Main.destory");
        return 0;
      }
    };

    System.out.println(car);
    CarFactory car2 = new CarFactory() {
      @Override
      public void make() {
        System.out.println("Main11.Make");
      }

      @Override
      public int destory() {
        return 0;
      }
    };

    car2.make();
    car.destory();
  }
}
```

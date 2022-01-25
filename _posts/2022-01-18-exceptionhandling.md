---
layout: single
title: "예외 처리(Exception Handling)"
---

## 예외처리(exception handling)
### 프로그램 오류
  - 컴파일 에러(compile-time error) : 컴파일할 때 발생하는 에로
  - 런타임 에러(runtime error) : 실행할 때 발생하는 에러
  - 논리적 에러 - 의도와 다르게 동작(실행시)
자바의 런타임 에러와 예외
  - 에러(error) : 프로그램 코드에 의해 수습 못하는 심각한 오류
  - 예외(exception) : 프로그램 코드에 의해 수습될 수 있는 약한 오류
### 정의와 목적
  - 에러는 처리 못하지만, 예외(exception)는 처리해야 한다.
  - 정의 : 프로그램 실행시 발생할 수 있는 예외의 발생에 대비한 코드를 작성 하는 것
  - 목적 : 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지 하는 것
### 예외 처리 구문(try catch)
  - 예외를 처리하려면 try-catch문 사용
  - try 블럭 내에서 예외가 발생 할 경우
  1. 발생한 예외와 일치하는 catch블럭이 있는지 확인
  2. 일치하는 catch블럭을 찾게 되면, 그 catch블럭 내의 문장들을 수행하고 전체 try-catch문을 빠전나가서 그 다음 문장을 계속해서 수행한다
  - try블럭 내에서 예외가 발생하지 않은 경우
  1. catch블럭을 거치지 않고 전체 try-catch문을 빠져나가서 수행을 계속한다.
```java
public class ExceptionEx2 {
    public static void main(String[] args) {
        int maxNum = 100;
        int result;
        int num;

        try {
            for (int i = 0; i < 10; i++) {
                num = (int) ((Math.random()) * 10);
                System.out.println(num);
                result = maxNum / num;
                System.out.println(result);
            }
        } catch (Exception e){
            System.out.println(e.getMessage());
        }
    }
}
```
## 예외 클래스의 계층구조
  - 예외 클래스는 크게 두가지로 나뉨
  - RuntimeException 클래스 : 프로그래머의 실수로 발생하는 예외  (예외처리 선택)
  - Exception클래스 : 외적인 요인에 의해 발생하는 예외   (예외처리 필수)
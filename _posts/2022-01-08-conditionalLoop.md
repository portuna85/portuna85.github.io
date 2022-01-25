---
layout: single
title: "조건문, 반복문(Conditional Loop)"
---

## 조건문종류 (if else, switch break)
## 반복문종류 (for, while)

### if문
#### if(조건문) { 문장 }
```java
public class FlowEx4 {
  public static void main(String[] args) {
    int score = 0;
    char grade = ' ';

    System.out.print("점수 입력해 주세요.>");
    Scanner sc = new Scanner(System.in);
    score = sc.nextInt();

    if (score >= 90) {
      grade = 'A';
    } else if (score >= 80) {
      grade = 'B';
    } else if (score >= 70) {
      grade = 'C';
    } else {
      grade = 'D';
    }
    System.out.println("당신의 학점은 " + grade + "입니다.");
  }
}
```

### switch문
#### switch(조건식){ 
#### case 값1: 
#### 문장
#### break;
#### case 값1:
#### 문장
#### break;
#### default:
```java
public class FlowEx10 {
    public static void main(String[] args) {
        int score = 0;
        char grade = ' ';
        Scanner sc = new Scanner(System.in);
        System.out.println("당신의 점수를 입력해주세요.");
        int i = sc.nextInt();
        switch (i / 10) {
            case 10: case 9:
                grade = 'A';
                break;
            case 8:
                grade = 'B';
                break;
            case 7:
                grade = 'C';
                break;
            default:
                grade = 'F';
        }
        System.out.println("당신의 학점은 " + grade + "입니다.");
    }
}
```
### for, while, do while 반복문
#### for(초기화 ; 조건식 ; 증감식)
#### 1. 초기화 -> 2. 조건식 -> 3. 수행될 문장 -> 4. 증감식
```java
public class FlowEx18 {
    public static void main(String[] args) {
        for (int i = 2; i <= 9; i++) {
            for (int j = 1; j <= 9; j++) {
                System.out.printf("%d X %d = %d\n", i, j, i * j);
            }
            System.out.println();
        }
    }
}
```
### while / do while 반복문
### while (조건식) { 조건식이 true일 때 수행될 문장 }
```java
public class FlowEx26 {
    public static void main(String[] args) {
        int sum = 0;
        int i = 0;

        while ((sum += ++i) <= 100) {
            System.out.printf("%d - %d%n", i, sum);
        }
    }
}
```
### do { 조건식이 true일 때 수행될 문장 } while(조건식)
```java
public class FlowEx29 {
    public static void main(String[] args) {
        for (int i = 0; i <= 100; i++) {
            System.out.printf("i = %d ", i);

            int tmp = i;
            
            // 3의 배수 면 !!출력
            // 3의 배수가 아니면 그냥 출력
            do {
                if (tmp % 10 % 3 == 0 && tmp % 10 != 0) {
                    System.out.print(" 짝");
                }
            } while ((tmp /= 10) != 0);
            System.out.println();
        }
    }
}
```
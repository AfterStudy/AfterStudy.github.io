---
layout: post
title: 람다
---


함수를 간단한 식(Expression)으로 표현하는 방법


```java
int sum (int a, int b) {
    return a + b;
}
// 위의 함수를 아래와 같은 식으로 변경한다.
(a, b) -> a + b
```

### 1. 함수를 람다로의 변이 과정


* 반환타입과 함수이름을 제거하고 {} 앞에 -> 를 추가한다.
* 컴파일 시 매개변수 타입을 추정하기에 생략한다.
* 'return', '{}', ';'도 생략한다.

```java
(int a, int b) -> {return a + b;}

(a, b) -> {return a + b;}

(a, b) -> a + b
```

### 2. 그 외 람다 특징

* 매개변수가 하나일 때 () 생략 가능
* 하나 뿐인 문장이면 '{}' 생략 가능
* 하지만 하나뿐인 문장이 return 문이라면 생략 불가

```java
(a) -> a+1
a -> a+1    // 위의 식과 같다. () 생략 가능

() -> System.out.println();    // 문장이 하나이면 {} 생략 가능
 
() -> return 10; //에러
```
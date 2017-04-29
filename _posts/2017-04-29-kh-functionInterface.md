---
layout: post
title: 함수형 인터페이스
---
<a href="https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html">
함수형 인터페이스 레퍼런스 문서
</a>

## 함수형 인터페이스란?

* 함수형 프로그래밍을 사용하기 위해 자바에서 추가된 인터페이스
* 고차원 함수를 자바 방식으로 변형


## 고차원 함수란?

* 함수를 값으로 취급한다.
* 함수를 함수의 매개변수로 사용할 수 있다.
* 함수를 함수의 리턴값으로 사용할 수 있다.

### 자바스크립트에서의 고차원 함수

```js
var f = functino() {}; //f라는 변수에 함수를 담는다.

function f2(a) {	//함수를 매개변수로 사용한다.
	a.call(this);
}

function() {
	return function() {	//함수를 리턴값으로 사용한다.
		return 1;
	}
}


```

## 함수형 인터페이스


### 매개변수가 없는 함수형 인터페이스

<table>
	<tr>
		<th>인터페이스</th>
		<th>호출 메서드</th>
		<th>설명</th>
	</tr>
	<tr>
		<td>java.lang.Runnable</td>
		<td>void run()</td>
		<td>리턴 값과 매개변수 둘다 없다.</td>
	<tr>	
</table>

.

### 하나의 매개변수를 가지는 함수형 인터페이스

<table>
	<tr>
		<th>인터페이스</th>
		<th>호출 메서드</th>
		<th>설명</th>
	</tr>
	<tr>
		<td>Supplier<T></td>
		<td>T get()</td>
		<td>리턴 값만 있다.</td>
	<tr>
	<tr>
		<td>Consumer<T></td>
		<td>void accept(T t)</td>
		<td>하나의 매개변수만 있다.</td>
	<tr>
	<tr>
		<td>Function<T,R></td>
		<td>R apply(T t)</td>
		<td>하나의 매개변수와 하나의 리턴 값을 가진다.</td>
	<tr>
	<tr>
		<td>Predicate<T></td>
		<td>boolean test(T t)</td>
		<td>하나의 매개변수를 가지고 booean값을 리턴한다</td>
	<tr>
</table>

.

### 두개의 매개변수를 받는 함수형 인터페이스

<table>
	<tr>
		<th>인터페이스</th>
		<th>호출 메서드</th>
	</tr>
	<tr>
		<td>BiConsumer<T></td>
		<td>void accept(T t, R r)</td>
	<tr>
	<tr>
		<td>BiFunction<T,R,U></td>
		<td>U apply(T t, R r)</td>
	<tr>
	<tr>
		<td>BiPredicate<T, R></td>
		<td>boolean test(T t, R r)</td>
	<tr>	
</table>

.

## 예제

```java
Runnable r = () -> System.out.println("test");
Supplier<String> s = () -> "test2";		//리턴 값만 있다
Consumer<String> c = a -> System.out.println(a);	//매개변수만 존재한다.
Function<String, Integer> f = a -> a.length();	//매개변수와 리턴값 둘다 존재한다.
Predicate<String> p = a -> a.equals("test5");	//하나의 매개변수를 가지고 boolean(참, 거짓)을 판별한다.
    
r.run();
System.out.println(s.get());
c.accept("test3");
System.out.println(f.apply("test4"));
System.out.println(p.test("test5"));
```

### 람다가 아닌 함수를 직접 구현한 방법 예제

```java
Supplier<String> s2 = new Supplier<String>() {
	@Override
	public String get() {
		System.out.println("hello");
		return "world";
	}
};

String temp = s2.get();
```




## Predicate 인페페이스 활용
<a href="https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html">
Predicate 레퍼런스 문서
</a>

### 메서드 정리

<table>
	<tr>
		<th>메서드</th>
		<th>설명</th>
	<tr>
	<tr>
		<td>and(Predicate<? super T> other</td>
		<td>and 연산</td>
	<tr>
	<tr>
		<td>or(Predicate<? super T> other)</td>
		<td>or 연산</td>
	<tr>
	<tr>
		<td>negate()</td>
		<td>not 연산</td>
	<tr>
	<tr>
		<td>isEqual(Object targetRef)</td>
		<td>같은 값인지 비교</td>
	<tr>
</table>

.

```java
Predicate<Integer> p = i -> i < 10;
Predicate<Integer> q = i -> i < 20;
Predicate<Integer> r = i -> i%2 == 0;

Predicate<Integer> notP = p.negate(); // i >= 10
Predicate<Integer> all = notP.and(q).or(r); // 10 <= i && i < 20 || i%2==0
Predicate<Integer> all2 = notP.and(q.or(r)); // 10 <= i && (i < 20 || i%2==0)

System.out.println(notP.test(10));//true
System.out.println(all.test(2)); // true
System.out.println(all2.test(2)); // false
```
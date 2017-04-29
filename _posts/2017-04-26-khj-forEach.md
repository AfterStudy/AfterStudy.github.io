---
layout: post
title: forEach
---

Java8 Iterable 인터페이스에 컬렉션을 반복해서 실행할 수 있는 forEach 메소드가 추가되었다.

## 구조

* default 메서드로 선언되어 있다.
* 파라미터
  * Consumer
* 예외
  * NullPointerException

```java
default void forEach(Consumer<? super T> action) {
	Objects.requireNonNull(action);
	for (T t : this) {
		action.accept(t);
	}
}

public static <T> T requireNonNull(T obj) {
	if (obj == null)
		throw new NullPointerException();
	return obj;
}
```

## Java 8 이전과 Java 8에서의 컬렉션 반복 실행

* 8 이전에는  for 문장을 사용해서 반복을 실행했다.(외부반복)
* 8 에서는 forEach 메서드를 사용해서 내부반복을 실행한다.
* 함수형 인터페이스를 사용해 내부 동작을 정의 하므로 재사용이 용이하다.

### java8 이전 컬렉션 반복실행
 
```java
for(String str : list) {
	System.out.println(str);
}
```

### java8 컬렉션 반복 : forEach 

```java
list.forEach(new Consumer<String>() {
	@Override
	public void accept(String arg0) {
		System.out.println(arg0);
	}
});

//람다식을 사용해서 코드 줄이기
list.forEach((str) -> System.out.println(str));
```
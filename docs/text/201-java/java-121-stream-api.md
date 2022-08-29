---
layout: default
title: java stream api 모음
parent: java
nav_order: 201121
---

## 함수형 프로그래밍 이란?
* 함수의 응용을 통해 명령을 지시하는 형태가 아닌 함수와 함수의 관계로 프로그래밍 하는 패러다임.

## java에서의 좋은예 나쁜예
```java
// GOOD
return Arrays.asList(enclosingInfo.getEnclosingClass().getDeclaredMethods())
        .stream()
        .filter(m -> Objects.equals(m.getName(), enclosingInfo.getName())
        .filter(m ->  Arrays.equals(m.getParameterTypes(), parameterClasses))
        .filter(m -> Objects.equals(m.getReturnType(), returnType))
        .findFirst()
        .getOrThrow(() -> new InternalError(...));

//BAD
Method matching =
Arrays.asList(enclosingInfo.getEnclosingClass().getDeclaredMethods())
.stream()
.filter(m -> Objects.equals(m.getName(), enclosingInfo.getName())
.filter(m ->  Arrays.equals(m.getParameterTypes(), parameterClasses))
.filter(m -> Objects.equals(m.getReturnType(), returnType))
.getFirst();
if (matching == null)
throw new InternalError("Enclosing method not found");
return matching;
```

### String to char Stream
```java
someString.chars()                       // IntStream 타입
    .boxed()                             // Stream<Integer>
    .forEach((word) -> {

    });
```

### Stream reverse
```java
someString.chars()
    .boxed()
    .sorted(Collections.reverseOrder())  // 뒤부터 읽도록 정렬
    .forEach((word) -> {

    });
```

### method 종류
```java
.stream
.filter
.peek // 중간 순회, 스트림 소모하지 않음 스트림 재사용
.forEach // 최종 순회
.map
.flatmap

1. 스트림 필터링 : filter(), distinct()
2. 스트림 변환 : map(), flatMap()
3. 스트림 제한 : limit(), skip()
4. 스트림 정렬 : sorted()
5. 스트림 연산 결과 확인 : peek()

IntStream stream = IntStream.of(7, 5, 5, 2, 1, 2, 3, 5, 4, 6);

stream.peek(s -> System.out.println("원본 스트림 : " + s))

    .skip(2)

    .peek(s -> System.out.println("skip(2) 실행 후 : " + s))

    .limit(5)

    .peek(s -> System.out.println("limit(5) 실행 후 : " + s))

    .sorted()

    .peek(s -> System.out.println("sorted() 실행 후 : " + s))

    .forEach(n -> System.out.println(n));

원본 스트림 : 7

원본 스트림 : 5

원본 스트림 : 5

skip(2) 실행 후 : 5

limit(5) 실행 후 : 5

원본 스트림 : 2

skip(2) 실행 후 : 2

limit(5) 실행 후 : 2

원본 스트림 : 1

skip(2) 실행 후 : 1

limit(5) 실행 후 : 1

원본 스트림 : 2

skip(2) 실행 후 : 2

limit(5) 실행 후 : 2

원본 스트림 : 3

skip(2) 실행 후 : 3

limit(5) 실행 후 : 3

sorted() 실행 후 : 1

1

sorted() 실행 후 : 2

2

sorted() 실행 후 : 2

2

sorted() 실행 후 : 3

3

sorted() 실행 후 : 5

5
```

### 참고 링크
* java 스트림 API <http://iloveulhj.github.io/posts/java/java-stream-api.html>

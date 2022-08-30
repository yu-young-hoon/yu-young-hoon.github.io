---
layout: default
title: java convention
parent: java
nav_order: 201102
---

## java top 10 coding guidlines

### 1. vairable Scopes, Readability, and Lambda Expression
변수의 범위는 가능한 사용하는 코드와 가깝게 선언해야 합니다. 변수는 범위 내에서만 사용 되고 보여야합니다.
지역 변수의 경우 선언되고 메소드의 끝까지 보이게 됩니다. 사용되는 시점의 최대한 가깝게 변수를 선언하면 가독성이 높고 디버깅을 간단하게 만듭니다.
```java
try
   Connection con = DriverManager.getConnection(DATABASE_URL,
      USERNAME,PASSWORD);
   Statement stmt = con.createStatement();
   ResultSet rs = stmt.executeQuery(SQL_QUERY)
){
   //...
}catch(SQLException e){
   e.printStackTrace();
}
```

java 8부터는 람다를 사용하여 직관적이고 간결하게 만들수 있습니다.
```java
Integer[] nums={90,71,26,34,42,35,66,57,88,89};

final List<Integer> l2 = Arrays.stream(nums)
.sorted().collect(Collectors.toList());
System.out.printf("After sorting: %s%n",l2);

final List<Integer> l3 = Arrays.stream(nums)
.filter(num -> num > 50).collect(Collectors.toList());
System.out.printf("Sorting only of numbers > 50
: %s%n", l3);
```

### 2. Class Fields
클래스의 멤버 변수와 메소드의 지역변수가 이름이 같은 경우가 종종있습니다.
```java
public class TestClass {
   private double commission = 5.5d;
   public double increaseCommission(final double newComm){
      double commission = newComm;
      commission += commission;
      return commission;
   }
   public double getCommission(){
      return commission;
   }
   public static void {
      TestClass m = new TestClass();
      System.out.println(m.increaseCommission(3.3));
      System.out.println(m.getCommission());
   }
}
```
이름이 같아서 생기는 충돌을 피하는 또다른 방법은 this 키워드를 사용하는것 입니다.
this.commission과 같이 접근하게 되면 항상 클래스의 멤버변수를 참조하여 오류를 피할수 있습니다.

### 3. Treating Method Arguments as Local Variable
자바에서는 한 번 선언 된 변수를 재사용 할 수 있습니다. 메서드 argument로 주어지는 non-final 변수도 다른 값으로 재사용 할 수 있습니다.
이런 메서드에서 전달 받은 값을 변경하면 메서드에서 가져온 원본 내용이 완전히 손실됩니다.
값을 다른 변수에 복사하고 필요한 처리를 수행하는 것으로 변경할수 있습니다.
그리고 다음과 같이 final 키워드를 사용하여 argument로 주어지는 변수를 제한하고 상수로 만들 수 있습니다.
```java
public double calculate(final double newVal){
   double tmp = newVal;
    // ...
   return tmp;
}
```

### 4. Boxing and UnBoxing
```java
public static void update(final double newVal){
   // ...
}

final Double val = null;
update (val);
```
오토 박싱은 우리가 원하는 결과대신 에러를 발생시킬수 있습니다.

## wrap type
* byte, short, int, long, char, Boolean and double
* wrap them up only when it is needed the most.

## variable naming
Map<A,B>: AToB

### 참고링크
* [http://kwangshin.pe.kr/blog/java-code-conventions-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%94%A9-%EA%B7%9C%EC%B9%99/ java code conventions]
* [https://www.developer.com/java/data/top-10-java-coding-guidelines.html how-to-use-annotations-effectively-in-java]
* [https://www.developer.com/java/data/how-to-write-methods-efficiently-in-java.html how-to-write-methods-efficiently-in-java]
* [https://www.developer.com/java/data/autoboxing-and-unboxing-in-java.html autoboxing-and-unboxing-in-java]

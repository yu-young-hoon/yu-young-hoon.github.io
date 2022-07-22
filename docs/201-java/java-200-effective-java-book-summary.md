---
layout: default
title: (book summary)effective java
parent: java
nav_order: 201200
---

==객체 생성과 파괴==
===01.생성자 대신 정적 팩터리 메서드를 고려하라===
* 장점
  ** 이름을 갖을수 있다(BigInteger.probablePrime 의미를 알수있다)
  ** 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다(immutable class, Boolean.valueOf(boolean))
  ** 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다(엄청난 유연성 Collections)
  ** 입력 매개 변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다(EnumSet)
  ** 정작 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다(Service provider framework 근간, JDBC)
* 단점
  ** 생성자가 없어 상속을 할 수 없다
  ** 정적 팩터리 메서드는 프로그래머가 찾기 어렵다
* 이름별 의미
  ** from: 매개 변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드(Date.from)
  ** of: 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계메서드(EnumSet.of)
  ** valueOf: from과 of의 더 자세한 버전(BigInteger.valueOf)
  ** getInstance: 매개변수를 받으면 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지는 않는다(StackWalker.getInstance)
  ** newInstance: 항상 새로운 인스턴스를 생성해 반환함을 보장한다(Array.newInstance)
  ** get(Type): 생성할 클래스가 아닌 반환할 객체의 타입을 반환, 다른 클래스의 팩터리 메서드를 정의할 때 쓴다(Files.getFileStore)
  ** new(Type): 생성할 클래스가 아닌 반환할 객체의 타입을 반환, 다른 클래스의 팩터리 메서드를 정의할 때 쓴다(새로운 인스턴스, Files.newBufferdReader)
  ** (type): getType, newType의 간결한 버전(Collections.list)

===02. 생성자에 매개변수가 많다면 빌더를 고려하라===
===03. private 생성자나 열거 타입으로 싱글턴임을 보장하라===
===04. 인스턴스화를 막으려거든 private 생성자를 사용하라===

===05. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라===
* 팩터리 메서드패턴

===06. 불필요한 객체 생성을 피하라===
* 정규식 캐싱
* 기본 타입 사용

===07. 다쓴 객체 참조를 해제하라===

===08.===
===09.===
==모든 객체의 공통 메서드==
===10.===
===11.===
===12.===
===13.===
===14.===
==클래스와 인터페이스==
===15.===
===16.===
===17.===
===18.===

=== 19. 상속을 고려해 설계하고 문서화 하라. 그러지 않았다면 상속을 금지하라 ===
* 상속용 클래스는 재정의할 수 있는 메서드들을 내부적으로 어떻게 이용해야하는지 문서로 남겨야한다.
* 재정의할 수 있는 메서드는 public, protected 접근제한제를 가진 메서드중 final이 아닌 메서드를 말한다.
* 문서는 @implSpec 태그를 메서드 주석에 붙이고 -tag "implSpec:a:Implementation Requirements:"를 지정해주면 javadoc이 태그를 활성화한다.
* 상속용 클래스틑 하위 클래스를 만들어 검증해야한다
* 하위 클래스 생성자는 재정의 가능 메서드를 호출해서는 안된다.

===20.===

===21.인터페이스는 구현하는 쪽을 생각해 설계하라===
* 인터페이스에 디폴트 메서드를 선언하면 구현하지 않은 모든 클래스에서 디폴트 구현이 쓰이게된다.
* 예를 들어 아파치 SynchronizedCollection이 removeIf를 재구현하지 않았다
* 디폴트 메서드는 기존 구현체에 런타임 오류를 일으킬 수 있다.
* 디폴트 메서드는 표준적인 메서드 구현을 제공하는 데 아주 유용한 수단이다.

===22.인터페이스는 타입을 정의하는 용도로만 사용하라===
* 상수 인터페이스틑 안티패턴이다
* 상수는 내부 구현이다
* 숫자 리터럴에 밑줄을 사용할수 있다
* 상수 클래스를 사용하고 인스턴스화할 수 없는 유틸리티 클래스를 만들어라
<source lang="java">
public class PhysicalConstants {
    private PhsicalConstants() {}

    public static final double AVOGARDROS_NUMBER = 6.022_140_857e23;
}
</source>

===23. 태그달린 클래스보다는 클래스 계층구조를 활용하라===
===24. 멤버 클래스는 되도록 static으로 만들라===
* 중첩 클래스(nested class)란 다른 클래스 안에 정의된 클래스를 말한다
* 정적(static) 멤버 클래스
  ** 나머지와 다르게 내부 클래스(inner class)가 아니다
  ** 바깥 클래스 private 멤버에도 접근이 가능하다
  ** 바깥 클래스와 함께 쓰일 때만 유용한 public 도우미 클래스(예 Calculator.Operation.PLUS)
  ** private 정적 멤버 클래스는 흔히 바깥 클래스가 표현하는 객체의 한 부분(구성요소)을 나타낼 때 쓴다(map의 키값을 표현하는 엔트리의 getKey, getValue, setValue는 map을 직접 사용하지 않는다)
* 멤버 클래스
  ** 비정적 멤버 클래스의 인스턴스는 this를 사용해 바깥 인스턴스의 참조를 가져올 수 있다
  ** 비정적 멤버 클래스는 바깥 인스턴스 없이는 생성할 수 없다(독립적으로 있어야하면 정적 멤버 클래스)
  ** 비정적 멤버 클래스는 바깥 인스턴스와 동시에 만들어 지거나 수동으로 만든다
  ** 비정적 멤버 클래스는 어댑터를 정의 할때 자주 쓰인다(Map의 keySet, entrySet, values등 컬랙션뷰과 Set, List의 반복자들을 구현할때)
  ** 바깥인스턴스 접근할 일이 없다면 static으로 정적 멤버 클래스로 만들자
  ** 비정적 멤버 클래스의 바깥 클래스의 인스턴스는 수거(GC)가 되지 못하거나 참조 때문에 시간 공간이 낭비된다
* 익명 클래스
  ** 이름이 없다
  ** 바깥 클래스의 멤버도 아니다
  ** 쓰이는 시점에 선언과 동시에 인스턴스가 만들어진다
  ** 상수 변수 이외의 정적 멤버는 가질 수 없다
  ** 초기화된 final 기본 타입과 문자열 필드만 가질 수 있다
  ** 표현식 중간에 등장하므로 길면 가독성이 떨어진다
  ** 작은 함수 객체나 처리 객체를 만드는대 사용했지만 람다가 그 역할을 대신한다
  ** 정적 팩터리 메서드를 구현할때 쓰였다(intArrayAsList 참고)
* 지역 클래스
  ** 지역변수를 선언할 수 있는 곳이면 어디서든 선언 할수 있고 유효범위도 지역변수와 같다

===25. 톱레벨 클래스는 한 파일에 하나만 담으라===
* 두클래스가 한 파일에 있으면 안된다
* 하나를 정적 멤버 클래스로 만들거나 두개의 파일로 분리하자

==제네릭==
===26. raw 타입은 사용하지 말라===
* List 인터페이스는 타입 매개변수 E를 받는다
* List<E>가 인터페이스의 이름이 된다
* 타입 매개변수를 받는 클래스와 인터페이스를 제네릭 클래스, 제네릭 인터페이스라고 하며 통틀어 제네릭 타입이라고 한다
* List<String>은 원소 타입이 String인 매개변수화 타입이라고 한다
* List는 제네릭 타입을 정의 하며 같이 정의 되는 raw 타입이며 컴파일 타임에 타입 오류가 발생하지 않기 때문에 사용하지 말아야 한다
* Collection<?>의 ?은 와일드 카드 타입이다
* 와일드 카드 타입은 안전하다
* <E extends Number> 한정적 타입 매개변수
* <T extends Comparable<T>> 재귀적 타입 한정
* List<? extends Number> 한정적 와일드카드 타입
* static <E> List<E> asList(E[] a) 제네릭 메서드
* 예외1: class 리터럴에 매개변수화 타입을 사용하지 못한다
  ** List.class로 사용
  ** List<String>.class 사용불가
* 예외2: instanceof연산자 사용시 raw타입을 사용한다
<source lang="java">
if (o instanceof Set) {
    Set<?> s = (Set<?>) o;
    ...
}
</source>

===27. 비검사 경고를 제거하라===
<source lang="java">
    // 경고 발생
    Set<Lark> exaltation = new HashSet();

    // 자바7에서 제공하는 다이아몬드 연산자를 사용하면 실제 타입을 추론해줘서 해결된다
    Set<Lark> exaltation = new HashSet<>();
</source>

javac -Xlint:uncheck 옵션을 사용할경우 uncheckd conversion 비검사 경고와 함께 설명해준다.

가능하면 비검사 경고를 모두 제거해야한다.

그렇지 않다면 런타임에 ClassCastException이 발생한다.

타입이 안전하다고 확신할 수 있다면 @SuppressWarnings("unchecked") 어노테이션으로 경고를 숨기고 주석을 달아야한다.

===28. 배열보다는 리스트를 사용하라===
* 배열은 공변(cocariant)이다. Child[]는 Parent[]의 하위 타입이된다.
* 제네릭은 불공변(invariant)이다. 각각의 리스트는 하위 타입도 상위 타입도 아니다.
* 배열은 실체화 된다. 런타임에도 원소 타입을 인지하고 확인한다.
* 제네릭은 런타임에 타입 정보가 소거된다. 실체화가 불가능 하다(비한정적 와일드 타입은 가능)
* 배열은 런타임에 안전하고 컴파일에 안전하지 않다. (런타임에 실패한다)
* 제네릭은 런타임에 안전하지 않고 컴파일에 안전하다. (컴파일에 실패한다)
* 둘을 섞어 쓰기 힘들고 오류나 경고를 만나면 배열을 리스트로 대체하자.

===29. 이왕이면 제네릭 타입으로 만들어라===
* 클라이언트에서 제네릭으로 변환하기 보다 제네릭 타입이 안전하고 편하다
* public Object[] elements; 대신 private E[] elements;를 사용해라
<source lang="java">
    // 실체화 불가 타입으로 new를 할때 사용한다
    @SuppressWarning("unchecked")
    return (E[]) new Object[];
</source>
* <E extends Delayed> 같이 제한을 두면 바로 가능하다
* 배열이 아닌 리스트를 성능을 위해 사용할 때도 있다

===30. 이왕이면 제네릭 메서드로 만들어라===
* 메서드도 제네릭으로 만들면 안전하고 편하다
* Collections의 sort, binarySearch는 모두 제네릭 메서드이다
<source lang="java">
    public static <E> Set<E> union(Set<E> s1, Set<E> s2) {
    }
</source>
* identify function 항등함수(입력 값을 수정 없이 그대로 반환하는 특별함수)의 경우 Function.identify를 사용할수 있지만 직접 구현할수 있다
<source lang="java">
    // 제네릭 싱글턴 팩터리 패턴
    private static UnaryOperator<Object> IDENTITY_FN = (t) -> t;

    @SuppressWarnings("unchecked")
    public static <T> UnaryOperator<T> identityFunction() {
        return (Unaryoperator<T>) IDENTITY_FN;
    }
    
    // 사용
    Unaryoperator<String> a = identityFunction();
    for (String s : arr)
        System.out.println(a.apply(s));

</source>
* 재귀적 한정타입
<source lang="java">
    public statc <E extends Compable<E>> E max(Collection<E> o) {
        if(o.isEmpty())
            throw new IllegalArgumentException("비었음");
        E result = null;
        for (E e : o)
            if (result == null || e.compareTo(result) > 0)
                result = Objects.requireNonNull(e);
        return result;
    }
</source>

===31. ===
===32. ===
===33. ===

==열거 타입과 애너테이션==
===34. ===
===35. ===
===36. ===
===37. ===
===38. ===
===39. ===
===40. ===
===41. ===

==람다와 스트림==
===42. ===
===43. ===
===44. ===
===45. ===
===46. ===
===47. ===
===48. ===

==메서드==
===49. ===
===50. ===
===51. ===
===52. ===
===53. ===
===54. ===
===55. ===
===56. ===

==일반적인 프로그래밍 원칙==
===57. ===
===58. ===
===59. ===
===60. ===
===61. ===
===62. ===
===63. ===
===64. ===
===65. ===
===66. ===
===67. ===
===68. ===

==예외==
===69. ===
===70. ===
===71. ===
===72. ===
===73. ===
===74. ===
===75. ===
===76. ===
===77. ===

==동시성==
===78. ===
===79. ===
===80. ===
===81. ===
===82. ===
===83. ===
===84. ===

==직렬화==
===85. ===
===86. ===
===87. ===
===88. ===
===89. ===
===90. ===

== 참고링크 ==
* [https://github.com/keesun/study/tree/master/effective-java java effective java 요약]

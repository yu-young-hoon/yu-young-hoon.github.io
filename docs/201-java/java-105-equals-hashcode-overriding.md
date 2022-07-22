---
layout: default
title: java equals, hashCode overriding 작성법
parent: java
nav_order: 201105
---

```java
public class SumClass implements Serializable {
    private Date someDate;
    private String a;
    private String b;
    private String c;

    @Override
    public boolean equals(Object obj) {

        if (obj == null) {
            return false;
        }

        if (obj == this) {
            return true;
        }

        if (!(obj instanceof SumClass)) {
            return false;
        }

        SumClass sdk = (SumClass) obj;
        return someDate.equals(sdk.someDate) && a.equals(sdk.a) && b.equals(sdk.b) && c.equals(sdk.c);

    }

    @Override
    public int hashCode() {
        int result = someDate != null ? someDate.hashCode() : 0;
        result = 31 * result + ( a != null ? a.hashCode() : 0 );
        result = 31 * result + ( b != null ? b.hashCode() : 0 );
        result = 31 * result + ( c != null ? c.hashCode() : 0 );
        return result;
    }

}
```

* 간단히 아래처럼 lombok을 사용할수 있다.
* @EqualsAndHashCode(of = {"someDate", "a", "b", "c"}, callSuper = false)
* 31로 제곱 하는 이유 <https://stackoverflow.com/questions/299304/why-does-javas-hashcode-in-string-use-31-as-a-multiplier>

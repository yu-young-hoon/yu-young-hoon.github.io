임시

## lookaround?!
정규표현식에서 lookaround는 특정 패턴의 앞이나 뒤를 보고 패턴을 찾는 방법이다. 
이중 lookbehind가 Java에서 어떻게 동작하는지와 유의할 점을 알아 보고자 합니다.

정규표현식에서 lookarond의 종류는 아래처럼 4가지가 있습니다..
* positive lookahead: (?=표현식) 표현식이 오른쪽에 매치될 때
* negative lookahead: (?!표현식) 표현식이 오른쪽에 매치되지 않을 때
* positive lookbehind: (?<=표현식) 표현식이 왼쪽에 매치될 때
* negative lookbehind: (?<!표현식) 표현식이 왼쪽에 매치되지 않을 때

## lookahead
* `asdf(?=ghjk)` 는 asdfghjk 에서 asdf 뒤에 ghjk가 있을 때 매치됩니다.
* `asdf(?!ghjk)` 는 asdfghjk 에서 asdf 뒤에 ghjk가 있을 때 매치됩니다.

## lookbehind
* `(?<=asdf)ghjk` 는 asdfghjk 에서 asdf 뒤에 ghjk가 있을 때 매치됩니다.
* `(?<!=asdf)ghjk` 는 asdfghjk 에서 asdf 뒤에 ghjk가 있을 때 매치됩니다.

## capture group과의 차이
* `(aaa)`
* `(?=aaa)`
* `(?<=aaa)`

## 평가 방식
Java continues to step back until the lookbehind either matches or it has stepped back the maximum number of characters

```azure
    if (ch == '?') {
            ch = skip();
            switch (ch) {
            case ':':   //  (?:xxx) pure group
            case '=':   // (?=xxx) and (?!xxx) lookahead
            case '!':
                if (ch == '=') {
                    head = tail = new Pos(head);
                } else {
                    head = tail = new Neg(head);
                }
            case '<':   // (?<xxx)  look behind
                if (ch == '=') {
                    head = tail = (hasSupplementary ?
                                   new BehindS(head, info.maxLength,
                                               info.minLength) :
                                   new Behind(head, info.maxLength,
                                              info.minLength));
                } else { // if (ch == '!')
                    head = tail = (hasSupplementary ?
                                   new NotBehindS(head, info.maxLength,
                                                  info.minLength) :
                                   new NotBehind(head, info.maxLength,
                                                 info.minLength));
                }
        }
```


```java
    /**
     * Zero width positive lookahead.
     */
    static final class Pos extends Node {
        Node cond;
        Pos(Node cond) {
            this.cond = cond;
        }
        boolean match(Matcher matcher, int i, CharSequence seq) {
            int savedTo = matcher.to;
            boolean conditionMatched = false;

            // Relax transparent region boundaries for lookahead
            if (matcher.transparentBounds)
                matcher.to = matcher.getTextLength();
            try {
                conditionMatched = cond.match(matcher, i, seq);
            } finally {
                // Reinstate region boundaries
                matcher.to = savedTo;
            }
            return conditionMatched && next.match(matcher, i, seq);
        }
    }
```

```java
    /**
     * Zero width positive lookbehind.
     */
    static class Behind extends Node {
        Node cond;
        int rmax, rmin;
        Behind(Node cond, int rmax, int rmin) {
            this.cond = cond;
            this.rmax = rmax;
            this.rmin = rmin;
        }

        boolean match(Matcher matcher, int i, CharSequence seq) {
            int savedFrom = matcher.from;
            boolean conditionMatched = false;
            int startIndex = (!matcher.transparentBounds) ?
                             matcher.from : 0;
            int from = Math.max(i - rmax, startIndex);
            // Set end boundary
            int savedLBT = matcher.lookbehindTo;
            matcher.lookbehindTo = i;
            // Relax transparent region boundaries for lookbehind
            if (matcher.transparentBounds)
                matcher.from = 0;
            for (int j = i - rmin; !conditionMatched && j >= from; j--) {
                conditionMatched = cond.match(matcher, j, seq);
            }
            matcher.from = savedFrom;
            matcher.lookbehindTo = savedLBT;
            return conditionMatched && next.match(matcher, i, seq);
        }
    }
```

```kotlin
Java takes things a step further by allowing finite repetition. You can use the question mark and the curly braces with the max parameter specified. Java determines the minimum and maximum possible lengths of the lookbehind. The lookbehind in the regex (?<!ab{2,4}c{3,5}d)test has 5 possible lengths. It can be from 7 through 11 characters long. When Java (version 6 or later) tries to match the lookbehind, it first steps back the minimum number of characters (7 in this example) in the string and then evaluates the regex inside the lookbehind as usual, from left to right. If it fails, Java steps back one more character and tries again. If the lookbehind continues to fail, Java continues to step back until the lookbehind either matches or it has stepped back the maximum number of characters (11 in this example). This repeated stepping back through the subject string kills performance when the number of possible lengths of the lookbehind grows. Keep this in mind. Don’t choose an arbitrarily large maximum number of repetitions to work around the lack of infinite quantifiers inside lookbehind. Java 4 and 5 have bugs that cause lookbehind with alternation or variable quantifiers to fail when it should succeed in some situations. These bugs were fixed in Java 6.
```

Zero-Length Assertions이란

역추적이란

### 참고링크
* https://www.regular-expressions.info/lookaround.html
* https://elvanov.com/2388
* https://community.appway.com/screen/kb/article/checking-strings-avoiding-catastrophic-backtracking-1482810891360 치명적 역추적
* https://blog.naver.com/dsyun96/222715934643 [Kotlin] 정규식 look-behind에서 반복 제한 이슈

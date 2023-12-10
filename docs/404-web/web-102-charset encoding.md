---
layout: default
title: web charset encoding
parent: web
nav_order: 404102
---

## Charset encoding
개발을 하면서 문자열 처리에 대해 겪었던 문제와 기본 개념을 정리 해보려 합니다.

최근에는 HTML5의 기본 charset이 utf-8이 되었고 Database 기본 character set과 서버 구동시 encoding을 utf-8로 하는 것이 기본이 되었기 때문에 단순한 인코딩이 문제가 된적은 없습니다.

하지만 예전에 개발을 하다보면 문자열이 ¾È³çÇÏ¼¼¿ä �븞�뀞�븯�꽭�슂 뻈돧쟏벼뿤 같은 문자열을 종종 만날수 있었고 당황했던 경험이 있습니다.

최근에 개발을 하면서 emoji와 accent 문자열로 인해 이슈를 겪었고 다시 한번 정리 해보는 겸, 혹시 경험해 보지 않으신 분 들을 위해 3가지의 기본적인 내용과 겪었던 3가지 문제와 해결 방법을 아래 적힌 순서대로 적었습니다.

* ascii unicode utf-16 euckr utf-8
* utf-8 정규화 비정규화
* mysql chracter set과 collation
* emoji 문자 문제
* accent 문자 문제
* html escape 문제

### ascii unicode ucs-2 utf-16 euckr utf-8차이
####ascii
ascii코드는 0부터 128까지의 1byte중 7bit를 사용하는 부호 체계입니다. 1bit는 Parity bit로 통신 에러 검출에 사용하는 방식입니다

ascii extended는 8bit를 사용하는 확장형 코드로 특수문자 기호를 포함합니다
{{:ascii code}}

#### unicode
유니코드는 Unicode Consortium가 제정하는 문자열 표기 산업 표준으로 문자와 코드가 1:1 매핑 되는 방식입니다

최신 release의 경우 https://www.unicode.org/releases/index.html에서 확인 할수 있습니다

문서를 열어보게 되면 코드 블록 마다 어떤 문자를 담고 있는지 코드 블록에 대한 설명, 코드의 차트, 유니코드를 구현하는 알고리즘 까지 정리 되어있습니다

0000–007F 블록은 ascii 코드와 동일한 코드를 두어 호환이 되도록 하였습니다 (Controls and Basic Latin)


! 코드 블록 ! 블록 이름 ! 블록 설명 !
| | |
한글에 대한 코드 블록은 한글 자모와 한글 음절로 구분되어있습니다.


유니코드는 전세계 언어들을 다룰수 있도록 나온 표준으로 1byte로 다국어를 포함하기 힘든 상황에서 2byte 3byte 4byte등을 사용하여 값의 구역을 나누고 다국어를 지원하도록 하였고 여러 인코딩 방식이 있습니다

#### ucs-2
ucs-2은 고정길이(2byte)를 가진 방식으로 늘어나는 유니코드를 포함 할수 없기 때문에 고정길이 4byte를 가진 ucs-4와 가변길이(2byte or 4byte)를 가진 utf-16에 포함 되어 사용이 점차 사라지게 되었습니다.

#### utf-16 euckr
euckr은 utf-16에 포함되는 한글 완성형 인코딩 방식입니다.
또 다른 완성형 인코딩 방식은 eucjp등 언어별로 존재하는데 utf-8방식과 달리 단일 인코딩 방식이 아니기 때문에 인코딩 방식을 혼동하여 바라지 않는 결과가 나올수 있습니다.

또한 utf-16은 가변길이지만 ucs-2에 기초하여 나왔기 때문에(2byte~4byte) 0~128까지 ascii와 동일한 값을 가지만 데이터의 길이는 2byte로 가져가기 때문에 데이터를 아낄수 있는 부분에서 utf-8보다 낭비를 하게됩니다

#### utf-8
utf-8은 가변길이(1~4byte)라는 특징을 가졌고 호환성이 좋기 때문에 가장 많이 사용됩니다. `EF BB BF`값을 가진 Byte Order Mark(BOM)를 문서 가장 처음에 표기하여 문서가 utf-8임을 나타내기도 하는데 권장되지 않습니다.

html5의 표준 인코딩 방식은 utf-8이고 일반적으로 유니코드라고 하면 utf-8방식을 말합니다.

utf-8의 장점은 영어의 경우 1byte 한글의 경우 3byte 처럼 가변적으로 문자의 block에 따라 가변적으로 문자를 기록 함으로서 데이터를 아낄수 있다는 장점과 단일 인코딩 방식이기 때문에 인코딩 방식을 혼동해서 생길수 있는 문제가 없어졌습니다.


### utf-8 정규화 비정규화 차이
!  ! NFC ! NFD ! NFKC ! NFKD ! 비고 !
| 각(AC01)    | 각 (AC01)   | 각 (1100 + 1161 + 11A8) | 각 (AC01)                          | 각 (1100 + 1161 + 11A8)                                 | 한글음절     |
| ㄱ (1100)   | ᄀ (1100)   | ᄀ (1100)               | ᄀ (1100)                          | ᄀ (1100)                                               | 한글자모     |
| ㄱ (3131)   | ㄱ (3131)   | ㄱ (3131)               | ᄀ (1100)                          | ᄀ (1100)                                               | 호환자모     |
| ㈀ (3200)   | ㈀ (3200)   | ㈀ (3200)               | (ㄱ) ( '(' + 1100 + ')' )          | (ㄱ) ( '(' + 1100 + ')' )                               | 자모괄호기호 |
| ㈎ (320E)   | ㈎ (320E)   | ㈎ (320E)               | (가) ( '(' + AC00 + ')' )          | (가) ( '(' + 1100 + 1161 +,')' )                        | 음절괄호기호 |
| ㈝㈝ (321D) | ㈝㈝ (321D) | ㈝㈝ (321D)             | (오전) ( '(' + C624 + C804 + ')' ) | (오전) ( '(' + 110B + 1169 + 110C + 1165 + 11ab + ')' ) | 오전괄호기호 |
| ㉠ (3260)   | ㉠ (3260)   | ㉠ (3260)               | ᄀ (1100)                          | ᄀ (1100)                                               | 자모원기호   |
| ㉮ (326E)   | ㉮ (326E)   | ㉮ (326E)               | 가 (AC00)                          | 가 (1100 + 1161)                                        | 음절원기호   |
| ﾡ (FFA1)    | ﾡ (FFA1)    | ﾡ (FFA1)                | ᄀ(1100)                           | ᄀ (1100)                                               | 자모반각기호 |
유니코드 정규화의 경우 NFD, NFC, NFKD, NFKC 방식이 있습니다.


맥의 경우 NFD(Normalization Form Canonical Decomposition 정준 분해)방식을 사용하고 있습니다

맥에서 파일을 저장하고 윈도우즈에서 열어보려고 할경우 ㄱㅏㄴㅏㄷㅏ.txt처럼 되는데 자음과 모음을 분해하여 저장하는 방식을 사용하고 있기 때문입니다.

그 반대로 일반적으로 사용되는 NFC(Normalization Form Canonical Composition 정준 결합)의 경우 자음 모음이 결합된 방식입니다.

NFD형식 예) `한 (U+D55C) → ᄒ (U+1112) + ᅡ (U+1161) + ᆫ (U+11AB)`

NFC형식 예) `ᄒ (U+1112) + ᅡ (U+1161) + ᆫ (U+11AB) → 한 (U+D55C)`

NFKC, NFKD의 경우 호환 분해 호환 결합으로 한글 특수 문자를 포합하여 분해 결합을 진행합니다.


### mysql chracter set과 collation
일반적으로 mysql chracter set의 경우 utf-8을 사용하게 되며 정렬 순서를 나타내는 collation의 경우 utf8-general-ci을 기본으로 사용합니다

utf8-general-ci 방식은 정렬이 빠르다는 장점이 있지만 utf8_unicode_ci 보다 정확도가 떨어진다는 단점이 있습니다
utf8mb4_general_ci 2010년 3월 24일에 utf8mb4 라는 charset을 추가된(MYSQL 5.5.3) 방식으로 4byte 문자를 지원하는 방식입니다.

이외에도 다양한 정렬 방식과 여러 종류의 chracter set이 존재하고 utf-16또한 정렬방식이 몇가지 존재 하지만 많이 사용되진 않고 있습니다.
`SHOW COLLATION;`을 통해서 사용하고 있는 mysql버전에서 사용할수 있는 collation을 확인할수 있고 default로 무엇이 설정되어있는지 확인할수 있습니다.

utf8mb4_0900_as_ci 처럼 나타낼때 뒤의 as, ai, cs, ci의 경우 accent문자와 case에 Sensitivity한지 InSensitivity한지를 나타냅니다.
* as는 accent에 sensitivity하다는 것입니다.
* ai는 accent에 Insensitivity하다는 것입니다.
* cs는 case에 sensitivity하다는 것입니다.
* ci는 case에 Insensitivity하다는 것입니다.

sensitivivity하다는 것은 정렬에 accent(발음기호), case(대소문자)를 사용한다는 것이고 Insensitivity하다는 것은 사용하지 않는 다는 것입니다.

Insensitivity할 경우 정렬에 사용되지 않기 때문에 unique, primary key에서 사용할 경우 같은 값으로 인식되어 duplicated 문제가 발생할수 있습니다.

utf8mb4_general_ci의 경우 accent와 case둘다 Insensitivity하기 unique한 값에 해당하는 collation을 사용할 경우 고려하여 코드를 설계해야합니다.


### emoji 문자 문제
emoji라고 불리는 이모티콘 기호는 utf-8에서는 \xF0\x9F\x98\x80부터 utf-16에서 1F600부터의 범위를 있습니다.

언어셋이 다르다면 같은 emoji를 나타내더라도 다른값을 가지게 됩니다.

```sql
insert into encoding (utf8,utf16) values ("😀", "😀");
select hex(`utf8`), hex(utf16) from encoding;
```
위 처럼 다른 언어셋을 가진 테이블에 입력 하게 되면 F09F9880 D83DDE00 처럼 다른 값이 나오게 됩니다.

```java
public class EmojiTest {
    @Test
    public void test01() {
        final String em = "\ud83d\ude00";
        System.out.println("em = " + em);
    }

    @Test
    public void test02() {
        byte[] a = {(byte) 0xF0,(byte)0x9F,(byte)0x98,(byte)0x80};
        System.out.println("em = " + new String(a));
    }
}
```
java에서 위처럼 코드를 작성하게 된다면 둘다 😀를 출력 하게 됩니다

```java
public final class EmojiConverter {
    private static Pattern EMOJI_PATTERN = Pattern.compile(
                    "[\ud800\udc00-\udbff\udfff]",
                    Pattern.UNICODE_CASE | Pattern.CANON_EQ | Pattern.CASE_INSENSITIVE);

    public static class EmojiSerializer extends JsonSerializer<String> {
        @Override
        public void serialize(String value, JsonGenerator gen, SerializerProvider provider)
                throws IOException {

            if(Strings.isNullOrEmpty(value)){
                gen.writeString("");
                return;
            }

            Matcher matcher = EMOJI_PATTERN.matcher(value);
            String cleanString = matcher.replaceAll("");
            gen.writeString(cleanString);

        }
    }
}
```
위와 같은 방식으로 컨버터를 만들어서 emoji를 제거 해서 입력 시킬수도 있습니다.


### accent 문자 문제
È 문자는 E와 다르게 accent(Diacritic 발음 구별 기호)기호가 붙어있습니다.

이러한 형태도 정규화가 된 형태이며 한글의 nfd와는 다르게 값을 단순히 더한 값은 아니고 유니코드 표를 따라가고 있습니다.

`   E +   ̀   ` =  U+0045 + U+0300 = U+00C8


{{#snippet:repository=https://github.com/yu-young-hoon/java-encoding|filename=src/test/java/AccentTest.java|branch=master|startline=8|endline=18}}
정규화가 된 상태의 È를 분해해서 결합된 것과 비교하게 된다면 Not equals이며 다시 결합하여 비교하면 equals가 되기 때문에 accent 뿐만 아니라 한글과 같이 분해가 되는 문자열의 정규화 분해결합은 신경써야합니다.

```java
    @Test
    public void accent02() {
        String nfc = "\u00c8";

        String nfcToNfd = Normalizer.normalize(nfc, Normalizer.Form.NFD);
        String removedAccent = nfcToNfd.replaceAll("[\\p{InCombiningDiacriticalMarks}]", "");

        String removedAccent2 = StringUtils.stripAccents(nfcToNfd);
        Assert.assertEquals("E", removedAccent);
        Assert.assertEquals("E", removedAccent2);
    }
```
accent를 제거하는 방법을 두가지 소개하자면 분해후에 정규식으로 제거하거나 apache common의 StringUtils의 stripAccents를 사용할수 있습니다. 결과값은 nfd가 된 형태이기 때문에 비교하거나 다시 사용해야할경우 nfc를 다시 해야합니다.

다른 언어와 마찬가지로 한글에도 accent기호가 있습니다.

방음(방점)으로 알려진 분음 부호 `>`  ` 〮`  ` 〯`를 사용하여 한글 에서 중 한국어를 위한 악센트를 표시할수 있습니다.

한글의 accent기호는 결합된 형태가 있는지는 잘 모르겠고 위처럼 제거를 할수 있습니다.


### html escape
```java
    @Bean
    public WebMvcConfigurerAdapter webConfigurerAdapter() {
        return new WebMvcConfigurerAdapter() {

            @Override
            public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
                super.configureMessageConverters(converters);

                converters.add(htmlEscapingConveter());
            }

            private HttpMessageConverter<?> htmlEscapingConveter() {
                ObjectMapper objectMapper = new ObjectMapper();
                MappingJackson2HttpMessageConverter htmlEscapingConverter = new MappingJackson2HttpMessageConverter();

                objectMapper.getFactory().setCharacterEscapes(new HTMLCharacterEscapes());
                htmlEscapingConverter.setObjectMapper(objectMapper);

                return htmlEscapingConverter;
            }
        };
    }
```
java에서 dto를 통해 view로 json 데이터를 꺼내줄때 html에 영향을 주는 문자열을 `{"name":"&lt;하하"}` 처럼 escape하게 됩니다

```js
$('<div/>').html(text).text();
```
자바스크립트에서 위처럼 dom을 생성하고 html안에 넣은후 결과를 다시 텍스트로 받아오는 방식으로 escape된 문자를 다시 되돌릴 수 있습니다


TODO UTF8 encoding process 정리 https://en.wikipedia.org/wiki/UTF-8#Encoding

### 참고링크
* [https://d2.naver.com/helloworld/76650 d2 한글인코딩]
* [https://gist.github.com/Pusnow/aa865fa21f9557fa58d691a8b79f8a6d 한글인코딩]
* [https://pragp.tistory.com/entry/Unicode-UCS2-UTF16-UTF8-UTF32 unicode 차이]
* [https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C_%EC%A0%95%EA%B7%9C%ED%99%94 유니코드 정규화]
* [https://blog.asamaru.net/2016/11/15/php-nfd-to-nfc/ nfd nfc 차이]
* [http://www.unicode.org/emoji/charts/full-emoji-list.html emoji full list]
* [https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html java doc pattern]

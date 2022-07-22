---
layout: default
title: java junit과 annotation 소개
parent: java
nav_order: 201106
---

```java
@BeforeClass : 테스트 클래스 내에서 수행 전 한 번만 실행, static method 여야 함
@AfterClass : 테스트 클래스 내에서 수행 후 한 번만 실행, static method 여야 함
@Before : 테스트 케이스 수행 전 반복실행
@After : 테스트 케이스 수행 후 반복실행
@Test : 테스트 메소드 지정
public void StringTest2() throws Exception{
    assertEquals(true,false);
}

```

## junit spring integration testing
```java
@SpringBootTest(classes = SomeApplication.class,
                webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class AuthControllerTest {

    private static String token = null;

    @LocalServerPort
    private int port;

    @Autowired
    private TestRestTemplate restTemplate;

    @Order(1)
    @Test
    @DisplayName("로그인")
    public void login() {

        HttpHeaders headers = new HttpHeaders();

        AuthTokenRequestDto authTokenRequestDto = new AuthTokenRequestDto();
        authTokenRequestDto.setId("someId");
        authTokenRequestDto.setPassword("somePassword");

        ResponseEntity<AuthTokenResponseDto> authTokenResponseDto
                = restTemplate.exchange("http://localhost:" + port + "/v1/auth/token",
                                        HttpMethod.POST,
                                        new HttpEntity<>(authTokenRequestDto, headers),
                                        AuthTokenResponseDto.class);

        assertEquals(authTokenResponseDto.getStatusCode(), HttpStatus.OK);
        assertNotNull(authTokenResponseDto.getBody().getToken());
        token = authTokenResponseDto.getBody().getToken();
    }

    @Order(2)
    @Test
    @DisplayName("내정보 보기")
    public void findUser() {

        HttpHeaders headers = new HttpHeaders();
        headers.add("SOME-TOKEN", token);

        ResponseEntity<String> authUser
                = restTemplate.exchange("http://localhost:" + port + "/v1/auth/user",
                                        HttpMethod.GET,
                                        new HttpEntity<>(headers),
                                        String.class);

        assertEquals(authUser.getStatusCode(), HttpStatus.OK);
        assertNotNull(authUser.getBody());
    }

    @Order(2)
    @Test
    @DisplayName("마케터의 파트너 불러오기")
    public void getPartnerByMarketer() {

        HttpHeaders headers = new HttpHeaders();
        headers.add("SOME-TOKEN", token);

        ResponseEntity<PartnerResponseDto> partnerResponseDto
                = restTemplate.exchange("http://localhost:" + port + "/v1/partners?marketerId={marketerId}",
                                        HttpMethod.GET,
                                        new HttpEntity<>(headers),
                                        PartnerResponseDto.class,
                                        "someData");

        then(partnerResponseDto.getStatusCode()).isEqualTo(HttpStatus.OK);
        then(partnerResponseDto.getBody().getPartnerDtoList().size()).isEqualTo(2);
    }
}
```

## ParameterizedTest
```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.Arguments;
import org.junit.jupiter.params.provider.MethodSource;
import org.junit.jupiter.params.provider.ValueSource;

import java.util.stream.Stream;

public class DataDrivenTest {
private final ArithmeticOperation arithmeticOperation = new ArithmeticOperation();

    @ParameterizedTest
    @ValueSource(ints = { 1, 2, 3, 4, 5 })
    void canAdd(int b) {
        assertTrue(arithmeticOperation.add(1, b) >= 2);
    }

    @ParameterizedTest(name = "can add {0} to {1} and receive {2}")
    @MethodSource("additionProvider")
    void canAddAndAssertExactResult(int a, int b, int result) {
        assertEquals(result, arithmeticOperation.add(a, b));
    }

    static Stream<Arguments> additionProvider() {
        return Stream.of(
            Arguments.of(1, 3, 4),
            Arguments.of(3, 4, 7),
            Arguments.of(10, 20, 30)
        );
    }
}
```

## 정리 필요
* assertj
* hamcrest
* jupiter api
* @ParameterizedTest

## 참고링크
* JUnit 4.x 어노테이션 <http://taewan.kim/post/junit4_annotation/>
* junit mockito verify <https://bestalign.github.io/2016/07/08/intro-mockito-1/>
* junit5 <https://javacan.tistory.com/entry/JUnit-5-Intro>
* junit integration testing <https://howtodoinjava.com/spring-boot2/testing/spring-integration-testing/>
* junit+mockito vs groovy+spock <https://yangbongsoo.gitbook.io/study/junit+mockito_vs_groovy+spock>
* junit5 nested test <https://mkyong.com/junit5/junit-5-nested-test-examples/>

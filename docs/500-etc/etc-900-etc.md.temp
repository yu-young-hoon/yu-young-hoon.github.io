## todo

* ETL: Data 추출(Extract), 변환(Transform), 적재(Load)
* Infrastructure as a Service(Iaas): 환경 제공, 가상 환경 기술
* Platform as A Service(Paas): API로 개발 환경 제공
* Software as a Service(Saas): 응용 어플리케이션 제공
* DevOps: 개발과 운영을 한팀에서 진행하는 개발 방법론
* 카오스엔지니어링: 비정상적인 상태를 만들어 약점을 찾아내는 방법
* 오프로딩: 모바일 데이터 오프라인망(wifi등등)으로 분산하여 처리
* Persistence: 영속성
* Context: 사전적 의미 맥락, 문맥으로 작업의 실행에 영향을 줄 수 있는 cpu register, call stack, memory의 상태
* Dead lock: 교착상태, 자원을 점유해서 대기에 빠지는것
* Live lock: 공명상태, 자원을 점유를 서로 방해를 해서 서로 진행이 안되는 상태
* Infrastructure as Code(IaC): 시스템을 수동으로 관리하는 대신 스크립트를 사용하여 컴퓨팅 인프라를 구성하는 방식
* APM: Application Performance Management의 약자. 애프리케이션의 성능을 관리하는 서비스.
* PoC: Proof of Concept. 개념 검증
* OpenStack: 표준 하드웨어에서 운용할 수 있는 모듈형 클라우드 인프라를 제공
* Ceph: 자유 소프트웨어 스토리지 플랫폼이며 단일 분산 컴퓨터 클러스터에서 오브젝트 스토리지를 구현하고 오브젝트, 블록 및 파일 레벨 스토리지를위한 인터페이스를 제공
* Kubernetes: 쿠버네티스는 컨테이너화된 애플리케이션의 자동 디플로이, 스케일링 등을 제공하는 관리시스템
* Ansible: 오픈 소스 소프트웨어 프로비저닝, 구성 관리, 애플리케이션 전개 도구
* FQDN: Fully Qualified Domain Name 서브도메인을 포함한 전체 도메인

----

<source>
하이드레이션
flash out content
가상돔


rx java 리엑트
optional, orElseThrow, ofNullablem ifpresent
부모를 자식으로 캐스팅 하지 못함


@EnableTransactionManagement: 트랜젝션 빈 설정 클래스 지정
@ControllerAdvice
@Laze: 멀티 모듈일때 효용 있음, 지연 로딩


redis
syncronized 지원
싱글 스레드
cluster mod 지원?
tpm
all or nothing
race condition
visitor pattern
increment


## 캐싱
로컬 캐시
항상 켜져 있는 캐시
session과 statement가 있음
session은 autoCommit이 켜져있지 않다면 트래젝션이 끝나기 전까지 유지
statement는 커밋 되지 않더라도 쿼리 한줄이 끝나면 종료
second level cache
mybatis-config에서 활성화
mapper xml에서 cache 태크로 설정
커밋이 되어도 session 캐시 데이터 유지

TDD
----
====error condition, illegal 컨디션====
illegal 발견이 테스트의 목표
SOA, MSA 차이	"SOA에서 API로 제공 더작개 쪼갬
기존 모놀리식 서버의 경우 컨트롤 비즈니스 로직이 하나로 묶여서 관리 및 배포됨 유지 보수 불편"
폭포수 에자일	"폭포수
요구사항 설계 개발 테스트 배포
애자일
확인 진행 확인 징행
====대용량 처리====
==== 분산 캐시, 성능측정 가능한 형태로 제시 ====
웹 캐시의 경우 cdn 서비스를 사용하였음
==== 스케일링, 분산처리, 퍼포먼스튜닝 ====
aws auto scaling, 로드벨런싱(L$ 스위치, L7 nginx)
jvisual vm실행




## 참고 web

----

==== 크로스도메인 이슈 해결 경험 ====
와일드 카드의 경우 막혔기 때문에 정규식으로 처리하였다

```
@Configuration
public class MyConfiguration {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurerAdapter() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping(""/**"");
            }
        };
    }
}
```

----

==== 서버 에러 코드 ====
200 성공 201 생성성공 400잘못된요청, 401권한, 403금지,404없음,500내부 서버 오류
1XX 조건부 응답, 2XX 성공, 3XX 리다이렉션 완료, 4요청오류, 5서버오류

----

==== 브라우저 랜더링 ====
Uniform Resource Identifier 입력

돔트리 구축 HTML 파싱, 렌더 트리 구축, 렌더 배치, 그리기

렌더 트리는 색상, 면적 같은 시각적 속성 배치

HTML을 모두 파싱하기 전에 점진적으로 진행

리플로우, 리페인트

리플로우는 모질라 게코, 웹킷은 배치

렌터 트리를 속성 변경으로 다시 렌더링 할때 발생

리페인트는 레이아웃은 영향을 주지 않지만 색상등 가시성 변화

리플로우 레이아웃 크기등 엘리먼트 위치 길으 다시 계산

최대한 말단 노드 변경, 인라인 스타일 사용하지 않는다

css 속성으로 변경하지 않는다

애니메이션의 경우 fixed, absolute로 해서 레이아웃을 건드리지 않는다

애니메이션은 덜부드럽게 처리한다

table-layout: fixed로 크기 고정해서 머리글로 크기 고정

cssText를 통해 한방에 변경

스크롤 같은경우를 적용할때 변수를 거쳐서 브라우저에게 캐시를 맞김

Google Chrome SpeedTracer로 분석

----

==== RESTFul 쓰는 이유 ====
GET : resource를 보내달라고 요청

POST : resource를 보내면서 생성해 달라고 요청, 결과 201

PUT :resource의 업데이트 하거나 resource가 없다면 생성

PATCH:서버에게resource의 업데이트를 요청함 _id를 찾아 일부만

DELETE:resource의 삭제를 요청

url locator, uri identifier

php의 경우 리소스의 경로를 나타낸 url이 기본, 적당하지 않기 때문에

제공하려는 리소스에대해서 CRUD를

http mathod로 구분하여 제공하겠다.

명사로만 자원, Uniform Interface, Stateless, Cacheable

Self-descriptiveness, Client-Server, HATEOAS url에 따라 다른 응답

----

==== HTTP1,1, HTTPS ====
하이퍼 텍스트 프로토콜 웹상에서 요청을 하기 위한 문서형식 요청

secure socket을 통해서 https로 요청하기도 함

공개키 암호화 방식

http2는 빠르다고 알고있음"

html meta태그에 viewport를 쓰셨던데 이게 무엇인가요? 	각각 다른 뷰의 크기를 고정해서 모바일 개발하기 쉽게

----

====  ====
네이버 검색엔진의 원리 	크롤링을 통한 정보수집, 디비 인덱스를 통한 검색, 자연어 처리를 통한 인식

----

==== 웹표준 ====
html5 형식, javascript, css 표준을 지키고

웹 접근성을 높이는것

툴팁, 장애인을 위한 음성출력등

----

==== CI프로그램 구현 ====
컨티뉴스 인터그래이션
소스를 검증
빌드 자동화, 테스팅 자동화

----

==== longpool / websocket 차이 ====
반복요청, 연결 물고있음, 헤더의 가벼움,

하지만 websocket도 longpool로 내부적 구현하기도 함

----

==== OSI7 계층, TCP, UDP 장단점 ====
물데네전세표응

tcp 연결 지향형, udp 비연결형

tcp의 경우 ack를 주고 받아서 받지 않았을경우 다시 보내줘서 신뢰성

ucp의 경우 보내고 끝 좀더 빠름

tcp 3-way hand shaking? tcp 연결 과정

종료에서는 4way hand shake"

----

==== rtp와 rtcp 차이점 ====
rtp 데이터 전송

rtcp 리포트 패킷 주고 받음 rtp의 플로우 컨트롤

rtsp 스트리밍 제어"

----

==== SQL 인젝션 방어 코드 ====
<code>
String query = “SELECT * FROM tb_user WHERE uId= ?”
stmt = conn.prepareStatement(query);
stmt.setString(1, uId);
</code>
xxs 크로스 사이스 스크립팅도 막아야함

----

==== http keep alive ====
http1.1 기능으로 http의 매번 접속하는 connection less 방식을

비용을 줄이기 위해 time out 시간 내에 소켓을 열어 기다리는 기능

브라우저가 http1.1의 request에 요구하면

서버가 time out을 설정하고 기능을 활성 하면 동작

----

==== handshake ====
{{:3way-handshake.jpg?400|}}

{{:4way-handshake.png?400|}}
time wait, con wait 발생

----

==== Tcp backlog ====
reqsk_queue, ack backlog, listen backlog 등이 있음

syn-ack 보낼때 큐에 저장 ack올때 큐에서 제거

미연결들에 대한 큐의 길이

TCP 연결 유지 방식

keep alive 설정, time out 되면 유지 프로브를 전송

연결 안되면 종료

----

==== L2스위치의단점이 무엇인가 ====
l1(허브, 리피터) 신호만 증폭

l2스위치(브리지, 스위치)

mac주소로 스위칭, 구조 간단, 성능 좋음

브로드캐스팅 패킷에 의해 성능저하, 라우팅 불가

목적지를 모르면 플루딩됨.

l3스위치(스위치, 라우터)
포트간 패킷 스위칭, l2에서 라우팅 기능 추가
브로드 캐스팅 성능 저하를 막을수 있다, 트래픽 체크 가생 랜등 부가기능
특정 프로토콜을 이용해야 스위칭 가능
목적지를 모르면 드랍
l4스위치
어플리케이션별로 우선순위를 두어 스위칭, tcp/ip 기반 동작
로드 밸런싱 기능 제공, 트래픽을 여러 서버로 분산 가능
프로토콜에 의존적, 고가, 설정 복잡"

----

==== tls ssl 차이 ====
ssl 비표준, ssl3.0부터 tls로 불림

공개키 방식 보안 통신

서버의 공개키로 정보 암호화

----

==== Grid툴 선정 기준은? ====
html에서 그리드를 표현함에 있어 많은 라이브러리가 있는걸 알고있지만 보통 직접 만들거나 템플릿을 사용했다.
Jqgrid가 있는것은 알고있다.

----

==== kafka, rabbitmq, activemq ====
rabbitmq의 클러스털링이 장점, 관리 ui 편리

activemq 브로커 설치 간단

kafka 대용량 처리, 컨슈머가 메시지를 가져가는 pull 방식, broker의 부담 경감, 프로토콜을 tcp 사용함으로서 오버헤드 감소

----

==== natty ====
event-driven 방식

논블로킹 비동기 io

여러가지 프로토콜 지원, gc부하 최소하 zero-copy bytebuf지원

여러 인터페이스 지원

----

==== node.js의 이벤트 드리븐 설명하시오 ====
노드제이에스의 경우 싱글스레드로 이벤트 루프가 하나만 동작합니다.
이벤트 루프에서 이벤트 큐에 이벤트가 있을경우 콜벡 함수를 실행합니다.
이런 동작은 옵저버 패턴을 통해 동작합니다.

----

==== 자바스크립트 라이브러리 ====
lodash	자바스크립트 라이브러리

reactJS	virtual dom 사용, 오프라인 돔트리에 적용했다가 연산이 끝나고 한번에 실제 돔에 적용
리렌터링 규모는 커지지만 한번만 사용

----

==== angularjs ====
앵귤러1사용 2는 타입스크립트를 도입해서 검증 코드 수고 줄임

일정상 1을 사용

엥귤러 2는 서버렌더링, 네이티브 코드 변환 가능, $scope와 $digest 제거

데이터를 받았다가 사용자응답에 맞게 컴포넌트 재구성해서 보여줌 spa 최적

typescript 사용으로 형지정 안해도 잘 작동

----

==== nodejs 비동기 ====
Single Thread기반의 비동기 IO 처리에서 온다. 하나의 쓰레드가 request를 받으면, 처리를 하고, File IO나 Network 처리 (데이타 베이스 접근)등이 있을 경우에는 IO 요청을 보내 놓고, 작업을 처리하다가, IO  요청이 끝나면 이벤트를 받아서 처리하는 이벤트 방식을 사용한다.

socket.io는 웹소켓을 포함한, AJAX 롤폴링등 여러개의 웹푸쉬를 abstraction하여, 브라우져에 상관 없이 개발자가 쉽게 socket.io API만 이용하면, 푸쉬를 구현할 수 있게 해주며, 싱글 쓰레드 기반의 멀티 플랙싱을 기반으로, 대용량 사용자에 대한 푸쉬 처리를 가능하게 해준다.

----

==== 스프링 멀티스레드, nodejs 싱글스레드 차이 ====
WAS는 Thread 수만큼 밖에 동시 connection 처리를 할 수 없기 때문에, node.js의 이 구조가 이런 대량 동시 Connection 처리에는 유리하다.

----

==== 봉쇄 비동쇄 ====
읽을게 있을때 까지 read에서 기다리는지 넘어가서 다른작업 하는지

----

==== 트래픽 초과 ====
병목이 어디서 발생하는지 확인, cpu 메모리 디스크 네트워크

스케일 업으로 더 빠른 디스크 마운트, 메모리 업, 랜카드 변경

스케일 아웃으로 서버 분산, 로드 벨런싱, 리플리케이션, 엑티브엑티브

----

==== Shell Scripting ====
배치 파일 또는 Spring Shell

```
@Usage("JDBC connection")
class jdbc {

  @Usage("connect to database with a JDBC connection string")
  @Command
  public String connect(
          @Usage("The username")
          @Option(names=["u","username"])
          String user,
          @Usage("The password")
          @Option(names=["p","password"])
          String password,
          @Usage("The extra properties")
          @Option(names=["properties"])
          Properties properties,
          @Usage("The connection string")
          @Argument
          String connectionString) {
     ...
  }

  @Usage("close the current connection")
  @Command
  public String close() {
     ...
  }
}

% jdbc connect jdbc:derby:memory:EmbeddedDB;create=true
```

----

==== Elasticsearch ====

시간이 갈수록 증가하는 문제를 해결하는 분산형 RESTful 검색 및 분석 엔진

서버사이드랜더링

[[Internet] CNAME과 A record의 차이 – TWpower's Tech Blog](https://twpower.github.io/40-difference-between-cname-and-a-record)




## OOP(객체지향 프로그래밍) 의미와 장단점
프로그래밍에서 필요한 데이터를 상태와 행위를 가진 객체로 취급해서 프로그램에 반영한것으로 객체와 객체의 상호작용을 통해 프로그램이 동작하는것
==장점==
코드의 재사용성이 높다

코드의 변경이 용이

직관적인 코드 분석, 가독성이 높다

개발 속도 향상

상속을 통한 장점 극대화
==단점==
처리속도가 절차지향보다 느리다

설계가 오래 걸린다

프로그램의 용량이 크다

----

## 객체 클래스 인스턴스
클래스로부터 메모리를 할당하여 객체를 사용할때의 이름이 인스턴스

클래스는 설계도, 객체는 동작과 정보를 가진것, 메모리에 적재된것이 인스턴스

인스턴스화 하는것은 java에서 new 키워드

----

상속	"부모의 속성과 기능을 이어받고 일부 기능을 변경하거나 확장해서 사용하는것
코드의 재사용성이 높아진다
개발의 속도가 빨라진다"				
캡슐화	"코드를 재수정 없이 재활용하는것
클래스라는 캡슐에 기능과 특성의 모음을 한데 묶는것"				
다형성 2	"하나의 변수, 함수명이 다른의미로 해석될수 있는것
부모의 기능을 변경해서 사용 오버라이딩
같은 함수의 이름에 다른 매개변수 오버로딩"				
인터페이스	기능과 선언을 분리, 기능의 사용 통로 제공				
델리게이트	기능을 실행하는걸 위임

구조 패턴	Adapter			x
Bridge			x
Composite			x
Decorator			x
Facade			x
Flyweight			x
Proxy			x
행위 패턴	Command			x
Interpreter			x
Iterator			x
Mediator			x
Template Method	"알고리즘을 여러 단계로 나누어
나눠진 알고리즘 단계를 메소드로 선언하고
알고리즘을 수행할 템플릿 메소드를 만든다
하위 클래스에서 나눠진 메소드들을 구현한다."		x	가장 많이
Visitor			x
State			x
Strategy	"추상적인 접근점을 만들어 접근점에서 서로 교환가능 하도록 한다
(interface) (set~~)"		x	가장 많이
Observer			x
Chain of Responsibility			x
Memento			x



preparedstatement
</source>

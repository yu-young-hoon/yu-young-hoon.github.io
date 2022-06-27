---
layout: default
title: Issue jpa dirty checking update를 하지 않아도 update 호출 되는 문제
parent: issue
nav_order: 101200
---

## 이슈
![](/docs/attach/jpa-dirty-chacking.png)

* update를 하지 않았는데도 jpa에서 update 호출
* 영속성 상태인 entity가 변경된다면 transaction이 종료될때 dirty checking 되며 변경점을 자동으로 저장
* dirty checking 발생 하지만 entity는 변경점이 없음

## 원인
```java
    @NotNull
    @Convert(converter = LimitedBidAttributeConverter.class)
    private BidLimit bidLimit;

    @Getter
    @AllArgsConstructor(staticName = "of")
    @NoArgsConstructor(access = AccessLevel.PROTECTED)
    public static class BidLimit {
        ...
    }
```

* 중첩 클래스를 컨버터로 적용하여 사용하고 있었지만 equals/hashcode가 작성되어 있지 않기 때문에 다르다고 인식
* transaction이 종료될때 dirty chacking 발생
* dirty chacking(변경 감지 순서 자바 orm 표준 jpa 프로그래밍 114p)
  ** 트랜젝션을 커밋하면 엔티티 매니저 내부에서 먼저 플러시(flush())가 호출된다.
  ** 엔티티와 스냅샷을 비교해서 변경된 엔티티를 찾는다. (equals)
  ** 변경된 엔티티가 있으면 수정 쿼리를 생성해서 쓰기 지연 SQL 저장소에 보낸다.
  ** 쓰기 지연 저장소의 SQL을 데이터 베이스에 보낸다.
  ** 데이터베이스 트랜잭션을 커밋한다.

## 해결
* 정상적으로 동작 하도록 중첩 클래스에 @EqualsAndHashCode 적용
* 또는 강제로 변경점이 추적되지 않도록 @Column(updatable = false) 적용

## 참고
* https://jojoldu.tistory.com/415

---
layout: default
title: Scala cats OptionT
parent: scala
nav_order: 200102
---

OptionT[F[_], A]는 F[Option[A]]의 경량 포장입니다.

Option Future 등 유형에 배치된 처리 시 OptionT를 사용하면 코드를 더욱 쉽게 정리할 수 있다.

```scala
val greetingFO: Future[Option[String]] = Future.successful(Some("Hello"))

val firstnameF: Future[String] = Future.successful("Jane")

val lastnameO: Option[String] = Some("Doe")

val ot: OptionT[Future, String] = for {
  g <- OptionT(greetingFO)
  f <- OptionT.liftF(firstnameF)
  l <- OptionT.fromOption[Future](lastnameO)
} yield s"$g $f $l"

val result: Future[Option[String]] = ot.value 

// 결과 Future(Some("Hello Jane Doe"))
```

### 참고링크
* OptionT[scara with Cats]에 대한 설명 <https://coder-question-ko.com/cq-ko-blog/374383>
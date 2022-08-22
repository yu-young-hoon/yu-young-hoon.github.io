---
layout: default
title: tool gradle configuration 종류
parent: tool
nav_order: 407115
---

gradle로 dependencies로 관리할때 어떠한 프로젝트에 대해 configuration을 붙여 주게 되는데<br>

예를 들면 compileOnly "org.projectlombok:lombok" 에서 org.projectlombok:lombok 프로젝트에 대한 configuration은 complieOnly가 되며 컴파일단계에서만 사용된다는 뜻이다.

이러한 configutarion은 여러가지 종류가 있고 아래처럼 task를 생성해서 확인해볼수 있다.

<source>
task checkConfiguration {
	for (config in configurations) {
		println config
	}
}
</source>

==참고링크==
* https://docs.gradle.org/current/userguide/userguide.html
* https://kwonnam.pe.kr/wiki/gradle/multiproject

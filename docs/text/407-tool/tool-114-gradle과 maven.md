---
layout: default
title: tool gradle과 maven
parent: tool
nav_order: 407114
---

==maven && gradle==
* 빌드 자동화 도구

==gradle==
* groovy

===설치(aws linux)===
* sudo wget https://services.gradle.org/distributions/gradle-5.4.1-bin.zip
* sudo mkdir /opt/gradle
* sudo unzip -d /opt/gradle gradle-5.4.1-bin.zip
* export PATH=$PATH:/opt/gradle/gradle-5.4.1/bin
* gradle -v

===gradlew===
* wrapper, gradle 버전 문제로 실행이 안되는 경우를 방지 하기 위한 호환용 스크립트

===setting.gradle===
<source>
rootProject.name = 'java-some-project'
include 'common'
</source>
* rootProject.name: root 프로젝트 이름
* include: 포함할 sub 프로젝트 이름

===build.gradle===

====plugins====
<source>
// root project: root/build.gradle.kts
plugins {
    kotlin("jvm") version "1.3.61"
}

// sub project: root/sub/build.gradle.kts
plugins {
kotlin("jvm")
}
</source>


* compileOnly 컴파일에서만 사용, lombok
* compile
* testCompile
* implementation
* testImplementation
<source>
rootProject.name = 'some-platform'

include 'common-library'
include 'batch:pick-ad-bid'
findProject(':batch:pick-ad-bid')?.name = 'pick-ad-bid'
include 'batch:pick-house-ad'

buildscript {
ext {
springBootVersion = '2.0.5.RELEASE'
}
repositories {
mavenCentral()
}
dependencies {
classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
}
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'groovy'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

sourceCompatibility = 1.8

bootJar {
baseName = 'taxbill-ad-sap'
version = '1.0.0-SNAPSHOT'

    from('libs') {
        include 'libsapjco3.*'
    }
}

dependencies {
compile project(':common-library')

    compile 'mysql:mysql-connector-java'
    implementation('org.springframework.boot:spring-boot-starter-batch')
    implementation('org.springframework.boot:spring-boot-starter-data-jpa')
    testImplementation('org.springframework.boot:spring-boot-starter-test')
    testImplementation('org.springframework.batch:spring-batch-test')
    
    compileOnly("org.projectlombok:lombok:${versions.lombok}")
    annotationProcessor("org.projectlombok:lombok:${versions.lombok}")
    testCompileOnly("org.projectlombok:lombok:${versions.lombok}")
    testAnnotationProcessor("org.projectlombok:lombok:${versions.lombok}")

    // Spock
    testCompile('org.spockframework:spock-core:1.1-groovy-2.4')
    testCompile('org.spockframework:spock-spring:1.1-groovy-2.4')
}
</source>

==maven==
* xml형식의 버전관리

==참고 링크==
* [https://bkim.tistory.com/13 gradle maven 차이]
* [http://dimdim.tistory.com/entry/Maven-%EC%A0%95%EB%A6%AC maven 정리]
* [https://mvnrepository.com/ maven repository]
* [https://kwonnam.pe.kr/wiki/gradle/multiproject gradle multiproject]
* [https://docs.gradle.org/current/userguide/multi_project_builds.html gradle multiproject2]

# 📚 Spring - Kotlin + Spring Boot (JPA) 사용시 추가 해야 할 Plugin, Dependencies

> 💡 Java에서는 별도의 설정 필요없지만 Kotlin에서는 Jvm, Jpa, Spring등을 추가해주어야 합니다.

## ♻️Gradle - Groovy 기준으로 설명하겠습니다.
Gradle – Groovy
* 전통적인 Gradle 빌드 스크립트 방식이고, 스크립트 문법이 간결하며 동적 언어 특성을 가집니다.
* 오랜 기간 사용되어온 방식이라 레퍼런스와 커뮤니티 자료, 예제가 풍부합니다.

Gradle – Kotlin
* Kotlin 언어를 사용하는 Gradle 빌드 스크립트 방식입니다.
* 정적 타입을 지원해서 컴파일 타임 오류 방지, 강력한 IDE 지원, 자동완성 및 리팩토링 편의성이 매우 뛰어납니다.

```kotlin
compileKotlin {
    kotlinOptions {
        jvmTarget = "17"
    }
}

compileTestKotlin {
    kotlinOptions {
        jvmTarget = "17"
    }
}
```

## 📟Plugin 추가 

* `Kotlin` 코드를 JVM 바이트코드로 컴파일(Java와 함께 빌드/상호운영 가능하게) 하기 위한 기본 플러그인
```kotlin
id 'org.jetbrains.kotlin.jvm' version '1.9.22'
```
---
* JPA용으로 엔티티를 자동 `open`처리 + 기본 생성자(`no-arg`) 부여
* `kotlin-jpa`는 사실상 `all-open`(클래스 자동 `open`)과 `no-arg`(기본 생성자 생성) 플러그인을 함께 적용해줍니다.
* `Kotlin`은 클래스가 기본 `final`이고 기본 생성자가 없어서, 프록시/리플렉션 쓰는 JPA에서는 필수 입니다.
* `JPA` 쓰면 `kotlin-jpa`는 사실상 필수
```kotlin
id "org.jetbrains.kotlin.plugin.jpa" version "1.9.22"
```
---
* Spring의 `@Component`/`@Configuration`/... 빈들을 자동 `open`처리해서 AOP/프록시가 가능하도록 해줌
* 이또한 자바와 달리 `Kotlin`클래스는 기본 `final`이라 필요
* 스프링 AOP/프록시 쓰면 `kotlin-spring`도 사실상 필수
```kotlin
id "org.jetbrains.kotlin.plugin.spring" version "1.9.22"
```
---
* `QueryDSL`등 프로세서 쓰면 `kapt`필수 (`Kotlin Annotation Processing Tool`)
```kotlin
id "org.jetbrains.kotlin.kapt" version "1.9.22"
```
---

## 📻Dependencies 추가 

* 리플렉션 지원 (Spring은 런타임에 리플렉션 많이 사용)
* 코틀린은 자바 리플렉션과 별도로 코틀린 리플렉션(`kotlin-reflect`)을 따로 추가해야 합니다. 
* **`Spring Data JPA`, `Jackson` 직렬화/역직렬화에서 꼭 필요!!**
```kotlin
implementation("org.jetbrains.kotlin:kotlin-reflect:1.9.22")
```
---
* `Jackson`이 `Kotlin`특성(`data class`, `default parameter`, `nullable type`)을 이해하도록 돕는 모듈 
* 없으면 `data class` 역직렬화에서 에러 자주 납니다.
```kotlin
implementation 'com.fasterxml.jackson.module:jackson-module-kotlin:2.13.3'
```
--- 
* `QueryDSL JPA`지원 라이브러리 `JPQL`대신 타입 세이프하게 쿼리를 작성할 수 있게 해줌
* `QueryDSL`은 빌드 시점에 Q클래스(`QEntity`) 를 생성해야 합니다.
* `Java`에서는 `annotationProcessor`를 쓰지만
* `Kotlin`에서는 `kapt`(`Kotlin Annotation Processing Tool`)을 사용해야 합니다.
```kotlin
implementation("com.querydsl:querydsl-jpa:5.0.0")
kapt("com.querydsl:querydsl-apt:5.0.0:jpa")
kapt("org.springframework.boot:spring-boot-configuration-processor")
```


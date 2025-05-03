# 📚 Kotlin - 3가지 타입

>Kotlin의 특이한 3가지 타입 Any - Unit - Nothing

---
## 1️⃣ Any

- Kotlin의 **모든 타입의 최상위 타입**입니다. (`Java`의 `Object`와 비슷)
- `Any` 타입에는 `equals()`, `hashCode()`, `toString()` 메서드가 기본적으로 정의되어 있습니다.
- 기본적으로 `null`을 포함할 수 없습니다.  
  → `null`을 허용하려면 `Any?`로 선언해야 합니다.

### 예시

```kotlin
fun printAgeIfPerson(obj: Any) {
    if (obj is Person) { // obj가 Person 타입이라면
        val person = obj as Person // 명시적 타입 캐스팅 obj에 Person객체가 들어감
        println(person.age)
    }

    // 또는 스마트 캐스트로 더 간단하게 작성 가능
    if (obj is Person) {
        println(obj.age)
    }
}

fun printAgeIfPerson2(obj: Any?) {
    val person = obj as? Person // 안전한 캐스팅 (null 가능) Person객체가 null이면 null반환
    println(person?.age)
}
```

--- 

> 💬 **스마트 캐스트**  
> `if (obj is Person)`과 같이 타입 체크를 하면 Kotlin이 자동으로 타입 캐스팅을 해줍니다.  
> `as?`를 사용하면 타입이 다르거나 null이어도 예외 없이 `null`을 반환합니다.

---

## 2️⃣ Unit

- Kotlin에서 `Unit`은 Java의 `void`와 비슷한 역할을 합니다.
- 하지만 Java의 `void`는 **타입이 아예 없지만**, Kotlin의 `Unit`은 **진짜 존재하는 타입**입니다.
- 함수가 아무 값도 반환하지 않을 때 반환 타입으로 사용합니다.
- `Unit`은 단 하나의 인스턴스만 존재합니다 (`object`처럼).

### 예시

```kotlin
fun printHello(): Unit { // Unit은 반환 타입을 적지 않으면 자동으로 Unit이 들어감 
    println("Hello, Kotlin!")
}

fun printHello() { // : Unit 생략 가능
    println("Hello, Kotlin!")
}

// Unit을 타입 인자로 사용할 수도 있음
val func: () -> Unit = { println("Lambda function!") }
```

> 💬 **함수형 프로그래밍에서 Unit의 의미**  
> → 단 하나의 값만 갖는 타입을 의미합니다. (`void`와는 개념이 다름)

---

## 3️⃣ Nothing

- `Nothing`은 **정상적으로 값을 반환하지 않는 함수**를 표현할 때 사용합니다.
- 예외를 던지는 함수나 무한 루프를 도는 함수가 여기에 해당합니다.
- `Nothing`은 어떤 값도 가질 수 없으며, 모든 타입의 하위 타입입니다.

### 예시

```kotlin
fun fail(message: String): Nothing {
    throw IllegalArgumentException(message)
}

fun infiniteLoop(): Nothing {
    while (true) {
        // 무한 루프
    }
}
```

> 💬 **Nothing은 언제 사용할까?**
> - 함수가 **절대 정상 종료되지 않을 때**
> - **코드를 더 명확하게 표현하고 싶을 때**  
    > (예: 무조건 예외를 발생시키는 유틸 함수)

---

# ✅ 요약

| 타입 | 설명 |
|:----|:-----|
| `Any` | 모든 타입의 최상위 타입. `Object`처럼 동작하지만 null을 포함하지 않음 (`Any?` 필요) |
| `Unit` | 반환값이 없는 함수에서 사용. 실제 존재하는 타입 (단 하나의 인스턴스) |
| `Nothing` | 정상 종료되지 않는 함수에서 사용. 예외 발생 또는 무한 루프 등에 사용 |
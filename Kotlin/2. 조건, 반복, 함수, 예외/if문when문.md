# 📚 Kotlin - `if문`, `when문` 정리

Kotlin은 Java와 비교해서 제어문(`if`, `when`)을 훨씬 **간결하고 표현력 있게** 사용할 수 있습니다.  
특히 Kotlin에서는 **if문과 when문이 "Expression(표현식)"** 이라는 점이 큰 특징입니다.

---

## 1️⃣ Kotlin의 if문

- Kotlin의 `if문`은 **Java와 문법이 거의 동일**합니다.
- **if문 자체가 Expression**이다.
    - 값처럼 사용할 수 있어서 **삼항 연산자(조건 ? A : B)** 가 따로 존재하지 않는다!

### ✅ Kotlin if문 예시

```kotlin
fun getPassOrFail(score: Int): String {
    return if (score >= 50) {
        "P"
    } else {
        "F"
    }
}
```

> `if` 블록이 끝나면 그 결과가 반환되어 바로 `return`이 가능!

### ✅ Kotlin 다중 조건 if문 예시

```kotlin
fun getGrade(score: Int): String {
    return if (score >= 90) {
        "A"
    } else if (score >= 80) {
        "B"
    } else if (score >= 70) {
        "C"
    } else {
        "D"
    }
}
```

---

## 2️⃣ Kotlin의 when문

- Java의 `switch문`을 Kotlin에서는 `when문`으로 대체합니다.
- `when문` 역시 **Expression**입니다! (결과를 반환 가능)
- `when`은 **값 뿐만 아니라 조건식**도 받을 수 있다.

### ✅ Kotlin when 기본 사용

```kotlin
fun getGradeWithSwitch(score: Int): String {
    return when (score / 10) {
        in 9..10 -> "A" // // 90 ~ 99 까지이면 A출력
        in 8..9 -> "B"
        in 7..8 -> "C"
        else -> "D"
    }
}
```

### ✅ Kotlin when 타입 체크 사용

```kotlin
fun startWithA(obj: Any): Boolean {
    return when (obj) {
        is String -> obj.startsWith("A") // // obj가 String 이면 startsWith 검사 아니면 false 반환 
        else -> false
    }
}
```

> 💬 `is` 키워드를 통해 타입 체크도 자연스럽게 가능!

---

## 3️⃣ Java vs Kotlin 비교

### 🔥 Java 코드 (if문)

```java
private void judgeNumber2(int number) {
    if (number == 0) {
        System.out.println("주어진 숫자는 0입니다");
        return;
    }
    if (number % 2 == 0) {
        System.out.println("주어진 숫자는 짝수입니다");
        return;
    }
    System.out.println("주어지는 숫자는 홀수입니다");
}
```

### 🔥 Kotlin 코드 (when문)

```kotlin
fun judgeNumber2(number: Int) {
    when {
        number == 0 -> println("주어진 숫자는 0입니다.")
        number % 2 == 0 -> println("주어진 숫자는 짝수입니다.")
        else -> println("주어지는 숫자는 홀수입니다.")
    }
}
```

> 💬 Kotlin은 **when 블록**을 이용해 여러 조건을 **자연스럽게 분기**할 수 있다.  
> 따로 `return`을 안 써도, 순차적으로 평가되어 필요한 블록만 실행!

---

# ✅ 요약

| 구분 | Kotlin 특징 |
|:---|:---|
| if문 | Expression(값처럼 사용 가능) |
| 삼항 연산자 | 존재하지 않음 (if로 대체) |
| when문 | switch문을 대체, 더 강력한 기능 |
| when문 특징 | 값뿐만 아니라, 타입 체크, 조건식까지 사용 가능 |
| 다중 조건 | when으로 깔끔하게 분기 가능 |

---

# 📌 정리

- Kotlin의 `if문`, `when문`은 **값을 반환하는 Expression**이다!
- **삼항 연산자 없이** if를 값처럼 사용할 수 있다.
- **when문은 switch보다 더 강력하며**, 타입 체크나 범위 조건까지 지원한다.
- Java에 비해 **코드가 훨씬 간결하고 명확**해진다.

> Kotlin은 "모든 것이 Expression"이라는 설계 철학 덕분에, **더 깔끔하고 함수형 스타일** 코드를 작성할 수 있습니다! 🚀


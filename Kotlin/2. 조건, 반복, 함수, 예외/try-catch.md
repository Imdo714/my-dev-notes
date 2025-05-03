# 📚 Kotlin - try-catch 예외처리 정리

Kotlin에서도 **`try-catch-finally`** 구문은 Java와 거의 비슷합니다.  
하지만 Kotlin만의 특별한 차이점들이 존재합니다.

---

## 1️⃣ Kotlin의 try-catch 문법

- 기본적인 **문법 구조는 Java와 동일**합니다.
- `catch` 블록은 여러 개 작성할 수 있습니다.
- `finally` 블록도 지원합니다.

```kotlin
try {
    // 예외가 발생할 수 있는 코드
} catch (e: ExceptionType) {
    // 예외 처리
} finally {
    // 항상 실행되는 블록
}
```

---

## 2️⃣ Kotlin의 try-catch는 **Expression**

- Kotlin에서는 `try-catch` 자체가 **Expression**입니다.
- 즉, 값을 반환할 수 있으며 바로 `return`하거나, 변수에 할당할 수 있습니다.

### ✅ 예시 1 : return에 사용하는 경우

```kotlin
fun parseIntOrThrow(str: String): Int {
    try {
        return str.toInt()
    } catch (e: NumberFormatException) {
        throw IllegalArgumentException("주어진 ${str}은 숫자가 아닙니다.")
    }
}
```

### ✅ 예시 2 : 값으로 사용하는 경우

```kotlin
fun parseIntOrThrowV2(str: String): Int? {
    return try {
        str.toInt()
    } catch (e: NumberFormatException) {
        null
    }
}
```

> 💬 **`try-catch` 결과 자체를 반환**하거나, **변수에 바로 할당**할 수 있다!

---

## 3️⃣ Kotlin의 예외는 **모두 Unchecked Exception**

- Kotlin에서는 모든 예외가 **Unchecked Exception**입니다.
- 즉, **명시적으로 throws 선언을 할 필요가 없습니다.**
- Java처럼 `throws IOException` 같은 예외 선언을 요구하지 않습니다.

```kotlin
fun readFile() {
    // IOException이 발생할 수 있어도 throws 작성 불필요
}
```

---

## 4️⃣ Kotlin의 try-with-resources

- Java에서는 try-with-resources를 위해 `try(resource)` 문법을 사용했지만,
- Kotlin에서는 **`use` 확장 함수**를 사용하여 리소스를 자동으로 닫을 수 있습니다.

### ✅ Kotlin에서 try-with-resources 스타일

```kotlin
BufferedReader(FileReader("test.txt")).use { reader ->
    println(reader.readLine())
}
```

> 💬 `use` 블록이 끝나면 자동으로 `close()`가 호출됩니다.

---

# ✅ 요약

| 구분 | Kotlin 특징 |
|:---|:---|
| try-catch 문법 | Java와 동일 |
| try-catch | Expression, 값을 반환할 수 있음 |
| 예외 타입 | 모두 Unchecked Exception (throws 불필요) |
| 리소스 관리 | `use` 확장 함수로 대체 (try-with-resources) |

---

# 📌 정리

- Kotlin에서는 `try-catch` 문을 **값처럼 사용할 수 있다는 점**이 큰 차이입니다.
- Checked Exception이 없기 때문에, 코드를 훨씬 깔끔하게 작성할 수 있습니다.
- 자원 관리를 `use`를 통해 훨씬 자연스럽게 처리할 수 있습니다.

> Kotlin의 예외처리는 Java보다 **간결하고 유연하게** 동작합니다! 🚀


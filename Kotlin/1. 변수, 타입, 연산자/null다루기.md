# 📚 Kotlin - Null 다루기 Safe Call, Elvis 연산자

Kotlin에서는 **null 안정성(Null Safety)**을 언어 차원에서 지원합니다.  
즉, **컴파일 타임에** null 가능성을 체크해주기 때문에 **NullPointerException(NPE)** 발생 가능성을 크게 줄일 수 있습니다.

> 💡 Java에서는 런타임까지 가야 NPE가 터지지만, Kotlin은 아예 코드 작성 단계에서 null 여부를 관리합니다.

---

## ✏️ 기본 예제

```kotlin
fun main() {
    
    // Kotlin에서는 null이 가능한 타입을 명시적으로 선언해야 합니다
    val str: String? = "ABC"
    println(str?.length)
    // Safe Call (`?.`) : str이 null이 아니면 length 호출, null이면 그냥 null 반환

    val str2: String? = "ABC"
    println(str2?.length ?: 0)
    // Elvis 연산자 (`?:`) : 앞이 null이면 뒤에 지정한 기본값(0)을 반환
}
```
---

## ✏️ 다양한 Null 처리 방식 예제 함수들

```kotlin
fun startWithA1(str: String?): Boolean {
    // null이면 예외를 던짐
    return str?.startsWith("A") ?: throw IllegalArgumentException("null이 들어왔습니다")
}

fun startsWithA2(str: String?): Boolean? {
    // null이면 null 반환
    return str?.startsWith("A")
}

fun startsWithA3(str: String?): Boolean {
    // null이면 false 반환
    return str?.startsWith("A") ?: false
}

fun startWith(str: String?): Boolean {
    // 절대 null이 아님을 확신할 때 `!!` 사용 (주의: 런타임 NPE 발생 가능성 있음)
    return str!!.startsWith("A")
}
```
## ✏️ 자바 코드
```java
public boolean startsWithA1(String str) {
    if (str == null) {
        throw new IllegalArgumentException("null이 들어왔습니다");
    }
    return str.startsWith("A");
}


public Boolean startsWithA2(String str) {
    if (str == null) {
        return null;
    }
    return str.startsWith("A");
}


public boolean startsWithA3(String str) {
    if (str == null) {
        return false;
    }
    return str.startsWith("A");
}
```
---

## ✅ Kotlin으로 변환할 때 장점

- **코드가 훨씬 짧고 읽기 쉽다**  
  → if문으로 null 체크하는 코드가 사라지고 `?.`, `?:` 같은 표현식으로 깔끔하게 작성 가능
- **Null 안전성이 강화된다**  
  → 컴파일 단계에서 null 가능성을 체크해주기 때문에 런타임 에러를 줄일 수 있다
- **표현이 의도에 더 직관적이다**  
  → `!!`, `?.`, `?:`를 통해 개발자의 의도를 코드에 명확하게 드러낼 수 있다
- **Elvis 연산자(`?:`) 덕분에 기본값 처리도 쉬워진다**
---
## 🏷️ 요약

- `?.` (Safe Call) : null이 아닐 때만 메서드 호출
- `?:` (Elvis 연산자) : null일 때 기본값을 반환
- `!!` (Not-Null 단정) : 무조건 null이 아님을 보장 (주의해서 사용!)
- Kotlin은 NullPointerException을 예방하기 위한 다양한 안전장치를 제공한다.
# 📚 Kotlin - Collection List

> 💡코틀린에서 컬렉션을 만들어줄 때 불변인지, 가변인지를 설정해 주어야 한다.

![Image](https://github.com/user-attachments/assets/5e8bcf74-a854-43a1-845e-5b29802223c1)

## 💡가변 리스트, 불변 리스트 
- 코틀린은 자체적으로 기본 컬렉션 타입인 List, Set, Map을 제공하고 있습니다.
- 코틀린은 두가지 성격의 컬렉션을 제공합니다.
- 가변 컬렉션(mutable) : 요소를 자유롭게 추가/삭제/수정할 수 **있는** 리스트입니다.✅
- 불변 컬렉션(immutable) : 요소를 추가, 삭제, 수정할 수 **없는** 리스트입니다.❌
- **mutable**이 붙으면 "변경 가능한" 컬렉션을 의미합니다.

| 불변 컬렉션     | 가변 컬렉션            |
| ---------- | ----------------- |
| `listOf()` | `mutableListOf()` |
| `setOf()`  | `mutableSetOf()`  |
| `mapOf()`  | `mutableMapOf()`  |

### 🚨중요🚨 
#### mutable은 "내용을 바꿀 수 있는" 컬렉션이라는 뜻이고, Kotlin에서는 데이터를 안전하게 다루기 위해 기본이 불변 컬렉션,필요할 때만 mutable 컬렉션을 사용합니다.

## 1️⃣리스트 생성 법
```kotlin
// 불변 리스트 생성
val numbers = listOf(100, 200)

// 가변 리스트 생성
val numbers2 = mutableListOf(100, 200)
numbers2.add(300) // 가변 리스트여서 요소 추가 가능

// 비어있는 리스트 생성 
val emptyList = emptyList<Int>()
```

## 2️⃣리스트 순회
```kotlin
// 0. 인덱스로 하나를 가져오기
println(numbers[0])

// 1. For-each 방식
for (number in numbers) {
    println(number)
}

// 2. 인덱스와 값 함께 사용
for ((index, value) in numbers.withIndex()) {
    println("$index $value")
}
```
## 3️⃣리스트의 Null 가능성
| 선언            | 의미                         |
| ------------- | -------------------------- |
| `List<Int?>`  | 리스트에 Null이 들어갈 수 있지만, 리스트는 절대 Null이 아님 |
| `List<Int>?`  | 리스트에는 Null이 들어갈 수 없지만, 리스트는 Null일 수 있음 |
| `List<Int?>?` | 리스트에 Null이 들어갈 수도 있고, 리스트가 Null일 수도 있음 |

---

## 1️⃣Map 
- Map 에서도 가변인지 불변인지 설정해주어야 합니다.
- mapOf를 사용할 때 to 중위 함수를 호출 해 Pair클래스에서 만들어주는 인피스 연산자 사용

```kotlin
// 불변 Map
val dayMap = mapOf(1 to "MONDAY", 2 to "TUESDAY")
```

- 요소 추가/수정이 가능하며, put()이나 map[key] = value 방식 모두 사용 가능.
- 기본 구현체는 LinkedHashMap.
```kotlin
// 가변 Map
val oldMap = mutableMapOf<Int, String>()
oldMap[1] = "MONDAY"
oldMap.put(2, "TUESDAY")
```

## 2️⃣ Map 리스트 순회

```kotlin
// Key 를 통해서 접근하는 식의 방식
for(key in oldMap.keys) {
    println(key)
    println(oldMap[key])
}

//  Entry라는 Key와 Value가 함께 들어있는 객체를 가져와 for문 사용
for((key, value) in oldMap.entries) {
    println(key)
    println(value)
}
```
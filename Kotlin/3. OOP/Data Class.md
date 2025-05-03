# 📚 Kotlin - 상속

> 💡**data class**는 데이터를 담는 용도로 특별히 설계된 클래스입니다.

## Data Class란?
- 데이터를 저장하기 위한 전용 클래스 DTO (Data Transfer Object)
- 자동으로 여러 유용한 함수들을 만들어줌
    - equals() / hashCode()
    - toString()
    - copy()
    - componentN() (구조 분해용)
- 이렇게 data 키워드를 붙이기만 하면 자동으로 여러 함수들 생성

```kotlin
data class Person(
    val name: String,
    val age: Int
)

fun main() {
    val p1 = Person("임도현", 24)
    val p2 = Person("임도현", 24)

    println(p1 == p2)
    // == 는 equals()를 의미함
    // 내용 비교 (name과 age가 같은지 비교)
    // Java에서는 equals() 직접 구현해야 함

    println(p1.toString())
    // toString() 자동 생성
    // 출력 결과: Person(name=임도현, age=24)
    // 객체 정보를 보기 좋게 출력 (디버깅 편함)

    val p3 = p1.copy(age = 30)
    // copy() 함수는 기존 객체를 복사해서 일부 값만 바꿔줌
    // Java에서는 생성자 또는 builder 패턴 사용해야 함
    println(p3)
    // Person(name=임도현, age=30)

    val (name, age) = p1
    // 구조 분해 선언 (destructuring declaration)
    // 내부적으로 component1(), component2() 호출됨
    // component1() → name
    // component2() → age

    println(name)               // 임도현
    println(age)                // 24
}
```

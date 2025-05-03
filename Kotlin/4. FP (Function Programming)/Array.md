# 📚 Kotlin - Array 배열

> 💡 Kotlin에서 배열은 여러 값을 하나의 변수에 담을 수 있는 자료구조입니다.

## 1️⃣배열 선언
- 생성과 동시에 초기화를 진행하고 싶을 경우 arrayOf(value)를 통해 생성 및 초기화를 할 수 있습니다.
- > val 변수명 = (자료형)ArrayOf(값1, 값2, 값3)
```kotlin
val arr:Array<Int> = arrayOf(1,2,3)
val arr2:Array<String> = arrayOf("test","test2")

//자료형은 생략 가능합니다
val arr = arrayOf(1,2,3)
val arr2 = arrayOf("test","test2")
```

- Array() 를 사용해 3개의 크기 0으로 초기화한다.
- >var 변수명 = (자료형)Array(크기, {초기값(생략가능)})
```kotlin
val arr: Array<Int> = Array(3) { 0 }  // [0, 0, 0]

// 람다식 사용 법
val arr: Array<Int> = Array(3) { i -> i } // [0, 1, 2]
```

## 2️⃣배열 순회 
- array.indices는 배열의 유효 인덱스 범위를 반환합니다.
- Java의 for (int i = 0; i < array.length; i++) 와 비슷한 방식입니다.

```kotlin
val array = arrayOf(100, 200)

for (i in array.indices) {
    println("$i ${array[i]}")
}
```

- withIndex() = 배열의 (index, value) 쌍을 만들어줌
- for ((index, value) in ...) = 그 쌍을 각각 변수로 분리해서 반복
```kotlin
for ((index, value) in array.withIndex()) {
    println("$index $value")
}
```
```java
// 자바 예시 withIndex() 랑 같은 방식
for (int i = 0; i < array.length; i++) {
    int index = i;
    int value = array[i];
}
```
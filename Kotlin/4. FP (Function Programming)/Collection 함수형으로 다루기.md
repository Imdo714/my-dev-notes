# 📚 Kotlin - Collection List 험수형으로 사용하기

> 💡


## 리스트 생성 
```kotlin
data class Fruit(
    val id: Long,
    val name: String,
    val factoryPrice: Long,
    val currentPrice: Long
) {
    fun isSamePrice(): Boolean = factoryPrice == currentPrice
}

fun main(){
    val fruits = listOf(
        Fruit(1L, "사과", 1_000, 1_500),
        Fruit(2L, "사과", 1_200, 1_500),
        Fruit(3L, "사과", 1_200, 1_500),
        Fruit(4L, "사과", 1_200, 1_500),
        Fruit(5L, "바나나", 3_000, 3_200),
        Fruit(6L, "바나나", 3_200, 3_200),
        Fruit(7L, "바나나", 2_500, 3_200),
        Fruit(8L, "수박", 10_000, 10_000)
    )
}
```

## 람다 생성 법 
> { 파라미터: 타입, 파라미터: 타입 ... -> 본문 }

## 필터(Filter)와 맵(Map)

- `filter {}` : 조건에 맞는 요소만 추출
- fruits에 존재하는 사과들만 apples에 저장 됨
```kotlin
// 요구사항 : 사과만 보여주세요!
val apples = fruits.filter { fruit: Fruit -> fruit.name == "사과" }
```

- `filterIndexed { index, it -> }` : 인덱스와 함께 필터링
- filter에서 인덱스가 필요한 경우 filter 대신 filterIndexed 사용
```kotlin
val applesIdx = fruits.filterIndexed { index, fruit ->
    println(index)
    fruit.name == "사과"
}
```

- `map {}` : 원소를 변형
- 사과의 가격들을 알려줘야 하는 경우에는 처음에 filter 기능을 이용해 사과만 필터링 한 다음 map 기능을 통해서 사과 인스턴스에서 가격들만 꺼내와서 applePrice 에 저장
```kotlin
// 요구사항 : 사과의 가격들을 알려주세요!
val applePrice = fruits.filter { fruit: Fruit -> fruit.name == "사과" }
    .map { fruit -> fruit.currentPrice }
```

- map에서 인덱스가 필요하다면?!
- map에서 인덱스가 필요하면 mapIndexed 를 사용
````kotlin
val applePricesIdx = fruits.filter { fruit: Fruit -> fruit.name == "사과" }
    .mapIndexed { idx, fruit ->
        println(idx)
        fruit.currentPrice
    }
````

## 다양한 컬렉션 처리 기능 

- `all` : 조건을 모두 만족하면 true 그렇지 않으면 false 즉, fruits가 모두 사과이면 true가 나옴
- 요구사항 : 모든 과일이 사과인가요 ?
```kotlin
val isAllApple = fruits.all { fruit: Fruit -> fruit.name == "사과" }
```

- `none` : 조건을 모두 불만족하면 true 그렇지 않으면 false 즉, fruits가 모두 사과가 아니면 true가 나옴
```kotlin
val isNoApple = fruits.none { fruit: Fruit -> fruit.name == "사과" }
```

- `any` : 조건을 하나라도 만족하면 true 그렇지 않으면 false 즉, 가격이 10,000원 이상인 과일이 하나라도 있으면 true가 나옴
- 요구사항 : 혹시 가격이 10,000원 이상의 과일이 하나라도 있나요?
```kotlin
val isAnyApple = fruits.any { fruit: Fruit -> fruit.currentPrice >= 10_000 }
```

- `count` : 개수를 센다. 즉, List에서 size랑 똑같다고 보면 됨
- 요구사항 : 총 과일 개수가 몇개인가요 ?!
```kotlin
val fruitCount = fruits.count()
```

- `sortedBy` : (오름차순) 정렬을 한다. 즉, 현재 가격을 기준으로 낮은 가격부터 높은 가격까지 보여줌
- 요구사항 : 낮은 가격 순으로 보여주세요 !
```kotlin
val fruitSortedBy =  fruits.sortedBy { fruit: Fruit -> fruit.currentPrice }
```

- `sortedByDescending` : (내림차순) 정렬을 한다. 즉, 현재 가격을 기준으로 높은 가격부터 낮은 가격까지 보여줌
```kotlin
val fruitSortedByDescending = fruits.sortedByDescending { fruit: Fruit -> fruit.currentPrice }
```

- `distinctBy` : 변형된 값을 기준으로 중복을 제거한다.
- 즉, 이름을 기준으로 fruit 중복을 제거 하고 map을 사용해 이름만 남게 함
- 과일이 여러 종류가 있더라도 사과 바나나 수박 이름만 증복이 제거된 상태로 남음
```kotlin
val distinctFruitNames = fruits.distinctBy { fruit: Fruit -> fruit.name }
    .map { fruit -> fruit.name }
```

##  List를 Map으로

- `groupBy {}` : 기준으로 그룹핑 (Key → List<Value>).
- 과일 이름이 Key이고 그 과일 이름을 토대로 과일들이 존재하는 map을 만들어야 한다면 ?
- fruit.name을 기준으로 그룹이 됨 즉, Key가 과일 이름이 되고 Value 에는 과일 리스트가 들어감
- 요구사항 : 과일 이름 -> List<과일> Map이 필요해요 !
```kotlin
val map: Map<String, List<Fruit>> = fruits.groupBy { fruit: Fruit -> fruit.name }
```

- associateBy 를 사용하게 되면 Value 값에 리스트가 "아닌 단일 객체"가 들어 감
- 중복되지 않는 키를 가지고 map을 만들때 사용
- 요구사항 : id -> 과일 Map이 필요해요 !

```kotlin
val mapKey: Map<Long, Fruit> = fruits.associateBy { fruit -> fruit.id }

// id -> 출고가 Map이 필요해요 !
val mapKeyId: Map<Long, Long> = fruits
    .associateBy( { fruit: Fruit -> fruit.id } { fruit: Fruit -> fruit.factoryPrice } )
```

- Key 에는 과일 이름 Value 값에는 가격이 들어가는 식
- 과일 이름 -> List<출고가> Map이 필요해요 !
```kotlin
val mapTotalPrice: Map<String, List<Long>> = fruits
    .groupBy( { fruit: Fruit -> fruit.name }, { fruit: Fruit -> fruit.factoryPrice } )
```

- Key가 사과이고 List<사과>만 존재하는 Map이 됨
```kotlin
val mapFilter: Map<String, List<Fruit>> = fruits.groupBy { fruit: Fruit -> fruit.name }
    .filter { (key, value) -> key == "사과" }
```

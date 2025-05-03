# 📚 자바 - ArrayList 클래스의 주요 메서드
> 💡 List 인터페이스를 구현한 ArrayList를 주로 사용

- `add()` : 리스트 끝에 원소를 추가합니다.
- `add(index, obj)` : 특정 인덱스에 원소를 추가합니다.
```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
System.out.println(list); // [Apple, Banana]

list.add(1, "Orange");
System.out.println(list); // [Apple, Orange, Banana]
```

- `addAll(collection)` : 주어진 컬렉션의 모든 객체를 리스트 끝에 추가합니다.
- `addAll(index, collection)` : 주어진 컬렉션의 모든 객체를 특정 인덱스 위치에 추가합니다.
```java
List<String> fruits = new ArrayList<>();
fruits.add("Grapes");
fruits.add("Mango");
list.addAll(fruits);
System.out.println(list); // [Apple, Orange, Banana, Grapes, Mango]
```

- `get(index)` : 특정 인덱스의 값을 반환합니다.
- `set(index, obj)` : 특정 인덱스에 원소를 저장합니다.
- `remove(obj)` : 리스트에서 특정 값을 삭제합니다.
- `remove(index)` : 특정 인덱스에 위치하는 값을 삭제합니다.
```java
String fruit = list.get(1);
System.out.println(fruit); // Orange

list.set(1, "Peach");
System.out.println(list); // [Apple, Peach, Banana, Grapes, Mango]

list.remove("Peach");
System.out.println(list); // [Apple, Banana, Grapes, Mango]

list.remove(0); // Apple 삭제
System.out.println(list); // [Grapes, Mango, Banana]
```

- `indexOf(obj)` : 리스트에서 특정 객체의 인덱스를 반환합니다. 객체가 없으면 -1을 반환합니다.
- `subList(fromIndex, toIndex)` : fromIndex와 toIndex-1까지의 부분 리스트를 반환합니다.
- `contains(obj)` : 리스트에 특정 원소가 포함되어 있는지 확인합니다.
```java
int index = list.indexOf("Grapes"); // 0번째 인덱스에 Grapes있음 
System.out.println(index); // 0 

List<String> subList = list.subList(1, 3); // 1번 인덱스 ~ 2인덱스 
System.out.println(subList); // [Mango, Banana]

boolean contains = list.contains("Grapes"); // list에 Grapes가 있음 
System.out.println(contains); // true
```

- `sort()` : 리스트 오름차순 정렬
- `sort(comparator)` : 리스트 내림차순 정렬 
```java
list.sort(null); // 기본 오름차순 정렬
System.out.println(list); // [Banana, Grapes, Mango]

list.sort(Comparator.reverseOrder()); // 내림차순 정렬
System.out.println(list); // [Mango, Grapes, Banana]
```
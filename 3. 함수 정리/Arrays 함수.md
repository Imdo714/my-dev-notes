# 📚 자바 - Array ↔ List 변환 정리

- `Arrays.asList(arr)` : 고정 길이 List 반환
  - add(), remove() 불가능 원본 배열과 동기화됨
- `new ArrayList<>(Arrays.asList(arr))` : 새로운 가변 리스트 생성
  - 수정 가능 / 배열과 독립
- `Stream.of(arr).collect(Collectors.toList())`
  - 가독성 좋음, 참조 타입만 가능

```java
String[] arr = {"a", "b", "c"};
List<String> list1 = Arrays.asList(arr);                   // 고정 크기 
List<String> list2 = new ArrayList<>(Arrays.asList(arr));  // 가변 크기
List<String> list3 = Stream.of(arr)                        // Stream 방식
                        .collect(Collectors.toList()); 
```

---

# 📚 자바 - 리스트(List) → 배열(Array)

- **`new String[list.size()]` → 크기와 같은 배열 전달**
- **`new String[0]` → 크기 부족하므로 자동으로 리스트 크기만큼 새 배열 생성**
  - **파라미터로 전달 받은 배열 객체의 길이기 원본 리스트보다 작은 경우, 자동으로 원본 리스트의 size 크기로 배열을 만들어준다.**
- **`new String[5]` → 여유 공간은 null로 채워짐**
  - **원본 리스트의 길이보다 배열의 크기를 더 크게 지정하면, 나머지 인덱스는 null 로 채워진다.**

```java
List<String> list = Arrays.asList("a", "b", "c");
String[] arr = list.toArray(new String[0]);  // ["a", "b", "c"]
String[] arr2 = list.toArray(new String[5]); // ["a", "b", "c", null, null]
```

---
# 📚 자바 - Arrays Function 
> 💡 Arrays는 **배열(Array)** 을 다루기 위한 유틸리티 클래스입니다.

- **`Arrays.sort()` : 오름차순으로 정렬**
  - **기본 정렬조건이 오름차순인 이유는 Class 내에 기본적으로 구현되어있는 `Comparable Interface`의 `compareTo` 메서드를 기준으로 하기 때문이다. Java에서 인스턴스를 서로 비교하는 클래스들은 모두 `Comparable` 인터페이스가 구현되어 있다.**
- **`Arrays.sort(arr, from, to)` : 정렬 (범위 지정)**
```java
int[] intArr = {5, 2, 4, 1, 3};
Arrays.sort(intArr); // 오름차순 정렬
System.out.println(Arrays.toString(intArr)); // [1, 2, 3, 4, 5]

int[] intArr = {5, 2, 4, 1, 3};
Arrays.sort(intArr, 1, 4); // index 1 ~ 3만 정렬
System.out.println(Arrays.toString(intArr)); // [5, 1, 2, 4, 3]
```

- **`reverseOrder()` : 내림차순 정렬** 
  - `Comparator.reverseOrder()` : 정렬 대상이 배열일 때 사용
  - `Collections.reverseOrder()` : 정렬 대상이 리스트일 때 사용 
    - 배열은 클래스이고 List는 Collection 이여서 함수 호출이 다릅니다.
```java
Integer[] integerArr = {1, 3, 5, 2, 4};
Arrays.sort(integerArr, Comparator.reverseOrder()); // 내림차순

List<String> list = Arrays.asList("A", "C", "B");
Collections.sort(list, Collections.reverseOrder()); // 내림차순
System.out.println(list); // [C, B, A]
```


- **`Arrays.asList()` : 배열(Array)을 ArrayList로 변환**
  - **고정 크기 리스를 반환하여 add, remove 불가능**
```java
String[] arr = {"A", "B", "C"};
List<String> list = Arrays.asList(arr);
```


- **`Arrays.fill()` : 배열 값 채우기** 
    - **`Arrays.fill(arr, value)` : 모든 요소를 특정 값으로 초기화**
    - **`Arrays.fill(arr, start, end, value)` : 일 부분만 채움**
```java
int[] arr = new int[5];
Arrays.fill(arr, 7); // 모든 값 7로 채움 → [7, 7, 7, 7, 7]

int[] arr = new int[5];
Arrays.fill(arr, 1, 4, 3); // index 1~3을 3으로 채움 → [0, 3, 3, 3, 0]
```

- **`Arrays.copyOf()` : 앞에서 부터 크기 지정 복사**
```java
int[] original = {1, 2, 3, 4, 5};
int[] copy = Arrays.copyOf(original, 3); // [1, 2, 3]
```

- **`Arrays.copyOfRange()` : 시작~끝 범위 복사**
```java
int[] original = {1, 2, 3, 4, 5};
int[] copy = Arrays.copyOfRange(original, 1, 4); // index 1~3 → [2, 3, 4]
```

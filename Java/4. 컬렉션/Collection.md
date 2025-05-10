# 📚 자바 - Collection 상속 인터페이스 List<> Set<>
> 💡 Collection<> 인터페이스는 중간 인터페이스입니다.

## Collection Framework 상속 구조
![Image](https://github.com/user-attachments/assets/108a9ee9-d391-4e0c-a86a-a7b6b4a1f96e)

| 인터페이스   | 구현 클래스                        | 특징                                                                 |
|---------|-------------------------------|----------------------------------------------------------------------|
| List    | ArrayList, LinkedList, Vector | 순서가 있는 데이터의 집합으로, 데이터의 중복을 허용함                |
| Set     | HashSet, TreeSet              | 순서를 유지하지 않는 데이터의 집합으로, 데이터의 중복을 허용하지 않음 |

       Iterable<E>        ← 최상위 루트 (for-each 사용 가능)
           ↑
      Collection<E>       ← List, Set 등의 부모 인터페이스
       /         \
    List<E>       Set<E>    ← 순서 O/중복 O  vs  순서 X/중복 X


## 🚨List<>인터페이스, Set<>인터페이스 차이🚨
| 항목         | `List`                          | `Set`                  |
| ---------- | ------------------------------- | ---------------------- |
| **중복 저장**  | 허용 (`add()` 하면 그대로 들어감)         | 허용하지 않음 (중복이면 무시됨)     |
| **저장 순서**  | 유지 (인덱스로 관리)                    | 유지하지 않음 (`HashSet` 기준) |
| **인덱스 접근** | 가능 (`list.get(0)`)              | 불가능 (`set.get()` 없음)   |
| **정렬**     | 기본 없음, 필요시 `Collections.sort()` | `TreeSet`은 자동 정렬됨      |
| **주 사용처**  | 순차적 데이터 저장, 순서 중요할 때            | 중복 없이 데이터 관리할 때        |


## List<> 인터페이스
- 객체를 일렬로 늘어놓은 구조를 가지고 있다.
- 객체를 인덱스로 관리하기 때문에 객체를 저장하면 자동 인덱스가 부여되고 인덱스로 객체를 검색, 삭제할 수 있는 기능을 제공한다.
- 🚨List 인터페이스는 **중복을 허용**하면서 **저장순서가 유지**되는 컬렉션을 구현하는데 사용된다.🚨

  | 메서드 | 설명 |
  |--------|------|
  | `void add(int index, Object element)` | 지정된 위치(index)에 객체(element)를 추가한다. |
  | `boolean addAll(int index, Collection c)` | 지정된 위치(index)에 컬렉션에 포함된 모든 객체들을 추가한다. |
  | `Object get(int index)` | 지정된 위치(index)에 있는 객체를 반환한다. |
  | `int indexOf(Object o)` | 지정된 객체의 위치(index)를 반환한다. (첫 번째 요소부터 순방향으로 탐색) |
  | `int lastIndexOf(Object o)` | 지정된 객체의 위치(index)를 반환한다. (마지막 요소부터 역방향으로 탐색) |
  | `int size()` | 저장되어 있는 객체의 개수를 반환한다. |
  | `Object remove(int index)` | 지정된 위치(index)에 있는 객체를 삭제한다. |
  | `void clear()` | 저장된 모든 객체를 삭제한다. |
  | `Object set(int index, Object element)` | 지정된 위치(index)에 객체(element)를 저장한다. |
  | `void sort(Comparator c)` | 지정된 비교자(comparator)를 사용하여 List를 정렬한다. |
  | `List subList(int fromIndex, int toIndex)` | 지정된 범위(fromIndex 이상 toIndex 미만)의 객체들을 반환한다. |

## ArrayList  특징
```java
List<저장할 객체 타입> list = new ArrayList<저장할 객체 타입>();
```
- 배열기반이다. 
- ArrayList는 List 인터페이스를 상속받는 클래스로, 데이터를 이름표 없이 무제한으로 보관할 수 있다.
- ArrayList에 추가되는 데이터는 저장순서가 유지되고 중복을 허용한다. 
- ArrayList에서 특정 인덱스의 객체를 삭제하거나 추가할 경우 바로 뒤 인덱스부터 인덱스가 바뀐다. 

**🚨일반 배열과의 차이점🚨**
- 배열은 생성할 때 크기가 고정되고 사용 중에 크기를 변경할 수 없지만, ArrayList는 저장 용량이 초과한 객체들이 들어오면 자동적으로 저장 용량이 늘어난다.


## LinkedList 
```java
List<저장할 객체 타입> list = new LinkedList<저장할 객체 타입>();
```
- LinkedList는 List 구현 클래스이므로 ArrayList와 사용 방법은 똑같지만 내부 구조는 완전히 다르다.
- ArrayList는 모든 데이터가 연속적으로 존재하지만 LinkedList는 불연속적으로 존재하는 데이터를 서로 연결한 형태로 구성되어 있다.
- LinkedList의 각 요소들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어있다. 

![Image](https://github.com/user-attachments/assets/d174a0f3-a764-441d-b5af-1f6a03cb8e13)

- 특정 인덱스의 객체를 추가 또는 삭제할 경우 앞뒤 링크만 변경되고 나머지 링크는 변경되지 않는다.
- 앞뒤 링크 정보만 변경하면 되므로 처리속도가 매우 빠르다.
- LinkedList는 불연속적으로 위치한 각 요소들이 서로 연결된 것이라 처음부터 n번째 데이터까지 차례대로 따라가야만 원하는 값을 얻을 수 있다.
- 그래서 LinkedList는 저장해야하는 데이터의 개수가 많아질수록 데이터를 읽어 오는 시간(접근시간)이 길어진다는 단점이있다.

![Image](https://github.com/user-attachments/assets/0c07a4dd-ace4-4099-b5c8-33d749e34932)
![Image](https://github.com/user-attachments/assets/65180200-63e3-4f2e-a289-56361cbee663)

**🚨ArrayList와 LinkedList의 차이🚨**

| 컬렉션      | 읽기 (접근시간) | 순차적 추가/삭제 | 중간에 추가/삭제 | 비고 |
|-------------|------------------|------------------|------------------|------|
| ArrayList   | 빠르다           | 빠르다           | 느리다           | 비효율적인 메모리 사용<br>검색이 빠르다 |
| LinkedList  | 느리다           | 느리다           | 빠르다           | 데이터가 많을수록 접근성이 떨어진다.<br>검색이 느리다 |

## Set<> 인터페이스
- 중복을 허용하지 않고 저장순서가 유지되지 않는다.
- 하나의 null만 저장할 수 있다.
- 인덱스로 관리하지 않기 때문에 인덱스를 매개값으로 갖는 메서드가 없다.

| 메서드                     | 설명                                                                 |
|--------------------------|----------------------------------------------------------------------|
| `boolean add(Object o)`   | 주어진 객체를 저장. 성공 시 `true`, 중복이면 `false` 반환              |
| `boolean contains(Object o)` | 주어진 객체가 저장되어 있는지 확인                                     |
| `void clear()`             | 저장된 모든 객체를 삭제                                               |
| `boolean remove(Object o)` | 주어진 객체를 삭제                                                    |
| `boolean equals(Object o)` | 동일한 컬렉션인지 비교                                                |
| `boolean isEmpty()`        | 컬렉션이 비어 있는지 확인                                             |
| `Iterator iterator()`      | 저장된 객체를 한 번씩 가져오는 반복자 반환                             |
| `int size()`               | 저장되어 있는 전체 객체 수 반환                                       |

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

for (String value : list) {
    System.out.println(value);
}
```

## HashSet 
```java
Set<저장할 객체 타입> set = new HashSet<저장할 객체 타입>(); 
```
- Set인터페이스를 구현한 가장 대표적인 컬렉션이며, **중복된 요소를 저장하지 않는다.**
- 이미 저장되어 있는 요소와 중복된 요소를 추가하고자 한다면 add메서드는 false를 리턴함으로써 중복된 요소이기 때문에 추가에 실패했다는 것을 알린다.
- 저장 순서를 유지하지 않으므로 저장순서를 유지하고자 한다면 `LinkedHashSet`을 사용해야한다.

### 중복을 걸러내는 과정
- `HashSet`은 객체를 저장하기 전에 먼저 객체의 `hashCode()` 메서드를 호출해서 해시코드를 얻어낸다. -> 그리고 이미 저장되어 있는 객체들의 해시코드와 비교한다.
- 동일한 해시코드가 있다면 다시 equals() 메서드로 두 객체를 비교해서 true가 나오면 동일한 객체로 판단하고 중복 저장을 하지 않는다.

## HashSet 활용 문제
> 알고리즘 문제 : https://www.acmicpc.net/problem/3052

- 문제를 보면 입력 값이 42로 나눈 서로 다른 값이 몇개인지 출력하는 프로그램이다.
- 입력 값을 받아 42로 나눈 값을 HashSet에 저장 그러면 증복 값은 추가 되지 않음
- 출력할 때 `set.size()`로 몇개인지 반환 
```java
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        Set<Integer> set = new HashSet<>();

        for (int i = 0; i < 10; i++) {
            int num = sc.nextInt();
            set.add(num % 42); // 
        }

        System.out.println(set.size());
    }
}
```
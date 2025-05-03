# 📚 자바 - Map
> 💡Map은 독립적인 인터페이스 트리를 가집니다.

## Collection Framework 상속 구조
![Image](https://github.com/user-attachments/assets/108a9ee9-d391-4e0c-a86a-a7b6b4a1f96e)

| 인터페이스   | 구현 클래스                        | 특징                                                                 |
|---------|-------------------------------|----------------------------------------------------------------------|
| Map     | Hashtable, HashMap, TreeMap   | 키(Key)와 값(Value)의 쌍으로 이루어진 데이터 집합. 순서를 유지하지 않으며, 키의 중복은 허용하지 않으나 값의 중복은 허용함 |


## Map 인터페이스
- **키(key)와 값(value)** 을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는데 사용된다. 
  - **여기서 키와 값은 모두 객체이다.**
- 키는 중복될 수 없지만 값은 중복을 허용한다.
- 기존에 저장된 데이터와 중복된 키와 값을 저장하려면 기존의 값은 없어지고, 마지막에 저장된 값이 남게 된다.
- 키로 객체들을 관리하기 때문에 키를 매개값으로 갖는 메서드가 많다.

| 메서드                             | 설명                                                                                 |
|----------------------------------|--------------------------------------------------------------------------------------|
| `Object put(Object key, Object value)` | 주어진 키로 값을 저장. 새로운 키면 `null` 반환, 동일한 키면 값을 대체하고 이전 값을 반환 |
| `void clear()`                   | Map의 모든 객체를 삭제                                                              |
| `Object remove(Object key)`     | 지정한 키에 해당하는 key-value 쌍을 삭제                                           |
| `boolean containsKey(Object key)`   | 지정된 키가 있는지 여부 반환                                                        |
| `boolean containsValue(Object value)` | 지정된 값이 있는지 여부 반환                                                        |
| `Set keySet()`                   | Map에 저장된 모든 키 객체를 `Set`으로 반환                                          |
| `Collection values()`           | 저장된 모든 값을 `Collection`에 담아 반환                                           |
| `Set entrySet()`                | Map의 key-value 쌍을 `Map.Entry` 타입 객체로 저장한 `Set`으로 반환                  |
| `Object get(Object key)`        | 지정된 키에 해당하는 값을 반환                                                      |
| `boolean equals(Object o)`      | 동일한 Map인지 비교                                                                 |
| `boolean isEmpty()`             | Map이 비어 있는지 여부 반환                                                         |
| `int size()`                    | 저장된 키의 총 수를 반환                                                             |

## HashMap
```java
Map<키 타입, 값 타입> map = new HashMap<키 타입, 값 타입>();
```
- Map 인터페이스를 구현한 대표적인 Map 컬렉션이다.
- Map의 특징, 키(key)와 값(value)을 묶어서 하나의 데이터(entry)로 저장한다는 특징을 갖는다.
- 해싱(hashing)을 사용하기 때문에 많은 양의 데이터를 검색하는데 있어서 뛰어난 성능을 보인다.
- 키(key)는 주로 String을 많이 사용한다.
  - 키는 저장된 값을 찾는데 사용되는 것이기 때문에 컬렉션 내에서 유일(unique)해야 한다.
  - String은 문자열이 같은 경우 동등 객체가 될 수 있도록 hashcod()와 equuals()메서드가 재정의 되어 있다.

```java
Map<String, Integer> map = new HashMap<String, Integer>();

map.put("국어", 95);
map.put("수학", 90);
map.put("영어", null); 	// 객체를 넣는 것이므로 Null 사용 가능

System.out.println("HashMap size : " + map.size()); // 3
System.out.println(map.get("국어")); // 국어 : 95 키 값으로 꺼내기
System.out.println(map.get("영어")); // 영어 : null
```
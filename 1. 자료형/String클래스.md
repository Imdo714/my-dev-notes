# 🔨 자바 - String 클래스
> 💡 String 클래스는 자바에서 문자열을 저장하는 데 사용되는 불변(immutable) 클래스입니다. 문자열을 다룰 때 가장 많이 사용되는 데이터 타입으로, 다양한 메서드를 제공합니다.

### 1. String 객체 생성 방법
* String 객체는 두 가지 방법으로 생성할 수 있습니다: 리터럴 방식과 생성자 방식입니다.
* 리터럴 방식으로 String 객체를 생성하면, 자바는 String Pool이라는 특수한 메모리 영역을 사용하여 문자열을 관리합니다.
* String Pool에서는 동일한 문자열을 중복 생성하지 않고 재사용합니다. 즉, "Hello Java"라는 문자열이 이미 존재하면, 새로운 객체를 생성하지 않고 기존 객체를 참조합니다.
* new 키워드를 사용하여 String 객체를 생성하면, 힙 메모리에 새로운 객체가 생성됩니다. 이 방식은 String Pool과 별개로 객체를 생성하기 때문에, 중복된 문자열을 재사용하지 않습니다.

```java
String str1 = "Hello Java"; // 리터럴 방식
String str2 = new String("Hello Java"); // 생성자 방식
```

### 2. String의 불변성
* String 클래스는 문자열을 저장하는 불변 클래스입니다.
* 문자열을 수정하려고 할 때 새로운 String 객체가 생성됩니다.
* 예를 들어, "Hello"라는 문자열을 변경하면, 새로운 "Hello World"라는 문자열이 생성됩니다. 기존의 "Hello" 문자열은 그대로 남습니다.
* 여기서 "Hello World"는 새로운 String 객체로 생성되고, 기존 "Hello" 문자열은 변경되지 않습니다.
* 자바에서는 동일한 문자열을 재사용하기 위해 String Pool을 사용하여 메모리 절약을 합니다. 즉, "Hello"와 같은 문자열 리터럴은 프로그램 내에서 중복 생성되지 않고, 하나의 객체를 공유합니다.
```java
String str1 = "Hello";
str1 = str1 + " World";  // 새로운 문자열 객체가 생성됩니다.
System.out.println(str1); // "Hello World"
```

### 3. 문자열 비교
* == 연산자 : 두 객체가 같은 메모리 주소를 참조하는지 비교합니다.
* equals() : equals()는 값 비교 (Value comparison) 를 합니다.
```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

boolean isEqual1 = str1.equals(str2);  // true  같은 값을 가지고 있음 
boolean isEqual3 = str1 == str2;       // true  같은 메모리 주소를 가짐
boolean isEqual3 = str1 == str3;       // false 다른 메모리 주소를 가짐 
```


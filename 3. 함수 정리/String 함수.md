# 📚 자바 - String Function 

---

- **`startsWith(str)` : 문자열이 특정 문자로 시작되는지 판별**
```java
String text = "Hello, world!";
System.out.println(text.startsWith("Hello")); // true
```


- **`equal(str)` : String 문자열 값 비교**
```java
String a = "java";
String b = "java";
System.out.println(a.equals(b)); // true
```


- **`indexOf(str)` : 특정 문자열이 대상 문자열의 몇 번째 인덱스에 위치하는지 반환**
- **특정 문자열이 없을 경우에는 -1을 리턴**
```java
String text = "banana";
System.out.println(text.indexOf("na")); // 2
System.out.println(text.indexOf("apple")); // -1
```

- **`substring` : 지정한 범위에 속하는 문자열 반환**
- **`substring(index)`: index 위치를 포함하여 이후의 모든 문자열을 리턴**
- **`substring(beginIndex, endIndex)` : beginIndex에서 endIndex-1까지의 부분 문자열을 반환**
```java
String text = "Hello, world!";
System.out.println(text.substring(7)); // "world!"

String text = "Hello, world!";
System.out.println(text.substring(0, 5)); // "Hello"
```

- **`replace(beforeStr, afterStr)` : 특정 문자열을 새로운 문자열로 치환**
```java
String text = "I like java.";
System.out.println(text.replace("java", "Python")); // "I like Python."
```


- **`toLowerCase(str)` : 문자열을 소문자로 변환**
- **`toUpperCase(str)` : 문자열을 대문자로 변환**
```java
String text = "HELLO";
System.out.println(text.toLowerCase()); // "hello"

String text = "hello";
System.out.println(text.toUpperCase()); // "HELLO"
```


- **`trim(str)` : 문자열의 앞뒤 공백 제거**
- **단, 문자열 내부의 공백은 replace(" ", "")를 사용해야 함**
```java
String text = "  hello world  ";
System.out.println(text.trim()); // "hello world"

String text = " a b c ";
System.out.println(text.replace(" ", "")); // "abc"
```


- **`charAt(index)` : 문자열 특정 위치에 있는 문자 반환**
- **인덱스 값으로 마이너스 값을 대입하거나, 문자열 길이보다 큰 인덱스 값을 대입하면 java.lang.StringIndexOutOfBoundsException 오류 발생**
```java
String text = "hello";
System.out.println(text.charAt(1)); // 'e'

// System.out.println(text.charAt(10)); // java.lang.StringIndexOutOfBoundsException
```


- **`String.valueOf(str)` : 지정된 값을 String으로 변환**
```java
int num = 100;
String strNum = String.valueOf(num);
System.out.println(strNum + "원"); // "100원"
```


- **`contains(str)` : 특정 문자열이 포함되어 있는지 확인**
```java
String text = "java programming";
System.out.println(text.contains("gram")); // true
```


- **`split(regex)` : 문자열을 특정 문자열을 기준으로 나는 후 배열을 반환**
```java
String fruits = "apple,banana,grape";
String[] arr = fruits.split(",");
for (String fruit : arr) {
    System.out.println(fruit);
}
// apple
// banana
// grape
```


- **`length()` : 문자열의 길이를 반환**
```java
String text = "kotlin";
System.out.println(text.length()); // 6
```



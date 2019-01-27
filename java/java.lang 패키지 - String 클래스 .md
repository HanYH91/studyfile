### 2. String 클래스

String 클래스 안에서 char[]로 저장된다.



[TOC]



#### 변경 불가능한(immutable) 클래스

String 클래스는 final 클래스이다. 따라서 상속 불가능하다. (=조상클래스가 될 수 없다.)

String 문자열을 '+' 연산자를 이용해서 문자열을 결합할 때, 
인스턴스내의 문자열이 바뀌는 것이 아니라 새로운 인스턴스가 생성되는 것이다.

```
String a = "a";
String b = "b";
a = a + b;
```

이 코드에서 "a"인 a값과 a+b인 a값의 주소는 전혀 다르다.

결합 때 '+'를 사용하는 것은 매번 새로운 인스턴스가 생성된다. 
이 인스턴스는 메모리공간을 차지하므로 결합횟수를 줄이는 것이 좋다.
문자열의 결합이나 추출이 많이 필요한 경우에는 StringBuffer클래스를 사용하는 것이 좋다.

변경이 많이 없다면 String이 가장 좋다. 변경이 안되는 읽기,쓰기용 이라서 안전하다.



#### 문자열의 비교

문자열을 만드는 방법은 두가지가 있다.

```
String str1 = "abc";					// "abc"의 주소가 str에 저장 됨
String str2 = "abc";				// "abc"의 주소가 str2에 저장 됨
String str3 = new String("abc")		// 새로운 String인스턴스를 생성
String str4 = new String("abc")		// 새로운 String인스턴스를 생성
```

"abc"의 주소는 하나이기 때문에 실질적으로 str1, str2가 가르키는 주소는 같고
새로운 인스턴스를 생성한 경우는 당연히 str3, str4의 주소는 서로 다르다.

```
str1 == str2 ?  true
str1.equals(str2) ? true
str3 == str4 ? false
str3.equals(str4) ? true
```

역시 위 코드를 보면 **str1과 str2의 주소는 같다**고 나오고 
**str3과 str4의 주소는 다르다**고 나온 것을 알 수 있다.



#### 빈 문자열 (Empty String)

```
String s = ""; 		// s = null; 과 같다.
char c = ' ';		// c = '\n0000'; 과 같다.
```

char[] chArr = new char[0]; (크기가 0인 배열)로 저장된다. int[] iArr = {}; (크기가 0인 인트 배열)

	char[] cArr = new char[0];  
	String s = new String(cArr); 	
```
String s = new String(""); 
```

따라서 위 두개는 같은 식이다.



#### String 클래스의 생성자와 메서드

##### 생성자 세가지.

new String("asd"), new String(char[]), new String(StringBuffer) 

##### 메소드

str.charAt(0);	: str에서 0번째 char값

str1.compareTo(str2) : 사전순서로 비교. str1이 앞이면 -1 뒤면 1 같으면 0.

"a".concat("b") : 합친다. 출력은 'ab'. ''+'' 연산이 생기기전에 사용하던함수. 기능적 차이는 없다.

"abc".contains("bc") :  "abc"에 "bc"가 포함되어있나 ? 출력은 true

"a.txt".endsWith("txt") : "txt"로 끝나는지? 출력은 true

"java.txt".startsWith("java", 1) : "java"로 시작하는지 ? 1번 문자 부터 체크. 출력은 false 

"a".equals("A") : 같은지. false.

"a".equalsIgnoreCase("A") : equals의 대소문자 무시 버전. true.

"abaaba".indexOf("ba") , "abaaba".indexOf('b')  : 몇번째에 있는지 찾기. 출력 1. 못찾으면 -1

"abaaba".indexOf("b", 2) : n번째 수 부터 검색 시작. 출력 4. 못찾으면 -1

"abaaba".lastIndexOf("ba") : 뒤에서부터 찾기. 출력 4.

"abaaba".lastIndexOf("b", 2) : n번째 수 부터 0번까지 검색. 뒤에서부터 찾기. 출력 1.

str.intern() : 해당 문자열의 주소를 반환. 리터럴 값으로 정의할 때 생각하면 됨.

str.length() : 길이. 배열은 ()가 없다.

"abcabc".replace("ab", "12") : 바꾸기. 12c12c 출력.

"abcabc".replaceAll("ab", "12") : 모두 바꾸기. 12c12c 출력.

"abcabc".replaceFirst("ab", "12") : 맨앞에 하나만 바꾸기. 12cabc 출력.		

String[] arr2   = "a,b,, c,d".split(",") : 빈칸 하나의 문자로 인식. 5개 출력되고 c앞에 띄어쓰기 포함됨.

String[] arr2   = "a,b,, c,d".split(",", 3) : 앞에서부터 최대 3개까지만 나눌 수 있음.

"01234".substring(2) : 2번 부터 끝 까지 자르기. 출력 234

"01234".substring(2,4) : 2번부터 4번 '전' 까지 자르기. 출력 23

"aBc".toLowerCase() : 소문자로. 출력 abc

"aBc".toUpperCase() : 대문자로. 출력 ABC

" a b c d ".trim() : 양쪽 빈칸 삭제. 출력 "a b c d"

String.valueOf(인트, 더블, 등) : 다른자료형 -> String 형으로 형변환.



##### replace, replaceAll 차이

replace는 단순 문자열만 확인해서 바꿔준다.
replaceAll은 정규표현식을 인식한다.		ex) "가나다.가".replaceAll("가.", "1") -> "1다.가"

```
정규표현식
|  -> abc|adc 는 abc,adc 모두 포함
()-> a(b|d)c는 abc|adc와 같음
* ->0개 이상 ,a*b는 b,ab,aab 를 포함한다. 
+ ->1개 이상
? ->0개 또는 1개, a?b는 b,ab를 포함한다.
{m,n} -> m개 이상 n개 이하, a{1,3}b는 ab,aab,aaab를 포함
[]사이의 문자중 하나를 선택한다. |를 여러개 쓴것과 같다.
[abc]d는 ad,bd,cd를 포함한다.
[a-z]는 a~z중 하나[^abc]는 알파벳 abc를 뺀 나머지, 
[abc]d는 ad,bd,cd를 뺀 ed,fd등
[^a-z]는 알파벳 소문자로 시작하지 않는 모든 문자열
^,$ : 각각 문자열의 처음과 끝을 나타낸다.
```

**[출처]** [replace와 replaceAll의 차이](https://blog.naver.com/emtete/120193607227)|**작성자** [감자촌](https://blog.naver.com/emtete)







#### join() 과 StringJoiner

##### join() 예제.

	String animals = "dog,cat,bear";
	String[] arr   = animals.split(",");	// arr = {"dog", "cat", bear}
	String str = String.join("-", arr);		// str = dog-cat-bear
##### StringJoiner 예제.

```
StringJoiner sj = new StringJoiner("/","[","]");
for(String s : arr)
	sj.add(s);			
String str = sj.toString();			// str = [dog/cat/bear]
```





#### 유니코드 보충문자

매개변수가 char, int인 것의 차이.
유니코드 = 2byte(16bit)  --->>> 20bit로 보충문자가 생겼다.
따라서 char 로 보충문자 표현을 못한다. (char는 2바이트 크기)
따라서 매개 변수가 int ch, char ch 차이는 보충문자 사용가능 여부이다. 
사실 보충문자 사용할 일은 거의 없기 떄문에 알아만 두자.





#### String.format()

printf 형식으로 입력받아서 String값으로 만들어준다.

```
String str = String.format("%d + %d = %c", 5, 3, '8');
```





#### String 형변환

##### ?? ---> String

```
String str = 1 + "";				// 간편. 성능 덜 중요한 경우 사용
String str = String.valueOf(1);		// 성능향상이 필요한 경우 사용
```

##### String ---> ??

```
int i = Integer.valueOf("1");	// valueOf 메소드 안에서 parseInt해준다.
int i = Integer.parseInt("1");	// 똑같은 함수.	
Double d = Double.parseDouble("1");		
Boolean b = Boolean.parseBoolean("1");	
Long l = Long.parseLong("1");			
```

16진법으로 a인 값을 s에 넣는다. 결과값 10.

```
int s = Integer.parseInt("a", 16);
```






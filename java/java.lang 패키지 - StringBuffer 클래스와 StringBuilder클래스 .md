### 3.StringBuffer 클래스와 StringBuilder클래스

String은 생성할 때 지정한 문자열을 변경할 수 없다. (그래서 문자열 변경시마다 인스턴스가 새로 생성 된다.)

StringBuffer는 클래스 변경이 가능하다. (muttable) 

내부적으로 편집을 위한 버퍼(Buffer)를 가지고 있다.

생성할 때  그 크기를 지정할 수 있다.

이 때, 편집할 문자열의 길이를 고려하여 버퍼의 길이를 충분히 잡아주는 것이 좋다.

문자열이 버퍼의 길이를 넘어서면, 버퍼를 늘려주는 작업이 추가로 필요하기 때문이다.

String과 똑같이 char[] 로 문자열을 저장한다.



[TOC]

####  StringBuffer의 생성자

StringBuffer(int x) -> x만큼의 크기의 char[]을 생성.

StringBuffer() -> 16크기의 char[]을 생성. 크기를 지정하지 않으면 크기 16으로 버퍼를 생성.

StringBuffer(String x) -> x의 크기 + 16 크기의 char[]을 생성. 지정한 문자열보가 16이 더 크게 버퍼를 생성.





#### StringBuffer의 변경

```
StringBuffer sb = new StringBuffer("abc");	// sb = "abc"
sb.append("123");							// sb = "abc123"
sb.append("4").append("5"); 				// sb = "abc12345"
```

	StringBuffer sb  = new StringBuffer("abc");
	StringBuffer sb2 = sb;
	sb.append("1");
	System.out.println(sb);		// abc1		
	System.out.println(sb2);	// abc1




#### StringBuffer의 비교

StringBuffer안의 내용을 비교하려면, String으로 변경 후 비교해야한다.	

	StringBuffer sb  = new StringBuffer("abc");
	StringBuffer sb2 = new StringBuffer("abc");
	System.out.println(sb == sb2);				// false
	System.out.println(sb.equals(sb2));			// false
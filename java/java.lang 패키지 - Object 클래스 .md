## java.lang 패키지

자바에 가장 기본이 되는 클래스들을 포함하고 있다.

import없이 사용할 수 있게 되어 있다.

1. Object 클래스
2. String 클래스
3. StringBuffered, StingBuilder 클래스
4. Math 클래스
5. wrapper 클래스





### 1. Object 클래스

모든 클래스들의 최고 조상. 그래서 모든 클래스에서 바로 사용 가능.

1. public boolean equals(Object obj) : 같은 주소를 가르키는지. 객체의 내용이 아니라 객체의 주소를 체크.
2. public int hashCode() : 해당 객체의 해시코드 반환.
3. public String toString() 
4. protected Object clone() : 복사본을 반환한다.
5. public Class getClass()
6. protected void finalize()  : 거의 사용안함 가비지 컬렉터 관련 함수.
7. public void notify() 
8. public void notifyAll() 
9. public void wait(), wait(long timeout), wait(long titmeout, int nanos) 

7, 8, 9번은 쓰레드 관련 함수. 나중에 쓰레드할때 공부.

[TOC]



#### public boolean equals(Object obj)

		Value v1 = new Value(10);
		Value v2 = new Value(10);		
	
		v1.equals(v2) -> false
		
		v2 = v1;
	
		v1.equals(v2) -> true
객체 안 변수의 내용이 아니라 객체의 주소를 체크해서 같은지 확인시켜준다.

String 클래스나 Data, File, wrapper 클래스 등에서는 오버라이딩해줘서 내용만 같아도 true가 나온다.

의외로 StringBuffer클래스에서는 오버라이딩 해주지 않았다.





#### public int hashCode()

해시함수를 구현한 것. 

해시함수 : 임의의 길이의 데이터를 일정한 크기의 데이터로 변환 시키는 함수. 압축이랑 비슷.

		String str1 = new String("abc");
		String str2 = new String("abc");
	
		System.out.println(str1.equals(str2));
		System.out.println(str1.hashCode());
		System.out.println(str2.hashCode());
		System.out.println(System.identityHashCode(str1));
		System.out.println(System.identityHashCode(str2));
결과 값 

```
true
96354
96354
166239592
991505714
```

만약 String 클래스가 아니라면 false가 나왔을 것이다.

String 클래스에서 문자열 내용이 같으면 같은 해시코드를 반환하도록 오버라이딩이 되어있다.

(equals도 String클래스에서 오버라이딩 되어있다. 따라서 문자열 주소가 아니라 내용을 비교한다.)

System.identityHashCode 는 객체의 주소값으로 해시코드를 생성하므로 다른 값이 나온다.





#### public String toString()

객체.toString() 하면 보통 클래스이름+해시코드 값이 나온다 (hashCode 값과는 다름)

그냥 객체만 출력하는 것과 같다. ex) System.out.println(str1) = System.out.println(str1.toString())

	public String toString() {
		return "kind : " + kind + ", number : " + number;
	}
그래서 이런 식으로 오버라이딩을 시켜줘서 사용하기도한다.

String 클래스, Date 클래스 등 몇몇 클래스들은 해시코드처럼 오버라이딩이 되어있어서 저장된 값이 출력된다.





#### protected Object clone() 

	class Card implements Cloneable {
		@Override
		public Object clone() {
			Object obj = null;
			try {
				obj = super.clone();  // clone()은 반드시 예외처리를 해주어야 한다.
			} catch(CloneNotSupportedException e) {}
			return obj;
		}
	}
		Card c1 = new Card();
		Card c2 = new Card();
	
		c1 = (Card)c2.clone();
Object 안에있는 clone 메소드는 protected 접근제어자이기 때문에  implements Cloneable가 필요한 것이다.



JDK1.5 부터 '공변 반환타입'이라는 것이 생겼다.

```
class Card implements Cloneable {
	@Override
	public Card clone() {
		Object obj = null;
		try {
			obj = super.clone();  // clone()은 반드시 예외처리를 해주어야 한다.
		} catch(CloneNotSupportedException e) {}
		return (Card)obj;
	}
}
```

	Card c1 = new Card();
	Card c2 = new Card();
	
	c1 = c2.clone();
이런식으로 반환 객체를 자손 객체타입으로 반환 가능하게 됐다. 번거로운 형변환이 줄었다.



		int[] arr = {1,2,3,4,5};
		int[] arrClone = arr.clone(); 
이런 식으로 implements Cloneable 없이 사용 가능하다. 
배열 클래스에서는 public제어자로 오버리이딩이 되어있기 때문이다.

		int[] arr = {1,2,3,4,5};
		int[] arrClone = new int[arr.length];
		System.arraycopy(arr, 0, arrClone, 0, arr.length);
이런 식으로도 사용가능하다. 같은결과가 나온다.

Vector, ArrayList, LinkedList, Hashset, TressSet, HashMap, TreeMap, Calendar, Date와 같은 클래스들도 
ArrayList list2 = (ArrayList)list.clone(); 과 같은 형식으로 복제가 가능하다.



얕은 복사, 깊은 복사가 있다.

얕은 복사는 복사하는 객체안의 객체를 공유하게 된다. 
깊은 복사는 객체안의 객체를 새로만든다.

```
class Circle implements Cloneable {
	Point2 p; 	// 원점
	double r;	// 반지름

	Circle(Point2 p, double r) {
		this.p = p;
		this.r = r;
	}	
	
	public Circle shallowCopy() { // 얕은 복사
		Object obj = null;
	
		try {
			obj = super.clone();
		} catch (CloneNotSupportedException e) {}

		return (Circle)obj;
	}

	public Circle deepCopy() { // 깊은 복사
		Object obj = null;

		try {
			obj = super.clone();
		} catch (CloneNotSupportedException e) {}

		Circle c = (Circle)obj; 
		c.p = new Point2(this.p.x, this.p.y); 

		return c;
	}

	public String toString() {
		return "[p=" + p + ", r="+ r +"]";
	}
}
```

위 코드를 보면 깊은 복사에는 		

```
	Circle c = (Circle)obj; 
	c.p = new Point2(this.p.x, this.p.y); 
```

이 두줄이 추가된 것을 볼 수있다.

```
	Circle c1 = new Circle(new Point2(1, 1), 2.0);
	Circle c2 = c1.shallowCopy();
	Circle c3 = c1.deepCopy();	

	System.out.println("c1="+c1);
	System.out.println("c2="+c2);
	System.out.println("c3="+c3);
	c1.p.x = 9;
	c1.p.y = 9;
	System.out.println("= c1의 변경 후 =");
	System.out.println("c1="+c1);
	System.out.println("c2="+c2);
	System.out.println("c3="+c3);
```

위와 같이 실행하면 결과가

```
c1=[p=(1, 1), r=2.0]
c2=[p=(1, 1), r=2.0]
c3=[p=(1, 1), r=2.0]
= c1의 변경 후 =
c1=[p=(9, 9), r=2.0]
c2=[p=(9, 9), r=2.0]
c3=[p=(1, 1), r=2.0]
```

이렇게 나온다. 얕은 복사를한 객체의 Point를 서로 공유하는 것을 알 수 있다.





#### public Class getClass()

		Card3 c  = new Card3("HEART", 3);       // new연산자로 객체 생성
	
		Class cObj = c.getClass();
	
		System.out.println(c);
		System.out.println(c.getClass());
		System.out.println("----------------------");		
		System.out.println(cObj.getName());
		System.out.println(cObj.toGenericString());
		System.out.println(cObj.toString());		
		System.out.println("----------------------");		
		System.out.println(cObj.getSuperclass());		
		System.out.println(cObj.getDeclaredFields()[0]);		
		System.out.println(cObj.getDeclaredFields()[1]);		
결과 ↓ (package 이름이 PK01 이다.)

```
HEART:3
class PK01.Card3
----------------------
PK01.Card3
final class PK01.Card3
class PK01.Card3
----------------------
class java.lang.Object
java.lang.String PK01.Card3.kind
int PK01.Card3.num
```


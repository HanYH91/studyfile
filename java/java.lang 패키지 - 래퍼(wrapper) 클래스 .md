### 5. 래퍼(wrapper) 클래스

기본형은 객체가 아니다. (int, double, char 등...)
높은 성능이지만, 객체가 필요한 경우가 있다.
매개 변수로 객체를 요구할 떄, 객체로 저장해야 할 때, 객체 간의 비교가 필요할 때 등...

기본형 8개 -> 8개의 객체 클래스가 있다.

int, char 빼고는 앞글자만 대문자이다. ex) Double, Long, Boolean 등...

##### 생성자

Character('a') 만 ' ' 를 사용해서 char값만 입력 가능.

나머지는 Integer(100), ("100") 나 Boolean(true), ("true") 처럼 해당 기본형 or String형으로 입력 가능.

##### 메소드

equals(x), compareTo(x), toString()

MAX_VALUE : 해당 타입의 최대 값

MIN_VALUE : 해당 타입의 최소 값 

SIZE : 해당 타입의 비트 수 ex) Integer : 32bits

BYTES :  해당 타입의 바이트 수 ex) Integer : 4bytes

TYPE : 해당 타입의 기본타입형 이름



#### Numver 클래스

사실 Object클래스 밑에 Boolean클래스, Character클래스, Number클래스가 있고, 
나머지 6개의 클래스는 모두 Number클래스의 자손이다.

Number 밑에는 Long보다 더 큰 범위의 BigInteger과
double보다 더 큰 범위의 BigDecimal이 있다.





#### 문자열을 숫자로 변환하기

앞의 String 클래스에서 했다. 복습으로 다시한번 해본다.

int -> parse 사용, Interger -> valueOf 사용 이었지만,
오토박싱 때문에 무의미해졌다. 

성능은 거의 차이없지만 parse가 조금 낫다. (어차피 valueOf 함수안에서 parse사용하기 때문에)

Integer.parseInt("aa", 16) 처럼 n진수 값도 입력 가능하다.





#### 오토박싱 & 언박싱 (autoboxing & unboxing)

객체 값을 넣는 곳에 기본형 값을 넣어도 자동으로 형변환 해서 연산 해준다
-> 오토박싱

기본형 값을 넣는 곳에 객체 값을 넣어도 자동 형변환해서 연산 해준다.
-> 언박싱

객체 + 기본형 = 기본형 같은 것들이 가능해지는 것.

자동으로 형변환 해주는 편리한 기능일 뿐, 자바의 원칙이 바뀐 것은 아니다 !!!




### 4. Math

생성자가 private라서 Math인스턴스 생성 불가능.

모든 메소드, 변수가 static이기 때문에 인스턴스 생성할 필요도 이유도 없다.

멤버 변수는 딱 2개 있는데 double E, PI 두가지 이다. (자연로그의 밑, 원주율)





#### 올림, 버림, 반올림

반올림 : round()를 사용하는데 무조건 소수점 1쨰자리 수를 반올림한다. 35.457 round하면 36이 된다.
		따라서 보통 3째 자리수 반올림하고 싶으면 *100 -> round -> /100.0 을 한다.
                함수 안쓰고 그냥 *100 -> +0.5 -> int(long)로 형변환 -> /100.0 해도 된다.

​		rint(123.45) 도 반올림인데 차이점은, round반환 값은 long, rint반환 값은 double이다.
​		-> round(123.45)는 /100.0 해야되지만 rint(123.45)는 /100 해도 된다.
​		round(-1.5) = -1이 나오지만, rint(-1.5) = -2.0 이 나온다. (?? -2가 맞지 않나..)

올림 : ceil(123.4) = 124	ceil(-1234.5) = -1234

내림 : floor(123.6) = 123	floor(-1234.5) = -1235





#### 예외를 발생시키는 메소드

메소드 이름에 'Exact'가 포함된 메소드들. 
정수형간의 연산에서 발생할 수 있는 오버플로우를 감지하기 위한 것.
ex) 인트 최대 값에서 +1을 한다면 오버플로우 발생 최소 값에서 -1하면 오버플로우...

```
int addExact(int x, int y);			// x + y
int subtractExact(int x, int y);	// x - y
int multiplyExact(int x, int y);	// x * y
int incrementExact(int a);			// a++
int decrementExact(int a);			// a--
int negateExact(int a);				// -a. 2진법으로 보면 ~a+1 (2의 보수)이라서 오버플로우.
int toIntExact(long a);				// (int)a
```

오버플로우시 ArithmeticException 을 발생 시킨다.





#### 삼각함수와 지수, 로그

수학관련 함수들. 몇개만 보고 가자.

```
sqrt(a) 	// 루트 a
pow(3, 2)	// 3의 2승 (9)
sin(PI/2)	// PI는 180도. cos도 있다.
```







#### StrictMath 클래스

Math 클래스는 OS의 메소드를 호출에서 사용한다.
즉 부동소수점의 경우 OS마다 다른 계산이 나올 수도 있다.
이를 위해 성능을 버리고 항상 같은 결과를 얻기위해 Math클래스를 새로 작성한 것이 StrictMath 클래스이다.





#### Math클래스이 메소드

abs(x) : x의 절대값.

ceil(x) : x 올림. 

floor(x) : x 내림.

max(x, y) : 둘 중에 큰 수. 

min(x, y) : 둘 중에 작은 수.

random() : 0부터 1보다 작은 수 랜덤. *44 +1 하면 1~45의 수가 나옴. 

round(x), rint(x) : 반올림. long형, double형. -0.5 차이.














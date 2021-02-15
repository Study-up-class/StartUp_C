# Project 7
### 7-1 : 매개변수와 실인자의 구분<br>
### 7-2 : 값에 의한 전달<br>
  
= Call by Value. 
```C++
void doSomething(int y)
{
    cout << "In func " << y << " " << &y << endl;
}

int main()
{
    doSomething(5);

    int x = 6;

    cout << "In main " << x << " " << &x << endl;

    doSomething(x);
    doSomething(x+1);
}
```
<a href='https://ifh.cc/v-RnK2LP' target='_blank'><img src='https://ifh.cc/g/RnK2LP.png' border='0'></a>
### 7-3 : 참조에 의한 인수 전달<br>
  
= Call by Reference
```C++
void addOne(int &y)
{
    y = y + 1;
}

int main()
{
    int x = 5;

    cout << x << " " << &x << endl;

    addOne(x);

    cout << x << " " << &x << endl;  
}
```
<a href='https://ifh.cc/v-5wuH1c' target='_blank'><img src='https://ifh.cc/g/5wuH1c.png' border='0'></a>
<br>
```C++
void foo(int &x)
{
    cout << x << endl;
}

int main()
{
    foo(6);

    return 0;
}
```
-> 오류가 생길까 안생길까 !!?? <br><br><br>
: 생긴다

1. reference 떼기  
2. 인자에 const 선언하기<br>

```C++
void foo(int *&ptr)
{
    cout << ptr << " " << &ptr << endl;
}

int main()
{
    int x = 5;
    int *ptr = &x;

    cout << ptr << " " << &ptr << endl;
    foo(ptr);

    return 0;
}
```
<a href='https://ifh.cc/v-Un5OJV' target='_blank'><img src='https://ifh.cc/g/Un5OJV.png' border='0'></a>

### 7-4 : 주소에 의한 인수 전달<br>
= Call by Address
```C++
void foo(int *ptr)
{
    cout << *ptr << " " << ptr << " " << &ptr << endl;
}

int main()
{
    int value = 5;

    cout << value << " " << &value << endl;
    
    int *ptr = &value;

    foo(ptr);
    foo(&value);

    return 0;
}
```
<a href='https://ifh.cc/v-fjQbZq' target='_blank'><img src='https://ifh.cc/g/fjQbZq.png' border='0'></a>
### 7-5 : 다양한 반환 값들값, 참조, 주소, 구조체, 튜플<br>
```C++
int getValue(int x)
{
    int value = x * 2;
    return value;
}

int main()
{
    int value = getValue(5);
    return 0;
}
```
: 가장 기본적인 반환
### 7-6 : 인라인 함수<br>
```C++
inline int min(int x, int y)
{
    return x > y ? y : x ;
}

int main()
{
    cout << min(5, 6) << endl;
    cout << min(3, 2) << endl;

    cout << (5 > 6 ? 6 : 5) << endl;
    cout << (3 > 2 ? 2 : 3) << endl;
}
```
-> inline 선언을 하면 함수가 아닌 것처럼 작동하게 됨.  
[참고] 인라인 함수란 ?? https://placeforjake.tistory.com/44
### 7-7 : 함수 오버로딩<br>
: 동일한 이름을 가진 함수를 여러 개 만드는 것  
```C++
int add(int x, int y)
{
    return x + y;
}

int add(double x, double y)
{
    return x + y;
}

int main()
{
    add(1, 2);
    add(3.0, 4.0);
}
```
### 7-8 : 매개변수의 기본값<br>
```C++
void print(int x = 1024)
{
    cout << x << endl;
}

int main()
{
    print(10);
    print();
}
```
-> defaul 값이 1024로 설정됨.
```C++
void print(int x = 10, int y = 20, int z = 30)
{
    cout << x << " " << y << " " << z << endl;
}

int main()
{
    print();
    print(100);
    print(100, 200);
    print(100, 200, 300);

    return 0;
}
```
: 값이 어떻게 나올까요 ~~ !!
### 7-9 : 함수 포인터<br>
```C++
int func()
{
    return 5;
}

int main()
{
    cout << func << endl;

    return 0;
}
```
: 값이 어떻게 나올까요 !!(ㅈㅅㄱ)    
(hint !) 함수도 메모리에 들어오고, 포인터다 !!  
```C++
int func()
{
    return 5;
}

int goo()
{
    return 10;

}
int main()
{
    int (*fcnptr)() = func;

    cout << fcnptr() << endl;

    fcnptr = goo;

    cout << fcnptr() << endl;

    return 0;
}
```
: func 와 func()은 다르다  
: 주소값, 값의 차이
### 7-10 : 스택과 힙<br>
<a href='https://ifh.cc/v-j3q5jS' target='_blank'><img src='https://ifh.cc/g/j3q5jS.jpg' border='0'></a>  
[참고] 스택과 힙 설명 (https://m.blog.naver.com/PostView.nhn?blogId=codingspecialist&logNo=221195242403&proxyReferer=https:%2F%2Fwww.google.com%2F)
### 7-11 : std vector를 스택처럼 사용하기<br>
벡터 : new delete이 스스로 작동하는 동적 배열<br>
### 7-12 : 재귀적 함수 호출<br>
재귀적 함수 호출 -> 자기 자신을 호출하는 함수
```C++
void countDown(int count)
{
    cout << count << endl;
    countDown(count - 1);
}

int main()
{
    countDown(5);

    return 0;
}
```
주의점) recursion 함수를 만들 때 꼭 탈출조건을 명시해야함.<br>
### 7-13 : 방어적 프로그래밍의 개념<br>
여러 오류들을 만날 때 (syntax error, segmantic error 등)를 염두해두고 코드를 작성해야함.<br>
### 7-14 : 단언하기 assert<br>
assert 함수는 디버깅 모드에서 개발자가 오류가 생기면 치명적일 것이라고 생각하는 곳에 심어둔 에러 검출용 코드  
디버깅 모드에서만 작동되기 때문에 다른 코드에 영향을 주지 않는 코드만 넣어야 함  <br>
[참고] assert (https://blockdmask.tistory.com/286)
### 7-15 : 명령줄 인수 command line arguments<br>
[참고] microsoft reference (https://docs.microsoft.com/ko-kr/cpp/cpp/main-function-command-line-args?view=msvc-160)
### 7-16 : 생략부호 Ellipsis<br>
ellipsis -> 매개 변수가 정해지지 않았으면 좋겠을 때(?) ...을 사용하여 매개변수의 갯수를 제한하지 않는다.  
[참고] ellipsis (https://buildabetterworld.tistory.com/28)

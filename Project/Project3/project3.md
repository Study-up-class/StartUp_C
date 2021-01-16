# Project 3
### 3-1 : 연산자 우선순위  
비트연산자(&)와 논리연산자 주의(&&)  
우리가 생각하는 대부분은 && 두개 쓰는 것 !  
<a href='https://ifh.cc/v-TgII6U' target='_blank'><img src='https://ifh.cc/g/TgII6U.png' border='0'></a>
<br><br>

### 3-2 : 산술연산자
**+ - * /(몫) %(나머지)**   
나누기를 할 때 나누는 수, 나뉘어지는 수 둘 중 하나라도 실수면 값이 실수로 나옴  
= : 등호 연산자 (같다가 아닌 복사 느낌)
```
z += y;  
z = z + y;
```
(덧 나 곱 나머지, 몫 다 가능)  <br><br>

### 3-3 : 증가 감소 연산자  
```
int x = 5;  
int y = ++x;  
int z = x--;  
  
cout << y << endl;  
cout << z << endl;
```  

```
int x = 6, y = 6;  
case 1) cout << ++x << " " << ++y << endl;  
case 2) cout << x++ << " " << y++ << endl;
```
<br><br>  
  
### 3-4 : sizeof, 쉼표 연산자, 조건부 연산자  
sizeof : 데이터 자료형의 크기를 알 고 싶을 때 사용 (byte)  
1 byte = 8 bits  
 
```
float a;  
sizeof(float); // 4  
sizeof(a); // 4  
```

sizeof에는 변수와 자료형을 넣을 수 있음   
sizeof를 연산자로 저장해 놓았기에 sizeof a;이렇게 해도 동일  
  
**comma operator**  
```
int x = 3;  
int y = 10;  
//int z = (++x, ++y);  
++x;  
++y;  
int z = y;  
```

앞에 것 계산, 뒤에 것 계산, 뒤에 값을 변수에 넣어줌  
comma operator잘 안쓰고, 풀어서 많이 사용함  
구분하는 경우로 더 많이 사용함  

```
int a = 1, b = 10;  
int z;  
  
z = a, b;
```
->이러할 경우 =이 ,보다 우선순위가 높기 때문에  
우리가 기대하는 것(z에 b값 대입)이 나오지 않음  
이러한 경우에는 괄호를 사용해 우선순위를 명확하게 해줘야함  
(근데 쓰지말자,,,)  
  
conditional operator(조건부 연산자) = arithmetric if(몰라도 될듯)  

```
bool onSale = true;  
const int price = (onSale == true)? 10 : 100 ;  
//if(price);  
  
//if(onSale)  
//  price = 10;  
// else  
//  price = 100;  
```

1-1학과 수업에서 지저분한 tf 문제로 나왔던 기억이 있는데, 난 틀렸었다    
  <br><br>
  
### 3-5 : 관계연산자  
변수간의 관계를 나타낼 때 사용함(비교) 
```
== ( = 아님)  
!=  
>  
<  
>=   
<= 
```
보통 같고 크다(작다)라고 하기 보다는  
크거나(작거나) 같다라고 말하니 그 순서를 기억하면 될 것  
  
cmath 라이브러리에 abs사용해서 작은 차이를 알아볼 수 있는게 있음  
오차한계 변수를 만들어줌  <br><br>

### 3-6 : 논리연산자
<a href='https://ifh.cc/v-qCiouC' target='_blank'><img src='https://ifh.cc/g/qCiouC.png' border='0'></a>  
<a href='https://ifh.cc/v-ZpAjNQ' target='_blank'><img src='https://ifh.cc/g/ZpAjNQ.png' border='0'></a>  
**주의할 점 : && 연산자는 왼쪽이 false면 오른쪽 항 계산을 건너뜀 ->시간 절약을 위해서**  
**주의할 점 : &&연산자가 ||연산자보다 우선순위가 높다**
  
드모르간 법칙의 성립
```
!(x || y);
!x && !y;

반대의 경우도 동일
```
  <br><br>
### 3-7 : 이진수 (손으로 적으면서 익히는 것이 더 나음)  
<a href='https://ifh.cc/v-qDb8TS' target='_blank'><img src='https://ifh.cc/g/qDb8TS.png' border='0'></a>  
▲ 2진수를 10진수로 변환하는 것  <br>
<a href='https://ifh.cc/v-9uuHop' target='_blank'><img src='https://ifh.cc/g/9uuHop.png' border='0'></a>  
▲ 양의정수 2진수의 덧셈  <br><br>

양의정수를 음의정수로 바꾸는 방법 : 양의 정수 비트의 보수를 취한 후 1을 더함 (같이 해봐요 ^____^)  <br><br>
<a href='https://ifh.cc/v-ToD33V' target='_blank'><img src='https://ifh.cc/g/ToD33V.png' border='0'></a>  
▲ signed와 unsigned의 차이에 따라 값이 다름  <br><br>
### 3-8 : 비트연산자  
(메모리가 귀했을 시절에 비트연산자를 이용해서 메모리를 아끼고, 더 빠르게 하기 위해서 사용을 했는데 요즘에는 잘 안함)  <br>
```
unsigned int a = 3;
cout << std::bitset<4>(a) << endl; // 0011
unsigned int b = a << 1;
cout << std::bitset<4> << endl; // 0110
```
** 왼 쪽으로 한 자리씩 밀 때 마다 2배수가 된다.**  
** 오른 쪽으로 한 자리씩 밀 때 마다 1/2배수가 된다.**  

```
~ not operator
1을 0으로, 0을 1으로 변환
```
<a href='https://ifh.cc/v-JsFkdH' target='_blank'><img src='https://ifh.cc/g/JsFkdH.png' border='0'></a>  
<a href='https://ifh.cc/v-4CesVS' target='_blank'><img src='https://ifh.cc/g/4CesVS.png' border='0'></a>  

<br><br>
### 3-9 : 비트플래그, 비트마스크  
이거를 위해서 비트연산자들을 배웠다고 해도 과언이 아니다.라고 느꼈다  ㅎ ㅎ  
flag처리를 할 때 비트 플래그를 사용하면 좋을 것 같다(새로운 것을 느낌)  
quiz ! 단점은 뭘까요 ? 

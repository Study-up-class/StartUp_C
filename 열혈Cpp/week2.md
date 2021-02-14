# new & delete

### strcpy & strcpy_s

##### strcpy
```C++
#define _CRT_SECURE_NO_WARNINGS
#include <iostream>

char* MakeStrAdr(int len)
{
  char* str = (char*)malloc(sizeof(char) * len);
  return str;
}

int main()
{
  char* str = MakeStrAdr(20);
  strcpy(str, "I am so happy~);

  std::cout << str << std::endl;
  free(str);

  return 0;
}
```
strcpy의 경우 메모리의 사이즈를 지정하지 않기때문에 오류 발생

#define _CRT_SECURE_NO_WARNINGS 를 사용하면 강제로 오류 없이 사용은 가능하다.

##### strcpy_s
```C++
#include <iostream>
#include <cstring>

char* MakeStrAdr(int len)
{
  char* str = new char[len];
  
  return str;
}

int main()
{
  char happy[] = "I am so happy~";
  char* str = MakeStrAdr(20);
  int len;
  
  len = sizeof(happy);
  strcpy_s(str, len, happy);
  
  std::cout << str << std::endl;
  
  delete []str;
  
  return 0;
}
```
strcpy_s는 strcpy와 동일하나 문자열의 길이를 설정해주어야 한다.

### new

new 연산자는 동적으로 메모리를 할당하는 연산자이다.(C에서 malloc과 유사하지만 동작 방식에 차이가 있다.)
* new 연산자는 malloc과 달리 형 변환이 필요가 없다.
* '주소를 저장할 포인터' = new '할당하고 싶은 크기의 자료형'
 
  ex.
  
      int * number = new int;     //int형의 크기인 4bytes가 number의 메모리에 할당된다
  
      int * array = new int[10];  //int형 데이터 10개에 해당되는 메모리의 크기가 array의 메모리에 할당된다

### delete

delete 연산자는 new 연산자로 동적 할당된 메모리를 해제한다.

  ex.
  
      delete ptr;     //ptr에 동적 할당된 메모리 해제
  
      delete []array  //배열 ptr에 동적 할당된 메모리 해제

```C++
#include <iostream>
#include <string.h>

char * MakeStrAdr(int len)
{
  char * str = new char[len];           //str의 메모리에 전달받은 len * char 만큼의 bytes 할당
  
  return str;
}

int main()
{
  char * str = MakeStrAdr(20);          //20개의 char만큼의 크기를 str의 메모리에 할당
  strcpy_s(str, 20, "I am so happy~");  //str에 "I am so happy~" 복사
  
  std::cout << str << std::endl;
  
  delete []str;                         //str에 할당된 메모리 해제
  
  return 0;
}
```

## 문제
#### 2차원 평면상에서의 좌표를 구조체로 받고, 두 점의 함을 계산하는 함수를 만들어라.

```C++
#include <iostream>

typedef struct __Point
{
  int xpos;
  int ypos;
}Point;

Point& PntAdder(const Point& p1, const Point& p2)
{
  Point* PntAdd = new Point;                    //구조체 포인터에 Point 크기만큼 메모리 할당
  PntAdd->xpos = p1.xpos + p2.xpos;             //구조체 멤버에 접근하여 값 할당
  PntAdd->ypos = p1.ypos + p2.ypos;
  
  return *PntAdd;
}

int main()
{
  Point* Pnt1 = new Point;                      //구조체 포인터에 Point 크기만큼 메모리 할당
  Point* Pnt2 = new Point;
  
  std::cout << "1번 x좌표: ";
  std::cin >> Pnt1->xpos;
  std::cout << "1번 y좌표: ";
  std::cin >> Pnt1->ypos;
  std::cout << "2번 x좌표: ";
  std::cin >> Pnt2->xpos;
  std::cout << "2번 y좌표: ";
  std::cin >> Pnt2->ypos;
  
  Point& PointAdd = PntAdder(*Pnt1, *Pnt2);     //PntAdder(*Pnt1, *Pnt2)에 대한 참조자 PointAdd 선언
  
  std::cout << std::endl << "최종 좌표: (" << PointAdd.xpos << " , " << PointAdd.ypos << ")" << std::endl;
  
  delete Pnt1;                                  //Pnt1에 할당된 메모리 해제
  delete Pnt2;                                  //Pnt2에 할당된 메모리 해제
  delete& PointAdd;                             //PointAdd에 할당된 메모리 
  
  return 0;
}
```
![18](https://user-images.githubusercontent.com/76034423/105818487-5821b980-5ffa-11eb-84e4-901f482751ee.JPG)


### time, rand, srand

```C++
#include <iostream>
#include <cstdlib>
#include <ctime>

int main()
{
  srand(time(NULL));
  
  for(int i=0; i<5; i++)
  {
    std::cout<<"random number#"<<i<<": "<<rand() % 100<<std::endl;
  }
  
  return 0;
}
```

* time함수: 1970년 1월 1일 0시 0분 0초 부터 경과된 시간을 초(sec)로 반환하는 함수
* srand함수: srand(seed)에서 seed값과 매칭되는 숫자가 정해지는 함수
* rand함수: 0부터 RAND_MAX(default: 32767) 사이의 임의의 숫자를 반환하는 함수 (한번 컴파일되면 이후에도 동일한 숫자가 나온다)

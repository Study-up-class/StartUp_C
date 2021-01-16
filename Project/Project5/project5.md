# Project 프로그램의 구조

## KeyWord
1. 중단 Halt
2. 점프 goto, break, continue
3. 조건 분기  if, switch
4. 반복(루프) while, do while, for
5. 예외처리 try, catch, throw

## 내용
- 기본적인 반복문 공부 

## 더미코드.
```
#include <iostream>

int main()
{
	std::cout << "I love you " << std::endl;
	return 0;

	std::cout << "I love" << std::endl;
	return 0;

	std::cout << "I" << std::endl;
	exit(0);
}
```

exit은 return과 달리 프로그램이 절대로 무조건 중단되어야 할 경우 사용

[조건문 if]
```
#include <iostream>

int main()
{
	int x, y, z;
	std::cin >> x >> y >> z;

/////////////////////////////////////////////////////////////////////////////
예제1.
	if(x > 10)
		std::cout << x << "is greater than 10" << std::endl; 
	else
	{
		std::cout << x << "not is greater than 10" << std::endl;	
	}

/////////////////////////////////////////////////////////////////////////////
예제2.
	if(x > 10)
		std::cout << x << "is greater than 10" << std::endl; 
                std::cout << x << std::endl;
	else
		std::cout << x << "not is greater than 10" << std::endl;

/////////////////////////////////////////////////////////////////////////////
예제3.
 	if(x >= 10)
		if(x <= 20)
			std::cout << "x if between 10 an 20 " << std::endl;
	else
	{
		std::cout << "No" << std::endl;
 	}   

/////////////////////////////////////////////////////////////////////////////
예제4.
    if(x > 0 && y >0)
        std::cout << "both numbers are positive" << std::endl;
    else if(x > 0 || y > 0)
        std::cout << "one of the numbers is positive" << std::endl;
    else
        std::cout << "Neither number is positive << std::endl;

/////////////////////////////////////////////////////////////////////////////
예제5. 
    if(x > 0 && y > 0 && z)
        std::cout << "three numbers are positive" << std::endl;
    else if(x > 0 || y > 0)
        std::cout << "two of the numbers is positive" << std::endl;
    else
        std::cout << "Neither number is positive" << std::endl;

/////////////////////////////////////////////////////////////////////////////
보너스
    if(x > y) return y;
    else    return x;

    return (x > y) ? y : x;

/////////////////////////////////////////////////////////////////////////////
	return 0;
}
```

[Switch case]
```
int main()
{
    int x;
    std::cin >> x;

    switch(x)
    {
    case 0:
        std::cout << "Zero";
        break;
    case 1:
        std::cout << "One";
        break;
    case 2:
        std::cout << "two";
        break;
    default:
        std::cout << Noooo << std::endl;
    }
```
Quiz.
아래 1,2 번 골라보시오.
```
    enum class Colors
    {
        BLACK,
        RED,
        GREEN
    };
    Colors col;
```
```
1. 스위치 문에 enum의 Class 명이 들어가야한다.
    switch(Colors)
    {
    case 0:
        std::cout << "BLACK";
        break;
    case 1:
        std::cout << "RED";
        break;
    case 2:
        std::cout << "GREEN";
        break;
    }    

2. 스위치 문에 enum의 Class 생성자 명이 들어가야한다.
    switch(col)
    {
    case 0:
        std::cout << "BLACK";
        break;
    case 1:
        std::cout << "RED";
        break;
    case 2:
        std::cout << "GREEN";
        break;
    }
```
Quiz
x의 출력 값을 구해보시오.
```

    switch(col)
    {
    case 0:
        std::cout << "BLACK";
        int x = 5;
        std::cout << x;
    case 1:
        std::cout << "RED";
        std::cout << x;
    case 2:
        std::cout << "GREEN";
    }
}
```

[goto 문]
```
#include <iostream>

int main()
{
    double x;

tryAgain:
    std::cout << " Enter a non-negative number" << std::endl;
    std::cin >> x;

    if(x < 0.0)
        goto tryAgain;
    
    std::cout << x;
    
    return 0;
}
```
하지만 goto문은 반복문을 대신하기 위해 basic에서 사용을 했었지만 스파게티 코드가 될 수 있다. 이제는 반복문이 있으니 은퇴시켜주자...

```
{
    goto Skip;
    int x = 5;

    Skip:
        x += 3;
    std::cout << x;
    return 0;
}
```

## [While문]

##### while문이란?
- while문은 조건이 참인 동안 반복시키는 선조건비교 순환(loop문)이다.
... 선 평가 후 실행문
##### while문 형식
```
while(조건식)
{
    반복할 문장;
}
```
```
    while(1)
    while(true)
    while(0)
    while(false)
    while(x && y)
    while(x || y)
    while(...)
```
```
int main()
{
    int x = 10;
    while(1)
    {
        int count1 = 0;
        static int count2 = 0;
        cout << count1 << count2 << x << endl;
        ++count1;
        ++count2;
        ++x;
        
        if(count1 >= 10 && count2 >= 10)
            break;
    }
    
    unsigned int count = 10;
    while(count >= 0)
    {
        if(count == 0) cout << "zero";
        else cout << count << " ";

        count --;
    }

    int other_count = 1;
    while(outer_count < 5)
    {
        int inner_count = 1;
        while(inner_count <= outer_count)
        {
            cout << inner_count++ << " ";
        }
        cout << end;
        ++outer_count;
    }
    return 0;
}
```

## [do While문] 
- 반복할 문장을 우선 한번 실행 후 조건이 참일 동안 반복하는 후 조건 비교 반복문
...선실행 후 평가문
```
do
{
    반복할 문장
}while(조건식);
```
```
{
    int selection;
    do
    {
        cout << "1. add" << endl;
        cout << "2. add" << endl;
        cout << "3. add" << endl;
        cout << "4. add" << endl;
        cin >> selection;
    }while(selection <= 0 || selection >= 5);
    
    cout << "Your selected" << selection << endl;
    return 0;
}
```
## [for 문]
- 반복횟수가 정해진 순서로 돌아간다.
```
for(초기식; 조건식; 증감식)
{
    반복할 문장;
}
```
```
int main()
{
    using namespace std;
    for(int count = 0; count < 10; count++)
        cout << count << endl;

    int count = 0;
    for(; count < 10; count++)
        cout << count << endl;
    
    for(;;count++)
        cout << count << endl;
        

}
```
## 참조 링크, 사이트

## 담당자
- 연태민.

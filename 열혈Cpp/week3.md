# 클래스(class)

### 구조체 변수의 선언

##### struct

```c++
#include <iostream>

#define ID_LEN  20
#define MAX_SPD 200
#define FUEL_STEP   2
#define ACC_STEP    10
#define BRK_STEP    10

struct Car
{
    char gamerID[ID_LEN];
    int fuelGauge;
    int curSpeed;

    void ShowCarState()
    {
        std::cout<<"소유자 ID: "<<gamerID<<std::endl;
        std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
        std::cout<<"현재 속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
    }

    void Accel()
    {
        if(fuelGauge<=0)
            return;
        else
            fuelGauge-=FUEL_STEP;

        if(curSpeed+ACC_STEP>=MAX_SPD)
        {
            curSpeed=MAX_SPD;
            return;
        }
        
        curSpeed+=ACC_STEP;
    }

    void Break()
    {
        if(curSpeed<BRK_STEP)
        {
            curSpeed=0;
            return;
        }

        curSpeed-=BRK_STEP;
    }

};

int main()
{
    Car run99={"run",100,0};
    run99.Accel();    //run99라는 구조체 안의 Accel 함수
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    Car sped77={"speed77",100,0};
    sped77.Accel();   //sped77이라는 구조체 안의 Accel 함수
    sped77.Break();
    sped77.ShowCarState();

    return 0;
}
```

![1](https://user-images.githubusercontent.com/76034423/107912744-6f711880-6fa2-11eb-9631-061e361168d4.JPG)

### 문제

두개의 좌표의 x와 y값을 더하거나 이동시키는 함수를 만들어라

```c++
#include <iostream>

struct Point
{
    int xpos;
    int ypos;

    void MovePos(int x, int y)
    {
        xpos+=x;
        ypos+=y;
    }

    void AddPoint(const Point &pos)
    {
        xpos+=pos.xpos;
        ypos+=pos.ypos;
    }

    void ShowPosition()
    {
        std::cout<<"["<<xpos<<", "<<ypos<<"]"<<std::endl;
    }

};

int main()
{
    Point pos1={12,4};
    Point pos2={20,30};

    pos1.MovePos(-7,10);
    pos1.ShowPosition();

    pos1.AddPoint(pos2);
    pos1.ShowPosition();

    return 0;
}
```

![7](https://user-images.githubusercontent.com/76034423/107912755-71d37280-6fa2-11eb-9230-ec01cd34c12a.JPG)
### enum 상수의 선언

```c++
#include <iostream>

namespace CAR_CONST   //namespace안의 enum 상수 선언을 통해 상수 값 
{
    enum
    {
        ID_LEN      =20,
        MAX_SPD     =200,
        FUEL_STEP   =2,
        ACC_STEP    =10,
        BRK_STEP    =10,
    };
}

struct Car
{
    char gamerID[CAR_CONST::ID_LEN];
    int fuelGauge;
    int curSpeed;

   
    void ShowCarState()
    {
        std::cout<<"소유자 ID: "<<gamerID<<std::endl;
        std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
        std::cout<<"현재 속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
    }

    void Accel()
    {
        if(fuelGauge<=0)
            return;
        else
            fuelGauge-=CAR_CONST::FUEL_STEP;

        if(curSpeed+CAR_CONST::ACC_STEP>=CAR_CONST::MAX_SPD)
        {
            curSpeed=CAR_CONST::MAX_SPD;
            return;
        }
        
        curSpeed+=CAR_CONST::ACC_STEP;
    }

    void Break()
    {
        if(curSpeed<CAR_CONST::BRK_STEP)
        {
            curSpeed=0;
            return;
        }

        curSpeed-=CAR_CONST::BRK_STEP;
    }

};

int main()
{
    Car run99={"run",100,0};
    run99.Accel();
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    Car sped77={"speed77",100,0};
    sped77.Accel();
    sped77.Break();
    sped77.ShowCarState();

    return 0;
}
```

![2](https://user-images.githubusercontent.com/76034423/107912748-70a24580-6fa2-11eb-9852-31a40055eb7a.JPG)


### 구조체 안의 함수를 외부로 뺄 수 있다.
```c++
#include <iostream>

namespace CAR_CONST
{
    enum
    {
        ID_LEN      =20,
        MAX_SPD     =200,
        FUEL_STEP   =2,
        ACC_STEP    =10,
        BRK_STEP    =10,
    };
}

struct Car
{
    char gamerID[CAR_CONST::ID_LEN];
    int fuelGauge;
    int curSpeed;

    void ShowCarState();    //상태정보 출력
    void Accel();           //엑셀, 속도증가
    void Break();           //브레이크, 속도감소
};

 void Car::ShowCarState()   //구조체 안에서 선언된 함수의 정의
{
    std::cout<<"소유자 ID: "<<gamerID<<std::endl;
    std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
    std::cout<<"현재 속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
}

void Car::Accel()
{
    if(fuelGauge<=0)
        return;
    else
        fuelGauge-=CAR_CONST::FUEL_STEP;
    if(curSpeed+CAR_CONST::ACC_STEP>=CAR_CONST::MAX_SPD)
    {
        curSpeed=CAR_CONST::MAX_SPD;
        return;
    }
        
    curSpeed+=CAR_CONST::ACC_STEP;
}

void Car::Break()
{
    if(curSpeed<CAR_CONST::BRK_STEP)
    {
        curSpeed=0;
        return;
    }

    curSpeed-=CAR_CONST::BRK_STEP;
}

int main()
{
    Car run99={"run",100,0};
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    return 0;
}
```

![3](https://user-images.githubusercontent.com/76034423/107912749-70a24580-6fa2-11eb-85e4-95f60a6cacc1.JPG)

```c++
#include <iostream>
#include <cstring>

namespace CAR_CONST
{
    enum
    {
        ID_LEN=20, MAX_SPD=200, FUEL_STEP=2,
        ACC_STEP=10, BRK_STEP=10
    };
}

class Car   //접근제어 지시자(private, public)을 선언하지 않으면 private으로 선언된다.
{
private:
    char gamerID[CAR_CONST::ID_LEN];
    int fuelGauge;
    int curSpeed;
public:
    void InitMembers(char *ID, int fuel);
    void ShowCarState();    //함수를 클래스 외부로 빼도, 클래스의 일부. 함수 내에서 private으로 선언된 변수에 접근 가능하다.
    void Accel();
    void Break();    
};

void Car::InitMembers(char *ID, int fuel)
{
    strcpy(gamerID,ID);
    fuelGauge=fuel;
    curSpeed=0;
}

void Car::ShowCarState()
{
    std::cout<<"소유자 ID: "<<gamerID<<std::endl;
    std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
    std::cout<<"현재 속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
}

void Car::Accel()
{
    if(fuelGauge<=0)
        return;
    else
        fuelGauge-=CAR_CONST::FUEL_STEP;

    if(curSpeed+CAR_CONST::ACC_STEP>=CAR_CONST::MAX_SPD)
    {
        curSpeed=CAR_CONST::MAX_SPD;
        return;
    }
        
    curSpeed+=CAR_CONST::ACC_STEP;
}

void Car::Break()
{
    if(curSpeed<CAR_CONST::BRK_STEP)
    {
        curSpeed=0;
        return;
    }

    curSpeed-=CAR_CONST::BRK_STEP;
}

int main()
{
    Car run99;
    run99.InitMembers((char*)"run99", 100); //string을 char*로 변환X, 강제 형변환
    run99.Accel();
    run99.Accel();
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    return 0;
}
```

![4](https://user-images.githubusercontent.com/76034423/107912750-713adc00-6fa2-11eb-8e29-65ce93867293.JPG)

## C++에서의 파일 분할

* .h    클래스의 선언을 담는다.
* .cpp  클래스의 정의를 담는다.

#### car.h
```c++
#ifndef __CAR_H__   //헤더파일의 중복포함 문제를 해결하기 위한 매크로 선언
#define __CAR_H__   //헤더파일의 중복포함 문제를 해결하기 위한 매크로 선언

namespace CAR_CONST
{
    enum
    {
        ID_LEN=20, MAX_SPD=200, FUEL_STEP=2,
        ACC_STEP=10, BRK_STEP=10
    };
}

class Car
{
private:
    char gamerID[CAR_CONST::ID_LEN];
    int fuelGauge;
    int curSpeed;
public:
    void InitMembers(char *ID, int fuel);
    void ShowCarState();
    void Accel();
    void Break();
};

#endif
```

#### car.cpp

```c++
#include <iostream>
#include <cstring>
#include "Car.h"    //헤더파일

void Car::InitMembers(char * ID, int fuel)
{
    strcpy(gamerID, ID);
    fuelGauge=fuel;
    curSpeed=0;
}

void Car::ShowCarState()
{
    std::cout<<"소유자 ID: "<<gamerID<<std::endl;
    std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
    std::cout<<"현재속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
}

void Car::Accel()
{
    if(fuelGauge<=0)
        return;
    else
        fuelGauge-=CAR_CONST::FUEL_STEP;

    if((curSpeed+CAR_CONST::ACC_STEP)>=CAR_CONST::MAX_SPD)
    {
        curSpeed=CAR_CONST::MAX_SPD;
        return;
    }
    curSpeed+=CAR_CONST::ACC_STEP;
}

void Car::Break()
{
    if(curSpeed<CAR_CONST::BRK_STEP)
    {
        curSpeed=0;
        return;
    }
    curSpeed-=CAR_CONST::BRK_STEP;
}
```

#### RacingMain.cpp

```c++
#include "Car.h"

int main()
{
    Car run99;
    run99.InitMembers((char*)"run99",100);
    run99.Accel();
    run99.Accel();
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    return 0;
}
```

![5](https://user-images.githubusercontent.com/76034423/107912752-713adc00-6fa2-11eb-9788-83ced535d2f8.JPG)

### inline 함수

* inline 함수는 클래스의 선언과 동일한 파일에 저장되어 컴파일러가 동시에 참조할 수 있게 해야 한다.

#### classinline.h

```c++
#ifndef __CLASSINLINE_H__
#define __CLASSINLINE_H__

#include <iostream>

namespace CAR_CONST
{
    enum
    {
        ID_LEN=20, MAX_SPD=200, FUEL_STEP=2,
        ACC_STEP=10, BRK_STEP=10
    };
}

class Car
{
private:
    char gamerID[CAR_CONST::ID_LEN];
    int fuelGauge;
    int curSpeed;
public:
    void InitMembers(char*ID, int fuel);
    void ShowCarState();
    void Accel();
    void Break();
};

inline void Car::ShowCarState()   //inline 함수는 class가 선언된 같은 파일에 저장되어야 한다.
{
    std::cout<<"소유자 ID: "<<gamerID<<std::endl;
    std::cout<<"연료량: "<<fuelGauge<<"%"<<std::endl;
    std::cout<<"현재속도: "<<curSpeed<<"km/h"<<std::endl<<std::endl;
}

inline void Car::Break()
{
    if(curSpeed<CAR_CONST::BRK_STEP)
    {
        curSpeed=0;
        return;
    }
    curSpeed-=CAR_CONST::BRK_STEP;
}

#endif
```

#### classinline.cpp

```c++
#include <cstring>
#include "classinline.h"

void Car::InitMembers(char * ID, int fuel)
{
    strcpy(gamerID, ID);
    fuelGauge=fuel;
    curSpeed=0;
}

void Car::Accel()
{
    if(fuelGauge<=0)
        return;
    else
        fuelGauge-=CAR_CONST::FUEL_STEP;

    if(curSpeed+CAR_CONST::ACC_STEP>=CAR_CONST::MAX_SPD)
    {
        curSpeed=CAR_CONST::MAX_SPD;
        return;
    }
    curSpeed+=CAR_CONST::ACC_STEP;
}
```

#### racinginline.cpp

```c++
#include "classinline.h"

int main()
{
    Car run99;
    run99.InitMembers((char *)"run99",100);
    run99.Accel();
    run99.Accel();
    run99.Accel();
    run99.ShowCarState();
    run99.Break();
    run99.ShowCarState();

    return 0;
}
```

![6](https://user-images.githubusercontent.com/76034423/107912753-71d37280-6fa2-11eb-8c04-01651c1d5c8e.JPG)

### 문제

##### 1.

계산기 기능의 Calculator 클래스를 정의하라

```c++
#include <iostream>

class Calculator
{
private:
    double x, y, add, min, div, mul;
    int num_add, num_min, num_div, num_mul;

public:
    void Init()
    {
        x=0;
        y=0;
        num_add=0;
        num_min=0;
        num_div=0;
        num_mul=0;
    }

    double Add(double x, double y)
    {
        add=x+y;
        num_add++;

        return add;
    }

    double Div(double x, double y)
    {
        div=x/y;
        num_div++;

        return div;
    }

    double Min(double x, double y)
    {
        min=x-y;
        num_min++;

        return min;
    }

    double Mul(double x, double y)
    {
        mul=x*y;
        num_mul++;

        return mul;
    }

    void ShowOpCount()
    {
        std::cout<<"덧셈: "<<num_add<<" 뺄셈: "<<num_min<<" 곱셈: "<<num_mul<<" 나눗셈: "<<num_div<<std::endl<<std::endl;
    }
};


int main()
{
    Calculator cal;
    cal.Init();

    std::cout<<"3.2 + 2.4 = "<<cal.Add(3.2,2.4)<<std::endl;
    std::cout<<"3.5 / 1.7 = "<<cal.Div(3.5,1.7)<<std::endl;
    std::cout<<"2.2 - 1.5 = "<<cal.Min(2.2,1.5)<<std::endl;
    std::cout<<"4.9 / 1.2 = "<<cal.Div(4.9,1.2)<<std::endl;
    cal.ShowOpCount();

    return 0;
}
```

![8](https://user-images.githubusercontent.com/76034423/107912756-71d37280-6fa2-11eb-856d-7dacf5f33e93.JPG)

##### 2
문자열을 저장하고 출력하는 기능을 하는, 문자열 정보를 내부에 저장하는 Printer라는 이름의 클래스를 만들어라.

```c++
#include <iostream>
#include <cstring>

#define LINE_LEN    20

class Printer
{
private:
    char* ch;

public:
    void SetString(char * str)
    {
        strcpy(ch,str);

    }

    void ShowString()
    {
        std::cout<<ch<<std::endl;
    }
};

int main()
{
    Printer pnt;
    pnt.SetString((char*)"Hello World!");
    pnt.ShowString();

    pnt.SetString((char*)"I Love C++");
    pnt.ShowString();

    return 0;
}
```

![9](https://user-images.githubusercontent.com/76034423/107912757-726c0900-6fa2-11eb-82ad-988130ec411d.JPG)

### 최종 예제

```c++
#include <iostream>

class FruitSeller
{
private:
    int APPLE_PRICE;
    int numOfApples;
    int myMoney;

public:
    void InitMembers(int price, int num, int money)
    {
        APPLE_PRICE=price;
        numOfApples=num;
        myMoney=money;
    }

    int SaleApples(int money)
    {
        int num=money/APPLE_PRICE;
        numOfApples-=num;
        myMoney+=money;

        return num;
    }

    void ShowSalesResult()
    {
        std::cout<<"남은 사과: "<<numOfApples<<std::endl;
        std::cout<<"판매 수익: "<<myMoney<<std::endl;
    }
};

class FruitBuyer
{
    int myMoney;        //private
    int numOfApples;    //private

public:
    void InitMembers(int money)
    {
        myMoney=money;
        numOfApples=0;
    }

    void BuyApples(FruitSeller &seller, int money)
    {
        numOfApples+=seller.SaleApples(money);
        myMoney-=money;
    }

    void ShowBuyResult()
    {
        std::cout<<"현재 잔액: "<<myMoney<<std::endl;
        std::cout<<"사과 개수: "<<numOfApples<<std::endl<<std::endl;
    }
};

int main()
{
    FruitSeller seller;
    seller.InitMembers(1000,20,0);
    FruitBuyer buyer;
    buyer.InitMembers(5000);
    buyer.BuyApples(seller, 2000);

    std::cout<<"과일 판매자의 현황: "<<std::endl;
    seller.ShowSalesResult();

    std::cout<<"과일 구매자의 현황: "<<std::endl;
    buyer.ShowBuyResult();

    return 0;
}
```

![10](https://user-images.githubusercontent.com/76034423/107912759-726c0900-6fa2-11eb-9460-c26313b48a98.JPG)

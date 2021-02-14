# 6.2
## 배열의 기초  
### quiz

```C++
void do(int array[20])
{
    std::cout << &array << std::endl;

}

int main()
{
    int array[20];
    std::cout << &array << std::endl;

    do(array);
}
```
    
    
# 6.6
## c언어 스타일의 배열 문자열
### example
```C++
char string[255];
std::cin << string;       //Hello world ! 입력
string[4] = '/0'
```

### strcpy vs strcpy_s
+ 기존의 c에서는 strcpy가 사용가능 하나 메모리를 구체적으로 지정해주지 않기 때문에 불안정성이 있음
+ 이를 보완하기 위해 c++에서는 메모리 사이즈가 파라미터로 들어가는 strcpy_s 사용이 권장(반강제) 됨

# 6.7
## 포인터의 기본적인 사용법
### example
```C++
int x;
cout << x << endl;
cout << &x << endl;   // 메모리 주소 직접 출력
```
+ 포인터 변수 : 메모리 주소를 담는 변수를 포인터 변수라고 한다
```C++
int *ptr = &x         // 변수 x의 메모리 주소를 담는 포인터변수 ptr 선언

cout << ptr << endl;  // x의 메모리 주소 출력
cout << *ptr << endl; // 포인터 변수 ptr을 de-reference 하여 메모리 주소의 값 x 출력
```
+ 위 선언부의 *과 아래 cout 부분의 *은 다르다.
+ 위의 *은 단순 포인터변수임을 표기하기 위한 수단이고 사실상 주소가 담겨있는 변수는 ptr이다.
+ *ptr은 ptr이 주소값이기때문에 이걸 de - reference하는 연산이다.

# 6.7a
## null pointer  
예외 처리시에 사용

# 6.8
## 포인터와 정적배열
```C++
int array[5] = {9, 7, 5, 3, 1};
cout << &array;
cout << &array[0];
```
+ &array = &array[0]
+ 배열의 주소값을 불러오면 첫 시작 주소값, 즉 [0]을 불러온다는 뜻

# 6.9
## 포인터 연산과 인덱싱
```C++
int *ptr = &value;
cout << ptr + 1;
```


# 6.11
## 메모리 동적 할당
### new delete


# 6.13 
## 포인터와 const
### quiz 1
```C++
const int n = 7;
1) int *ptr = &n; (x)
2) const int *ptr = &n; (o)
```
### quiz 2
```C++
int value = 5;
const int *ptr = &value;
1) *ptr = 6; (x)
2) value = 6; (o)
```

### quiz 3
```C++
int value1 = 5;
const int *ptr = &value1;

int value2 = 6;
ptr = &value2;
```
+ pointer에서의 const는 &value1 즉 메모리 주소에 들어있는 값을 안바꾸겠다는 의미
+ ptr에 들어있는 메모리주소는 바꿀 수 있다.



# 6.14 
## 참조변수
### reference를 쓰는 이유?
+ 함수 내부, 즉 지역변수 외의 지역에서도 값에 대한 영향력을 행사할 수 있어서

### example
+ function(int x) VS function(int& x) ?
```C++

void do_normal(int array[20])
{
    for (int i = 0; i < 20; i++)
        array[i] = 3;
}

void do_reference(int &array[20])
{
    for (int i = 0; i < 20; i++)
        array[i] = 3; 
}

int main()
{
    int array[20] = {1, 2, 3, 4, 5};
    do_normal(array);
    for (int i = 0; i < 20; i++)
        std::cout << array << std::endl;
    
    do_reference(array);
    for (int i = 0; i < 20; i++)
        std::cout << array << std::endl;

    return 0;
}
```
# 6.15
## 참조와 const
### example
+ function(int& x) VS function(const int& x)  ??
```C++
int a = 1;
function(a);
function(1);
```

# 6.16
## 포인터와 참조의 멤버 선택 연산자
### example
```C++
struct Person
{
    int age;
    double weight;
}

int main()
{
    Person person;

    person.age = 5;
    person.weight = 30;

    Person &ref = person;    // case : reference
    ref.age = 15;

    Person *ptr = &person;   // case : pointer
    ptr->age = 15;
    (*ptr).age = 15;
}
```

# 6.17
## for-each 반복문
### example
```C++
int array[] = { 1, 2, 3, 4, 5};
for (int number : array)
    std::cout << array[number];
```

# 6.18
## Void Pointer

# 6.19
## 이중 포인터와 동적 다차원 배열
+ 2차원 행렬 구현에서 이중 포인터를 자주 사용
### example
```C++
int main()
{
    const int row = 3;
    const int col = 5;

    const int s2da[row][col] =
    {
        {1, 2, 3, 4, 5},
        {1, 2, 3, 4, 5},
        {1, 2, 3, 4, 5},
    };

    int *r1 = new int[col] { 1, 2, 3, 4, 5};
    int *r2 = new int[col] { 1, 2, 3, 4, 5};
    int *r3 = new int[col] { 1, 2, 3, 4, 5};

    int **rows = new int*[row] {r1, r2, r3};

    return 0;
}
```








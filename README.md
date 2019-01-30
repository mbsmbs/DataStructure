## 기본 자료구조

### 자료구조는 자료를 효율적으로 이용할 수 있도록 컴퓨터에 저장하는 방법을 말합니다.

#### 배열 : 같은 자료형의 변수로 이루어진 요소(element)가 모여 직선 모양으로 줄지어 있는 자료구조 입니다.

```C
//배열의 요소 개수와 각 요소의 값을 출력합니다.
#include <stdio.h>

int main(int argc, char const *argv[])
{
    int i;
    int a[5] = {1, 2, 3, 4, 5};//배열 생성, 초기화
    int na = sizeof(a) / sizeof(a[0]); // 요소의 개수
    printf("배열 a의 요소 개수는 %d 입니다.\n", na);

    for(i = 0; i < na; i ++)
    {
        printf("a[%d] = %d\n", i, a[i]);
    }
    return 0;
}
```

#### 메모리 할당 기간과 동적 객체 생성
##### int형 객체를 동적으로 생성하고 해제합니다.
```C
//int형 포인터 변수를 동적으로 생성하고 해제합니다.
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int * x; // int형 포인터 변수를 생성

    x = calloc(1, sizeof(int)); // calloc함수를 이용하여 포인터 변수 x에 정수형 메모리 사이즈만큼 한개의 메모리 공간을 할당
    
    if(x == NULL) // x에 할당 된 메모리 공간이 없으면
    {
        puts("메모리 할당에 실패했습니다.");
    }
    else // x에 할당 된 메모리 공간이 있으면 
    {
        *x = 57; // 포인터에 연결된 메모리의 값에 57을 대입
        printf("*x = %d\n", *x); // 대입된 값을 출력
    }

    free(x); // x에 할당된 메모리를 해제한다.
    
    return 0;
}
```

##### int형 배열을 동적으로 생성하고 해제합니다.
```C
//int형 배열을 동적으로 생성하고 해제합니다.
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int i; // 반복문에서 사용할 int형 변수를 선언
    int *a; // 메모리 공간을 할당해줄 정수형 포인터 변수를 선언
    int na; // 배열의 요소 갯수 값을 입력 받을 변수를 선언
    printf("요소 개수 : "); // 출력
    scanf("%d", &na); // 값을 입력 받아서 위에서 선언된 na에 대입
    a = calloc(na, sizeof(int)); //위에서 선언된 포인터 변수에 정수형 메모리 사이즈로 요소 갯수만큼 메모리공간을 생성

    if(a == NULL) // 포인터 변수에 메모리 할당이 안된경우
        puts("메모리 확보에 실패했습니다.");
    else // // 포인터 변수에 메모리 할당 된경우
    {
        printf("%d개의 정수를 입력하세요.\n"); // 출력
        for( i = 0; i < na; i++) // 요소갯수만큼 반복
        {
            printf("a[%d] : ", i); // 출력
            scanf("%d", &a[i]); // 입력받은 값들을 그 배열의 첫번째 요소 부터 na번째 요소까지 대입
        }
        
        printf("각 요솟값은 아래와 같습니다.\n"); // 출력
        
        for(i = 0; i < na; i++) // 요소갯수만큼 반복
        {
            printf("a[%d] = %d\n", i, a[i]); //배열의 첫번째 값부터 요소갯수 번째 값까지 출력
        }

        free(a); // a에 할당된 메모리 공간 해제
    }
    
    return 0;
}
```

##### 배열 요소의 최댓값을 구합니다.
```C
// 배열 요소의 최댓값을 구합니다. (값을 입력합니다.)
#include <stdio.h>
#include <stdlib.h>

//요소 갯수가 n인 배열 a의 요소의 최대 값을 구하는 함수
int maxof(const int a[], int n) // 함수안에 매개변수로 배열표기 const int a[]는 const int * a와 같습니다. 즉 포인터 선언
                                // const는 함수안에서 배열의 값들을 읽기는 가능하나 쓰기는 불가능함.
                                // n은 요소갯수
{
    int i; //반복문에서 사용할 변수 선언
    int max = a[0]; // a 배열의 첫번째 값을 최대 값으로 설정

    for(i = 1; i < n; i++) // 함수 선언시 입력 받은 2번쩨값 ~ n값 만큼 반복 
    {
        if(a[i] > max) max = a[i]; // 2번째부터 n번째까지 max와 비교하면서 크면 max에 대입
    }
    return max; // 최종 max의 값을 반환한다.
}

int main(void)
{
    int i; // 반복문에서 사용할 변수 선언
    int * height; // 포인터 변수 선언
    int number; // 사람 수를 입력 받을 변수 선언
    
    printf("사람 수 : "); // 출력
    scanf("%d", &number); // 입력 받은 값을 number변수에 대입
    
    height = calloc(number, sizeof(int)); // 포인터 변수에 정수형 메모리공간을 number수 만큼 할당한다. 
    
    printf("%d 사람의 키를 입력하세요.\n", number); // number의 값을 출력
    
    for( i = 0; i < number; i++) // number 수 만큼 반복
    {
        printf("height[%d] : ", i); // 출력
        scanf("%d", &height[i]); // 차례대로 입력받은 값을 생성된 배열의 첫번째부터 number번째 까지 차례대로 대입을 하고
    }
    
    // maxof함수의 인자 값을 height에 입력된 사람의 키 정보와 number에 입력받은 사람의 수 정보를 넣고 함수 호출 및 출력
    // const int a[] =  const int * a = height = calloc(number, sizeof(int)) & int n = number
    printf("최댓값은 %d입니다.\n", maxof(height, number)); 
    
    free(height); //height에 할당한 메모리 해제

    return 0;
}
```

##### 배열 요소의 최댓값을 구합니다. (값을 난수로 생성)
```C
// 배열 요소의 최댓값을 구합니다. (값을 난수로 생성)
#include <stdio.h>
#include <stdlib.h>
#include <time.h>


//n개의 요소를 가진 a배열의 최대값을 구합니다.
int maxof(const int a[], int n)
{
    int i; // 반복문에서 사용할 변수 선언
    int max = a[0]; // 최대값 초기화
    for(i = 0; i < n; i++) // 요소갯수 n번 만큼 반복
    {
        if(a[i] > max) max = a[i]; //배열의 값들을 차례대로 max값과 비교하고 만약에 크면 max에 대입
    }
    return max; // 최종 max 반환
}

int main(int argc, char const *argv[])
{
    int i; // 반복문에 사용할 변수 선언
    int * height; // 포인터 변수 선언
    int number; // 사람 수의 정보를 담을 변수 선언
    
    printf("사람 수 : "); // 출력
    scanf("%d", &number); // 입력받은 수를 number에 대입
    
    height = calloc(number, sizeof(int)); // 포인터 변수에 정수형 메모리 사이즈로 number 갯수 만큼 메모리 할당
    
    srand(time(NULL)); // 시간으로 난수의 seed를 초기화
    
    for(i = 0; i < number; i++) // number 만큼 반복
    {
        height[i] = 1 + rand() % 90; // 100 ~ 189의 난수를 생성, 대입
        printf("height[%d] = %d\n", i, height[i]); // height에 차례대로 대입
    }
    
    printf("최대값은 %d입니다.\n", maxof(height, number)); // maxof함수를 호출하여 최대값을 받고 출력

    free(height); //height에 할당된 메모리 해제

    return 0;
}
```

##### 배열을 역순으로 정렬합니다.
```C
//배열을 역순으로 정렬합니다.
#include <stdio.h>
#include <stdlib.>

//type형 x와 y값을 교환
#define swap(type, x, y) do{ type t = x; x =y; y =t;} while(0)

// 요소 갯수가 n인 배열 a의 요소를 역순으로 정렬
void ary_reverse(int a[], int n)
{
    int i;
    for( i = 0; i < n / 2; i++) // 입력받은 요소 갯수 만큼 반복
    {
        swap(int, a[i], a[ n - i - 1 ]); // do{ int t = a[i]; a[i] = a[n - i - 1]; a[n - i - 1] = t;} while(0);
    }
}

int main(int argc, char const *argv[])
{
    int i;
    int * x; // 배열 첫번째 요소의 포인터
    int nx; // 배열 x의 요소 개수

    printf("요소 개수 : ");
    scanf("%d", &nx); // 요소 개수 입력 받음

    x = calloc(nx, sizeof(int)); // x에 int형 size에 nx 수 만큼 메모리 할당
    
    printf("%d개의 정수를 입력하세요.\n", nx); // 요소갯수 출력
    
    for(i = 0; i < nx; i++) // 요소 갯수만큼 반복
    {
        printf("x[%d] = %d\n", i, x[i]); // 출력
    }
    
    ary_reverse(x, nx); //x에 배열 생성했고 nx 배열의 요소갯수를 입력 받았으니 역순으로 정렬하는 함수 호출
    
    printf("배열의 요소를 역순으로 정렬했습니다.\n");
    
    for(i = 0; i < nx; i++)
    {
        printf("x[%d] = %d\n", i, x[i]);
    }

    free(x); // 배열 x 해제

    return 0;
}
```

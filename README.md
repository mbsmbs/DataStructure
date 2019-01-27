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
##### calloc()와 malloc() 2가지
##### calloc()

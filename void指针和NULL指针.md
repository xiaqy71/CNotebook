# void指针和NULL指针

## void 指针

void：无类型

不可使用 void 定义一个变量，但是可以用 void 定义指针  
​`void *p`​,称之为通用指针，  
任何类型的指针都可以赋值给 void 指针  
例

```c
#include <stdio.h>

#define MAX 100

int main(void)
{
    int num = 1024;
    int *pi = &num;
    char *ps = "FishC";
    void *pv;

    pv =  (int *)pi;
    printf("pv: %p, pi: %p \n", pv, pi);

    pv = ps;
    printf("pv: %p, ps: %p \n", pv, ps);

    return 0;
}
```

*不要尝试直接对 void 指针进行解引用， 一定要使用的话在前面加上强制类型转换*

## NULL 指针

在c语言中，NULL的定义如下:  
​`#define NULL ((void)*)0)`​

NULL 用于指针和对象，表示控制， 指向一个不被使用的地址。  
当还不清楚将指针初始化为什么地址时， 先将它初始化为 NULL

```c
#include <stdio.h>

int main()
{
        int array[5] = {1, 2, 3, 4, 5};
        int *pi = &array[2];
        void *pv;

        pv = pi;
        pv++;
        pi = pv;

        printf("%d\n", *pi);

        return 0;
}
```

打印的是 67108864

‍

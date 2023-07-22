# switch语句

```c
#include <stdio.h>

int main() {
    int n1, n2;
    char c;
    scanf("%d%c%d", &n1, &c, &n2);
    switch (c)
    {
    case'+':
        printf("%d%c%d=%d\n", n1, c, n2, n1 + n2);
        break;
    case'-':
        printf("%d%c%d=%d\n", n1, c, n2, n1 - n2);
        break;
    case'*':
        printf("%d%c%d=%d\n", n1, c, n2, n1 * n2);
        break;
    case'/': {
        if (n2 == 0) {
            printf("除数不能为0\n");
            break;
        }
        printf("%d%c%d=%d\n", n1, c, n2, n1 / n2);
        break;
    }
    default:
        printf("输入错误\n");
        break;
    }
    return 0;
}
```

任意两个 case 跟随的整型常量值不能相同

‍

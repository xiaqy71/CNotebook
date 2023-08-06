# 题解

##  1. <a name=''></a>稀疏矩阵

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int row = 0, col = 0;
    scanf("%d%d", &row, &col);
    int **nums = (int **)malloc(sizeof(int *) * row);
    for (int i = 0; i < row; i++) {
        nums[i] = (int *)malloc(sizeof(int) * col);
    }
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            scanf("%d", &nums[i][j]);
        }
    }
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < col; j++) {
            if (nums[i][j] != 0) {
                printf("%d %d %d\n", i + 1, j + 1, nums[i][j]);
            }
        }
    }
    return 0;
}

```

##  2. <a name='-1'></a>矩阵转置

```c
#include <stdio.h>

int main(void) {
    int nums[100][100];
    int n, m;
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            scanf("%d", &nums[i][j]);
        }
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {
            int t = nums[i][j];
            nums[i][j] = nums[j][i];
            nums[j][i] = t;
        }
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", nums[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

##  3. <a name='-1'></a>图像旋转

```c
#include <stdio.h>

int main(void) {
    int nums[100][100];
    int m = 0, n = 0;
    int c = 0, v = 0;
    scanf("%d%d", &m, &n);
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &nums[i][j]);
        }
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            printf("%d ", nums[m - 1 - j][i]);
        }
        printf("\n");
    }
    return 0;
}

```

##  4. <a name='-1'></a>蛇形填数

```c
#include <stdio.h>

int main(void) {
    int nums[20][20] = {0};
    int n = 0, k = 1, t = 0;
    int i = 0, j = 0;
    scanf("%d", &n);
    j = n - 1;
    t = n;
    while(k <= n * n){
        while(i < t){
            nums[i][j] = k++;
            i++;
        }
        i--;
        j--;
        while(j > n - t){
            nums[i][j] = k++;
            j--;
        }
        while(i > n - t){
            nums[i][j] = k++;
            i--;
        }
        while(j < t - 2){
            nums[i][j] = k++;
            j++;
        }
        t--;
    }
    for (int i = 0; i < n;i++){
        for (int j = 0; j < n;j++){
            printf("%2d ", nums[i][j]);
        }
        printf("\n");
    }
    return 0;
}

```

##  5. <a name='-1'></a>机器翻译

```c
#include <stdio.h>
#include <stdlib.h>

int memory[1001] = { 0 }; //内存 下标表示单词 数值代表在内存中的位置
int ans = 0;//记录查找次数
int m, n, x;//m表示内存大小 n是文章单词数 x代表当前单词

void rep() {//重置内存
    int sum = 0;//前移次数
    if (memory[x] == 0 && ans >= m) {//需要查找 并且内存已满
        ans++;
        for (int i = 0; i <= 1000; i++) {
            if (memory[i] >= 1) {
                memory[i]--;//将单词在内存中的位置前移1
                sum++;
            }
            if (sum == m) {
                break;
            }
        }
        if (m > 0) {
            memory[x] = m;
        }

    }

}

int main() {
    scanf("%d%d", &m, &n);
    int i = 1;
    while (i <= n) {
        scanf("%d", &x);
        if (memory[x] == 0 && ans < m) {
            ans++;
            memory[x] = ans;
        }
        else {
            rep();
        }
        i++;
    }
    printf("%d", ans);
    return 0;
}
```

##  6. <a name='-1'></a>删除有序数组中的重复项

```c
int removeDuplicates(int* nums, int numSize) {
    if (numsSize == 0 || numsSize == 1) {
        return numsSize;
    }
    int k = 1;
    int p0 = 0, p1 = 1;
    while (p1 < numsSize) {
        if (nums[p0] == nums[p1]) {
            p1++;
        }
        else {
            k++;
            nums[++p0] = nums[p1];
        }
    }
    return k;
}
```

##  7. <a name='-1'></a>移除元素

```c
int delValEqual(int* nums, int numSize, int val) {
    if (numSize == 1 && *nums == val) {
        return 0;
    }
    int p0 = 0;
    int p1 = numSize - 1;
    int newNumSize = 0;
    while (p0 <= p1) {
        if (nums[p0] == val) {
            while (nums[p1] == val && p0 < p1) {
                p1--;
            }
            nums[p0] = nums[p1];
            p1--;
        }
        p0++;
        newNumSize++;
    }
    return newNumSize;
}
```

##  8. <a name='1'></a>文件读写1

```c
#include <stdio.h>
#include <string.h>

int main() {
    int sum = 0;
    int i = 0;
    //1.打开文件
    FILE* fr = fopen("in.txt", "r");
    FILE* fw = fopen("out.txt", "w");
    if (fr == NULL || fw == NULL) {
        printf("文件打开失败!\n");
        return -1;
    }
    //2.读文件
    char buf[100] = "";
    fgets(buf, 100, fr);
    for (int i = 0; buf[i]; i++) {
        sum += buf[i] - '0';
    }
    //3.写入
    fprintf(fw, "%d", sum);
    //4.关闭文件
    fclose(fr);
    fclose(fw);
    return 0;
}
```

##  9. <a name='2'></a>文件读写2

```c
#include <stdio.h>
#include <string.h>

int main() {
    int sum = 0, num = 0;
    char result[100] = "";
    int ch = 0;

    FILE* fr = fopen("in.txt", "r");
    FILE* fw = fopen("out.txt", "w");

    if (fr == NULL || fw == NULL) {
        printf("文件打开失败!\n");
        return -1;
    }

    while (fscanf(fr, "%d", &num) != EOF) {
        sum += num;
    }

    fprintf(fw, "%d", sum);

    fclose(fr);
    fclose(fw);
    return 0;
}
```

##  10. <a name='-1'></a>画三角形

```c
void DrawTriangles(int n) {
    char ch = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i + 1; j++) {
            printf("%c", 'A' + (ch % 26));
            ch++;
        }
        printf("\n");
    }
}
```

## 百鸡问题

```c
int HundredChickenProblem(int x, int y, int z, int n, int m)
{
    int count = 0;
    int m1 = 0, m2 = 0, m3 = 0;
    for (m1 = 0; m1 <= m / x; m1++)
    {
        for (m2 = 0; m2 <= (m - x * m1) / y && m2 <= (m - m1); m2++)
        {
            m3 = m - m1 - m2;
            if (m3 % z == 0 && m1 * x + m2 * y + m3 / z == n)
                count++;
        }
    }
    return count;
}
```

## 买笔

```c
void PurchasePen(int x)
{
    int count[3] = { 0 };
    if (x > 7)
    {
        while (x)
        {
            switch (x % 4)
            {
            case 0:
            {
                count[2]++;
                x -= 4;
            }
                break;
            case 1:
            {
                count[1]++;
                x -= 5;
            }
                break;
            default:
            {
                count[0]++;
                x -= 6;
            }
                break;
            }
        }
    }
    for (int i = 0; i < 3; i++)
    {
        printf("%d ", count[i]);
    }
    printf("\n");
}

```

## 四位完全平方数

```c
void ExactlySquaredNumber(){
    for (int i = 1; i < 10;i++){
        for (int j = 0; j < 10;j++){
            printf("%d\n", i * 1100 + j * 11);
        }
    }
}
```

## 分解质因数

```c
void DecomposePrimeFactors(int n) {
    if(n == 0 || n == 1){
        return;
    }
    if(n是素数){
        for (int j = 2; j < (MAX+1);j++){
            if(n % j == 0){
                printf("%d*", j);
                DecomposePrimeFactors(n / j);
                break;
            }
        }
    }
    else{
        printf("%d", n);
    }
}
```

## 括号匹配

```c
int validParentheses(char *s)
{
    char temp[100] = "";
    int end = -1;
    for (int i = 0; s[i] != '\0';i++)
    {
        if(s[i] == '{' || s[i] == '[' || s[i] == '(')
        {
            temp[++end] = s[i];
        }
        else if(s[i] == '}')
        {
            if(temp[end] == '{')
            {
                end--;
            }
            else
            {
                return 0;
            }
        }
        else if(s[i] == ']')
        {
            if(temp[end] == '[')
            {
                end--;
            }
            else
            {
                return 0;
            }
        }
        else if(s[i] == ')')
        {
            if(temp[end] == '(')
            {
                end--;
            }
            else
            {
                return 0;
            }
        }
    }
    return 1;
}
```

## 大数加法

```c
void swap(char* c1, char* c2) {
    char t = *c1;
    *c1 = *c2;
    *c2 = t;
}

void reverse(char* str)
{
    int i = 0;
    int j = strlen(str) - 1;
    while (i < j) {
        swap(&str[i++], &str[j--]);
    }
}


char* solve(const char* s, const char* t)
{
    if(s == NULL && t == NULL){
        char* str = (char*)malloc(sizeof(char)*2);
        strcpy(str,"0");
        return str;
    }
    int count = 0;
    int rex = 0;
    int index = 0;
    int i = strlen(s) - 1;
    int j = strlen(t) - 1;
    char* str = (char*)malloc(sizeof(char));
    while (i >= 0 || j >= 0)
    {
        count++;
        int n1, n2;
        n1 = i >= 0 ? s[i] - '0' : 0;
        n2 = j >= 0 ? t[j] - '0' : 0;
        int n = (n1 + n2 + rex) % 10;
        rex = (n1 + n2 + rex) / 10;
        str = (char*)realloc(str, sizeof(char) * (count + 1));
        str[index++] = n + '0';
        i--;
        j--;
    }
    if (rex != 0)
    {
        count++;
        str = (char*)realloc(str, sizeof(char) * (count + 1));
        str[index++] = rex + '0';
    }
    str[count] = '\0';
    reverse(str);
    return str;
}
```

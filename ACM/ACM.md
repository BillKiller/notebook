# ACM

## 暴力枚举

### 丑数

```

18005 It is not ugly number
时间限制:2000MS  内存限制:65535K
提交次数:0 通过次数:0

题型: 编程题   语言: G++;GCC
Description
Ugly numbers are numbers whose only prime factors are 2, 3 or 5. The sequence1, 2, 3, 4, 5, 6, 8, 9, 10, 12, ...shows the 
first 10 ugly numbers. By convention, 1 is included. Then, here are the first 10 Not ugly numbers:7, 11, 13, 14, 17, 19, 
21, 22, 23, 26. Given the integer n, write a program to find and print the n'th Not ugly number.



输入格式
First line is T（T<=10000）, the number of cases.
The T lines following. Each line of the input contains a positive integer n (n <= 100000000).


输出格式
For each case, output the n'th Not ugly number .


输入样例
3
1
2
9


输出样例
7
11
23


作者 admin

```

### 解析

我们使用暴力枚举，为了让我们不出现重复，我们使用按照顺序来枚举，首先2产生的数字就可以枚举2，3，5这三个数字，但是3却不能枚举2，因为2枚举过了，例如2x3 如果 3的时候枚举3x2那就重复了，这样不仅大大减少速度。因为丑数很少我们统计一下丑数的差距这些就是非丑数，然后我们就可以得到非丑数了.

```cpp
#include <iostream>
#include<queue>
#include <algorithm>
#include <cstdio>

const int maxn = 5e9+7;
using namespace std;
struct node {
    long long val;
    int e;
    friend bool operator < (const node a,const node b) {
        return a.val>b.val;
    }
};
priority_queue<node>pq;
vector<long long>number;
int main() {
    node t;
    t.val =1;
    t.e =1;
    pq.push(t);
    int ans=0;
    while(!pq.empty()) {
        node  t = pq.top();
        pq.pop();
        number.push_back(t.val);
        ans++;
        if(t.val > maxn)continue;
        switch(t.e) {
        default:
        case 2:
            node t2;
            t2.val = t.val*2ll;
            t2.e = 2;
            pq.push(t2);
        case 3:
            node t3;
            t3.val = t.val*3ll;
            t3.e = 3;
            pq.push(t3);
        case 5:
            node t5;
            t5.val = t.val*5ll;
            t5.e = 5;
            pq.push(t5);
        }
    }
    int tt;
    scanf("%d",&tt);


    while(tt--) {
        long long n;
        long long  ugly=0;
        long long  un_ugly = 0;
        scanf("%lld",&n);
        long long ans = 0;
        for(int i = 1; i<number.size(); i++) {
            if((un_ugly + number[i]-number[i-1]-1)>=n) {
                ans = (n-un_ugly) + number[i-1];
                break;
            }
            un_ugly = un_ugly + number[i]-number[i-1]-1;
        }
        cout<<ans<<endl;
    }
}

```


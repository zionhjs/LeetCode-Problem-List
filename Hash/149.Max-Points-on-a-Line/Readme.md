### 149.Max-Points-on-a-Line

#### 解法1
此题不能试图固定一个点、再构建直线斜率的hash表 map<double,int>Map 来确定直线的种类。因为靠相除得到的斜率会有数值误差，在最新的测试样例中无法通过。  
对于一个点 (x0,y0),判断是否和另外两点(x1,y1),(x2,y2)构成直线的判据是
```cpp
(y1-y0)*(x2-x0)==(y2-y0)*(x1-x0)
```
正确的思路：  
遍历点P[i]. 对于固定的起始点P[i]，考虑会和剩下的点构成多少不同的直线。  

于是遍历剩下的点，比如P[j]，看是否P[j]和P[i]能构成一个新的直线。建立一个Hash Map，如果在这个表中发现已经有一条直线P[k]，使得P[k],P[j],P[i]满足之前的那个关系，说明P[j]已经属于P[k]、P[i]构成的直线上，则Map[k]++. 如果遍历Map之后没有找到任何归属，就将这个点加入hash表作为新的key，即Map[j]=1，表示连接P[i]、P[j]所代表的一条新直线。遍历完所有的j之后，查看此时Map里面最多个数的那项，代表P[i]所能构建的最多点的直线。    

最外边的大循环，遍历完P[i]之后，最大的结果就出来了。

注意点：  
1. 如果P[j]和P[i]重合，那么这些点可归属任意的直线，需要在Map里特殊处理。  
2. 如果用C++，则在上述的判断三点共线的数学等式里，必须都转换为long long类型才能得到正确的比较结果。

#### 解法2
之前提到，如果计算斜率 k = (y1-y0)/(x1-x0)作为key的话，会因为精度不足而产生错误。

一个巧妙的解决方法是，因为x0,y0,x1,y1都是整数，可以令 a=y1-y0, b=x1-x0, 那么一对tuple值 (a/gcd(a,b), b/gcd(a,b))则可以代表一条直线斜率的特征，成为可以信赖的key放入字典内统计该直线上的点的数目.


[Leetcode Link](https://leetcode.com/problems/max-points-on-a-line)
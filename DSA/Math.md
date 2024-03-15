# ceil() 
This function returns the smallest possible integer value which is greater than or equal to the given argument.
***Require : ```#include <cmath>``` or ```#include <math.h>```***

**Syntax:**
```c++
ceil(double num)
```

**For example:**

```c++
cout << ceil(69.1);
// output: 70
cout << ceil(7.00001);
// output: 8
cout << ceil(2)
// output: 2
```

# Calculate sum from 1 to n
If you want to calculate the sum from 1 to n, you can do this approach with O(1) BigO instead of O(n), which use for loop normally.

**Formula:**
```sum of 1 -> n : n*(n+1)/2```

**For example:**

✅ Do this
```c++
int n = 100;
int sum = n*(n+1)/2;
// output: sum = 5050
```
❌ Don't do this 
```c++
int sum = 0;
for(int i=1;i<=100;i++) sum+=i;
// output: sum = 5050;
```

# Calculate sum from x to n (Very easy to use)
Calculate the sum from ```x -> n``` with O(1) BigO.

**Formula**
```sum of x -> n : (n*n+n-x*x-x)/2+x;```

**Explain**
Instead of using for loop from ```x``` to ```n```, we can calculate the sum of ```1 -> x``` and ```1 -> n```, then take two of them and subtract the sum of ```x``` from the sum of ```n```.

We create ```s1``` is the sum of ```1 -> x``` and ```s2``` is the sum of ```1 -> n```, because ```s2``` is greater than ```s1``` and.

**Follow the steps**

* Step 1: We take the sum of ```1 -> x``` and ```1 -> n```
```s1 = x*(x+1)/2```
```s2 = n*(n+1)/2```
* Step 2: We take the total sum of ```x -> n```
```s = s2 - s1 + x```
Now in this step, why do I add ```x``` in ```s```?
Assuming that, we run two for loops from ```1 to x``` and ```1 to n```, then we take the sum of them, and we subtract them from each other. Because ```n``` is greater than ```x```, if we run two for loops, then we meet two ```x```. You guys got this stage? So if we let two of those sum minus each other then no more ```x``` in the total sum. That is why I add ```x``` to ```s```.
* Step 3: Compact expression
```
    s = s1 - s2 + x
<=> s = n * (n + 1) / 2 - x * (x + 1) / 2 + x
 => s = (n * n + n - x * x - x)/2+x
```

**For example:**

✅ Do this
```c++
int m = 10;
int n = 100;
int sum = (n*n+n - m*m-m) / 2 + m;
// output: sum = 5005
```
❌ Don't do this 
```c++
int s = 0;
for(int i=m;i<=n;i++) s+=i;
// output : s = 5005
```
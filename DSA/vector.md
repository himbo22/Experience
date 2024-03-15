# Initialize a vector
* Simply
```c++
vector<int> a;
```
* With certain size
```c++
vector<int> a(3);
```
* With certain size and specifically value
```c++
vector<int> a(3,1);
for(int i=0;i<3;i++) cout << a[i] << " ";
// output : 1 1 1
```
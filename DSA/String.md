# Sub String :
Syntax :
```c++
string t = s.substr([start],[end]);
or
string t = s.substr([position to end]);
```
For instance : 
```c++

string s = "1231";
string t = s.substr(1,2);
-> t == "23"

or

string s = "1231";
string t = s.substr(2);
-> t == "31"

```
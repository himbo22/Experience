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

# Compare String : 
We can use max(a,b) : 
```c++
string s = "123"
string t = "321"

-> max(s,b) will be "321"
```

# Create a character with certain quantity :

We use : 
```c++
int quantity = 3;
char c = 'a';
string s = string(quantity, c);
```
And the result will be :
```c++
-> s = "aaa";
```
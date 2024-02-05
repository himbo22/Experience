# TextView

## Change text color
Use,..
```java
Color.parseColor("#bdbdbd");
```
like,
```java
mTextView.setTextColor(Color.parseColor("#bdbdbd"));
```
Or if you have defined color code in resource's color.xml file than

(From API >= 23)
```java
mTextView.setTextColor(ContextCompat.getColor(context, R.color.<name_of_color>));
```
(For API < 23)
```java
mTextView.setTextColor(getResources().getColor(R.color.<name_of_color>));
```
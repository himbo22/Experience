# Stroke circle:
```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <stroke
        android:width="1dp"
        android:color="#78d9ff"/>
</shape>
```
![Stroke circle](https://i.stack.imgur.com/k8vyX.png)

# For solid circle use:
```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid
        android:color="#48b3ff"/>
</shape>
```
![Solid circle](https://i.stack.imgur.com/ITaSM.png)

# Solid with stroke:
```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#199fff"/>
    <stroke
        android:width="2dp"
        android:color="#444444"/>
</shape>
```
![Solid circle](https://i.stack.imgur.com/cTina.png)

*Note*: To make the oval shape appear as a circle, in these examples, either your view that you are using this shape as its background should be a square or you have to set the height and width properties of the shape tag to an equal value.
#theme.xml

```xml
<resources>
    <!-- Base application theme. -->
    <style name="Theme.SoundScape" parent="Theme.MaterialComponents.DayNight.NoActionBar.Bridge">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/purple_500</item>
        <item name="colorPrimaryVariant">@color/purple_700</item>
        <item name="colorOnPrimary">@color/white</item>
        <!-- Secondary brand color. -->
        <item name="colorSecondary">@color/teal_200</item>
        <item name="colorSecondaryVariant">@color/teal_700</item>
        <item name="colorOnSecondary">@color/black</item>
        <!-- Status bar color. -->
        <item name="android:statusBarColor">?attr/colorPrimaryVariant</item>
        <!-- Customize your theme here. -->
        <!-- colorAccent is used as the default value for colorControlActivated
         which is used to tint widgets -->
        <!-- THIS IS WHAT YOU'RE LOOKING FOR -->
        <item name="colorAccent">#949494</item>
    </style>

    <style name="Theme.App.SplashScreen" parent="Theme.SplashScreen">
        <item name="android:windowBackground">@drawable/background_splash</item>
        <item name="postSplashScreenTheme">@style/Theme.SoundScape</item>
    </style>

    <style name="circle">
        <item name="cornerSize">50%</item>
    </style>

    <style name="text_field" parent="Widget.MaterialComponents.TextInputLayout.OutlinedBox">
        <item name="boxStrokeColor">@color/gray_text</item>
        <item name="startIconTint">@color/gray_text</item>
        <item name="endIconTint">@color/gray_text</item>
        <item name="android:textColorHint">@color/gray_text</item>
        <item name="hintTextColor">@color/gray_text</item>
        <item name="boxCornerRadiusTopStart">@dimen/_8sdp</item>
        <item name="boxCornerRadiusTopEnd">@dimen/_8sdp</item>
        <item name="boxCornerRadiusBottomStart">@dimen/_8sdp</item>
        <item name="boxCornerRadiusBottomEnd">@dimen/_8sdp</item>
        <item name="boxStrokeErrorColor">@color/orange_button</item>
    </style>

</resources>
```


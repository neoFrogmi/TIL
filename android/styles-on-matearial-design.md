Styles on material design
=========================

In Android, in order to maintain your corporation colors, there are a set of colors that can be setted to define it.
You can do it in styles.xml.

These colors defines the ActionBar/Toolbar colors, main window color and text colors.

![Alt text](https://developer.android.com/training/material/images/ThemeColors.png)

Our styles.xml looks like this
```<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/frogmi_background_primary</item>
        <item name="colorPrimaryDark">@color/frogmi_background_primary_dark</item>
        <item name="colorAccent">@color/frogmi_main_green</item>
        <item name="android:windowBackground">@color/frogmi_background_primary</item>
    </style>
</resources>```

Note
----
This syntax is compatible with Api level < 21. If your app is 100% Api 21 based, please read this.
https://developer.android.com/training/material/theme.html

# FABActivityTransitionLayout
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-FabTransitionActivity-green.svg?style=true)](https://android-arsenal.com/details/1/2763)

**Easily transition from the tap of a `Floating Action Button` to a new activity opening with a circular reveal animation.**
*(Based on [FabTransitionLayout](https://github.com/bowyer-app/FabTransitionLayout))*

![transitionactivity](https://github.com/coyarzun89/FabTransitionActivity/blob/master/art/fabTransitionActivity.gif)

Warning: The new version `0.2.0` now has a `minSdkVersion` of `15` as the [CircularReveal](https://github.com/ozodrukh/CircularReveal) dependency has moved from `14` to `15`

Usage
====
### build.gradle

Add the following to your `build.gradle`

```
//Very important, don't forget it..
repositories {
    mavenCentral()

    maven {
        url "https://jitpack.io"
    }
}

defaultConfig {
    minSdkVersion 15
}

dependencies {
    compile 'com.github.coyarzun89:fabtransitionactivity:0.2.0'
}


```

### Layout XML

Add a `com.github.fabtransitionactivity.SheetLayout` after your `FloatingActionButton` within the same container.

```java
<!-- Container (CoordinatorLayout, RelativeLayout etc.) -->
    
    <!-- Contents -->

    <android.support.design.widget.FloatingActionButton.. />

    <com.github.fabtransitionactivity.FABActivityTransitionLayout
        android:id="@+id/bottom_sheet"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_gravity="bottom"
        app:ft_container_gravity="center"
        app:ft_color="@color/primary"
        android:elevation="2dp"/>

<!-- End Container -->
```

### Code Steps

* Call `setFab(..)` on your `FABActivityTransitionLayout`, passing the `Floating Action Button` as as parameter
* `setFabAnimationEndListener(..)`
* Set your `Floating Action Button` to call your `FABActivityTransitionLayout` `expandFab()`
* Override `onFabExpandAnimationEnd()` to open your activity or perform an action:
```java
    @Override
    public void onFabAnimationEnd() {
        Intent intent = new Intent(this, AfterFabAnimationActivity.class);
        startActivityForResult(intent, REQUEST_CODE);
    }
```
* Lastly, remember to call `contractFab()` after your opened activity has ended, for example:
```java
    @Override
   public void onActivityResult(int requestCode, int resultCode, Intent data) {
       if (requestCode == REQUEST_CODE){
           mSheetLayout.contractFab();
        } else {
           super.onActivityResult(requestCode, resultCode, data);
        }
   }
```

**See the `Demo` project for an example of this.**

# Credits
This library uses the following libraries:
* [CircularReveal](https://github.com/ozodrukh/CircularReveal)

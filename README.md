[中文版README](https://github.com/youmi-obg/android-offerwall-sdk/blob/main/README_cn.md)



1.Add **youmiAdsWall-release.aar** into the **libs** folder in the app directory（if there is no **libs** folder , please create a new folder named **libs**）



2.To install via gradle, add the following to your app’s build.gradle 

```
dependencies {

  implementation fileTree(dir: 'libs', include: ['*.jar'])

  implementation(name:'youmiAdsWall-release',ext:'aar') 
}
```



3.The dependency used in **youmiAdsWall-release.aar**

```
dependencies {

    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "com.squareup.retrofit2:converter-gson:2.9.0"
    implementation 'com.jakewharton.retrofit:retrofit2-rxjava2-adapter:1.0.0'
    implementation 'com.squareup.okhttp3:okhttp:5.0.0-alpha.2'

    implementation "com.github.bumptech.glide:glide:4.12.0"
    annotationProcessor("com.github.bumptech.glide:compiler:4.12.0")
    implementation 'com.google.code.gson:gson:2.8.8'

    implementation 'io.reactivex.rxjava2:rxjava:2.2.20'
    implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'

    implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.1.2'
    implementation 'com.scwang.smart:refresh-layout-kernel:2.0.3'
    implementation 'com.scwang.smart:refresh-header-material:2.0.3'

    implementation 'androidx.appcompat:appcompat:1.3.1'
    implementation 'com.google.android.material:material:1.4.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.1'
}
```

If there is already the same dependency (version can be different) in your app’s dependency, it can be used normally. If not, you have to add the dependency.



4.Add YoumiOffersWallSdk.init(this,"your_aid") to the **onCreate()** method in the **Application** class of the project. “your_aid” is your account ID registered in Youmi. “your_aid” can not be empty, otherwise the SDK will not work.

```
class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        YoumiOffersWallSdk.init(this,"your_aid")
    }
 }
```



5.Add YoumiOffersWallSdk.startOffersWall(context, userId) to where it start the SDK offer wall. **context** is an instance of the **Context** class; **userId** is String type, and **userId** is the unique ID of your APP’s user.

```
btn_test.setOnClickListener {
    YoumiOffersWallSdk.startOffersWall(context,"userId")
}
```

1. Add youmiAdsWall-release.aar into the libs folder in the app directory（if there is no libs folder , please create a new folder named libs）


2. To install via gradle, add the following to your app’s build.gradle
   implementation(files("libs/youmiAdsWall-release.aar"))


3. The dependency used in youmiAdsWall-release.aar

    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "com.squareup.retrofit2:converter-gson:2.9.0"
    implementation 'com.jakewharton.retrofit:retrofit2-rxjava2-adapter:1.0.0'
    implementation 'com.squareup.okhttp3:okhttp:5.0.0-alpha.2'
    implementation "com.squareup.okhttp3:logging-interceptor:5.0.0-alpha.2"
    
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
    implementation 'androidx.work:work-runtime:2.7.1'
If there is already the same dependency (version can be different) in your app’s dependency, it can be used normally. If not, you have to add the dependency.


4. Add multiDexEnabled true to defaultConfig in build.gradle

```
defaultConfig {
    applicationId "com.youmi.sdk.demo"
    minSdk 16
    targetSdk 30
    versionCode 1
    versionName "1.0"

    multiDexEnabled true
    testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
}
```


5. Add tools:replace="android:theme" to <application> in AndroidManifest.xml

```
<application
    android:name=".MyApp"
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/Theme.MyApplication"
    tools:replace="android:theme">
    <activity
        android:name=".MainActivity"
        android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />

            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```


6. Add YoumiOffersWallSdk.init(this,"your_aid") to the onCreate() method in the Application class of the project. “your_aid” is your account ID registered in Youmi. “your_aid” can not be empty, otherwise the SDK will not work.

```
class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        YoumiOffersWallSdk.init(this,"your_aid")
    }
 }
```


7. Add YoumiOffersWallSdk.startOffersWall(context, userId) to where it start the SDK offer wall. context is an instance of the Context class; userId is String type, and userId is the unique ID of your APP’s user.

```
btn_test.setOnClickListener {
    YoumiOffersWallSdk.startOffersWall(context,"userId")
}
```


Any questions about SDK integrations, feel free to contact us.
Email: mkt@youmi.net
‪WhatsApp: +8618028539642

1.将youmiAdsWall-release.aar添加到App的目录下的libs文件夹中（如果没有该文件夹，自行创建个该命名的文件夹）



2.在app目录下的build.gradle中，在dependencies中引用，引用方式为
   implementation(files("libs/youmiAdsWall-release.aar"))



3.aar中使用到的依赖总共有

    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "com.squareup.retrofit2:converter-gson:2.9.0"
    implementation 'com.jakewharton.retrofit:retrofit2-rxjava2-adapter:1.0.0'
    implementation "com.squareup.okhttp3:logging-interceptor:5.0.0-alpha.2"
    implementation 'com.squareup.okhttp3:okhttp:5.0.0-alpha.2'

    implementation "com.github.bumptech.glide:glide:4.12.0"
    implementation 'androidx.legacy:legacy-support-v4:1.0.0'
    annotationProcessor("com.github.bumptech.glide:compiler:4.12.0")
    implementation 'com.google.code.gson:gson:2.8.8'

    implementation 'com.flurry.android:analytics:13.3.0'
    implementation 'com.google.android.gms:play-services-ads-identifier:18.0.1'

    implementation 'io.reactivex.rxjava2:rxjava:2.2.20'
    implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'

    implementation 'org.greenrobot:eventbus:3.1.1'
    implementation 'com.airbnb.android:lottie:3.4.0'


    implementation 'androidx.work:work-runtime:2.7.1'
    implementation 'org.jetbrains.kotlin:kotlin-stdlib:1.6.10'
    implementation 'androidx.appcompat:appcompat:1.3.1'
    implementation 'com.google.android.material:material:1.4.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.1'
    testImplementation 'junit:junit:4.+'
    androidTestImplementation 'androidx.test.ext:junit:1.1.3'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
在app的依赖中，如果有相同的依赖（版本不同也可以）即能正常使用，如果没有需要添加上该依赖



4.在项目的build.gradle中的defaultConfig中加上   multiDexEnabled true

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



5.在项目的AndroidManifest.xml中的<application>目录中加入tools:replace="android:theme"

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



6.SDK的接入方式，在项目的Application类中的onCreate( )方法内，
   
   使用 YoumiOffersWallSdk.getInstance().setOfferWallCallback { s, l ->
         }
   去注册本地回调，s为第三方传入的uid，l为每次完成任务成功后获取到的积分。（如果不需要本地回调可以不添加该函数）
   
   使用 YoumiOffersWallSdk.getInstance().init(this,"your_aid")  
    "your_aid"为你在有米官网注册成功后的渠道aid，该aid不能为空，如果为空无法正常使用SDK功能
   

```
class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        YoumiOffersWallSdk.getInstance().setOfferWallCallback { s, l ->
          
        }
   
        YoumiOffersWallSdk.getInstance().init(this,"your_aid")
    }
 }
```





7.SDK广告墙的启动方式，在需要跳转到SDK的地方，添加代码
    YoumiOffersWallSdk.getInstance().startOffersWall(context，userId) 
    context为Context类的实例，userId为String类型，userId为该APP用户的唯一Id

```
btn_test.setOnClickListener {
    YoumiOffersWallSdk.getInstance().startOffersWall(context,"userId")
}
```



如果对SDK有任何问题，请联系我们
Email: mkt@youmi.net
‪WhatsApp: +8618028539642‬

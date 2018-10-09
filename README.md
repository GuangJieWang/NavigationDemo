# Android JetPack组件之Navigation学习
## 什么是Navigation

要了解navigation需要先了解Android Jetpack，Android Developers中对[Android Jetpack](https://developer.android.google.cn/jetpack/) 有详细的介绍，不了解的可以去官网查看。

- Android Jetpack 架构组件Architecture之一
- 简化了Android应用程序中导航的实现
- [官网地址](https://developer.android.google.cn/topic/libraries/architecture/navigation/)

## Navigation能做什么

利用Navigation组件对 Fragment 的原生支持，您可以获得架构组件的所有好处（例如生命周期和 ViewModel），同时让此组件为您处理 FragmentTransaction 的复杂性。此外，Navigation组件还可以让您声明我们为您处理的转场。它可以自动构建正确的“向上”和“返回”行为，包含对深层链接的完整支持，并提供了帮助程序，用于将导航关联到合适的 UI 小部件，例如抽屉式导航栏和底部导航。

##如何使用Navigation

**1. Android Studio版本为3.2及以上**

- 目前最新版本为Android Studio3.2

- 相关下载地址为[https://developer.android.google.cn/studio/](https://developer.android.google.cn/studio/)

**2. 添加项目依赖**

```groovy
implementation 'android.arch.navigation:navigation-fragment-ktx:1.0.0-alpha06'
implementation 'android.arch.navigation:navigation-ui-ktx:1.0.0-alpha06'
```

**3. 创建Navigation**

- 在新建的项目中，找到res文件夹，选中点击右键，选择New-> Android Resource File，如下图：

<div  align = "left">
    <img src= "https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/create.png?raw=true"/>
</div>

- 在弹出的对话框中，File name一栏中，填写文件名，例如"navigation_main"，Resource type一栏选择 Navigation，然后点击OK，如下图：

<div align = "left">
    <img src = "https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/navigation_main.png?raw=true"/>
</div>
- 如果Resource type中没有navigation，则需要在File->Settings，左侧菜单中选择Experimental，然后在右侧Editor中选择Enable Navigation Editor，然后重启AndroidStudio，如下图：

<div align = "left">
    <img src = "https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/setup_navigation.png?raw=true"/>
</div>

- 创建完成后，会发现在res文件夹目录下，出现了一个新的文件夹“navigation”，然后我们刚才创建的"navigation_main.xml"也放在里面，如下图：

<div align = "left">
    <img src = "https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/new_navigation.png?raw=true"/>
</div>


- 打开activity_main.xml文件，添加fragment控件。

```xml
<fragment
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/my_nav_host_fragment"
    android:name="androidx.navigation.fragment.NavHostFragment"
    app:defaultNavHost = "true"
    app:navGraph = "@navigation/navigation_main"/>
```

- 打开“navigation_main.xml”文件，选择“design”模式，点击左上角加号按钮，如下图：

<div align = "left">
    <img src="https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/new_fragment.jpg?raw=true"/>
</div>

- 创建MainFragment文件，如下图：

<div align = "left">
    <img src= "https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/main_fragment.png?raw=true"/>
</div>

- 在fragment_main.xml文件中添加两个按钮（goToAccount、goToSettings）：

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/constraintLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainFragment">
    <Button
        android:id="@+id/goToAccount"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="GO TO ACCOUNT"
        app:layout_constraintBottom_toTopOf="@+id/goToSettings"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_chainStyle="packed" />
    <Button
        android:id="@+id/goToSettings"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="GO TO SETTINGS"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/goToAccount" />
</android.support.constraint.ConstraintLayout>
```

- 分别创建AccountFragment和SettingsFragment文件

<div align= "left">
    <img src="https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/account_fragment.png?raw=true"/>
     <img src="https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/settings_fragment.png?raw=true"/>
</div>

- 在“navigation_main.xml”文件中创建它与另外两个Fragment界面联系，打开navigation_main.xml文件，如下，将action中id分别修改为‘toAccount’、‘toSettings’。

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/navigation_main"
    app:startDestination="@id/mainFragment">

    <fragment
        android:id="@+id/mainFragment"
        android:name="com.example.navigation.MainFragment"
        android:label="fragment_main"
        tools:layout="@layout/fragment_main">
        <action
            android:id="@+id/toAccount"
            app:destination="@id/accountFragment" />
        <action
            android:id="@+id/toSettings"
            app:destination="@id/settingsFragment" />
    </fragment>
    <fragment
        android:id="@+id/accountFragment"
        android:name="com.example.navigation.AccountFragment"
        android:label="fragment_account"
        tools:layout="@layout/fragment_account" />
    <fragment
        android:id="@+id/settingsFragment"
        android:name="com.example.navigation.SettingsFragment"
        android:label="fragment_settings"
        tools:layout="@layout/fragment_settings" />
</navigation>
```

- 在MainFragment中实现onViewCreate()方法，添加如下代码：

```kotlin
goToAccount.setOnClickListener(Navigation.createNavigateOnClickListener(R.id.toAccount))
goToSettings.setOnClickListener {
     it.findNavController().navigate(R.id.toSettings)
}
```

- 带参传递

1. 修改fragment_account.xml文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AccountFragment">

    <EditText
        android:id="@+id/editName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:ems="10"
        android:inputType="textPersonName"
        android:text="Name" />

    <Button
        android:id="@+id/nextBtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|center_horizontal"
        android:text="NEXT" />
</FrameLayout>
```

2. 添加NameFragment文件

<div align= "left">
    <img src="https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/name_fragment.png?raw=true"/>
</div>

3. 修改AccountFragment文件

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        nextBtn.setOnClickListener {
            val name = editName.text.toString()
            val bundle = Bundle()
            bundle.putString("nameArg", name)
            it.findNavController().navigate(R.id.toName, bundle)
        }
    }
```

4. 修改NameFragment文件

```kotlin
 override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        nameText.text = arguments?.getString("nameArg")
    }
```

### 类型安全的方式传递参数

在项目build.gradle文件中添加如下代码：

```groovy
dependencies{
    classpath 'android.arch.navigation:navigation-safe-args-gradle-plugin:1.0.0-alpha06'
}
```

在app的build.gradle文件中添加如下代码

```groovy
apply plugin: 'com.android.application'
apply plugin: 'androidx.navigation.safeargs'
```

在navigation_main.xml文件中，选中nameFragment，右侧菜单中双击Argument项，添加name、type、default value，如下图：

<div align= "left">
    <img src="https://github.com/GuangJieWang/NavigationDemo/blob/master/screenShot/add_argument.png?raw=true"/>
</div>

在navigation_main.xml文件中查看相应argument。

```xml
        <argument
            android:name="nameArg"
            android:defaultValue=" "
            app:argType="string" />
```





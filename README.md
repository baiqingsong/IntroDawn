# 欢迎页的使用

* [引用](#引用)
* [使用](#使用)
* [参考地址](#参考地址)


## 引用
在外层app的build.gradle中添加：
```
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```
build.gradle中调用：
```
dependencies {
    compile 'com.github.apl-devs:appintro:v4.2.0'
}
```
**引导页面需要继承包里自带类AppIntro或者时AppIntro2**


## 使用
使用方法时activity中嵌套fragment。
activity继承AppIntro或者AppIntro2类
通过addSlide来添加显示页面，调用多个addSlide显示多个页面
fragment可以自己定义，也可以通过AppIntroFragment或者AppIntro2Fragment的newInstance方法创建
```
addSlide(new FirstFragment());
addSlide(new SecondFragment());
addSlide(new ThirdFragment());
addSlide(new FourthFragment());
addSlide(AppIntroFragment.newInstance("dawn","引用项目中的引导页",R.drawable.background02, Color.WHITE));
```
动画效果
```
setFadeAnimation()
setZoomAnimation()
setFlowAnimation()
setSlideOverAnimation()
setDepthAnimation()
```
也可以通过setCustomTransformer(transformer);来创建自定义动画效果

整体代码：
```
public class IntroActivity extends AppIntro {
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Note here that we DO NOT use setContentView();

        // Add your slide fragments here.
        // AppIntro will automatically generate the dots indicator and buttons.
        addSlide(new FirstFragment());
        addSlide(new SecondFragment());
        addSlide(new ThirdFragment());
        addSlide(new FourthFragment());

        // Instead of fragments, you can also use our default slide
        // Just set a title, description, background and image. AppIntro will do the rest.
//        addSlide(AppIntroFragment.newInstance(title, description, image, backgroundColor));
        addSlide(AppIntroFragment.newInstance("dawn","引用项目中的引导页",R.drawable.background02, Color.WHITE));
        // OPTIONAL METHODS
        // Override bar/separator color.
        setBarColor(Color.parseColor("#3F51B5"));//设置底栏bar的颜色
        setSeparatorColor(Color.parseColor("#2196F3"));//底栏bar与fragment之间的分割线的颜色

        // Hide Skip/Done button.
        showSkipButton(true);//是否设置跳转按钮
        setProgressButtonEnabled(true);

        // Turn vibration on and set intensity.
        // NOTE: you will probably need to ask VIBRATE permission in Manifest.
        setVibrate(true);//设置抖动
        setVibrateIntensity(30);
        setFadeAnimation();
    }

    @Override
    public void onSkipPressed(Fragment currentFragment) {
        super.onSkipPressed(currentFragment);
        // Do something when users tap on Skip button.
        startActivity(new Intent(this, MainActivity.class));
        finish();
    }

    @Override
    public void onDonePressed(Fragment currentFragment) {
        super.onDonePressed(currentFragment);
        // Do something when users tap on Done button.
        startActivity(new Intent(this, MainActivity.class));
        finish();
    }

    @Override
    public void onSlideChanged(@Nullable Fragment oldFragment, @Nullable Fragment newFragment) {
        super.onSlideChanged(oldFragment, newFragment);
        // Do something when the slide changes.
    }
}
```
底栏颜色值设置全透明效果会整体显示图片


## 参考地址
[https://github.com/apl-devs/AppIntro](https://github.com/apl-devs/AppIntro "参考地址")
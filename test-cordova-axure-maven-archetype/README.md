#test-cordova-axure-maven-archetype
本项目由cordova-axure-maven-archetype快速生成而来，用于将Axure开发的原型项目包装为Cordova项目


##Features
- 继承**cordova-ionic-maven-archetype**的内核和相关解决方案
- 自动添加Mobile First相关的meta tag和屏幕适配directive


##Quick Start
###1、Wrap Axure Prototype
Axure开发的原型存在如下问题：

- 没有添加Mobile First相关的meta tag
- 没有做到屏幕适配

我们通过**axurecordovawrapper-maven-plugin**自动解决上述问题，同时它还能自动添加额外的资源文件,详细配置如下：
```XML
<configuration>
    <wrapperPath>www/lib</wrapperPath>
    <wrapFileSets>
        <wrapFileSet>
            <directory>www</directory>
            <includes>
                <include>**/*.html</include>
            </includes>
            <needScaleScreen>true</needScaleScreen>
            <extraFiles>
                <extraFile>www/app.js</extraFile>
                <extraFile>www/core/core.js</extraFile>
                <extraFile>www/core/core.boot.js</extraFile>
            </extraFiles>
        </wrapFileSet>
    </wrapFileSets>
</configuration>
<executions>
    <execution>
        <id>wrap-html-file</id>
        <phase>generate-resources</phase>
        <goals>
            <goal>wrap</goal>
        </goals>
    </execution>
</executions>
```

将Axure开发的原型拷贝至**www**下，执行wrap-axure-prototype即可。

![wrap-axure-prototype](http://zhoujianhui.bitbucket.org/cordova/cordova-axure-prototype-wrap.png)

###2、Build Cordova Project
整个构建过程可以参考**cordova-ionic-maven-archetype**生成的项目中的**README.md**.


##Add Custom Business To Prototype
Axure开发的原型项目有可能需要添加业务功能尤其是和手机交互的功能，比如：拍照，扫码等。我们推荐使用**AngularJS**进行开发。
目前我们内置了一个sayHello的示例，它位于**dummy/dummy.controller.js**,将其注入到test-cordova-axure-maven-archetype.js中,然后在index.html引用即可。
```JavaScript
angular.module("test-cordova-axure-maven-archetype", [
    "test-cordova-axure-maven-archetype.core",
    "test-cordova-axure-maven-archetype.dummy"]);
```

如何使用sayHello方法，参见如下代码
```HTML
<body ng-controller="dummyController as dummy">
    <input type="text" ng-model="dummy.name">
    <input type="button" value="Say Hello" ng-click="dummy.sayHello(dummy.name)">
    ...
    <script type="text/javascript" src="dummy/dummy.controller.js"></script>
</body>
```

你可以仿照此示例开发自己的业务功能,当然你事先要具备AngularJS的基本知识。


##常见问题
1、无法构建"aapt.exe exited with code 1"
检查一下www中的文件名称是否含有中文

2、生成APP首页出现Axure的页面导航栏
Axure导出的原型中的index.html中含有导航栏，推荐删除此index.html将真正的首页html文件重命名为index.html

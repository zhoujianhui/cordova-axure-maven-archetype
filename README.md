#cordova-axure-maven-archetype
本项目用于将Axure开发的原型包装为Cordova项目

##使用方法
cordova生成项目的命令如下：
```
cordova create <PATH> [ID [NAME [CONFIG]]]
```

现在我们使用maven archetype命令：
```
mvn archetype:generate 
-DarchetypeGroupId=org.zhoujianhui.archetypes
-DarchetypeArtifactId=cordova-axure-maven-archetype
-DarchetypeVersion=0.0.1-SNAPSHOT
-DinteractiveMode=false 
-DgroupId=org.zhoujianhui
-DartifactId=test-cordova-axure-maven-archetype
-Dversion=0.0.1-SNAPSHOT 
[-DappId=org.zhoujianhui.testcordovaaxuremavenarchetype] 
[-DappName=test-cordova-axure-maven-archetype]
```

对比来看：

- PATH=artifactId,生成项目所在的目录
- ID=appId,应用的ID (Reverse-domain-style package name - used in config.xml's <widget id>)
- NAME=appName,应用的名称（Human readable name - used in config.xml's <widget name>）

其中[]表示可选，默认值为：

- appId=groupId.artifactId.replace("-","")，不能包含"-"
- appName=artifactId

**PS:**
为了避免通过原型生成项目耗时较长的问题（有可能是从公网遍历所有的原型导致）
第一次执行时，可添加archetypeCatalog参数指向原型所在的Nexus私服id（见Maven的settings.xml）
```
-DarchetypeCatalog=nexus
```

第二次执行时，可将archetypeCatalog参数指定为local，因为第一次已将原型下载到Maven的本地库
```
-DarchetypeCatalog=local
```


## 包装 Axure开发的原型
详见生成的原型项目的[README.md](https://github.com/zhoujianhui/cordova-axure-maven-archetype/test-cordova-axure-maven-archetype)介绍。

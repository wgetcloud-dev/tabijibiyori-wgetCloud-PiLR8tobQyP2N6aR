
### 1\.简介


上一篇宏哥已经讲解和分享了如何通过引入jar包来搭建Java\+Playwright自动化测试环境，这一种是比较老的方法，说白了就是过时的老古董，但是我们必须了解和知道，其实maven搭建无非也就是下载引入相关的jar包，只不过相比之下是简单方便了，了解其本质可以帮助我们更好的学习maven搭建环境。今天宏哥就来讲解和分享一下，如何通过引入maven来搭建Java\+Playwright自动化测试环境。


**Apache Maven**是一个软件项目管理和综合工具。基于项目对象模型（POM）的概念，Maven可以从一个中心资料片管理项目构建，报告和文件。由于现在企业和公司中Java的大部分项目都是基于Maven, 而且也是比较流行、方便、简单的一种方式。因此宏哥为了照顾到企业或者公司用的java项目中用到maven的童鞋或者小伙伴们，这里也简单的介绍和分享一下。在Maven项目中使用Playwright非常简单。废话不多说，直接进入今天的主题。


### 2\.在eclipse中搭建maven


#### 2\.1安装maven


1\.下载maven的bin，在apache官方网站可以下载。在Files下面下载对应的maven版本(官网的是最新版本)，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210618171911793-260760334.png)


2\.查看maven对应的JDK版本，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621144525418-1035730648.png)


3\.进入maven对应的JDK版本，网址：http://maven.apache.org/docs/history.html。如下图所示：![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621144658154-1233288664.png)


4\.下载的apache\-maven\-3\.8\.1\.zip不需要安装，只需解压即可，将apache\-maven\-3\.8\.1解压到E盘根目录下，放在你本地电脑磁盘空间比较充足的磁盘，宏哥放在E盘，并解压，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621094250899-1723765648.png)


#### 2\.2配置maven环境变量


1\.设置三个环境变量,我的电脑\>选择“属性”\-\>“高级系统设置”\-\>“环境变量”\-\>“系统变量”\-\>“新建”




```
MAVEN_HOME : C:\apache-maven-3.3.9
MAVEN : %MAVEN_HOME%\bin
MAVEN_OPTS : -Xms256m -Xmx512m
```


如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621101553421-1368343657.png)


2\.在path最前面加上： %MAVEN%; 。要特别注意这里的分号，其实环境变量配置和JDK的差不多。


#### 2\.3验证maven是否安装成功


 1\.Cmd\-\>mvn \-version，成功则出现以下界面，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621101841695-1510572946.png)


### 3\.maven配置仓库


maven的仓库可以分为三种，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701132733644-684382512.png)


#### 3\.1配置本地仓库


1\.建立手动仓库maven\_repository，宏哥建立在F盘，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621102052730-1440288169.png)


2\.给Maven添加本地仓库：


作用：构建Maven项目时，首先会从本地库查找资源，如果本地库没有，Maven就会从远程库下载资源到本地库，下次使用的时候就不用再去远程库下载了。


localRepository节点用于配置本地仓库，本地仓库其实起到了一个缓存的作用，它的默认地址是 C:\\Users\\用户名.m2。当我们从maven中获取jar包的时候，maven首先会在本地仓库中查找，如果本地仓库有则返回；如果没有则从远程仓库中获取包，并在本地库中保存。此外，我们在maven项目中运行mvn install，项目将会自动打包并安装到本地仓库中。


在Maven的安装路径中的conf文件夹中配置settings.xml：在文中找到localRepository注释行，localRepository节点默认是被注释掉的，需要把它移到注释之外，然后将localRepository节点的值改为我们在上边创建的仓库的目录并添加如下：




```
F:\maven_repository  
```


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621103340973-2102089915.png)


#### 3\.2配置私服


给Maven配置mirror：mirror就是镜像， 主要提供一个方便地切换远程仓库地址的途径。在Maven的安装路径中的conf文件夹中配置settings.xml：在文中找到行并在其中添加如下：




```

     nexus-aliyun
     *
     Nexus aliyun
     http://maven.aliyun.com/nexus/content/groups/public
 
```


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621110035813-1452603362.png)


注: 千万注意, 只可配置一个(另一个要注释!) 不然两个可能发生冲突 ,导致jar包下不下来 !!!


mirror相当于拦截器，将对远程仓库的请求重定向到mirror指定的地址，如上面的代码将对central的请求重定向到http://maven.aliyun.com/nexus/content/groups/public/。


### 4\.在eclipse中安装maven插件


1\.打开Eclipse,进入help \-\- \>Install New Software...点Add按钮输入：




```
Name：m2e
location：http://download.eclipse.org/technology/m2e/releases
```


如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621111358734-1242552792.png)


2\.点击“OK”后，等相关应用下载好以后，选中点击“next”，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621111804896-618106638.png)


3\.点击next直到安装完成。设置Maven插件所关联的Maven程序：选择Eclipse菜单栏的Window\-\-\>Preferences\-\-\>Maven\-\-Installations菜单项， 点击add，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621112301604-1441899271.png)


4\.点击add,选择Maven的具体安装目录，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621112743820-2103782928.png)


5\.选择好目录，添加好maven的安装目录，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621112826460-889090205.png)


6\.选中maven的安装目录，点击“OK”，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621113026588-299737541.png)


### 5\.设置自定义的本地仓库


1\.选择Eclipse菜单栏的Window\-\-\>Preferences\-\-\>Maven\-\-UserSettings菜单项， 修改为我们自定义仓库位置下的settings.xml文件， 修改好后点击OK按钮。如下图所示：![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621113946171-639451406.png)


### 6\.查看是否maven设置成功


查看是否maven设置成功：file \- new \- other \- maven ，出现maven project表示配置成功，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621150553086-795518941.png)


### 7\.eclipse中新建maven项目


1\.依次点击eclipse的file \- new \- other ，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621153308830-1340547003.png)


2\.在搜索框输入关键字“maven”，然后选中“maven project”，如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621153458991-860289036.png)


3\.选择创建后的工作区——项目存放的地址。如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621160838780-257206243.png)


4\.选择Maven项目的模板也叫项目类型（quikstart或者webapp等等），，如果选择create a simple project，则跳过了下面的步骤，也就不存在这个问题了，但是如果需要选择项目类型，则不能勾选create a simple project）如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621160944549-791466042.png)


5\.宏哥为了省事，直接选中create a simple project，点击next，输入Group Id和Artifact Id。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701111109606-517784329.png)


6\.点击“Finish”，查看新建的maven项目，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701111152344-1504642.png)


到此，创建maven项目成功！！！



### 8\.maven项目加载playwright依赖jar


#### 8\.1加载playwright依赖


maven项目加载playwright依赖就不想上一篇java项目加载playwright那么费事需要把jar包引入到项目下，maven项目只需要将相关的jar包依赖配置到pom.xml文件中就会自动加载了。因此要给上面创建的maven项目中加载playwright依赖jar包，只需在pom.xml中引入playwright的jar包即可；具体步骤如下：


1\.查看maven仓库：[http://mvnrepository.com/](https://github.com)  如下图所示：


![](https://img2020.cnblogs.com/blog/1232840/202106/1232840-20210621165435772-2089093383.png)


2\.搜索playwright, 输入playwright，点击“Search”，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240702083129007-1408234563.png)


3\.点击“[Playwright Main Library](https://github.com):[西部世界官网](https://tianchuang88.com)”,查看自己需要的playwright版本，playwright我们都会选择最新的（宏哥这里用1\.40\.0举例一下，最新可能有bug，老的可能有些方法不支持，宏哥这里选择一个不新也不旧的），如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701112129484-74324843.png)


4\.下载playwright\-1\.40\.0版本，点1\.40\.0进入页面后，只需要单击下边的编码就自动全选复制了。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701112510627-2090548169.png)




```

<dependency>
    <groupId>com.microsoft.playwrightgroupId>
    <artifactId>playwrightartifactId>
    <version>1.40.0version>
dependency>
```


5\.copy到maven项目中的pom.xml中,如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701112815219-2009880094.png)


6\.playwright的jar包maven会自动加载，从右边路径可以看到jar的路径在本地仓库。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701113210429-1338266687.png)


需要其他的jar包只需配置到pom.xml中即可！是不是比之前介绍的方法简单多了哈！


#### 8\.2修改jdk版本


因为playwright的Java需要Java8以上，所以需要重新配置jdk。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701113356996-1764853320.png)


1\.右键JRE System Library\[JavaSe\-1\.7] \-\>properties。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701113522989-34755499.png)


2\.选择javaSE\-1\.8，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701113625127-681250508.png)


3\.点击“OK”后，就变成JavaSE\-1\.8了，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701114040927-149796132.png)


好了，至此，基于maven的ava\+Playwright自动化测试环境搭建就搭建成功了。


### 9\.牛刀小试


上边已经介绍完环境的搭建，下边就仿照官方示例，写一个基本的入门代码看看环境是否搭建成功。


#### 9\.1代码设计


![](https://img2024.cnblogs.com/blog/1232840/202406/1232840-20240628142931784-154586366.png)


#### 9\.2参考代码




```
package com.bjhg.playwright;

import com.microsoft.playwright.*;
import java.nio.file.Paths;

/**
 * @author 北京-宏哥
 * 
 * @公众号:北京宏哥（微信搜索，关注宏哥，提前解锁更多测试干货）
 * 
 * 《刚刚问世》系列初窥篇-Java+Playwright自动化测试-2-环境准备与搭建-基于Maven（详细教程）
 *
 * 2024年6月30日
 */

public class Test_Playwright {
    
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
          Browser browser = playwright.chromium().launch();
          Page page = browser.newPage();
          page.navigate("https://www.baidu.com/");
          page.screenshot(new Page.ScreenshotOptions().setPath(Paths.get("example.png")));
          System.out.println(page.title());
        }
      }

}
```


#### 9\.3运行代码


1\.运行代码，右键Run AS，就可以看到控制台输出（会下载 `Playwright` 包并安装适用于 `Chromium、Firefox` 和 `WebKit` 的浏览器二进制文件，如果没有看到就是上一篇搭建已经下载了，需要删除文件，再次运行代码），如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701130850589-445892496.gif)


2\.运行代码，控制台打印。如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701133422621-1075655168.png)


3\.在代码根目录找到截图，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701132602556-112186562.png)


### 10\.小结


1\.必须先下载并安装JDK，配置JDK的环境变量JAVA\_HOME，否则maven将无法使用。


2\.eclipse安装maven插件后必须重新定位maven到本地maven目录。


3\.宏哥带你看一下，是否将相关playwright的依赖下载到本地仓库（宏哥已经创建项目并运行了），如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701115136716-2084664746.png)


4\.运行代码后，打开下载文件目录（下载 `Playwright` 包并安装适用于 `Chromium、Firefox` 和 `WebKit` 的浏览器二进制文件），如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701130529526-1352152094.png)


5\.Eclipse开发工具创建的maven项目的左上角都有一个大写的蓝色M，如下图所示：


![](https://img2024.cnblogs.com/blog/1232840/202407/1232840-20240701132313793-1221371869.png)


这一篇绝大多数主要就是关于maven的，后边关于playwright的很简单，有了上一篇的宏哥的各种填坑和基础，相信熟悉maven的小伙伴或者童鞋们应该就能快速的将环境搭建好了，而且结合上一篇和这一篇的相关知识，应该很快就理解学废了吧。


好了，今天就分享到这里！仅供大家学习和参考，今天时间不早了，又要和大家说再见了，感谢你耐心地听宏哥絮叨！！！




以Tomcat8.5.77为例，在GitHub或者[官网](https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.77/src/apache-tomcat-8.5.77-src.tar.gz)下载Tomcat的源码，解压之后，使用IDEA打开。

首先要为项目选择SDK，右键IDEA窗口右上角的小齿轮，选择`Project Structure`，设置JDK版本：

![img](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318000659276-20220318152429635.png)

由于tomcat是ant项目，首先右键点击目录中的`build.xml` ，然后选择`Add as Ant Build File`：

![img](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318000444415-20220318152430148.png)

添加之后，右侧应该会出现一个 `Ant` 的菜单，选择菜单中的 `ide-intellj` 右键运行，进行依赖的下载和项目的编译：

![Image](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318152332662-20220318152430305.png)

依赖会下载到`用户目录`下的`tomcat-build-libs`文件夹下，把该文件夹下的所有文件添加到项目的lib里，除此之外，我们还需要手动下载一个`ant`的[jar包](https://repo1.maven.org/maven2/org/apache/ant/ant/1.10.9/ant-1.10.9.jar) ，然后同样添加到项目的lib里：

![Image](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318152340379-20220318152430622.png)

如果上个阶段编译正常，在目录中就会出现一个`output`文件夹，可以理解为是tomcat的工作目录。

在`Project Structure`中把这个 `output`文件夹设置为项目的输出目录（这里直接复制绝对路径就行）：

![img](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318001629609-20220318152430795.png)

然后右键项目中的`java`目录，设置为项目的源码目录：

![img](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318001831685-20220318152431352.png)

添加一个 `Application` 的运行，主类为 `org.apache.catalina.startup.Bootstrap`：

![Image](https://image-1302577725.cos.ap-beijing.myqcloud.com/uPic/image-20220318152406183-20220318152431601.png)

运行的 VM 参数为：

```text
-Dfile.encoding=UTF8
-Dcatalina.home="{Tomcat源码路径}/output/build"
-Duser.language=en
-Duser.region=US
```

然后点击右上角的运行，如果一切正常，Tomcat就会成功启动，浏览器输入 `localhost:8080` 就能看到默认页面了。

如果想要部署自己的 `jsp` 页面或者web项目，要在`output/build/webapps` 目录下进行部署，在源码根目录的 `webapps` 文件夹里部署是不会生效的。
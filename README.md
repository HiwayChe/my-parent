### 练习搭建SSM框架
- 没有前端页面，对Controller做单元测试，模拟前端调用

#### 规则
- 金额字段用Long类型，精确到分



#### 注意事项
- 运行maven项目的时候如果有parent项目的话会报找不到parent项目的POM，需要把parent工程install到本地repository里。
- mybatis-generator在逆工程生成java的时候，不能只对create\_time和update\_time生成getter而不生成setter，这2个字段应该不允许程序更改。
- 在执行mybatis-generator:generate的时候，报dependency的版本号缺失，因为这个dependency是在后面加入到my-parent项目的，所以需要把my-parent重新install。
- 在执行mybatis-generator:generate的时候，由于加入了MybatisPaginationPlugin插件，会报can't instantiate MybatisPaginationPlugin，造成这个问题的原因是由于分页插件和maven插件在不同的classloader加载造成的，因此需要将MybatisPaginationPlugin抽离到my-helper工程，install到本地repository，在my-user里加入对my-helper的依赖。
- my-helper工程的pom类型是jar,因此需要加入org.apache.maven.plugins:maven-jar-plugin这个build插件，开始用的版本是3.0.2，结果pom文件报错：`org.apache.maven.archiver.MavenArchiver.getManifest(org.apache.maven.project.MavenProject, org.apache.maven.archiver.MavenArchiveConfiguration) `，需要将这个版本号将为2.4即可解决。
- 通过tomcat7:run去运行项目，在debug的时候会报：Source not found，找不到源码错误，可以下载一个dynamic source lookup插件，地址：[插件](http://ifedorenko.github.com/m2e-extras/)， 参考：[SO问题描述](https://stackoverflow.com/questions/9474981/java-debugging-source-not-found)。安装完插件重新运行tomcat:run会在console中打印一行红字`Dynamic source lookup support loaded.`，表示插件开始工作。

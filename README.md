### 练习搭建SSM框架


#### 规则
- 金额字段用Long类型，精确到分



#### 注意事项
1. 运行maven项目的时候如果有parent项目的话会报找不到parent项目的POM，需要把parent工程install到本地repository里。




#### 未解问题
1. mybatis-generator在逆工程生成java的时候，不能只对create\_time和update\_time生成getter而不生成setter，这2个字段应该不允许程序更改。
2. 在执行mybatis-generator:generate的时候，总是报org.mybatis.generator:mybatis-generator-core的版本号丢失，但是这个版本号在my-parent中已经定义了，因此只能在my-user/pom.xml中写死。
3. 在执行mybatis-generator:generate的时候，由于加入了MybatisPaginationPlugin插件，会报can't instantiate MybatisPaginationPlugin，造成这个问题的原因是由于分页插件和maven插件在不同的classloader加载造成的，因此需要将MybatisPaginationPlugin抽离到my-helper工程，install到本题repository，在my-user里加入对my-helper的依赖。
4. my-helper工程的pom类型是jar,因此需要加入org.apache.maven.plugins:maven-jar-plugin这个build插件，开始用的版本是3.0.2，结果pom文件报错：`org.apache.maven.archiver.MavenArchiver.getManifest(org.apache.maven.project.MavenProject, org.apache.maven.archiver.MavenArchiveConfiguration) `，需要将这个版本号将为2.4即可解决。
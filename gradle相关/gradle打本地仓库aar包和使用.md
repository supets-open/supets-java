
1 发布module設置
apply plugin: 'maven'
group = 'com.supets.pet.utils.fresco'
version = '2.0.0'

uploadArchives {
    repositories {
        mavenDeployer {
            repository(url: uri('../repo'))
        }
    }
}
2 使用library

由于没有使用maven center，使用的时候需要提供自己的url地址，在build.gradle中加入：

allprojects {
 repositories {
 mavenCentral()
 //这里加入自己的maven地址
 maven {
 url "http://127.0.0.1:8081/nexus/content/repositories/juude-id/"
 }
 }


然后在dependency里加入compile语句。

dependencies {
...
 compile 'net.juude.droidviews:droidViews:1.0'
}

这样就可以正常使用了
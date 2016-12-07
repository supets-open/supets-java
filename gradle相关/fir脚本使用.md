fir项目管理
========

# 参考资料

 [小红书Android客户端演进之路](http://www.ebrun.com/20160812/186914.shtml)

 [小红书测试版本](http://fir.im/xiaohongshu)

 [小红书Android客户端演进之路](http://blog.isming.me/2016/08/08/red-android-evolution/?utm_source=tuicool&utm_medium=referral)

 [小红书大神链接](http://blog.isming.me/archives/)

 [一个上传apk到fir的gradle插件](http://blog.isming.me/2015/08/01/gradle-fir-plugin/)

 [小红书APP部分界面分析和优化](http://www.zcool.com.cn/work/ZMTg2OTc3MzY=/2.html)

#  代码片段

	buildscript {
	    repositories {
	        jcenter()
	        mavenCentral()
	    }
	    dependencies {
	        classpath 'com.android.tools.build:gradle:2.2.2'
			//引入插件
	        classpath 'me.isming:firup:0.4.1'
	        classpath 'com.squareup.okhttp:okhttp:2.2.0'
	        classpath 'com.squareup.okhttp:okhttp-urlconnection:2.2.0'
	        classpath 'org.json:json:20090211'
	    }
	
	}
	
	apply plugin: 'me.isming.fir'
	
	fir {
	    appId = "######"   //app的appid,在fir中可以找到
	    userToken = "######"  //fir用户的token，也在在fir中找到
	
	    def versionCode="163";
	    def versionName = "2.1.0";
	    def appName = "疯狂桔子";
	    def fileName = "Supets_localhost_V${versionName}_build${versionCode}_release.apk"
	
	    apks {
	        release {
	            sourceFile file("/Supets/build/outputs/apk/" + fileName)
	            name appName  //app的名称
	            version versionName  //app的版本version
	            build versionCode   //app的版本号
	            changelog "update"  //更新日志
	            icon file("/Supets/src/res/drawable-xxhdpi/icon.png")  //app的icon的路径
	        }
	    }
	}
	
	allprojects {
	    repositories {
	        mavenCentral()
	        jcenter()
	    }
	}

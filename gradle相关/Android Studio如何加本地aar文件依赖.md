Android Studio如何加本地aar文件依赖?
=====

1. 在Module中建立"libs"目录(如果没有的话)
2. 把aar文件拷入libs目录(假设为abc.aar)
3. 在Module的build.gradle中加入：

	    repositories {
	
	    flatDir {
	
	    dirs 'libs'
	
	    }
	
	    }

4. 在Module的build.gradle中的dependencies中加入

	
		compile(name:'abc',ext:'aar')
	
	task makeJar(type: Copy) {
	    delete 'build/libs/supetscommons.jar'
	    from('build/intermediates/bundles/release/')
	    into('build/libs/')
	    include('classes.jar')
	    rename ('classes.jar', 'supetscommons.jar')
	}
	
	makeJar.dependsOn(build)
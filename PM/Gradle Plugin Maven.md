> Thinking

```
:maven # gradle upload 执行方式 gradlew uploadArchives

uploadArchives
	repositories.mavenDeployer
		repository(url: uri('E:/env/repo')) # 配置本地仓库路径，项目根目录下的repository目录中
			# repository(url: uri('libs'))
			# repository(url: uri("${rootProject.projectDir}/"))
			# repository(url:  'maven.repo.local' )
		pom.groupId = "yes.ican.logmap-android" # 唯一标识（通常为模块包名，也可以任意）
        pom.artifactId = "LogMap" # 项目名称（通常为类库模块名称，也可以任意）
        pom.version = "1.0.0" # 版本号
        pom.packaging = "aar" # 
        pom.project {
			name  'viewlibrary'
			groupId  'secondriver'
			artifactId  'viewlibrary'
			version  '1.2.0'
			packaging  'aar'

			licenses {
				license {
					name  'The Apache Software License, Version 2.0'
					url  'http://www.apache.org/licenses/LICENSE-2.0.txt'
					distribution  'repo'
				}
			}

			developers {
				developer {
					id  'secondriver'
					name  'secondriver'
				}
			}
		}

task uploadLocal(type: Upload) {
    // 需要把config设置成project的，要不然会报错
    configuration = project.configurations.findByName('archives')
    repositories {
        mavenDeployer {
            repository(url: uri('C:/Users/Developer/Desktop/StarryAndroidSupport/repo'))
            pom.groupId = "czw.starry"// 唯一标识（通常为模块包名，也可以任意）
            pom.artifactId = "starry-java" // 项目名称（通常为类库模块名称，也可以任意）
            pom.version = "1.0.0" // 版本号
        }
    }
}

uploadArchives.dependsOn uploadLocal # 
```

> Memory

```

```


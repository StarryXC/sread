> Thinking

```
gradlew uploadArchives
```

> Memory

```
plugins {
    id 'java'
    id 'maven'
}
java {
    sourceCompatibility = JavaVersion.VERSION_1_7
    targetCompatibility = JavaVersion.VERSION_1_7
}
// 会将源码上传到私服
task sourceJar (type:Jar) {
    classifier = 'sources'
    from sourceSets.main.allSource
}
artifacts {
    archives sourceJar
}
uploadArchives {
    repositories {
        mavenDeployer {
            pom {
                groupId = "yes.ican.logmap-android" // 唯一标识（通常为模块包名，也可以任意）
                artifactId = "LogMap" // 项目名称（通常为类库模块名称，也可以任意）
                version = "1.0.0" // 版本号
                packaging = "aar"
                project {
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
            }
            // url:  'maven.repo.local'
            //
            repository(url: uri('libs')) { // 配置本地仓库路径
                authentication(userName: '账号', password: '密码')
            }
            snapshotRepository(url: uri('libs')) { // 私服快照地址
                authentication(userName: '账号', password: '密码')
            }
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
uploadArchives.dependsOn uploadLocal
```


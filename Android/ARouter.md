> Thinking

```
ARouter

源码解析
    初始化流程
    navigation 流程
```

> Memory

```
https://github.com/alibaba/ARouter

android {
    defaultConfig {
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [AROUTER_MODULE_NAME: project.getName()]
            }
        }
    }
}
implementation 'com.alibaba:arouter-api:1.5.2'
annotationProcessor 'com.alibaba:arouter-compiler:1.5.2'

api compiler | AROUTER_MODULE_NAME javaCompile annotationProcessor arguments kapt arguments arg

ARouter # init inject | build withString navigation
RouteType # id className | ACTIVITY SERVICE BOARDCAST CONTENT_PROVIDER FRAGMENT PROVIDER METHOD UNKNOWN
RouteMeta
	Postcard # withObject navigation
IProvider # init
	InterceptorService # doInterceptions
@Route # RoutePath
@Autowired # 自动装配

```


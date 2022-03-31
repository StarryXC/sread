> Thinking

```

```

> Memory

```
https://github.com/greenrobot/greenDAO

classpath 'org.greenrobot:greendao-gradle-plugin:3.3.0'
plugins {
    id 'org.greenrobot.greendao'
}
implementation 'org.greenrobot:greendao:3.2.2'
implementation 'org.greenrobot:greendao-generator:3.2.2'
greendao {
    schemaVersion 1
    daoPackage 'yes.ican.android.db.greendao.gen'
    targetGenDir 'src/main/java'
    //targetGenDirTest：设置生成单元测试目录
    //generateTests：设置自动生成单元测试用例
//     OrmLite、SugarORM、Active Android、Realm 与 GreenDAO
}




```


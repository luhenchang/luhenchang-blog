```
sourceSets { 
        main{jniLibs.srcDirs = ['lib']}
    }
kts写法如下    
sourceSets {
    getByName("main") {
        jniLibs.srcDirs("libs")
    }
}

ndk {
            // 设置支持的 SO 库架构
            abiFilters += listOf("armeabi-v7a", "arm64-v8a", "x86_64","arm64")
 }
```
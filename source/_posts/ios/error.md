
### ld: library not found for -lstdc++.6.0.9

部分项目依赖 libstdc++.6.0.9 的会在Xcode 10无法运行

其原因是Xcode 10中将libstdc++.6.0.9库文件删除，原本功能迁移至其他库

    /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS12.0.sdk/usr/lib/libstdc++.6.0.9.tbd
    
    
参考信息来源

    http://ilongge.cn/2018/09/18/Mac--Xcode10_library_not_found_for_-lstdc++_6_0_9/
    
    
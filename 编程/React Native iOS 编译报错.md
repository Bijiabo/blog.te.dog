错误信息：
```
./node_modules/react-native/third-party/glog-0.3.4/src/base/mutex.h:105:10: 'config.h' file not found
```

解决方案：
https://github.com/facebook/react-native/issues/16097 

```
In the Terminal, navigate to the react-native/third-party/glog folder inside node_modules (for me, this was cd node_modules/react-native/third-party/glog-0.3.4)
Once actively in this folder, run ../../scripts/ios-configure-glog.sh
Glog is configured and the required config.h header file is created for Xcode to find**"
```

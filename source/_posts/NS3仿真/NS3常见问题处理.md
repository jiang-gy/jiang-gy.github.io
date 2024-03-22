## 编译问题

### 1 NS3编译错误

```bash
cc1plus: all warnings being treated as errors
```

解决方法

```bash
CXXFLAGS="-Wno-error" ./waf configure  #注意等号前后没有空格，进行该配置之后再进行编译 即可忽略警告
```




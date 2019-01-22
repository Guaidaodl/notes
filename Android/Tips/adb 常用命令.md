
## Activity Manager 相关

- 强行停止指定应用
  ```
  adb shell am force-stop <package-name>
  ```

### 安装 testOnly 的包
```
adb install -t
```

### 覆盖安装 apk
```
adb install -r
```

### Dump 出 Log
```
adb logcat -d
```

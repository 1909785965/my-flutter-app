# 在Mac上运行Flutter应用到小米手机的步骤指南

## 一、准备工作

### 1. 开启小米手机的开发者选项

1. 打开手机设置 -> 我的设备 -> 全部参数
2. 连续点击「MIUI版本」7次，直到出现「您现在处于开发者模式」提示

### 2. 开启USB调试

1. 返回设置主页面，找到并进入「更多设置」
2. 进入「开发者选项」
3. 开启「开发者选项」开关
4. 开启「USB调试」开关
5. 开启「USB安装」开关（允许通过USB安装应用）
6. 开启「USB调试（安全设置）」开关（允许调试应用的权限）

## 二、连接手机与Mac

### 1. 使用USB数据线连接

- 使用小米原装或高质量的USB数据线连接手机和Mac
- 手机上会弹出「USB用途」选择框，选择「传输文件」或「文件传输」模式
- 如果没有弹出选择框，下拉通知栏手动选择

### 2. 安装Android File Transfer（如果需要）

Mac系统需要安装Android File Transfer才能与Android设备正常通信：
1. 访问 https://www.android.com/filetransfer/
2. 下载并安装Android File Transfer
3. 安装完成后打开应用

## 三、验证连接

### 1. 检查adb是否能检测到设备

在Mac终端中运行：
```bash
adb devices
```

如果成功连接，会显示类似：
```
List of devices attached
ABC1234567890	device
```

### 2. 检查Flutter是否能检测到设备

在Flutter项目根目录运行：
```bash
flutter devices
```

如果成功，会显示您的小米手机信息。

## 四、运行Flutter应用

### 1. 确保应用已准备好

- 确保已运行过 `flutter pub get`
- 确保应用已通过 `flutter build apk --debug` 成功构建过

### 2. 运行应用

在Flutter项目根目录运行：
```bash
flutter run --debug
```

应用将自动安装并运行在您的小米手机上。

## 五、常见问题及解决方案

### 1. adb devices 不显示设备

- 检查USB数据线是否正常
- 检查手机USB连接模式是否为「传输文件」
- 重新插拔USB数据线
- 在手机上重新授权USB调试

### 2. 安装失败

- 检查「USB安装」开关是否开启
- 检查手机存储空间是否充足
- 尝试在命令后添加 `--no-android-upgrade` 选项

### 3. 运行时权限问题

- 检查「USB调试（安全设置）」开关是否开启
- 在手机上手动授予应用所需权限

## 六、无线调试（可选）

如果您不想一直连接USB数据线，可以使用无线调试功能：

1. 确保手机和Mac在同一WiFi网络下
2. 通过USB连接手机
3. 在终端运行：`adb tcpip 5555`
4. 断开USB连接
5. 在终端运行：`adb connect <手机IP地址>:5555`
6. 确认连接：`adb devices`

完成后，您可以使用 `flutter run` 无线运行应用。

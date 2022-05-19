+++
title = "分发到应用商店"
description = "Distributing to App Stores"
tags = [
    "go",
    "golang",
    "hugo",
    "development",
]
date = "2022-05-18"
categories = [
    "Development",
    "golang",
]
menu = "main"
weight=90
+++
# 分发
---
## 分发到应用商店
---

按照打包页面中所述打包图形应用程序可提供可直接共享或分发的文件或捆绑包。但是，签名并上传到应用商店和市场是需要特定于平台的配置的额外步骤，我们将在此页面中介绍。

在每个步骤中，我们将使用一个新工具，该工具是 `fyne` 命令行实用程序的一部分。该`fyne release`步骤处理每个商店的签名和准备工作，但参数因平台而异，如下所示。
### macOS App Store (since fyne 1.4.2)

实现准备:

* 运行 macOS 和 Xcode的Apple mac 
* Apple 开发账号
* Mac App Store 应用证书
* Mac App Store 安装证书
* App Store的Apple Transporter 程序

1. 设置您的应用程序/版本，以便为在[AppStore Connect](https://appstoreconnect.apple.com)上传构建版本做好准备。

2. 捆绑完成的应用程序以进行发布：

```
$ fyne release -appID com.example.myapp -appVersion 1.0 -appBuild 1 -category games
```

3. 将拖动到`Deliver`上，然后点击`.pkg`。

4. 返回 AppStore Connect 网站，选择您的版本以供发布，然后提交以供审核。

### Google Play Store (Android)

实现准备:

* Google Play Console 账号
* 分发密钥库 (创建说明参考[android docs](https://developer.android.com/studio/publish/app-signing))

1. 设置您的应用/版本，准备在[Google Play Console](https://play.google.com/apps/publish)管理中心上传构建版本。关闭`Play app signing`选项，因为我们自己管理它。

2. 捆绑完成的应用程序以进行发布：

```
$ fyne release -os android -appID com.example.myapp -appVersion 1.0 -appBuild 1
```

1. 将`.apk`文件拖到 Play 管理中心应用版本页面上的构建放置区中。

2. 开始推出新版本。

### iOS App Store (since fyne 1.4.1)

实现准备:

* 运行 macOS 和 Xcode 的 Apple Mac
* Apple Developer 账号
* iOS App Store 分发证书
* App Store 的 Apple Transporter 应用

1. 设置您的应用/版本，以便为要上传到[AppStore Connect](https://appstoreconnect.apple.com)的构建版本做好准备。

2. 捆绑完成的应用程序以进行发布：

```
$ fyne release -os ios -appID com.example.myapp -appVersion 1.0 -appBuild 1
```

1. 将`.ipa`拖动到`Deliver`上，然后点击“交付”。

2. 返回 AppStore Connect 网站，选择您的版本以供发布，然后提交以供审核。

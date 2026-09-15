# 记得点餐（DingCan）

打开 App 后会立刻弹出一条通知「记得点餐」，然后程序自动关闭；通知会一直留在通知栏里。

## 行为说明

- 打开 App 即发送一条通知（标题：记得点餐）
- 发送后立即关闭自己，且不留在「最近任务」中
- 通知保留在通知栏，点击它可再次打开 App
- Android 13+ 首次打开会先申请通知权限：必须点「允许」，通知才会显示（这是系统限制）

## 用 GitHub Actions 编译出 APK

1. 在 GitHub 新建仓库，把本文件夹（DingCan）里的全部文件上传到**仓库根目录**。
2. push 到 `main` 或 `master` 后，Actions 自动运行 **Android CI**；也可在 Actions 页用 **Run workflow** 手动触发。
3. 打开该次运行记录，在页面底部 **Artifacts** 下载 `DingCan-debug-apk`，解压即得 `app-debug.apk`。

## CI 会自动修复常见问题

工作流里的 **Prepare project** 步骤会先打印仓库里的全部文件，然后自动：

- 自动定位 Gradle 工程目录（文件被放进子文件夹也能找到）
- 自动补回缺失或**损坏**的 `gradlew`、`gradle/wrapper/gradle-wrapper.jar`、`gradle-wrapper.properties`

也就是说，即使漏传了 Gradle Wrapper 那几个文件，CI 也会自己去下载官方版本再编译。

**如果仍然失败**，请把 **Prepare project** 和 **Build debug APK** 两步的日志发出来 —— 日志里有完整文件清单，一眼就能定位。

## 版本与工具链（已锁定）

| 项目 | 版本 |
| --- | --- |
| versionCode | 1 |
| versionName | 1.0.0 |
| compileSdk / targetSdk | 34 |
| minSdk | 26（Android 8.0） |
| Android Gradle Plugin | 8.5.2 |
| Gradle | 8.7 |
| Kotlin | 1.9.24 |
| JDK | 17 |
| checkout / setup-java / upload-artifact | v5 / v5 / v7（都跑在 Node 24 上） |

## 本地编译（可选）

```bash
./gradlew assembleDebug
# 产物：app/build/outputs/apk/debug/app-debug.apk
```

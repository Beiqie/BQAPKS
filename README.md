# 记得点餐（DingCan）

打开 App 后会立刻弹出一条通知「记得点餐」，然后程序自动关闭；通知会一直留在通知栏里。

## 行为说明

- 打开 App 即发送一条通知（标题：记得点餐）
- 发送后立即关闭自己，且不留在「最近任务」中
- 通知保留在通知栏，点击它可再次打开 App
- Android 13+ 首次打开会先申请通知权限：必须点「允许」，通知才会显示（这是系统限制）

## 用 GitHub Actions 直接编译出 APK

1. 在 GitHub 新建一个仓库，把本文件夹（DingCan）里的**全部文件**上传上去。
   - 注意必须包含 `.github/workflows/android-ci.yml` 和 `gradle/wrapper/gradle-wrapper.jar`。
2. push 到 `main` 或 `master` 分支后，Actions 会自动运行 **Android CI**。
3. 打开该次运行记录，在页面底部的 **Artifacts** 中下载 `DingCan-debug-apk`，解压后就是 `app-debug.apk`。
4. 也可以在 Actions 页面用 **Run workflow** 手动触发。

## 版本与工具链（已锁定，保证一次编译成功）

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

## 本地编译（可选）

```bash
./gradlew assembleDebug
# 产物：app/build/outputs/apk/debug/app-debug.apk
```

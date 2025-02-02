# Android Studio を新しくしたら、Androidのビルドができなくなった

## 参考

- https://github.com/hoshi005/flutter_mirai_3

## 概要

- Android Studio のバージョンは以下

```
Android Studio Ladybug Feature Drop | 2024.2.2
Build #AI-242.23726.103.2422.12816248, built on December 18, 2024
Runtime version: 21.0.4+-12422083-b607.1 aarch64
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
Toolkit: sun.lwawt.macosx.LWCToolkit
macOS 15.3
GC: G1 Young Generation, G1 Concurrent GC, G1 Old Generation
Memory: 2048M
Cores: 12
Metal Rendering is ON
Registry:
  ide.experimental.ui=true
  i18n.locale=
Non-Bundled Plugins:
  com.github.copilot (1.5.32-242)
```

## 事象

- 新たにFlutterプロジェクトを作成する
- iOSはビルド可能。カウントアップアプリが実機転送できる
- Androidに対してビルドを行うと、以下のエラーが発生する

```sh
Launching lib/main.dart on Pixel 7 in debug mode...

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':gradle:compileGroovy'.
> Failed to run Gradle Worker Daemon
   > A problem occurred starting process 'Gradle Worker Daemon 6'

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
> Get more help at https://help.gradle.org.

BUILD FAILED in 2s
Error: Gradle task assembleDebug failed with exit code 1

Exited (1).
```

- Android Studio を起動しビルドしようとすると、以下のエラーが発生する
  - 作成されたプロジェクトのGradleは`8.3`であるが、Android Studio 2024.2.2 は`8.9`以上を推奨している

```sh
Your build is currently configured to use incompatible Java 21.0.4 and Gradle 8.3. Cannot sync the project.

We recommend upgrading to Gradle version 8.9.

The minimum compatible Gradle version is 8.5.

The maximum compatible Gradle JVM version is 20.

Possible solutions:
 - Upgrade to Gradle 8.9 and re-sync
 - Upgrade to Gradle 8.5 and re-sync
```

- `Upgrade to Gradle 8.9 and re-sync` を選択し、プロジェクトをアップデートする
- この時点でアプリのビルドと実行は可能になる。
- Android Gradle Plugin のバージョンを8.8にアップデート可能
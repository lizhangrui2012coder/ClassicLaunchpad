# 启动台

原生 Swift + AppKit 菜单栏应用，无第三方依赖，中文界面。

## 构建

需要 macOS、Xcode 26 或更新版本及对应 SDK。首次使用先打开 Xcode 完成组件安装。

```bash
./scripts/build.sh
```

生成 `dist/Launchpad.app`，双击打开即可。脚本不会自动安装或启动应用。

运行内置检查：

```bash
./scripts/build.sh --test
```

完整液态玻璃效果需要 macOS 26；旧系统提供材质回退，尚未逐版本验证。应用使用临时签名供本机构建，公开分发需自行完成 Developer ID 签名和 Apple 公证。

## 功能

- 五指捏合打开，动画跟随手势进度。
- 搜索、文件夹、拖拽排序、跨页拖动、允许留空的网格布局。
- 跟随本机壁纸，支持背景虚化、液态玻璃、菜单栏入口与设置。

## 系统手势冲突

macOS 26：在“系统设置 → 触控板 → 更多手势”关闭“显示桌面”。系统应用列表的捏合手势与此开关联动，关闭后再尝试自定义启动台。

较早系统：关闭“启动台”捏合手势；如张开手势冲突，再关闭“显示桌面”。

五指输入使用私有 MultiTouchSupport 接口，系统更新可能影响兼容性。壁纸同步读取系统配置和静态缓存，不是动态壁纸视频；缓存格式变化也可能影响同步。

## 本地数据

布局：`~/Library/Application Support/ClassicLaunchpad/layout.json`。

bundle identifier：`local.classiclaunchpad`。更新前先退出旧版本，避免两份应用同时响应。

## 上传 GitHub

本目录可单独作为一个 GitHub 仓库。上传 `Sources/`、`scripts/`、`docs/`、`README.md` 和 `.gitignore`，无需上传 `build/`、`dist/` 或个人历史。

完整源码位于 `Sources/Launchpad/main.swift`；中文使用说明见 `docs/`。

## 固定到 Dock

打开构建生成的 `dist/Launchpad.app` 后，右键 Dock 中的新图标 → 选项 → 在程序坞中保留。点击图标即可打开启动台，Esc 收起后继续常驻。可将原来的系统应用列表图标拖出 Dock，再把此图标拖到相同位置。

## DMG 安装包

运行 `./scripts/package-dmg.sh`，生成 `dist/Launchpad.dmg`。打开后将 App 拖到 Applications 安装。
# ClassicLaunchpad

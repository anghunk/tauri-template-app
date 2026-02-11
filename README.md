# Tauri Template App

这是一个使用 Tauri + Vue 3 + TypeScript 构建的桌面应用程序。

```bash
npm install
```

启动开发服务器（热重载）：

```bash
npm run tauri:dev
```

构建生产版本：

```bash
npm run tauri:build
```

构建产物将在 `src-tauri/target/release` 目录中。

## 项目结构

```
.
├── src/                  # Vue 前端源码
│   ├── App.vue          # 主组件
│   ├── main.ts          # 入口文件
│   └── style.css        # 全局样式
├── src-tauri/           # Tauri 后端（Rust）
│   ├── src/
│   │   └── main.rs      # Rust 主程序
│   ├── Cargo.toml       # Rust 依赖配置
│   └── tauri.conf.json  # Tauri 配置
├── index.html           # HTML 入口
├── vite.config.ts       # Vite 配置
└── package.json         # 项目配置
```

## 下一步

1. 安装依赖: `npm install`
2. 运行开发服务器: `npm run tauri:dev`
3. 开始开发你的应用！

## 资源

- [Tauri 文档](https://tauri.app)
- [Vue 3 文档](https://vuejs.org)
- [Vite 文档](https://vitejs.dev)

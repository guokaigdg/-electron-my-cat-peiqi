

## 安装依赖
```bash
$ npm install
$ yarn
```

## 启动项目
```bash
$ npm dev
```


## 使用 Forge 的 make 命令来创建可分发的应用程序：

```bash
npm run make
```
```
> my-electron-app@1.0.0 make /my-electron-app
> electron-forge make

✔ Checking your system
✔ Resolving Forge Config
We need to package your application before we can make it
✔ Preparing to Package Application for arch: x64
✔ Preparing native dependencies
✔ Packaging Application
Making for the following targets: zip
✔ Making for target: zip - On platform: darwin - For arch: x64
```

## Electron-forge 会创建 out 文件夹，您的软件包将在那里找到：

```bash
// 以 macOS 为例
out/
├── out/make/zip/darwin/x64/my-electron-app-darwin-x64-1.0.0.zip
├── ...
└── out/my-electron-app-darwin-x64/my-electron-app.app/Contents/MacOS/my-electron-app
```
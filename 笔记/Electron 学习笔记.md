title: Electron 学习笔记
## 调用文件选择器选择文件/多选文件/选择目录
渲染进程内，引用 `require('electron').remote.dialog`
```JavaScript
var dialog = require('electron').remote.dialog;
var selectedDirectoryPath = dialog.showOpenDialog({ properties: ['openDirectory', ]});
```
主进程内，引用 `require('electron').dialog`
```JavaScript
var dialog = require('electron').dialog;
var selectedDirectoryPath = dialog.showOpenDialog({ properties: ['openDirectory', ]});
```

## 模拟鼠标点击
```JavaScript
webview.sendInputEvent({type:'mouseDown', x:300, y: 230, button:'left', clickCount: 1});
webview.sendInputEvent({type:'mouseUp', x:300, y: 230, button:'left', clickCount: 1});
```
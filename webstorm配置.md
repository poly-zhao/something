### 1. 导入creator引擎源码

1. 下载cocos creator源码,  https://github.com/cocos-creator/engine 
2. Settings-->Languages&Frameworks-->JavaScript-->Libraries , 点击右侧`add` 
3. 点击弹出对话框的 `+` , 选择`attach directories` , 选择下载源码所在的文件路径, 如`C:\CocosCreator\resources\engine`

### 2. 隐藏与显示指定文件夹

- 隐藏的文件夹
  1. 打开`project` 标签栏 (alt+1)
  2. 右击需要隐藏的文件夹-->Mask Directory as --> Excluded

- 取消隐藏的文件夹
  1. 点击`project` 栏右上角的`show options menu` 按钮
  2. 勾选`show excluded files `

### 3. 过滤(不显示)某类文件

1. `Settings` --> `Editor` --> ` File Types` 
2. 右侧最下方`Ignore files and folders` 输入框中添加要过滤文件, 如`*.meta` 过滤所有后缀为meta`的文件
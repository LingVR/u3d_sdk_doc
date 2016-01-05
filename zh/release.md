# v0.4.0

## Editor
* 只支持 5.3 或更新版本的 Unity
* Editor 中不再提供双目预览
* 支持 OSX 版本 Unity
* 兼容 Unity 5.3 VR Sample

## 渲染

* 改用原生代码进行渲染，针对 Adreno 和 Mali GPU 进行了优化

## 陀螺仪

* 提高了预测值的准确度

## 从 0.3 升级到 0.4

* 删除以下目录和文件：

    LingVR\
    Plugins\x86\
    Plugins\x86_64\
    Plugins\Android\libRenderingPlugin.so
    
* 导入 0.4 版本的 SDK
    
        
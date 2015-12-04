# 使用 SDK

## 功能

本 SDK 主要提供以下模块：

* 双目摄像机

	用两个camera组成一个组件，可以在场景中直接使用，每个摄像机的相关值都经过精心测试，使其更真实模拟人类的双目视觉效果。
	
* 陀螺仪

	此模块直接获取相关传感器的原始值，并对他们进行滤波、融合等处理，
	计算出手机当前的方位，用来驱动3D场景中的双目摄像机旋转，使用户旋转头部时能实时看到场景的不同方向，给用户更真实的体验。

* 反畸变

	用户经过透镜看到的3D场景会产生不同程度的畸变，对于沉浸式体验更为严重，使用户产生不适应的感觉，因此需要对3D场景内容进行反向畸变，
	进而抵消透镜导致的畸变，使用户看到无畸变的3D场景。
	
## 内容

导入 SDK 后的目录结构如下：

LingVR 目录下放置的是场景中需要的资源，Plugin 目录下是不同平台的依赖库。

## 集成步骤

### 项目设置

因为 VR 应用的特殊性，必须把设备朝向设置成 Landscape Left 。其他朝向会导致程序初始化的时候退出。

### 添加双目相机

VR 相机由 LvrManager 统一管理。只需要将 Prefabs 目录下的 LvrManager 预制体拖拽到场景中，就能看到双目效果。
在 Editor 中可以通过按住 Ctrl 或者 Alt 键拖动鼠标，模拟头部转动。
别忘了移除场景中的其他相机。

LvrManager 提供了一些参数

### 用户交互

VR 眼镜属于可穿戴设备，不能使用普通的触屏事件交互。我们提供了一种 Gaze Pointer 来模拟 3D 虚拟世界中的“光标”。
这个 3D 光标在 GazeInputModule.cs 脚本中实现，它是 Unity Input Module 的一个拓展。使用时，先在场景中添加一个 EventSystem 对象：

GazeInputModule 的 Cursor 对象要绑定到 LvrManager 预制体下的 Gaze Pointer：

这样，场景里的物体就可以通过 EventTrigger 来捕捉 Gaze Pointer 事件。
另外，要使场景内的 UI 能够响应 Gaze Pointer 事件，需要把该 UI 所处的 Canvas 的 EventCamera 指定到 LvrManager 预制体的 MainCamera：

### 调试

	你可以通过 Unity Remote 4 连接到 Unity Editor 进行调试，Editor 能够获取到陀螺仪的数据。

## Q&A

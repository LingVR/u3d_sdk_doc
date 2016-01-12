# 使用 SDK
开始使用 SDK 制作 VR 应用吧!

## 集成步骤

只需要简单的几步就可以集成 SDK。

### 1.导入 SDK

通过 Assets -> Import Package -> Custom Package 菜单导入。
	
导入 SDK 后的目录结构如下：

	Assets\
		LingVR\
			Demo\					// demo 相关
			Doc\					// 文档
			Materials\				// 材质
			Prefabs\				// 预制物体
			Resources\				// 着色器和相关贴图
			Scripts\				// SDK 脚本
			Icon\					// LingVR icon
		Plugins\					// 依赖的库文件

### 2.项目设置

* 禁用 Player setting -> Other Settings -> Virtual Reality Support

* 因为 VR 应用的特殊性，必须把设备朝向设置成 Landscape Left 。其他朝向会导致程序初始化的时候退出。

* 同时，出于性能考虑，禁用 32-bit Display Buffer 和 24-bit Depth Buffer:

    ![项目设置](images/settings.png)

* 如果需要支持"灵境小白 2" 的外接传感器，则要在 AndroidMenifest.xml 中添加一个服务和三个权限：

        <service android:name="com.lingvr.sensorbox.UdService3"></service>
    
    	<uses-feature android:name="android.hardware.usb.host" />
    	<uses-permission android:name="com.android.example.USB_PERMISSION"/>
    	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>

### 3.添加双目相机

VR 相机由 LvrManager 统一管理。只需要将 Prefabs 目录下的 LvrManager 预制体拖拽到场景中，替换掉你游戏当前的主相机即可。

从 0.4 版本开始，不再在 Editor 的 Game view 中提供双目渲染预览。但你仍可以在 Editor 中可以通过按住 Ctrl 或者 Alt 键拖动鼠标，模拟头部转动。

另外 LvrManager 提供了一些参数：

* Eye Texture Scale -> 调整双眼分辨率，范围为原分辨率的 0.0 ~ 1.0，较低的分辨率能极大的提高性能
* Use Unity Remote Input -> 是否使用 [Unity Remote 4](http://docs.unity3d.com/Manual/UnityRemote4.html) 调试工具获取手机传感器数据

### 4.用户交互

#### 手柄

我们为灵境小白配置的手柄（通过蓝牙连接到安卓手机）使用了安卓标准键值：

|        |     |                      |
|--------|-----|----------------------|
| 返回键 | 4   | KEYCODE_BACK         |
| 菜单键 | 103 | KEYCODE_BUTTON_R1    |
| 音量+  | 24  | KEYCODE_VOLUME_UP    |
| 音量-  | 25  | KEYCODE_VOLUME_DOWN  |
| A键    | 96  | KEYCODE_BUTTON_A     |
| B键    | 97  | KEYCODE_BUTTON_B     |
| 摇杆上 | 19  | KEYCODE_DPAD_UP      |
| 摇杆下 | 20  | KEYCODE_DPAD_DOWN    |
| 摇杆左 | 21  | KEYCODE_DPAD_LEFT    |
| 摇杆右 | 22  | KEYCODE_DPAD_RIGHT   |


![joystick](images/joystick.png)

注意：这里的菜单键实际映射的是 R1 键！需要在 Edit -> Project Settings -> Input 菜单里额外配置一下：

![joystick](images/r1button.png)

你可以通过设置绑定在 LvrManager 下的 `LvrController` 中的 `useController = true` 来启用手柄，然后获取键值的当前状态：

	kv = LvrController.keyValues;
	
`keyValues` 是一个 `KeyValuse` 结构体，里面包含了所有键值当前状态：

	public struct KeyValues
	{
		public bool buttonA;
		public bool buttonB;
		public bool buttonBack;
		public bool buttonR1;
		public float axisX;
		public float axisY;
	}
		
然后你就可以通过获取这些键值的状态来处理一些事件了，比如：

	void Update()
	{
		if (kv.buttonA)
			attack();
		if (kv.buttonB)
			jump();
		if (kv.buttonBack)
			pause();
	}
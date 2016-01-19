# VR application design

## Performance requirement
Every frame in VR programme need to be rendered saperately for both eyes; therefore the performance problem should be considered before design the VR content. High frame rate is the foundation of VR experience, which you could cauciously use it or avoid it.

* blending

	Overusing of blending will affect performance.

* alpha test

Using mipmap and compressed texture will contribute to performance.

Luanch static batching and dynamic batching in Project Setting.
	
Also VR does not suit for open spaces. Closed space will not only improve performance, but also help getting better VR immersion.

### Frame rate

Applications should run closely to 60 Fps. Higher frame rate will effectively avoid dithering and enhance VR experience.


### Scene

Per scene targets:

* 50,000 ~ 100,000 triangles
* 50,000 ~ 100,000 vertex
* 50 ~ 100 draw calls

### Resolution

High resolution will increase the sence of reality, but also increase the rendering burden. LvrManager has a eyeTextureScale parameter that can be used to adjust resolution in order to balance between visual effect and programme performance.
For example if good visual effect can also be achieved by using half resolution on a 2560x1440 screen phone, eyeTextureScale should then be 0.5.

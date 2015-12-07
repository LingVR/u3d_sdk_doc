# LingVR Unity3D SDK 开发指南

* [简介](introduction.md)
* [VR 设计](design.md)
* [使用 SDK](development.md)

# 生成其他格式

* 安装 [node.js](https://nodejs.org/en/)

* 执行安装 gitbook 命令
	
		npm install gitbook-cli -g
	
* 生成 PDF(需要安装 [calibre](http://www.calibre-ebook.com/download_windows))

		gitbook pdf . ./lingvr_u3d_sdk_book.pdf
	
* 生成静态网站

		gitbook build
		
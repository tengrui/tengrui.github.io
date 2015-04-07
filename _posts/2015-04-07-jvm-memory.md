---
layout: post
title:  "小试Java虚拟机内存管理(Java 8)"
date:   2015-04-07 22:49:00
tag:    Java
categories: SharePoint
---
最近研究了一下Java虚拟机的内存管理。大体上分为两部分：垃圾回收算法和内存分配。举个不恰当的比喻，好比汽车的变速箱和发动机。当'转速/内存使用'偏高时，就会触发'换挡/垃圾回收'。

Java虚拟机的内存分配，大体上可分为年轻代（Young Generation），老年代（Tenured Generation）以及元空间（Metaspace）。其中，新生代又分为Eden（伊甸园）,S0和S1（Survivor，幸存者乐园）。（参考《Java程序员修炼之道》及VisualVM）

注：Java 8取消了原来的永久代（PermGen），改为元空间（Metaspace）了。

对应于Java虚拟机的参数设置：

	-Xmn的大小 = Eden + S0 + S1
	-Xmx的大小 = Eden + S0 + S1 + Old
	-XX:SurvivorRatio用来分配Eden和S的比例
	-XX:MaxMetaspaceSize表示Metaspace的最大值（-XX:MaxPermSize在Java 8种已经没用了）

所以Xmn的大小不能超过Xmx，而且最好也不要相等，否则Old空间就变成0了。有些书上说SurvivorRatio的默认值为8:1:1，但是目测Java 8里面的默认值为1:1:1

通过VisualVM可以很直观地观察上面的改动。

![press](http://tengrui.github.io/public/upload/visualvm.jpg)

以观察Eclipse的启动时间为例，需要不断地修改Eclipse的配置文件，并重启Eclipse，操作系统都快被我玩坏了。不过目前VisualVM也有Bug，Metaspace的最大值好像一直是1G左右，最终我把MaxMetaspaceSize改为20m，Eclipse启动出错，说明这个参数是起作用的，从而证明了VisualVM存在Bug。

	!SESSION 2015-04-07 20:49:06.963 -----------------------------------------------
	eclipse.buildId=4.3.2.M20140221-1700
	java.version=1.8.0_25
	java.vendor=Oracle Corporation
	BootLoader constants: OS=win32, ARCH=x86_64, WS=win32, NL=en_US
	Framework arguments:  -product org.eclipse.epp.package.standard.product
	Command-line arguments:  -os win32 -ws win32 -arch x86_64 -product org.eclipse.epp.package.standard.product
	
	This is a continuation of log file D:\01_Programming\01_Java\workspace\.metadata\.bak_0.log
	Created Time: 2015-04-07 20:49:40.681
	
	!ENTRY org.eclipse.ui 4 0 2015-04-07 20:49:40.697
	!MESSAGE Unhandled event loop exception
	!STACK 0
	org.eclipse.swt.SWTException: Failed to execute runnable (java.lang.OutOfMemoryError: Metaspace)
		at org.eclipse.swt.SWT.error(SWT.java:4397)
		at org.eclipse.swt.SWT.error(SWT.java:4312)
		at org.eclipse.swt.widgets.Synchronizer.runAsyncMessages(Synchronizer.java:138)
		at org.eclipse.swt.widgets.Display.runAsyncMessages(Display.java:4145)
		at org.eclipse.swt.widgets.Display.readAndDispatch(Display.java:3762)
		at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine$9.run(PartRenderingEngine.java:1113)
		at org.eclipse.core.databinding.observable.Realm.runWithDefault(Realm.java:332)
		at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.run(PartRenderingEngine.java:997)
		at org.eclipse.e4.ui.internal.workbench.E4Workbench.createAndRunUI(E4Workbench.java:140)
		at org.eclipse.ui.internal.Workbench$5.run(Workbench.java:611)
		at org.eclipse.core.databinding.observable.Realm.runWithDefault(Realm.java:332)
		at org.eclipse.ui.internal.Workbench.createAndRunWorkbench(Workbench.java:567)
		at org.eclipse.ui.PlatformUI.createAndRunWorkbench(PlatformUI.java:150)
		at org.eclipse.ui.internal.ide.application.IDEApplication.start(IDEApplication.java:124)
		at org.eclipse.equinox.internal.app.EclipseAppHandle.run(EclipseAppHandle.java:196)
		at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.runApplication(EclipseAppLauncher.java:110)
		at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.start(EclipseAppLauncher.java:79)
		at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:354)
		at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:181)
		at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
		at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
		at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
		at java.lang.reflect.Method.invoke(Unknown Source)
		at org.eclipse.equinox.launcher.Main.invokeFramework(Main.java:636)
		at org.eclipse.equinox.launcher.Main.basicRun(Main.java:591)
		at org.eclipse.equinox.launcher.Main.run(Main.java:1450)
	Caused by: java.lang.OutOfMemoryError: Metaspace

其实我本来是想调优的，但是Windows 7 64位环境上，无论怎么调整参数，最后的启动时间都是6、7秒的样子，所以最后只能变成调"劣"了。（下图为《深入理解Java虚拟机》中测量启动时间的Eclipse插件）

![press](http://tengrui.github.io/public/upload/startup.jpg)

结论：

1. Java虚拟机的内存管理没有想象中那么复杂，如果结合VisualVM这种工具来学习，能起到事半功倍的效果。
1. Java内存空间有时还是挺浪费的，尤其是默认情况下，SurvivorRatio比例为1:1:1的情况下，大概有三分之一的空间一直为空。
1. 关于JVM内存参数的设定还是很有用的，尤其想搞清楚一些问题，希望尽快重现的时候，可以按需求修改空间大小，达到快速把事情搞砸的目的。
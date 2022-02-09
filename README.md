# semeru-issue-15-reproducer
Reproducer for https://github.com/ibmruntimes/Semeru-Runtimes/issues/15

This is a trivial Ant script meant to showcase how the Ant decompression code fails on Semeru Runtimes for MacOs.

Just clone it and place the archive you want to decompress in the root folder. Name it `archive.tar.gz`.

Then invoke the build by calling `ant decompress`. This assumes Ant is installed on the system and is on the path. 
I've tested with the latest version I could find (Apache Ant(TM) version 1.10.10 compiled on April 12 2021).

The issue I'm getting with a "bad" archive is:

```
java.io.IOException: Invalid file path
	at java.base/java.io.File.getCanonicalPath(File.java:624)
	at java.base/java.io.File.getCanonicalFile(File.java:651)
	at org.apache.tools.ant.util.FileUtils.isLeadingPath(FileUtils.java:1331)
	at org.apache.tools.ant.taskdefs.Expand.extractFile(Expand.java:335)
	at org.apache.tools.ant.taskdefs.Untar.expandStream(Untar.java:154)
	at org.apache.tools.ant.taskdefs.Untar.expandFile(Untar.java:108)
	at org.apache.tools.ant.taskdefs.Expand.execute(Expand.java:157)
	at org.apache.tools.ant.UnknownElement.execute(UnknownElement.java:292)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at org.apache.tools.ant.dispatch.DispatchUtils.execute(DispatchUtils.java:99)
	at org.apache.tools.ant.Task.perform(Task.java:350)
	at org.apache.tools.ant.Target.execute(Target.java:449)
	at org.apache.tools.ant.Target.performTasks(Target.java:470)
	at org.apache.tools.ant.Project.executeSortedTargets(Project.java:1401)
	at org.apache.tools.ant.Project.executeTarget(Project.java:1374)
	at org.apache.tools.ant.helper.DefaultExecutor.executeTargets(DefaultExecutor.java:41)
	at org.apache.tools.ant.Project.executeTargets(Project.java:1264)
	at org.apache.tools.ant.Main.runBuild(Main.java:827)
	at org.apache.tools.ant.Main.startAnt(Main.java:223)
	at org.apache.tools.ant.launch.Launcher.run(Launcher.java:284)
	at org.apache.tools.ant.launch.Launcher.main(Launcher.java:101)
```

To obtain further information on what exactly Ant fails on you can remote debug the Ant process, for example like this: https://forgetfulprogrammer.wordpress.com/2012/12/13/debugging-ant-tasks-when-executing-from-the-command-line/

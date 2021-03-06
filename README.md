# android-ffmpeg-java-demo
#说明
以前一直希望可以做一个播放器，所以当时就接触了ffmpeg这个库，当时打算使用JNI的方式进行底层的调用，无奈整个逻辑比较麻烦，因此进度一再搁浅。

后来进一步的了解中发现，其实对于视频的处理，方法是很多的
* 直接以C的代码进行处理，调用ffmpeg库的函数
* JAVA在命令行调用C的程序进行处理，调用ffmpeg程序

经过一段时间的探索，对于ffmpeg的交叉编译已经没什么大问题了，那么我们就来使用这个库吧。

这个demo主要演示，通过JAVA在命令行调用FFMPEG的二进制程序来完成一些视频的处理功能。这个ffmpeg的二进制程序是在交叉编译的过程中生成的。使用的java wrapper是[guardianproject's android-ffmpeg-java](https://github.com/guardianproject/android-ffmpeg-java)，当然我自己有做一些优化，比如使用我自己编译的最新的ffmpeg替换了它原版使用的ffmpeg程序，开发环境也换到了android studio，还添加了一些方法的实现。

##视频剪切
原理：JAVA开启一个命令行，在命令行中调用ffmpeg的程序，根据传入的参数进行相关处理。

```
ffmpeg -ss 00:00:00 -t 00:00:30 -i test.mp4 -vcodec copy -acodec copy output.mp4
* -ss 指定从什么时间开始
* -t 指定需要截取多长时间
* -i 指定输入文件
```
##视频合并
原理：JAVA开启一个命令行，在命令行中调用ffmpeg的程序，根据传入的参数进行相关处理。

```
//进行视频的合并
ffmpeg -f concat -i list.txt -c copy concat.mp4
```

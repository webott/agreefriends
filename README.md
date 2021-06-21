# agreefriends
PC微信机器人接口api之实战分析微信同意好友call
Q：2645542961
今天分析一下同意好友请求的call，这个需要两个参数，v1和v2，这两个参数哪里来呢，就是在别人加你的时候，收到的消息里面含有的参数，我们可以用一个小号加下自己的微信，然后这边接收到个xml消息，里面含有一些信息，
![image](https://user-images.githubusercontent.com/73727649/122732878-42fe3d80-d2af-11eb-99ab-2d34859a8bc9.png)
然后我们附加微信到CE，把v1复制进去查找，在PC微信页面随便切换一下，再次搜，左边地址变的更少，
![image](https://user-images.githubusercontent.com/73727649/122732910-47c2f180-d2af-11eb-8209-ad257617c3ba.png)
把过滤出来的地址，移到下面，然后我们观察这个地址，一般是地址间隔大的，概率高，所以我们先从间隔大的入手，我们在OD下一个内存访问断点，然后在PC微信点击一下别人请求的同意加好友按钮，发现断点没有，说明这个地址不是的，然后我们在CE再复制一个地址，试第二个，同样的流程，看看断点是否端下来，然后试了几个地址，最终一个地址，断点断下来了，
![image](https://user-images.githubusercontent.com/73727649/122732947-4f829600-d2af-11eb-8cbe-1209f8a23255.png)
然后删除这个断点，在右下角窗口，右键，在反汇编窗口中跟随，返回上一层，在左上角窗口，下一个断点，然后再在PC微信点击一下同意，发现断下来了，调试一下这个断点，发现他给eax赋值了，然后把里面一个关键的call删掉，运行过去，发现点击同意按钮的时候没有提示，再恢复后，又可以提示了，说明这个call很关键。
![image](https://user-images.githubusercontent.com/73727649/122732972-56110d80-d2af-11eb-81ea-b55bd8f92aef.png)
![image](https://user-images.githubusercontent.com/73727649/122732987-58736780-d2af-11eb-96e7-f56bb67c65b4.png)
通过调试，找到各个参数需要的call。然后这个理解了的话，比如自动收款，也就通了。
![image](https://user-images.githubusercontent.com/73727649/122733067-6a550a80-d2af-11eb-8767-8837eca08601.png)
目前已经实现了很多有趣的功能，运行稳定，比如：发各种消息，
接收各种消息，群管，下载文件，加好友，检测僵尸粉等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流，Q：2645542961


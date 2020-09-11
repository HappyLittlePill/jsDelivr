GitHub+jsDelivr+FFmpeg打造切片视频床

#### 准备工作：

- 一个视频文件out.avi

- 下载FFmpeg

------

#### 操作步骤：

1. 把视频转码为**视频编码 h.264，音频编码 aac 格式**的 mp4 文件

   ```
   ffmpeg -i 源视频文件.xxx -vcodec h264 -acodec aac 目标文件.mp4
   如：ffmpeg -i out.avi -vcodec h264 -acodec aac out.mp4
   ```

2. 将mp4转换为ts格式文件

   ```
   ffmpeg -y -i 源mp4文件路径 -vcodec copy -acodec copy -aac h264_mp4toannexb 目标ts文件
   如：ffmpeg -y -i out.mp4 -vcodec copy -acodec copy -vbsf h264_mp4toannexb out.ts
   ```

3. 将ts文件切片并转换为m3u8格式

   ```
   ffmpeg -i 待转换ts文件路径 -c copy -map 0 -f segment -segment_list 目标m3u8文件 -segment_time 单个切片时长(0-60s) 目标ts切片文件名称
   
   如：ffmpeg -i out.ts -c copy -map 0 -f segment -segment_list out.m3u8 -segment_time 5 %03d.ts
   ```

4. 将得到的所有*.ts文件+生成的xxx.m3u8文件一起上传到GitHub仓库的同一个文件目录下

5. 加上jsDelivr加速后的网址，即获得在线m3u8播放器可以播放的视频网址

   视频链接格式：`https://cdn.jsdelive.net/gh/GitHub用户名/库名/文件目录/xxx.m3u8`

   如：`https://cdn.jsdelivr.net/gh/HappyLittlePill/jsDelivr/测试/out.m3u8`

------

#### 播放效果：

[在线m3u8播放器](https://www.m3u8play.com/?play=https://cdn.jsdelivr.net/gh/HappyLittlePill/jsDelivr/%E6%B5%8B%E8%AF%95/out.m3u8)

![image-20200911141720619](https://cdn.jsdelivr.net/gh/HappyLittlePill/jsDelivr/img/image-20200911141720619.png)

------

#### 参考文档：

[小白也能白嫖:jsDelivr+FFmpeg打造切片视频床](https://www.bilibili.com/read/cv6103017)

[FFmpeg安装(Linux)以及MP4转码为ts和m3u8](https://blog.csdn.net/hk_shao/article/details/86688756?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)

[ffmpeg转码视频真的好用！（ffmpeg的简单使用方法）](https://blog.csdn.net/hk_shao/article/details/86688756?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)

[ffmpeg 命令行转码案例](https://blog.csdn.net/n66040927/article/details/80880606)


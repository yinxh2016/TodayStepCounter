# TodayStepCounter
>最近在项目中研究计步模块，每天0点开始记录当天的步数，类似微信运动。碰到了不少坑今天有时间整理出来给大家看看。
做之前在google、baidu、github上搜了个遍没找到好的，大多数都是需要在后台存活，需要后台Service。
对于现在的各大手机厂商为了提高电池的续航里程（省电），基本上AlertManager、android.intent.action.BOOT_COMPLETED、后台Service都是被干掉的。
后台保活策略Service，基本上没什么用，被手机系统干掉只是时间问题，所以我认为最好也不要去做，就算后台存活了，用户看到这个app非常费电也会被删除的。
项目地址：https://github.com/jiahongfei/TodayStepCounter

#####目前android计步有两种方式
######系统计步芯片
>在Android4.4版本之后，部分机型实现了Sensor.TYPE_STEP_COUNTER传感器，用于纪录用户行走的步数。从手机开机开始纪录，手机关机时重置为0。 
这个记步芯片是系统级别的，相对之前老版本的传感器记步，性能有一些优化：
不会因为App单独用了记步的功能而额外耗电
系统芯片记步是持续的，能够优化部分机型后台不记步的问题。

######加速度传感器计算方式
>加速度传感器非常耗电，导致App的耗电量很高，影响用户体验。
需要后台实时运行才能实现记步的功能，如果App进程被系统或者安全软件杀死，导致记步功能没办法使用

###我采用Sensor.TYPE_STEP_COUNTER传感器实现

替换Pixel3温控文件的magisk模块
==============
增强高温性能表现，在低电量以及高温关机前关闭两个大核（高温指温度55度以上），使用quiet-therm-adc温度传感器，其他品牌手机传感器名称不一样，无法使用。
以下是温控文件参数说明
-------------------


```
[HIGH-SS-CPU4-SP0]      #标题无意义
algo_type ss            #采用ss温控策略
sampling 500            #采样时间，单位ms
sensor xo-therm-adc     #监控传感器名称
device cpu4             #控制设备，CPU4代表4567四个大核心
set_point 39000         #触发调节机制的温度点
set_point_clr 38000     #解除调节机制的温度点
time_constant 0         #采样错误时的延迟调整时间
device_perf_floor 2323200 #设置当前温度区间下自动降频的下限（2.3232GHz），此下限仍无法降温则待温度上升至下一个温度区间按照下一个区间的设置继续降频
```
```
[HIGH-BAT_SOC_HOTPLUG_MONITOR]
algo_type   monitor                         #采用监控策略
sampling   2000
sensor    soc
thresholds   10                             #动作触发点
thresholds_clr   11                         #动作清除点
actions   hotplug_6+hotplug_7+cpu4          #动作控制对象：热插拔6号核心+热插拔7号核心+大核心频率等级控制
action_info   1+1+1286400                   #动作信息：关闭+关闭+1.2864GHz
descending                                  #触发点清除点倒序，没有此指令则正序
```
```
[BATTERY-MONITOR]
algo_type       	monitor                   #采用监控策略
sampling        	2000                      
sensor			xo-therm-adc                    
thresholds      	42000		44000		46000     
thresholds_clr  	41000		43000		45000
actions 		battery		battery		battery    #动作控制对象
action_info		1		2		3                    #动作指令，此例中为电池充电电流
```

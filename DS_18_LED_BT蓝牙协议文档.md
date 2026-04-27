> # 老顾的LED系列产品蓝牙协议
## 说明：
 * 适用于DS18_LED_BTC，Pipedream Lighting项目
## 蓝牙广播名称：
 * `QHM-xxxx`，`xxxx` 代表 `2` 个字节的物理地址
 * `Triones-xxx`,`xxxx` 代表 `2` 个字节的物理地址 `(CC2540型)`
## 写: 16位
 * 服务：FFD5
 * 特征：FFD9
 * 属性：Write | Write without response
## 读：16位 
 * 服务：FFD0
 * 特征：FFD4
 * 属性：Notify
## 数据格式：
 * 固定长度：无
 * 命令头: ?? (1 bytes)
 * 数据：?? (n bytes)
 * 命令尾：?? (1bytes)
## 校验方式：
 * 无
--- 
--- 
>>## 功能 
### 开关
 * 指令：0xDD
 * 开关：0x23 = 开，0x24 = 关 
 * 命令尾：0x33
 * 例子：
   ```javascript
   DD+23+33
   DD+24+33
   ```
---
 * ❗️❗️❗️Triones设备指令如下：
 * 指令：0xCC
 * 例子：
   ```javascript
   CC+23+33
   CC+24+33
   ```
### 显示固定的单色模式
 * 指令：0xB6
 * red：0x00~0xFF
 * green: 0x00~0xFF
 * blue: 0x00~0xFF
 * 暖白: 0x00
 * 状态标志: 0xF0 = 更改RGB，0x0F = 更改W
 * 命令尾：0xAA
 * 例子：`红色(EB3223)`
   ```javascript
   B6+EB+32+23+00+F0+AA
   ```
---
 * ❗️❗️❗️Triones设备指令如下：
 * 指令：0x56
 * 例子：`红色(EB3223)`
   ```javascript
   56+EB+32+23+00+F0+AA
   ```
### 音乐模式下，颜色数据
 * 指令：0x78
 * red：0x00~0xFF
 * green: 0x00~0xFF
 * blue: 0x00~0xFF
 * 暖白: 0x00
 * 状态标志: 0xF0 = 更改RGB，0x0F = 更改W
 * 命令尾：0xEE
 * 例子：`红色(EB3223)`
   ```javascript
   78+EB+32+23+00+F0+EE
   ```
### 显示指定模式的颜色
* ```javascript
  🔥🔥🔥 model:
        七彩渐变 = 0x25
        红色渐变 = 0x26 
        绿色渐变 = 0x27 
        蓝色渐变 = 0x28 
        黄色渐变 = 0x29 
        青色渐变 = 0x2A 
        紫色渐变 = 0x2B 
        白色渐变 = 0x2C 
        红绿渐变 = 0x2D 
        红蓝渐变 = 0x2E 
        绿蓝渐变 = 0x2F 
        七彩频闪 = 0x30 
        红色频闪 = 0x31 
        绿色频闪 = 0x32 
        蓝色频闪 = 0x33 
        黄色频闪 = 0x34 
        青色频闪 = 0x35 
        紫色频闪 = 0x36 
        白色频闪 = 0x37 
        七彩跳变 = 0x38
  ```
 * 指令：0x2A
 * mode：0x25~0xFF
 * speed: 0x01~0x1F
 * 命令尾：0x44
 * 例子：`七彩跳变，跳变速度：1`
   ```javascript
   2A+38+01+44
   ```
---
 * ❗️❗️❗️Triones设备指令如下：
 * 指令：0xBB
 * 例子：`七彩跳变，跳变速度：1`
   ```javascript
   BB+38+01+44
   ```   
### 设置外麦模式
 * 指令：0x01
 * 外麦开启状态：0xF0 = 开启，0x0F = 关闭 
 * 外麦模式值：0x00~0x03
 * 外麦灵敏度：0x00~0x64
 * 例子：
   ```javascript
   01+F0+00+64+00+18
   ``` 
---
* ❗️❗️❗️Triones设备没有设置外麦的指令
### 查询设备数据
 * 指令：0x7F
 * 命令尾：0x77
   ```javascript
   7F+01+77
   ```   
### 设备返回数据
 * 指令：0x66
 * 数据：n bytes
 * 命令尾：0x99
 * 格式：
   ```javascript
   66+设备名0x04+开/关机(1byte)+指定的颜色模式(1byte)+运行/暂停状态(1byte)+速度值(1byte)+red(1byte)+green(1byte)+blue(1byte)+暖白(1byte)+版本号0x03+99
   ```    
---
---
>> ## 其他的一些值的范围和取值   
* R: 0x00--0xFF 
* G: 0x00--0xFF 
* B: 0x00--0xFF 
* play: 0x20
* pause: 0x21 
* 音乐模式:0x42 
* W:0x00--0xFF   

---
---
* [点击查看文档原文件](https://docs.google.com/viewer?url=https://raw.githubusercontent.com/tucici/qzkj/master/PipedreamLighting通讯协议V3.xls&embedded=true)
* [点击查看Troines(CC2540)文档原文件](https://docs.google.com/viewer?url=https://raw.githubusercontent.com/tucici/qzkj/master/PipedreamLighting(troines即CC2540型)通讯协议.xls&embedded=true)
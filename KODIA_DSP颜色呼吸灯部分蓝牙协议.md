> # 张毕华的的KODIA DSP项目里的呼吸灯功能蓝牙协议
## 说明：
 * 只适用于KODIA DSP 项目里的颜色呼吸灯部分
## 蓝牙广播名称：
 * 名字包含`DSP`
## 写: 16位
 * 服务：FAA0
 * 特征：FAA1
## 读：16位 
 * 无定义
## 数据格式:
 * 帧头 FE(1bytes)+指令(1bytes)+数据长度(1bytes)+数据(Nbytes)+校验(1bytes) 
## 校验方式：
* `🔥🔥🔥指令+数据，按字节进行按位异或运算，结果取低8位` 
 * xor = 指令 ^ 数据
 * crc = xor & 0xFF
--- 
--- 
>>## 功能 
### 呼吸灯自定义颜色状态
 * 指令：0xAA
 * 数据长度：0x01  
 * 开关：0x00 = 开，0x01 = 关
 * 校验码：1byte
 * 例子：
   ```javascript
   打开：FE+AA+01+00+AA
   关闭：FE+AA+01+01+AB    
   ```
### 呼吸灯自定义颜色模式
 * 指令：0xBB
 * 数据长度：0x01 
 * 模式: 0x00 =  animation模式， 0x01 = color cycle模式
 * 校验码：1byte
 * 例子：
   ```javascript
   animation模式： FE+BB+01+00+BB
   colorcycle模式：FE+BB+01+01+BA
   ```
### 自定义颜色
 * 指令：0xCC
 * 数据长度：0x03
 * red：0x00~0xFF
 * green：0x00~0xFF
 * blue：0x00~0xFF
 * 校验码：1byte
 * 例子：`红色(EB3223)`
   ```javascript
   FE+CC+03+EB3223+20
   ```

> # BT+MP3功能说明(AC6926A)：
## 说明：
 * 采用UART与外部HOST MCU通讯
 * UART波特率：115200，无奇偶校验位
 * AC6926 上电之后，默认处于BT工作模式
## 蓝牙广播名称：
 * `BT-Audio`

## 数据格式：
 * 起始符(2byte)+数据包长度(1byte)+命令(1byte)+数据(n byte)+结束符
 * 起始符: CC20 (2 bytes)
 * 数据包长度：?? (1bytes)
 * 命令：?? (1 bytes)
 * 数据：?? (1 bytes)
 * 结束符：?? (1 bytes)
## 校验方式：
 * 无
--- 
--- 
>>## 功能 
### BT/MP3模式
 * 指令：0x02
 * BT模式：0x00
 * MP3模式：0x01
 * 例子：`切换到BT模式`
   ```javascript
   CC20+06+02+00+55
   ```

### BT PAIR操作
 * `BT模式有效` 
 * `清除当前的BT连接，并一直处于等待新的链接状态直到有新的连接成功。`  
 * 指令：0x03
 * 例子：`配对`
   ```javascript
   CC20+06+03+00+55
   ```
### TWS LINK操作命令
 * `BT模式有效`  
 * 指令：0x04
 * 清除当前的TWS连接，并处于等待新的配对链接状态，直到有新的配对连接成功 或 时间超过30秒：0x00
 * 清除当前的TWS连接，且不再处于等待新的配对链接状态
 * 例子：``
   ```javascript
   CC20+06+04+00+55
   ```   
### MP3播放操作命
 * `MP3模式有效`  
 * 指令：0x05
 * 停止：0x00
 * 暂停：0x01
 * 播放：0x02
 * 上一曲：0x03
 * 下一曲：0x04
 * 例子：`播放`
   ```javascript
   CC20+06+05+02+55
   ``` 
### 修改蓝牙名称
 * 指令：0xFF
 * 名称数据：32个 utf8字节，名字长度不足补0
 * 例子：
   ```javascript
   CC20+FF(32个byte名字)+55
   ```      
### 获取AC6926当前状态命令 
 * `BT模式/MP3 模式均有效`  
 * 指令：0x01
 * 例子：``
   ```javascript
   CC20+06+01+00+55
   ```     
### AC6926当前状态数据包返回 
 * 起始符：0xCC,0x20
 * 数据包长度：0x54
 * 命令：0x01
 * 当前工作模式：0x00/0x01(BT/MP3模式)
 * BT PAIR状态：0x00/0x01/0x02(无连接/已连接/可连接)
 * U盘连接状态：0x00/0x01(无连接/已连接)
 * MP3播放状态：0x00/0x01/0x02(停止/暂停/播放)
 * 当前歌曲总时间长度：时/分/秒（3byte）
 * 当前歌曲播放进度：时/分/秒（3byte）
 * 当前歌曲名称：ascll码（64byte）
 * 总歌曲数量：2byte
 * 当前播放歌曲：2byte
 * 结束符：0x55
---
---
###  2025/06/12 改版（改原有的，或新增） 
### BT/MP3模式
 * 指令：0x02
 * BT模式：0x01
 * MP3模式：0x00
 * 例子：`切换到BT模式`
   ```javascript
   CC20+06+02+01+55
   ```
### MP3播放操作命
 * `MP3模式有效`  
 * 指令：0x05
 * 停止：0x00
 * 暂停/播放：0x01
 * 上一曲：0x02
 * 下一曲：0x03
 * 例子：`播放`
   ```javascript
   CC20+06+05+01+55
   ``` 
### 主控内部发单片机数据 
 * `播放会立马主动发，停止播放会等10秒后发`
 * 主控内部DAC已开始播放：
   ```javascript
   0xCC,0x20,0x06,0x10,0x01,0x55
   ```
 * 主控内部DAC已停止播放：
   ```javascript
   0xCC,0x20,0x06,0x10,0x00,0x55
   ```
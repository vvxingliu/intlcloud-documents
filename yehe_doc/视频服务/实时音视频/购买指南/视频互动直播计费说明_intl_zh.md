>!本文档仅针对 TRTC 低延时直播房间内的计费作出相关说明。若将 TRTC 房间内的音视频流旁路到云直播系统中，让观众通过直播 CDN 观看，将产生额外的费用，详情请参见 [CDN 直播观看 > 相关费用](https://intl.cloud.tencent.com/document/product/647/35242)。


<span id="Billing_items"></span>
## 用量统计方式

实时音视频 TRTC 按 [房间](https://intl.cloud.tencent.com/document/product/647/37714) 内所有用户产生的 [视频时长](#v_duration) 和 [语音时长](#s_duration) 来统计视频互动直播服务的用量。

>!时长统计精度为秒，以当月累计秒数转换成分钟数后进行计费，不足一分钟按一分钟计。


<span id="v_duration"></span>
### 视频时长
视频时长是指用户进入 TRTC 房间后订阅了音视频流并且成功接收到了视频画面的时间。TRTC 会根据用户**实际接收到的视频分辨率**划分视频档位，然后分别对不同档位的视频时长进行计费。
视频档位与分辨率的对应关系如下表所示：

|视频档位|实际接收分辨率|
|-------|--------|
|标清 SD|不高于640 × 480（含）|
|高清 HD|640 × 480 - 1280 × 720（含）|
|超清 HD+|高于1280 × 720|

- 用户订阅视频时，不管该视频里面有没有包含音频，都只统计一次视频时长，不会重复计算语音时长。
- 单个用户同时订阅多路视频时，其订阅的每一路视频时长将分别统计后叠加计算。
- TRTC 全平台 SDK 都不会限制您的视频分辨率，您可以根据实际业务需求自行 [设定画面质量](https://intl.cloud.tencent.com/document/product/647/35153)。


<span id="s_duration"></span>
### 语音时长
视频互动直播场景下的语音时长 = 用户在 TRTC 房间内的总停留时长 - 接收视频画面时的停留时长。
例如，某用户在00:00进入 TRTC 房间，00:50离开房间，其在房间内停留的情况如下图所示：
![](https://main.qcloudimg.com/raw/b127abe248a205842a6216ccbd7c111e.png)
图中蓝色部分记为该用户的语音时长，即`总停留时长 - 接收视频画面时的停留时长 = 50分钟 - 15分钟 = 35分钟`。


- 只有当用户没有订阅视频时，才会统计语音时长。
- 用户成功进入 TRTC 房间后，只要没有订阅视频，即使不上行推流也会统计语音时长。
- 用户可能会在同一个房间内多次进出，TRTC 会实时统计其多段语音时长后叠加计算。


<span id="Fixed_price"></span>
## 服务定价

视频互动直播服务的刊例价如下表所示：

|计费项|单价（美元/千分钟）|
|---|---|
|语音|0.99|
|标清 SD|1.99|
|高清 HD|3.99|
|超清 HD+|14.99|


TRTC 为您提供音视频通用套餐包，可按照**1:2:4:15**分别抵扣语音、标清 SD、高清 HD 和超清 HD+ 时长，例如1分钟高清视频时长扣除4分钟通用套餐包时长。
通用套餐包定价如下表所示：

<table>
     <tr>
         <th style="text-align:center">套餐包类型</th>  
         <th style="text-align:center">套餐包时长（千分钟）</th> 
         <th style="text-align:center">刊例价（美元/千分钟）</th> 
         <th style="text-align:center">套餐内单价（美元/千分钟）</th> 
         <th style="text-align:center">套餐包价格（美元）</th> 
          <th style="text-align:center">折扣</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">固定套餐包</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center"><97%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center"><82%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">自定义套餐包</td>   
         <td style="text-align:center">0 ＜ T ＜ 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">套餐内单价*套餐包时长 T</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T ＜ 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center"><97%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center"><82%</td>   
     </tr> 
</table>


>?表格中套餐内单价按每千分钟单价向上取整精确到小数点后3位，实际计费按每分钟单价精确到小数点后8位。

通用套餐包说明：
- 通用套餐包的有效期为购买当日 - 次年当月最后一天。
 例如，2020年05月01日购买的套餐包，其有效时间为2020年05月01日 - 2021年05月31日。
- 通用套餐包可以叠加购买，根据各类型用量实际产生的时间实时从通用套餐包中扣除相应分钟数，优先使用先过期的套餐包进行抵扣。
- 新购套餐包支付成功后5分钟左右生效，**新购套餐包生效后会立即扣除购买新套餐包当日0点起产生的未被其他套餐包抵扣过的用量**。
- 为了不影响您线上业务的正常运行，**通用套餐包用完或过期后不会自动停服**，超出套餐包的用量将采用 [后付费](#post-payment) 的计费方式。
- 所有通用套餐包到期后未消耗的分钟数将自动清零且无法恢复。


<span id="post-payment"></span>
### 后付费
当服务用量无套餐包可抵扣或超出套餐包余量时，将采用后付费的方式，按 [刊例价](#Fixed_price) 计费。
TRTC 后付费有 [日结](#daily) 和 [月结](#monthly) 两种结算周期：

#### 日结后付费<span id="daily)
2020年09月01日起首次在 TRTC 控制台创建 [应用](https://intl.cloud.tencent.com/document/product/647/37714) 的用户，后付费生效后默认采用**日结**方式结算。按日计费，每天上午10点扣除前一天产生的费用。


<span id="monthly"></span>
#### 月结后付费
2020年08月31日及之前首次在 TRTC 控制台创建 [应用](https://intl.cloud.tencent.com/document/product/647/37714) 的用户，后付费生效后默认采用**月结**方式结算。按月计费，每月01日 - 05日从您的账户余额中扣除前一月产生的费用，详情以 [计费账单](https://intl.cloud.tencent.com/document/product/555/7432) 为准。
>!
- 后付费只能通过先购买套餐包，待购买的所有套餐包都消耗完或过期后自动开通，无法直接开通。
- 结算周期无法自主变更，若您希望将月结变更为日结，可以 [提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。
- 若您的账户因余额不足而无法抵扣账单费用时，您使用的其他腾讯云服务也可能会因为账户欠费而自动停服。例如，云端录制依赖**云直播**和**云点播**，如果腾讯云账户欠费，将导致云端录制失败。

<span id="Billing_examples"></span>
## 计费示例
>!本文计费示例采用刊例价计算，您可以通过 [购买套餐包](https://buy.cloud.tencent.com/trtc) 的方式节省费用。

### 纯语音时长示例
假设用户 A、B、C 三人一起在 TRTC 房间内持续停留了30分钟。A、B、C 三人始终没有接收视频画面。
则该 TRTC 房间产生的语音时长**总费用**为 `语音时长单价 × 所有用户语音时长之和 = 0.99美元/千分钟 × (30分钟 + 30分钟 + 30分钟) / 1000 = 0.0891美元`。

### 纯视频时长示例

假设用户 A、B 一起在 TRTC 房间中持续停留了45分钟。A、B 都始终接收对方的视频流。A 、B 实际接收到的视频分辨率如下表所示：

<table>
     <tr>
         <th style="text-align:center">时间</th>  
         <th style="text-align:center"> A 接收 B 的分辨率</th> 
         <th style="text-align:center"> B 接收 A 的分辨率</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">前30分钟</td>   
         <td style="text-align:center">1280 × 720（高清）</td>
         <td style="text-align:center">1920 × 1080（超清）</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">后15分钟</td>   
         <td style="text-align:center">640 × 360（标清）</td> 
         <td style="text-align:center">640 × 360（标清）</td>
     </tr> 
</table>

**分析：**
- A 产生的用量及费用：
  - A 接收 B 的分辨率前30分钟位于高清档，后15分钟位于标清档。
  - A 产生的费用为 ` 高清视频时长单价 × 高清视频时长 + 标清视频时长单价 × 标清视频时长 = 3.99美元/千分钟 × (30分钟 / 1000) + 1.99美元/千分钟 × (15分钟 / 1000）= 0.14955美元`。
- B 产生的用量及费用：
  - B 接收 A 的分辨率前30分钟位于超清档，后15分钟位于标清档。
  - B 产生的费用为 `超清视频时长单价 × 超清视频时长 + 标清视频时长单价 × 标清视频时长 = 14.99美元/千分钟 × (30分钟 / 1000) + 1.99美元/千分钟 × (15分钟 / 1000）= 0.47955美元`。

则该 TRTC 房间产生的**总费用**为 `用户 A 产生的费用 + 用户 B 产生的费用 = 0.6291美元 `。

### 语音时长和视频时长混合示例

假设用户 A、B 一起在 TRTC 房间中持续停留了45分钟。A 始终接收 B 的视频流；B 前30分钟接收了 A 的视频流，后15分钟没有接收 A 的视频流。A 、B 实际接收到的视频分辨率如下表所示：

<table>
     <tr>
         <th style="text-align:center">时间</th>  
         <th style="text-align:center">A 接收 B 的分辨率</th> 
         <th style="text-align:center">B 接收 A 的分辨率</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">前30分钟</td>   
         <td style="text-align:center">1280 × 720（高清）</td>
         <td style="text-align:center">1920 × 1080（超清）</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">后15分钟</td>   
         <td style="text-align:center">640 × 360（标清）</td> 
         <td style="text-align:center">语音（无视频）</td>
     </tr> 
</table>


**分析：**
- A 产生的用量及费用：
  - A 接收 B 的分辨率前30分钟位于高清档，后15分钟位于标清档。
  - A 产生的费用为 ` 高清视频时长单价 × 高清视频时长 + 标清视频时长单价 × 标清视频时长 = 3.99美元/千分钟 × (30分钟 / 1000） + 1.99美元/千分钟 × (15分钟 / 1000)= 0.14955美元`。
- B 产生的用量及费用：
  - B 接收 A 的分辨率前30分钟位于超清档，后15分钟没有接收 A 的视频流。
  - B 产生的费用为 `超清视频时长单价 × 超清视频时长 + 语音时长单价 × 语音时长 = 14.99美元/千分钟 × (30分钟 / 1000) + 0.99美元/千分钟 × (15分钟 / 1000）= 0.46455美元`。

则该 TRTC 房间产生的**总费用**为 `用户 A 产生的费用 + 用户 B 产生的费用 = 0.6141美元 `。



## 相关文档
- [计费概述](https://intl.cloud.tencent.com/document/product/647/34610)
- [免费试用](https://intl.cloud.tencent.com/document/product/647/39784)
- [语音互动直播计费说明](https://intl.cloud.tencent.com/document/product/647/39785)
- [语音通话计费说明](https://intl.cloud.tencent.com/document/product/647/39787)
- [视频通话计费说明](https://intl.cloud.tencent.com/document/product/647/39788)
- [云端录制计费说明](https://intl.cloud.tencent.com/document/product/647/38385)
- [云端混流转码计费说明](https://intl.cloud.tencent.com/document/product/647/38929)
- [购买指引](https://intl.cloud.tencent.com/document/product/647/35440)
- [计费常见问题](https://intl.cloud.tencent.com/document/product/647/39789)
v

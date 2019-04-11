# AR 

## 0.系统构成元素

### 0.1系统总体布局：

![系统总体布局](https://github.com/chaorents/AR-/blob/master/%E7%B3%BB%E7%BB%9F%E6%80%BB%E4%BD%93%E5%B8%83%E5%B1%80.png)

原有设备图示：

![example](https://github.com/chaorents/AR-/blob/master/example.png)

在指南区放置实验卡，右侧仓储设置区显示投影，整体设置：20m x 15m，即为长20格，宽15格（每格表示1m^2^）





### 0.2系统基本参数设计

#### 0.2.1仿真元素分类

表系统仿真元素

|  序号  | 名称               | 说明                                                         |                             备注                             |
| :----: | ------------------ | ------------------------------------------------------------ | :----------------------------------------------------------: |
|   1    | 货架               | 由二维码进行标识。数量20个，尺寸：7m x 3m。每层3个托盘，高3层。两侧有小车取货位置。 |  每次试验时尽量摆满仿真区域。少于8个货架时，系统进行提示。   |
|   2    | 托盘               | 作为放置商品的载体，尺寸为叉车可以叉上即可。                       |                1个托盘放置25个商品（5行5列）                 |
|   3    | 商品               | 每种商品一种颜色，需要设置20种商品                           |                                                              |
|   4    | 入库作业区         | 由二维码进行标识。系统试验时，必须有入库作业区元素。且入库作业区一侧需要设置小车取货位置。尺寸：14x4 | ![入库作业区](https://github.com/chaorents/AR-/blob/master/%E5%85%A5%E5%BA%93%E4%BD%9C%E4%B8%9A%E5%8C%BA.png) |
|   5    | 出库作业区         | 由二维码进行标识。系统试验时。必须有出库作业区元素。且入库作业区一侧需要设置小车取货位置。尺寸：14x4 | ![出库作业区](https://github.com/chaorents/AR-/blob/master/%E5%87%BA%E5%BA%93%E4%BD%9C%E4%B8%9A%E5%8C%BA.png) |
|   6    | 仓库办公室         | 由二维码进行标识。仓储布局时候。至少有一个仓储办公室。尺寸：8x6 |          用户没有放置仓库办公室元素，系统进行提示。          |
|   7    | 搬运车辆           | 由二维码进行标识。种类见1.2搬运车辆类型。                    | 仓储布局实验时，由用户扫描二维码确定搬运车辆。输入完成后，系统默认2个堆高机叉车（整托叉货物）和2个电动拣选车（单个商品拿 |
|   8    | 实验内容区         | 由二维码进行标识。印刷到A4纸张右上角。标识不同实验内容。     | 实验步骤及实验参数设置、实验数据由投影设备投影到实验内容区。 |
|   9   | 商品品类           | 由二维码进行标识。主要完成不同商品的参数设置及模拟订单的生成。以及托盘码盘及商品货架负载能力的计算。 |                           数量为20                           |
| 10 | 学生学号及姓名 | 由二维码进行标识。每次实验前，由学生进行标识。考虑学生分组，系统可记录多个学生学号。 |         可考虑使用学生手机生成学号及姓名二维码。         |

#### 0.2.2系统内涉及到的搬运车辆类型

如表所示，系统应设置如下4种搬运车辆类型，并应支持用户增加类型。参数应可设置。

| 序号 | 叉车名称     | 叉车参数                                                     | 仿真设计                                                     | 备注                                                         |
| ---- | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | 堆高机叉车   | （1）    长宽高：2x0.8x0.9 （2）    最小转弯半径：1.6   （3）      最小通道宽度：2.7   （4）    行走速度（满载/空载）：5.5/6（Km/h）   （5）    提升速度（满载/空载）：80/120（mm/s）   （6）    下降速度（满载/空载）：120/100（mm/s）   （7）    承载能力：1-1.6吨.   （8）    提升高度4.8米。 | 在仿真系统中主要体现的通道宽度。当用户选择堆高机叉车时，通道至少要3米（仿真系统简化为3个单元格）。行驶速度简化为1米/秒。货架取放一次托盘时间进行如下设定：（1）第1层取放时间为10S。（2）第2层为40S。（3）第3层为60S。在出入库缓冲区取放一次托盘时间为10S | 用图标1代表堆高车叉车。考虑仿真效果，行驶速度要考虑连续性，不能跳。取放托盘时间系统记录为真实时间，仿真效果为真实时间除以20 |
| 2    | 前移式叉车   | （1）    长宽高：2x1.0x2.0   （2）    最小转弯半径：1.8   （3）    最小通道宽度：2.6   （4）    行走速度（满载/空载）：5.5（Km/h）   （5）    提升速度（满载/空载）：100/180（mm/s）   （6）    下降速度（满载/空载）：120/100（mm/s）   （7）    承载能力：1-1.6   （8）    提升高度6.0米。 | 同堆高机叉车。                                               | 用图标2代表前移式叉车。                                      |
| 3    | 平衡重式叉车 | （1）    长宽高：3x1.0x2.0   （2）    最小转弯半径：1.7   （3）    最小通道宽度：3.4   （4）    行走速度（满载/空载）：13（Km/h）   （5）    提升速度（满载/空载）：340/400（mm/s）   （6）    下降速度（满载/空载）：600/300（mm/s）   （7）    承载能力：1.8   （8）    提升高度6.0米。 | 选型此叉车时，通道宽度至少3.5米。行驶速度为2米/秒。货架取放一次托盘时间进行如下设定：（1）第1层取放时间为10S。（2）第2层为20S。（3）第三层为30S。在出入库缓冲区取放一次托盘时间为10S | 用图标3代表平衡重叉车。                                      |
| 4    | 电动拣选车   | （1）长宽高：2.5x1x2.5 （2）最小转弯半径1.6 （3）最小通道宽度：1.5 （4）行走速度：4km/h（5）提升速度（满载/空载）：110/160（mm/s） （6）下降速度：150/130 （7）承载能力：1吨 （8）提升高速 3米 | 此叉车主要完成拣选作业。要求通道宽度为1.5个单元格。按照不同订单，不同层布局。系统默认进行如下设定：（1）第1层取放时间为10S。（2）第2层为30S。（3）第三层为60S。在出入库缓冲区取放一次托盘时间为10S. | 用图标4代表电动拣选车。                                      |


仿真参数进行如下假设：

| 叉车速度 | 慢：0.5.快：1                   |
| -------- | ------------------------------- |
| 语音拣选 | 是：提高5s   否：默认为否       |
| 休息     | 是：30分钟休息一次   否：不休息 |
| 产品尺寸 | 大：默认为大   小：小尺寸       |

注：前3类叉车主要完成整托盘出入库管理。第4类叉车（电动拣选车）可以完成拣选作业。

采用第4类拣选叉车作业时，总工作时间由如下时间组成：总时间=组织时间（去办公室取拣选作业单时间）+车辆行驶时间（搬移时间）+拣选时间（人工拣货时间）+不动时间（升降时间）+丢失时间（是否休息）

#### 0.2.3系统订单模型

订单按照正态分布模型。

#### 0.2.4系统订货模型

默认时，每种商品在库存中至少一托盘，仓库中有空位置时，随机在入库作业区出现商品托盘。

****

## 1.实验1：仓储组织

### 1.1存储面积

### ![1.1仓储组织：存储面积](https://github.com/chaorents/AR-/blob/master/1.1%E4%BB%93%E5%82%A8%E7%BB%84%E7%BB%87%EF%BC%9A%E5%AD%98%E5%82%A8%E9%9D%A2%E7%A7%AF.png)

设置目的：让学生练习操作AR设备同时，对仓储面积有所认识。

### 1.2仓库典型布局

![1.1仓储组织：仓库典型布局](https://github.com/chaorents/AR-/blob/master/1.2%E4%BB%93%E5%82%A8%E7%BB%84%E7%BB%87%EF%BC%9A%E4%BB%93%E5%BA%93%E5%85%B8%E5%9E%8B%E5%B8%83%E5%B1%80.png)

设置目的：设计仓库布局，放置装卸货台、办公室和尽可能多的货架，并尽可能缩短出入库距离。并使用堆高车叉车进行出入库仿真，验证不同仓储布局对出入库效率影响。

与入库区的平均距离和与出库区的平均距离：为所有货架与入库区和出库区的平均距离。

托盘出库的平均时间：所有小车从接到订单到将货物出库的时间/订单数量

初始库存状态：以摆放10个货架为例：1个货架能否摆放9个托盘。总共可放置90个托盘。如按照平均分配商品数量既每种商品托盘数量为：90除以20，既4.5托盘，取整为4托盘。剩余10托盘从20种商品中随机生成。90托盘商品随机摆放到72个储位（或90托盘其中有45托盘随机摆放在货架，剩余45托盘在入库缓冲区）。

订单生成规则如下：20种商品每种商品出库2托盘，为40托盘。剩余10托盘为序号为1-10商品，每种商品1托盘。

### 1.3车辆搬运效率

![1.3仓储组织：车辆搬运效率](https://github.com/chaorents/AR-/blob/master/1.3%20%E4%BB%93%E5%82%A8%E7%BB%84%E7%BB%87%EF%BC%9A%E8%BD%A6%E8%BE%86%E6%90%AC%E8%BF%90%E6%95%88%E7%8E%87.png)

设计目的：
	设计仓库布局，通过用户选择不同搬运车辆（堆高机叉车、前移式叉车、平衡重式叉车）的仿真操作，分析不同搬运设备和仓库布局对出入库效率的影响。

与入库区的平均距离和与出库区的平均距离：为所有货架与入库区和出库区的平均距离。

托盘出库的平均时间：所有小车从接到订单到将货物出库的时间/订单数量

初始库存状态：以摆放10个货架为例：1个货架能否摆放9个托盘。总共可放置90个托盘。如按照平均分配商品数量既每种商品托盘数量为：90除以20，既4.5托盘，取整为4托盘。剩余10托盘从20种商品中随机生成。90托盘商品随机摆放到72个储位（或90托盘其中有45托盘随机摆放在货架，剩余45托盘在入库缓冲区）。

订单生成规则如下：20种商品每种商品出库2托盘，为40托盘。剩余10托盘为序号为1-10商品，每种商品1托盘。
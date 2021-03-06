##唯众良品微信商城第二版本
@(lianger)[模块化|业务理解]

**总模块化预览** 活动模块 &nbsp;&nbsp;&nbsp;收藏模块&nbsp;&nbsp;&nbsp;会员福利模块&nbsp;&nbsp;&nbsp;商品模块&nbsp;&nbsp;&nbsp;购物车模块&nbsp;&nbsp;&nbsp;订单模块&nbsp;&nbsp;&nbsp;支付模块&nbsp;&nbsp;&nbsp;vip模块&nbsp;&nbsp;&nbsp;数据统计模块&nbsp;&nbsp;&nbsp;收货地址模块&nbsp;&nbsp;&nbsp;商品评论模块&nbsp;&nbsp;&nbsp;意见反馈&nbsp;&nbsp;&nbsp;物流查询&nbsp;&nbsp;&nbsp;客户服务&nbsp;&nbsp;&nbsp;搜索模块


[TOC]
##快速预览区

####1.首页
| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 轮播图  | 点击到商品列表或者品牌商品详情页 |     |
| 品牌列表     |  点击跳到品牌商品列表  |    |
|品牌收藏     | 收藏到品牌收藏中心，可取消收藏   |    |

**关联表--->**  `广告轮播    品牌活动表  商品表`



>轮播图表设计预览
>>CREATE TABLE `app_banner` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(255) NOT NULL,
  `goods_id` varchar(255) NOT NULL COMMENT '商品id，根据type类型选择',
  `pic_url` varchar(255) NOT NULL COMMENT '图片地址',
  `type` tinyint(4) NOT NULL COMMENT '0: 品牌活动商品列表跳转，1：品牌活动商品详情页面跳转',
   `where_page` tinyint(4) NOT NULL COMMENT '0: 首页，1：会员福利页，2：会商品搜索页，3：待扩展',
  `start_time` datetime NOT NULL DEFAULT '0000-00-00 00:00:00',
  `end_time` datetime NOT NULL DEFAULT '0000-00-00 00:00:00',
  `sort` int(11) NOT NULL DEFAULT '99' COMMENT '排序',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8 COMMENT='广告轮播';

-------------------
>品牌商品活动列表
>>CREATE TABLE `app_promotion` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(16) NOT NULL DEFAULT '' COMMENT '活动名称',
  `describe` varchar(128) NOT NULL DEFAULT '' COMMENT '描述',
  `img` varchar(128) NOT NULL DEFAULT '' COMMENT '图片',
  `goods_ids` text COMMENT '商品id',
  `start_time` int(10) NOT NULL COMMENT '开始时间',
  `end_time` int(10) NOT NULL COMMENT '结束时间',
  `status` enum('on','off') NOT NULL DEFAULT 'on' COMMENT '状态，on=开，off=关',
  `sort` int(8) NOT NULL COMMENT '排序',
  `time` int(10) NOT NULL COMMENT '修改日期',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=17 DEFAULT CHARSET=utf8 COMMENT='首页活动';



####2.会员福利

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| banner图  | 点击跳到品牌商品列表 |     |
| 商品列表     |  点击单个商品跳到商品详情页  |    |
|收藏功能     |  收藏到单品收藏中心，可取消收藏  |    |



####3.分类搜索

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 搜索  | 根据商品名称模糊和精确搜索相关商品，按精确度排序 |     |
| 商品大类     |  点击展开商品分类的子类  |    |
|商品子类     | 点击跳转到该子类的商品列表页  |    |
| banner图  | 点击跳到品牌商品列表 |     |




####4.品牌列表

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 排序条件  | 可根据点击[综合][销量][价格][新品]等四个条件进行排序 | 后期应该有更多的筛选条件    |
| 商品列表  | 展示商品的简要信息，点击可跳转到商品详情页面 |     |
| 收藏功能   |收藏到单品收藏中心，可取消收藏  |    |



####5.商品详情

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 商品缩略介绍图  | 根据商品名称模糊和精确搜索相关商品，按精确度排序 |     |
| 商品信息     |  点击展开商品分类的子类  |    |
|联系客服    | 点击跳转到该子类的商品列表页  |    |
| 评论展示  | 好评率统计，评论的列表展示，注意用户信息加密 | 回复功能延后    |
|商品展示    | 展示商品的详细信息  |    |
|加入购物车    |  点击条件到购物车  |    |
|立即购买    |  直接提交到确定订单页面  |    |
|用户浏览    |  用户浏览时自动添加一条我的足迹访问记录  |    |


####6.收藏品牌

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 品牌列表     |  点击跳到品牌商品列表  |    |


####7.单品收藏

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 品牌商品列表     |  点击跳到品牌商品详情页  |    |


####8.购物车

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 商品列表     |  点击跳到商品详情页  |    |
| 编辑     |  选中将商品移除购物车,可移至收藏页面 |    |
| 结算     |  点击结算确认用户勾选的商品，提交到确认订单页面 |    |



####9.确认订单

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 收货地址     |  获取默认收货地址，如无则让用户添加收获地址，否则不允许提交订单  |    |
| 商品列表     |  可是单个或多个商品，随用户需求定 |    |
| 唯众良品承诺信息     |  如专注品质  品牌保证等 |  后期根据用户提交订单的重量或者满多少价格来自动识别运费  |
| 运费信息     |  目前运费是统一价 |    |
| 联系客服     |  点击拨打客服电话 |  后期  |
| 确认订单     |  点击跳转到支付页面 |    |



####10.支付

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 订单信息     |  显示订单编号和应支付金额  |    |
| 查看订单     |  点击跳转到该订单详情页面 |    |
| 跳转支付     |  自动跳转到微信支付页面 |    |
| 返回首页    |  点击返回到商品搜索页 |    |


####11.订单列表

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 待付款｜ 待收货｜待评价｜退货返修 ｜我的订单 |  根据type类型显示不同的订单列表  |
|  联系卖家   | 未付款订单显示，目前是直接拨打客服电话  |  后期加上其他通信插件  |
|  删除订单   |  未付款或已过期，已完成的订单显示，点击将订单状态更新为用户已删除  |    |
|  申请退货   | 点击跳转至申请退货页面  |    |
|  查看物流   | 点击跳转至物流100快递查询系统  |  后期接入第三方物流订单查询系统  |
|  确认收货  |  点击将订单改为已收获状态  |    |
|  去付款  |  点击再次发起支付交易  |    |
|  评价 |  点击跳转到评价商品页面，判断的条件必须是该用户下的订单才可以评论 |    |
|  已完成｜完成  |  无操作  |    |


####12.订单详情

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 供应商     |  显示订单编号和应支付金额  |    |
| 订单信息     |  展示订单的详细信息 |    |
| 订单状态     |  根据订单状态显示不同的操作按钮(删除订单｜申请退货｜查看物流｜联系卖家｜确认收货｜去付款｜评价) |    |


####13.申请退货页

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 订单商品信息     |  根据订单状态查询订单可退货商品信息  |    |
| 退货退款     |  根据订单状态显示选择退货或退款  |    |
| 退货原因     |  给出相关退货标签，被添加文本加以描述退货理由 |    |
| 申请退货     |  弹出模态框给予申请提示 |    |



####14.商品评价

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 标签     |  后台程序控制相关评价标签  |    |
| 评价内容     | 必须满15个字符串以上，80个字符以下的评价  |    |
| 提交     |  模态框友好提示|    |


####15.查看物流

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 查看物流状态     |  目前仅跳转至物流100|  后期接入物流查询  |




####16.个人中心

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 待付款｜ 待收货｜待评价｜退货返修 ｜我的订单    |  根据type类型筛选订单，并统计相关数量 |    |
|  收货地址   | 点击跳转到我的收获地址列表  |    |
|  会员卡中心   | 点击跳转到VIP中心  |    |
|  我的足迹   | 点击跳转至我的足迹页面  |    |



####17.收获地址列表

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 收获地址列表     |  判断收获地址是否属于默认收获地址，并根据默认收货地址排序  |    |
| 设置默认收货地址     |  点击选中，并确认将某地址设置为默认收货地址 |    |
| 删除收获地址     |  根据收获地址id删除该收获地址   |
| 添加收获地址     |  点击跳转至添加收获地址列表   |


####18.添加收获地址

| 功能      |   说明 | 备注  |
| :-------- | --------:| :--: |
| 添加收获地址信息     |  姓名，手机号，城市三级联动，详细地址  |
| 设置默认收货地址     |  点击选中，并确认将某地址设置为默认收货地址  |
| 确认田添加     |  点击跳转至收获地址列表  |



####19.会员卡中心





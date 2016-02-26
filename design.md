More Than Calendar
===

mtc 是 more than calendar 缩写，以下简称 mtc

设计参考来自

- 日历
- 提醒事项
- 备忘录
- trello cards
- 进度条
- IOS calendar api
- Google calendar api
- Exchange calendar api

calendar 已经可以完成大部分 GTD 需求

但缺少一些东西，特别是定制化的需求，项目进度，过滤器等

trello 的 card 支持如下特性，和 calendar event 对比

- 成员 (event 也可以邀请)
- 标签 (event 支持分组和颜色)
- 评论
- CheckList (提醒事项，event 中没有)
- 截止日期（event 只有执行时间跨度）
- 附件 （event 支持图片，地点等）
- 移动 （event 移动等于改执行时间）


mtc 的设计
---

### 解决的问题

#### list

引入 project 项目的概念，本质是 cards 集合，类似 trello 的 list

card 的关联性，用来管理复杂项目，一个项目通常需要多个 card，有先后顺序，全部完成才算完成

trello 的 card 有 checkList，根据 checkList 也可以有一个进度展示

但缺点是 CheckList 过于简单，没有单独的时间，顺序依赖等关系，因此 trello 也提供了 CheckList 转 card 的功能

模板，模板生成 list，list 是模板的实例，避免重复工作，填写参数就可以生成一个模板，等于生成一篮子 cards

#### 模板事例

一个互联网项目 project list 模板

先建立 namespace，例如 `team:frontend:update banner`，没名字的话就用 `team:frontend:timestamp`

namespace 是有从属关系的 name，方便过滤

建立如下 cards

- 需求，内容为项目大体描述，需求 bugzilla id, 成员为需求人
- 具体 design，design wiki review id
- 开发，开发 bugzilla id，成员为开发人员，执行时间，执行时长，内容有开发依赖
- 代码 review，review id
- 提测，成员为测试人员，内容有团队联调等
- 上线，namespace 设置为 `project namespace:上线`， 内容为上线 bugzilla id，截止时间
- 上线回测与数据分析


### 本质

mtc 本质是一大堆 card，但提供很多视图，和过滤器


### 希望实现的效果

默认打开 list 页面，和 trello 类似，还不确定是横排还是竖排

list 展示进度，和小米购买类似

可以换成日历视图

可以生成报表

提醒下一个截止的 card


### 视图

- cards 列表
- 日历视图，可生成时间报表，比如周报
- namespace 视图，及项目视图
- 个人视图，按成员分类

项目进度视图属于 namespace 视图，进度 = (已完成 + 进行中 / 2) / 全部

建立 card 的时候可以选择 namespace 加入收藏列表

当 namespace 视图的视图的时候，仅收藏的 namespace 才可以显示

### card

结合 calendar 的 event 和 trello 的 card

card 拥有 namespace，用来内容过滤与分组

#### card 维度与属性

- 内容
- namespace 类似 category，分组从属关系
- 标签 支持多个
- 状态：todo doing done，默认值 todo
- 创建人
- 修改人
- 优先级
- 难度
- 时间
	- 建立时间，肯定有
	- 修改时间，肯定有，默认为建立时间
	- 预期开始执行时间，建议有
	- 执行时长，非必需
	- 实际完成时间，建议有
	- 截止时间，建议有
- Checklist
- 附件
- 成员
- 评论 笔记 = 自己的评论
- 活动 Activity

#### 时间

在日历中显示时间为**执行时间**，没有的话就显示**建立时间**

一个 card 的单个时间取值（用来时间排序），优先级从上到下

- 开始执行时间
- 完成时间
- 截止时间
- 建立时间

一个 card 的生命周期，或者时间周期

已完成：建立时间 - 完成时间
否则：建立时间 - 截止时间

#### 动作

- 创建 card
- 修改 card
	- 移动 card
	- 修改内容
- 删除 card


### 过滤器

像京东那样

- 标签过滤
- 创建人过滤
- namespace 过滤
	- 完整 namespace 过滤等于找出一个项目
- 时间过滤
	- 时间范围过滤（card 时间在筛选范围就会被选出）
- 成员过滤
- 状态过滤
- 优先级过滤


### 排序

- 优先级排序
- 时间排序
- namespace 排序


### 智能化

根据截止时间，优先级，难度等属性判断当前应该做什么，做事情的顺序


### 可加入日历

可以做一个 app，然后接入系统日历

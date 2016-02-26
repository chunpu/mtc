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

但缺少一些东西，特别是定制化的需求

比如 trello 的 cards 支持如下特性，和 calendar event 对比

- 成员 (event 也可以邀请)
- 标签 (event 支持分组和颜色)
- 评论
- CheckList (提醒事项才支持)
- 截止日期
- 附件 （event 支持图片，地点等）
- 移动 （event 移动等于改时间）

mtc 的设计
---

### 解决的问题

card 的关联性，一个项目通常需要多个 card，有先后顺序，全部完成才算完成

模板，大部分工程都统一模板，填写参数就可以生成一个模板，模板等于一篮子 cards

trello 的 card 有 checkList，根据 checkList 也可以有一个进度展示

但缺点是 CheckList 过于简单，没有单独的时间，顺序依赖等关系，因此 trello 也提供了 CheckList 转 card 的功能

#### 模板事例

一个开发过程

建立如下 card

- 需求
- 具体 design
- 开发
- 代码 review
- 提测
- 上线
- 上线回测与数据分析


### 本质

mtc 本质是一大堆 card，但提供很多视图，和过滤器

#### 视图

- cards 列表
- 日历视图，可生成时间报表，比如周报
- namespace 视图，及项目视图
- 个人视图，按成员分类

进度视图属于 namespace 视图，进度 = 已完成 / 全部

### card

结合 calendar 的 event 和 trello 的 card

card 拥有 namespace，用来内容过滤与分组

#### card 维度与属性

- 内容
- namespace
- 标签
- 创建人
- 修改人
- 优先级
- 难度
- 所需执行时间
- Checklist
- 附件
- 成员
- 笔记
- 评论

### 动作 activity

- 创建 card
- 修改 card

### 过滤器

- 创建人过滤
- 时间过滤
	- 时间范围过滤


### 时间

- 建立时间
- 修改时间
- 预期开始执行时间
- 预期结束执行时间 或者 需要执行时长
- 实际完成时间
- 截止时间

在日历中显示时间为**执行时间**，没有的话就显示**建立时间**

一个 card 的单个时间取值（用来时间排序），优先级从上到下

- 开始执行时间
- 完成时间
- 截止时间
- 建立时间

一个 card 的生命周期，或者时间周期

已完成：建立时间 - 完成时间
否则：建立时间 - 截止时间


### 智能化

根据截止时间，优先级，难度等属性判断当前应该做什么，做事情的顺序


### 可加入日历

可以做一个 app，然后接入系统日历

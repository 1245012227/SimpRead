> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [sspai.com](https://sspai.com/post/69394)

> 日常浏览少数派时，遇到好的文章或者种草推荐，我都会把相关的链接发送到 Notion。

日常浏览少数派时，遇到好的文章或者种草推荐，我都会把相关的链接发送到 Notion。Notion 的文章和视频记录库中就存放着大量文章，每天晚上打开 Notion，一一阅读摘抄消化，形成完整的阅读闭环。突然，钉钉弹窗显示有新的 Tapd task 需要处理，点击查看 task 的大致内容，如果是需要敏捷开发流程的 task 直接丢进 Notion 的 Tapd 数据库，如果是其他简单的 task 则发送到滴答清单做 Check。对于滴答清单，更重要的是记录日常琐事，比如取快递、朋友生日、打电话等。

这里提到了日常工作生活中会遇到的三大场景：

*   工作
*   提升（我更情愿说是输入，有输入才有输出）
*   日常的生活杂事

我用 Notion + 滴答清单把工作生活安排的妥妥当当，轻松搞定。

![](https://cdn.sspai.com/2021/10/18/aa1fde0a2c2a5ab0692f6f82c9328910.png)![](https://cdn.sspai.com/2021/10/18/697507a46e2dfb7e45682d0e5547d002.png)![](https://cdn.sspai.com/2021/10/18/fa525de8ba0bddd872c65ae13bd3cf7e.png)

### 滴答清单

滴答清单简洁易用效率高，全平台支持。可以通过微信创建任务，开启智能识别日期来设置提醒，使用番茄计时保持专注，从记录到完成，滴答清单 10 + 个平台的 30 + 功能，只为确保每一个环节都简单快捷。这是官方说的，我使用滴答清单本质工作：清单。

使用场景

*   日常琐事
*   人际交往
*   工作中遇到的临时处理或者不需要经过敏捷开发流程的任务

### Notion

Notion 是一款提供笔记、任务、数据库、看板、维基、日历和提醒等组件的应用程序。你可以将这些组件连接起来，来创建自己的系统，用于知识管理、笔记记录、数据管理、项目管理等，另外官方和社区也提供了很多不错的模板可直接 Duplicate。我用 Notion 替代了印象笔记（虽然我是印象笔记专业版的老用户，奈何印象笔记太不思进取了），目前 Notion 的主要使用场景如下：

*   待读
*   追剧
*   输入计划（书单、新技能、博客文章等）
*   工作中需要敏捷开发流程的 task、工作日志
*   每日一记
*   其他资料

（这两款 App 均有全平台支持，滴答清单免费版有数量和功能限制，每月 16 月可获得全功能，当然按年付费更优惠些；Notion 免费版有块限制，绑定教育邮箱可免费获得全功能）

### 我的工作生活流

结合自身需求和使用场景，整合了滴答清单和 Notion，构建了我的工作生活流。这里秉承的原则是，Notion 承担工作项目、自身输入和目标管理，而滴答清单是生活琐事和那些能较快处理的工作任务。

![](https://cdn.sspai.com/2021/10/18/d7aa4b72a54b750a2563cbeb5133e6a5.png)

1.  日常的生活杂事分发给滴答清单
2.  工作中遇到的临时处理或者不需要经过敏捷开发流程的任务分发给滴答清单
3.  工作中需要敏捷开发流程的任务，主要来自 Tapd，分发给 Notion
4.  输入指网上冲浪的待读、待看或者是个人提升计划，像学习摄影、阅读书单等分发给 Notion
5.  Notion 新增或更新 item 触发 AutoMate 同步条件
6.  AutoMate 执行同步操作将 Notion 的 item 同步到 Google Calendar
7.  Google Calendar 将新建的日程通过 Email 发送到我的邮箱（可供检查同步是否成功）
8.  滴答清单订阅 Google Calendar

以上是主要实现的流程，能满足基本的三大场景。在苹果手机主屏幕上直接添加滴答清单的小组件，可以清晰的一览今天的任务。

另外如果你觉得滴答清单的小组件不美观，也可以使用 ios 日历应用订阅滴答清单和 Google Calendar。但需要注意的是移动端的滴答清单默认是订阅了 ios 日历的。于是会出现这样的情况（滴答清单本身任务是 A，Google Calendar 是 G）：

滴答清单 = A+ ios 日历 + G

iso 日历 = A+G

简单的数学运算后：滴答清单 = 2A + 2G，显示就会存在重复。这时候在滴答清单的 iso 日历中隐藏 A 和 G，那么滴答清单 = A+ G，显示就正常了。

或许你会有疑问，ios 日志取消订阅 Google Calendar，只订阅滴答清单，问题不就迎刃而解了吗？而现实是 NO NO NO....，因为 ios 订阅滴答清单只会显示 A，而订阅的 G 是不会显示的。ios 日历小组件长这样，绿色是 A，其他是 G。

![](https://cdn.sspai.com/2021/10/18/0a472d598aad91c042aee12eb9b7f2c1.jpg)

### Notion 同步到滴答清单

前面提到了 AutoMate，来看看我的工作生活流中的 5、6、7 是怎么产生的。

**背景**

对于工作中确认需要敏捷开发流程的 task 或者大型项目，我希望能在滴答清单中看到它的 Deadline，打开滴答清单或者手机小组件上可查看整体的工作安排，这一点 Notion 是做不到的。通常可以把任务分两次分发给滴答清单和 Notion，但这里有一个痛点：如果 Notion 内 task 的 Deadline 发生变更，需要及时手动去修改滴答清单对应的 task，由于相同的 task 分布在两个 APP 内，手动同步操作本身就很容易被各种事情打断遗忘。那么问题来了，有什么解办法能实现自动同步呢？于是开始寻求解决方案。

以往使用过 IFTTT，它旨在帮助人们利用各网站的开放 API，将 Facebook、Twitter 等各个网站或应用衔接，完成任务，使 “每个人都可以成为整个互联网不用编程的程序员”。另外还有 Zaiper 和 Automate 也是提供类似的服务。

简单对比下 Zaiper、Automate 和 IFTTT。网页设计美观与否就一千个哈姆雷特了。但从功能角度上来说 ，IFTTT 和 Zaiper 对于 Notion 只提供新增 item 的 API，显然不满足我的需求。而 Automate 功能上强大些，提供了新增 item 和更新属性的操作。同步时效上，在免费账户下，IFTTT 最快，Automate 5 分钟，Zapier 15 分钟，最后我选择了 AutoMate。

![](https://cdn.sspai.com/2021/10/18/17c5e9ea9bbbd714cf0c279815016cb5.png)

**问题**

由于 Automate 是国外服务，想直接从 Notion 同步到滴答清单，似乎不太可能。只能同步到 TickTick（滴答清单海外版），但 TickTick 和滴答清单账号数据是不相通的。如果你直接使用 TickTick 会更方便，对于订阅了滴答清单高级版的我，当然要物尽其用，况且滴答清单可以通过微信创建任务，易用性上更好。既然不能直接硬钢，那就曲线救国。

**解决办法**

将 Google Calendar 当做中间件，从 Notion 同步到 Google Calendar，滴答清单再订阅 Google Calendar，就实现了 Notion 到滴答清单。有了思路，说干就干。

首先我在 Google Calendar 建立了 2 个日历：inbox 和 work。字面上就能理解 inbox 承担的是事件收集功能，而 work 就是有明确 Deadline 的事件集，inbox 和 work 事件上不存在交集的。根据需求我在 Automate 中创建了 3 个自动化任务。

![](https://cdn.sspai.com/2021/10/18/607a9465dcfd94d25e2ca0fc2060f614.png)![](https://cdn.sspai.com/2021/10/18/61d662bb42cbde7098b26dea5e5f81ae.png)

**ANotionAInbox**

Notion 新增的 item 会直接新增进 inbox，通常这些事件还没有明确的 Deadline，Google Calendar 新建日历事件的 startTime 和 endTime 设置为 item 的创建时间（CreatedTime），Location 设置为 item 的 id（是为了之后 item 属性更新能搜索到 inbox 新增事件）

**UNotionDInboxAwork**

一旦确定好 Deadline 时间，Notion 的 Deadline 属性变更，根据 item id 在 inbox 搜索事件，获取事件 id，再删除 inbox 事件，最后在 work 中新增事件。事件的 startTime 和 endTime 设置为 item 的 Deadline，Location 设置为 item 的 id。

**UNotionDWorkAWork**

Notion 的任何属性变更会触发搜索，这次是在 work 中进行搜索，获取事件 id，更新事件。

Notion 属性变更会同时触发 **UNotionDInboxAwork** 和 **UNotionDWorkAWork。**

![](https://cdn.sspai.com/2021/10/18/797dbc386b40550d90d7c25cad2f4264.png)

图中

*   否（1）：不是第一次属性变更，UNotionDInboxAWork 执行失败，因为在第一次属性变更时 inbox 中对应的事件已删除；
*   否（2）：是第一次属性变更，如果不是 Deadline 属性，UNotionDInboxAWork 执行失败，因为 work 中新增事件的 startTime 和 endTime 设置的是 Deadline，而 Notion 新增 item 时 Deadline 是空的
*   是（1）：UNotionDWorkAWork 在第一次属性变更时执行失败，work 中还没有创建该事件

另外如果不是第一次属性变更，任何属性的变化，UNotionDWorkAWork 都执行成功，如果是 Deadline 属性，会更新事件的 startTime 和 endTime，其他属性不变。

3 个同步任务执行成功后，都会发 Email 到指定账号

![](https://cdn.sspai.com/2021/10/18/62566824f42e326032300b898df3fa67.png)

Automate 的注意事项：

*   只能設定最多 5 個自動化流程（上方說明就代表 2 個流程）
*   1 個月最多只能同步 300 次（只要一個流程有触发成功，就算 1 次同步）
*   触发同步的時間為 5 分鐘 1 次

以上就是我的工作生活流，有很多地方存在 bug，但基本满足我的需求，目前使用起来还是比较顺畅的，如果更好的想法欢迎大家分享。

相关阅读：

[如何用「滴答清单」和「Notion」进行时间和目标管理](https://zhuanlan.zhihu.com/p/131595710)

[如何自动同步 Notion 和 Google Calendar 的任务？使用 Automate.io 建立自动化流程](https://medium.com/pm%E7%9A%84%E7%94%9F%E7%94%A2%E5%8A%9B%E5%B7%A5%E5%85%B7%E7%AE%B1/%E5%A6%82%E4%BD%95%E8%87%AA%E5%8B%95%E5%90%8C%E6%AD%A5-notion-%E5%92%8C-google-calendar-%E7%9A%84%E4%BB%BB%E5%8B%99-8d9ae356e952)
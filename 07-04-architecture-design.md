### MVC模式

MVC 模式代表 Model-View-Controller（模型-视图-控制器） 模式。这种模式用于应用程序的分层开发。

- **Model（模型）** - 模型代表一个存取数据的对象。它也可以带有逻辑，在数据变化时更新控制器。
- **View（视图）** - 视图代表模型包含的数据的可视化。在该项目中相当于小程序
- **Controller（控制器）** - 控制器作用于模型和视图上。它控制数据流向模型对象，并在数据变化时更新视图。它使视图与模型分离开 

### 架构问题

用户提交任务后，发布者与任务接受者之间转账如何保证数据库事务的一致性

### 解决方案

* 使用数据库事务的最高隔离级别(**SERIERLIZED**)进行串行化处理
* 使用数据库的锁机制锁住需要修改的某一行，可以使用乐观锁或者悲观锁

### 逻辑视图

![](https://github.com/sysu-team1/Dashboard/blob/master/images/07-04-architecture-design.PNG?raw=true)

### 物理视图

![](https://github.com/sysu-team1/Dashboard/blob/master/images/07-04-architecture-design1.PNG?raw=true)


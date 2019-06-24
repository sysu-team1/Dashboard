# 第五次小组讨论会议记录


### 时间：2019年6月10号

### 地点：至善园学生活动中心

### 参会人员：曾晖 马佳 廖志勇 梁毓颖 朱多煜 廖三锋

### 会议目标：api完善已经进行文档任务的分配

### 会议内容：

##### 获取任务
* url: /tasks/search/
* method: GET
* request:


| 参数名   | 必选   | 类型   | 说明   |
|:----|:----|:----|:----|
| publisher_id   | 否   | int   | 发布者id   |
| accepter_id   | 否   | int   | 接收者id   |
| tag   | 否   | string   | 任务标签   |
| text   | 否   | string   | 根据任务title或content查询   |
| task_id   | 否   | int   | 任务id   |
| last_id   | 否   | int   | 当前显示的任务列表最老的那个task id，用来获取下滑获取更多task，若一个任务都还没有，则传入-1   |
| status   | 否   | string   | 任务状态，与accepter_id搭配使用。(1) all: 所有的任务  (2) ongoing: 进行中，未完成，未过期(3) finished: 已完成(4) complete: 未完成，已过期（只与接受的任务搭配） |
| last_accept_time   | 否   | string   | 格式："2019-06-05 22:02:24"  当前显示的接受任务列表中最晚的接受时间，若一个任务都还没有，则传入空字符串，与accepter_id搭配使用。作用类似last_id   |


>* 参数说明：
>  * publisher_id，accepter_id，tag，text，task_id 最多只能选一个
>  * 选择 publisher_id，tag，text 作为参数时，或者没有参数时，必须加 last_id 作为参数
>  
```
http://localhost:5000/tasks/search/?tag=取快递&last_id=-1
http://localhost:5000/tasks/search/?last_id=-1
```
>
>  * 选择 publisher_id 或 accepter_id 作为参数时，必须加 status 作为参数
>  
```
http://localhost:5000/tasks/search/?publisher_id=1000003&status=all&last_id=-1
```
>
>  * 选择 accepter_id 作为参数时，必须加 last_accept_time 作为参数
>  
```
http://localhost:5000/tasks/search/?accepter_id=1000002&status=all&last_accept_time=2019-06-11 23:01:53
http://localhost:5000/tasks/search/?accepter_id=1000002&status=ongoing&last_accept_time=
```
>
>  * 选择 task_id 作为参数时，无需加其他参数
> 
```
http://localhost:5000/tasks/search/?task_id=1
```
>

* response:

```
{
  "error": 0,
  "data": {
    "msg": "获取成功"/"2019-06-11 23:01:53"(last_accept_time),
    "tasks":[
      {
        "id": 1,
        "publish_id": 1000003,
        "publish_time": "2019-06-05 22:02:24",
        "limit_time": "2019-06-05 22:01:49",
        "limit_num": 1,
        "accept_num": 0,
        "title": "222",
        "content": "222",        
        "tag": "取快递",
        "image_path": "http://localhost:5000/_uploads/photos/ZlBKRp-1.png",
        "reward": 22, 
        "publisher": {"openid": 1000003, "email": "email3@qq.com", "password": "pass3", "student_id": "16340003", "name": "16340003", "sex": "男", "collage": "药学院", "grade": 2014, "edu_bg": "本科", "tag": "", "signature": "word12 word13 word14 word15 word16 word17 word18 word19 word20 word21 word22", "cash": 2299}
      },
      {
        
      },
      ...
    ]
  }
}
```

##### 更新用户信息
* url: /user/update/
* method: POST
* request:
	* body:

| 参数名 | 必选 | 类型 | 说明 |
|:----|:----|:----|:----|
| openid   | 是   | int   | 学生或组织id   |
| <attr_name>   | 是   | -   | 属性名作为参数名   |
| <attr_name>   | 否   | -   | 属性名作为参数名   |
| ...   | 否   | -   | 属性名作为参数名   |
| old_password   | 否   | string   | 当修改密码时，需要传入旧密码   |

> 参数说明：
> 
>  * attr_name可以为以下任意一个以上，个数不限
> 
```
{"password": "pass3", "student_id": "16340003", "name": "16340003", "sex": "男", "collage": "药学院", "grade": 2014, "edu_bg": "本科", "signature": "word12 word13 word14 word15 word16 word17 word18 word19 word20 word21 word22"}
```
>
>  * 若要修改password，则要加一个old_password属性

* response:

```
{"error": 0, "data": {"msg": "更改成功"}}
{"error": 1, "data": {"msg": "不存在该学生或组织"}}
{"error": 1, "data": {"msg": '请输入旧密码'}}
{'error': 1, "data": {'msg': '旧密码错误'}}
{'error': 1, "data": {'msg': '邮箱不可修改'}}
```

##### **文档分工**
**1、[About](01-about)（项目概况）（曾晖）**

**2、[Team profile](02-team-profile)（团队组建与分工）**

**3、[Investigation](03-investigation)（项目前期调研/竞品分析）（马佳）**

**4、[Vision](04-vision)（项目愿景）（多鱼）**

**5、[Product Backlog](05-product-backlog)（产品特性库）（多鱼）**

**6、[Requirement specification](06-requirements)（需求规格说明书）**

     - 6.1 [Usercase Diagram and UML Activity Diagram](06-01-usecase-diagram-and-uml-activity-diagram)（马佳、曾晖）

     - 6.2 [Use Cases](06-02-use-cases)（用例+活动图）（马佳、曾晖）

     - 6.3 [Domain Models](06-03-domain-model)（领域模型）（毓颖）
 
     - 6.4 [State Models](06-04-state-model)（状态模型）（志勇）
 
     - 6.5 [System Sequence Diagrams](06-05-system-sequence-diagram)（功能模型）（多鱼 ）
 
     - 6.6 [Supplementary Requirements](06-06-supplementary-requirements)（补充需求）（曾晖）

**7、[Design](07-designs)（设计说明书）**

     - 7.1 UI design（界面设计）

          - [XX 用例 UI 设计](07-01-01-XX-ui-design)（多鱼）

     - 7.2 Database design（数据库设计）

        - 7.2.1 [用户及权限系统数据库设计](07-02-01-database-design)（毓颖）

          - 7.2.2 [数据库ER模型图](07-02-02-database-er-model)（毓颖）

     - 7.3 [Interface API design](07-03-API)（接口 API 设计）

     - 7.4 [Architecture design](07-04-architecture-design)（架构设计）（三锋）

     - 7.5 [Usecase design](07-05-usecase-design)（用例设计）（ 马佳 ）

**8、生产规范与指南**

    - 8.1 [代码规范](08-01-code-qualification)（曾晖）

     - 8.2 [REST API设计规范](08-02-RESTful-api-design-standard)（三锋）

     - 8.3 [架构设计、详细设计（BCE方法）到应用程序框架映射指南]
 (08-03-framework-design-BCE-and-app-archit)（志勇）
 
     - 8.4 [部署说明](08-04-deployment-doc)
*
*9、[成品展示](09-demo-video)（曾晖）**

     - 9.1 XX短视频（马佳 ）

**X1 meet_recording（已完成）**

      - [Inception meeting (2019/04/02)]

     - [Iteration 1 meeting (2019/04/11)]

     - [Iteration 2 meeting (2019/04/22)]

     - [Iteration 3 meeting (2019/05/20)]

     - [Iteration 4 meeting (2019/06/10)]

**X2 [KANBAN]**

**X3 [auditing-records](x3-auditing)**

**X4 [Tech/Work Report](x4-techniques)**

**X5 [Final Report](x5-summary)（曾晖）**



| 成员   | 文档   |
|:----|:----|:----:|
| 廖志勇   | 06-04-state-model <br> 07-03-API <br> 08-03-framework-design-BCE-and-app-archit   |
| 廖三锋   | 07-04-architecture-design <br> 08-02-RESTful-api-design-standard   |
| 梁毓颖   | 06-03-domain-model <br> 07-02-01-database-design   |
| 马佳   | 03-investigation <br> 06-01-usecase-diagram-and-uml-activity-diagram <br> 06-02-use-cases <br> 07-03-API  07-05  08-04-deployment-doc   |
| 曾晖   | 01-about <br> 06-01-usecase-diagram-and-uml-activity-diagram <br> 06-02-use-cases <br> 06-06-supplementary-requirements <br> 09-demo-video（视频录制）<br>  x5-summary（小组总结）   |
| 多鱼   | 04-vision <br> 05-product-backlog <br> 06-05-system-sequence-diagram <br> 07-01-01-XX-ui-design   |


文档编写可参考：[https://rookies-sysu.github.io/Dashboard/](https://rookies-sysu.github.io/Dashboard/)



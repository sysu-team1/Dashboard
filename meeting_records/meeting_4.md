# 第四次小组讨论会议记录


### 时间：2019年5月31号

### 地点：至善园学生活动中心

### 参会人员：曾晖 马佳 廖志勇 梁毓颖 朱多煜 廖三锋

### 会议目标：根据前端的需求进一步补充和完善api

### 会议内容：

##### 登录

  * url: /user/login/
  * method: POST
  * request:

```
String email
String password
```

  * response:
 
```
{
  "error": 0,
  "data": {
    "openid": 
  }
}
```

![图片](https://uploader.shimo.im/f/wDOuTQcOVpodAVut.png!thumbnail)

##### 注册
  * url: /user/register/
  * method: POST
  * request:

```
String email
String password
String validate_code
String name
String student_id
String grade
String collage
String sex
```

  * response:

```
{
  "error": 0,
  "data": {
    "msg": "注册成功",
    "id": 123,
  }
}
```

![图片](https://uploader.shimo.im/f/aXdmN3cGOwYcuRPZ.png!thumbnail)

##### 验证码

  * url: /user/get_verification_code/
  * method: POST
  * request:
  
```
String email
```

  * response:

```
{
  "error": 0/1,
  "data": {
    "msg": "验证码已发送"/"原验证码未过期",
  }
}
```

![图片](https://uploader.shimo.im/f/KyipO4R9FG4h1R20.png!thumbnail)

##### 创建任务

  * url: /tasks/create/
  * method: POST
  * request:
    * body:

```
publish_id, 发布人id ，也就是open_id
limit_time, ddl
limit_num, 限制人数数量
title, task标题
content, 内容（如果tag为'问卷'，则内容为问卷的内容）
tag, 标签
reward
```

  * response:

```
"error": 0/1,
"data": {
  "msg": "余额不足/创建成功/没有图片上传/创建成功/图片上传失败",
}
```

##### 搜索任务

  * url: /tasks/search/?
  * method: GET
  * request:
    * 参数：

```
（publisher_id = 
或 accepter_id = 
或 tag = 
或 text = 
或 task_id = ）# 以上参数最多选一个，分别按照发布者id、接受者id、tag、text（标题或内容）、任务id进行查询
last_id = ? # last_id是当前显示的任务列表最老的那个task id，用来获取下滑获取更多task，若一个任务都还没有，则传入-1。（用task_id查询时不用传入last_id）

```

如：
/tasks/search/?accepter_id=10001&last_id=-1
/tasks/search/?task_id=10002

  * response:

```
{
  "error": 0,
  "data": {
    "msg": "获取成功",
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
        "publisher": ""
      },
      {
        
      },
      ...
    ]
  }
}
```

# 接受任务

  * url: /tasks/accept/
  * method: POST
  * request:
    * body:

```
int accepter_id
int task_id
```

  * response

```
{'error': 0/1,
'data': {
  'msg': 'Accept successfully.'/'No such task.'/'No such student.'/'Has been accepted.'
  }
}
```

-----------------------------
>* 没有以下API

##### 发问卷

  * url: /user/questpaper
  * method: POST
  * request:

```
String id
String quest_name
String questions //#分割
String deadline_date
String people_type//面向的对象
String paticipate_number//参与人数限制
```

  * response

```
{
  "error": 0,
  "data": {
    msg: "发布成功",
    id:  //问卷id
  }
}

```

##### 填问卷功能

  * url: /user/fillpaper
  * method: POST
  * request:

```
String id
String quest_name
String deadline_date
String people_type//面向的对象
String paticipate_number//参与人数限制
```

  * response

```

```

##### 请求任务列表
>* 说明：请求任务是请求平台中的所有可以接受的任务，用于用户筛选

  * url: ？
  * method: POST
  * request:
  
```
String id // 用户openid
```

  * response

##### 请求我的任务列表
>* 说明：请求我的任务是请求该用户id的所有任务任务，包括已完成和未完成

  * url: ？
  * method: POST
  * request:
 
```
String id // 用户openid
```

  * response

```
Strign title   // 任务标题 
number reward // 奖励
String desc  // 描述
String tags[3] // 前端设置最多三个tag，可以少于等于3，至少1
bool completed // 任务完成状态，
number participate_number // 参与人数限制
number respondent_number // 已参与人数
time publish_time
```


```
CREATE TABLE `students` (
  `openid` int(11) NOT NULL AUTO_INCREMENT COMMENT '用户的唯一标识符',
  `email` varchar(20) NOT NULL COMMENT '学校邮箱',
  `password` varchar(20) NOT NULL COMMENT '密码',
  `student_id` varchar(10) NOT NULL DEFAULT '' COMMENT '学号',
  `sex` enum('未知','男','女') DEFAULT 'unknown' COMMENT '用户性别',
  `collage` varchar(20) DEFAULT '' COMMENT '学院',
  `grade` int(11) NOT NULL DEFAULT '2016' COMMENT '入学年级',
  `edu_bg` enum('本科','硕士','博士') DEFAULT 'undergraduate' COMMENT '学历',
  `tag` varchar(100) DEFAULT '' COMMENT '与任务相关的标签',
  `signature` varchar(300) DEFAULT '' COMMENT '用户签名',
  PRIMARY KEY (`openid`),
  FULLTEXT KEY `stu_tag` (`tag`)
)

CREATE TABLE `organizations` (
  `openid` int(11) NOT NULL AUTO_INCREMENT COMMENT '组织的唯一标识符',
  `email` varchar(20) NOT NULL COMMENT '学校邮箱',
  `password` varchar(20) NOT NULL COMMENT '密码',
  `description` varchar(300) DEFAULT '' COMMENT '组织描述',
  PRIMARY KEY (`openid`)
)

CREATE TABLE `tasks` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '任务id',
  `publish_id` int(11) NOT NULL COMMENT '发布者id',
  `publish_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '发布时间',
  `limit_time` timestamp NULL DEFAULT '2000-01-01 00:00:00' COMMENT '限时',
  `limit_num` int(11) DEFAULT '-1' COMMENT '任务可接受人数',
  `accept_num` int(11) DEFAULT '0' COMMENT '任务已接受人数',
  `title` varchar(50) NOT NULL COMMENT '发布任务标题',
  `content` varchar(300) NOT NULL COMMENT '发布任务内容',
  `tag` varchar(30) DEFAULT NULL COMMENT '任务tag',
  PRIMARY KEY (`id`),
  KEY `publish` (`publish_id`,`id`),
  FULLTEXT KEY `task_tag` (`tag`),
  FULLTEXT KEY `task_text` (`title`,`content`)
)

CREATE TABLE `accepts` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '接受id',
  `tag` varchar(30) DEFAULT NULL COMMENT '任务tag',
  `accept_id` int(11) NOT NULL COMMENT '接受者id',
  `task_id` int(11) NOT NULL COMMENT '任务id',
  `accept_time` timestamp NULL DEFAULT CURRENT_TIMESTAMP COMMENT '接受时间',
  `finish_time` timestamp NULL DEFAULT '2000-01-01 00:00:00' COMMENT '完成时间',
  PRIMARY KEY (`id`),
  KEY `task` (`task_id`,`finish_time`),
  KEY `accept` (`accept_id`,`finish_time`),
  CONSTRAINT `accepts_ibfk_1` FOREIGN KEY (`accept_id`) REFERENCES `students` (`openid`) ON DELETE CASCADE,
  CONSTRAINT `accepts_ibfk_2` FOREIGN KEY (`task_id`) REFERENCES `tasks` (`id`) ON DELETE CASCADE
)

CREATE TABLE `problems` (
  `id` int(11) NOT NULL AUTO_INCREMENT COMMENT '问题id',
  `task_id` int(11) NOT NULL COMMENT '关联的任务的id',
  `description` varchar(100) DEFAULT '' COMMENT '问题描述',
  `all_answers` varchar(100) DEFAULT '' COMMENT '问题答案',
  PRIMARY KEY (`id`),
  KEY `task_id` (`task_id`),
  CONSTRAINT `problems_ibfk_1` FOREIGN KEY (`task_id`) REFERENCES `tasks` (`id`) ON DELETE CASCADE
)

CREATE TABLE `answers` (
  `accept_id` int(11) NOT NULL COMMENT '接受id',
  `problem_id` int(11) NOT NULL COMMENT '问题id',
  `answer` int(11) NOT NULL DEFAULT '-1' COMMENT '具体答案的选项',
  PRIMARY KEY (`accept_id`,`problem_id`),
  KEY `problem_index` (`problem_id`),
  CONSTRAINT `answers_ibfk_1` FOREIGN KEY (`accept_id`) REFERENCES `accepts` (`id`) ON DELETE CASCADE,
  CONSTRAINT `answers_ibfk_2` FOREIGN KEY (`problem_id`) REFERENCES `problems` (`id`) ON DELETE CASCADE
)
```


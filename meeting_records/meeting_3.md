# 注册功能
  * url: /user/register
  * method: POST
  * request:
```
String email
String password
String validate_code
String name
String student_id
String grade
String major
String sex
```
  * response:
```
{
  "error": 0,
  "data": {
    msg: "注册成功",
    id:
  }
}
```
# 登录功能
  * url: /user/login
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
    msg: "登录成功",
    id:
  }
```
# }

发问卷功能
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
```
}


# 填问卷功能
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

# 后台文件目录
```
tools/
    utils.py  # 邮件
    db.py  
responses/
    login_or_register.py  # 注册登录
    create_task.py  # 创建任务、问卷
    get_accept_task.py  # 获取自己接受的任务  
    search_task.py  # 搜索任务
    get_all_task.py  # 获取所有的任务
    get_publish_task.py  # 获取自己发布的任务
    my.py  # 我自己的 -- 设置、(历史浏览、我的关注)。。
config.py  # 大写
app.py
```

| 后台成员   | 任务   | 
|:----|:----|
| 梁毓颖   | 数据库、(历史浏览、我的关注、)获取、修改用户信息、获取自己接受的任务   | 
| 廖志勇   | 登录、注册（保存验证码）、获取任务（搜索）、接受任务   | 
| 马佳   | 邮件验证、创建任务、问卷、获取自己发布的任务   | 






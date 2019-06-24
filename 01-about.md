---
layout: default
title: 关于项目
---

# 关于项目
{:.no_toc}

* 目录
{:toc}

| 版本 |   日期    | 描述 |  作者   |
| :--: | :-------: | :--: | :-----: |
| v1.1 | 2019-6-22 | 草案 | zengh |

## 1、项目简介

挣闲钱是面向大学生的，通过做任务挣钱的云平台，它属于以运营为中心的服务软件，也可以理解为面向大学生的专业“众包”系统。用户只需在本平台即可获得权威的兼职服务,主要特点包括：

* 客户通过平台验证身份的真实有效，保证任务与完成任务的真实性
* 每个用户既可以接收任务也可以发布相应的任务
* 每个用户可以指定给特定的群体完成
* 多用户同时在线抢任务
* 引入信用积分，评估是否具有接受任务的能力
* 提供申诉
* . . . . 
## 项目结构

1. [ClientUI](https://github.com/sysu-team1/clientUI)
2. [BackEnd](https://github.com/sysu-team1/BackEnd)

## 2、重要分析设计文档


* [需求规格说明书](06-requirements)
* [软件设计说明书](07-designs)
* [产品演示视频](09-demo-video)


## Demo

![查看正在进行、已完成、过期以及自己发布的任务](https://github.com/sysu-team1/Dashboard/blob/gh-pages/images/%E6%9F%A5%E7%9C%8B%E4%BB%BB%E5%8A%A1.gif?raw=true)

其余Demo可到[demo-videoes](09-demo-video)中查看更多

## 3、敏捷开发迭代管理与大事纪

* Inceptions (week2)
    - goal: 就产品“产品范围、愿景和核心业务”达成一致
    - 前期工作：
        - 产品调查：调查优帮、万圈、华农校园互助、互助校园等现有的微信小程序或APP
        - 团队组织: 确认分工， [团队组建与分工](02-team-profile)
    - 项目启动会议：所有人
    - 项目愿景等文档： 626zdysdq [项目愿景](04-vision)

* Iteration 1 (3 weeks from 2019 Apr 12  to 2019 May 5)
    - goals:
        - 明确基本的项目框架、需求
        - 明确产品的定位
        - Backlog
        - 学习不同微信小程序开发框架，确认开发框架
        - 规范小程序开发以及后端开发的代码规范
        - 登录注册基本demo的构建
    - milestones
        - metting 2，确定小程序的使用框架 (2019/4/12)
* Iteration 2 (4 weeks from 2019 May 5 to 2019 Jun 2)
    - goals:
    前端：
        - UI设计 
        - 根据需求构建登录注册系统
        - 构建学生信息管理系统
        - 构建任务管理系统
        - 构建搜索系统
        - 用例图设计以及领域模型设计
    后端：
        - 后台服务器API的部署和完成
        - 任务的搜索API的完成
        - 任务的发布API的完成
        - 任务的接收API
        - 图片上传与获取
        - 个人信息的API
    - milestones
        - 小程序基本系统的完成，登录注册与后台连接成功(2019/5/30)
        
* Iteration 3 (2 weeks from 2019 Jun 2 to 2019 Jun 22)
    - goals:
        - UI再设计
        - 系统与后台交互的再构建与修改
        - 学生信息认证的构建
        - 其他文档的完成
    - milestones
        - 其他文档的完成，(2019/6/22)

* Iteration 4 (1 week from 2019 Jun 22 to 2019 Jun 29)
    - goals: 
        - 小程序系统的再测试
        - 后台API的再测试
        - 测试文档的再完善
    - milestones
        - ...


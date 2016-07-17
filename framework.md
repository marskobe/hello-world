# **AcFun** 开发手册

---- 
- 简介
	- 架构原理
	- 架构功能
	- 优劣势
- 开发规范
  - api的返回值
  - 批量查询
  - 批量添加,修改,删除
- 业务功能
	- 用户服务
	- 封禁服务
	- 地区服务
	- 日志服务
	- 通知服务
	- 邮件服务
	- 短信服务
	- 验证码服务
	- 上传服务
	- CMS管理界面
	- 虚拟货币服务(计划中，未完成)
	- 审核服务(计划中，未完成)
	- 第三方登录(计划中，未完成)
	- 意见反馈(计划中，未完成)







## 简介
### 架构设计
#### 1. 架构原理
![](https://raw.githubusercontent.com/Dreampie/cloud-config-repo/master/DeploymentDiagram.png)

架构主要组成包括：
##### Spring Cloud Config Server(config-server):
  
   基于git的统一配置文件管理同步中心，配置内容会以Java属性或者YAML文件的形式体现。该Config Server会将这些文件合并为环境对象，其中包含易于理解的Spring属性模型以及作为REST API存在的配置文件。任何应用程序都能够直接调用该REST API当中所包含的配置数据，但我们也可以将智能客户端绑定方案添加到Spring Boot应用程序当中，并由后者自动将接收自Config Server的配置信息分配至任意本地配置当中。

##### Spring Cloud Bus(config-server):
  
   基于Amqp的配置分发服务，能够在保障一致性的前提下将配置内容分发到多个应用程序实例当中。然而根据其设计思路的限定，我们目前只能在应用程序启动时对其配置进行更新。在向Git中的某一属性发送新值时，我们需要以手动方式重启每个应用程序进程，从而保证该值被切实纳入应用当中。很明显，大家需要能够在无需重启的前提下完成对应用程序配置内容的更新工作。  

##### Spring Cloud Netflix(eureka-server):
  
   针对多种Netflix组件提供打包方案，其中包括Eureka、Ribbon、Hystrix以及Zuul，目前我们未使用Zuul，降低框架复杂度。
   Eureka是一套弹性服务注册实现方案。其中服务注册属于服务发现模式的一种实现机制，提供的负载均衡机制仅支持单循环条件。
   Ribbon提供的客户端IPC库则更为精巧，其同时具备可配置负载均衡机制与故障容错能力。Ribbon能够通过获取自Eureka服务器的动态服务器列表进行内容填充。
   Hystrix能够为断路器以及密闭闸门等分布式系统提供一套通用型故障容错实现模式。断路器通常会被作为一台状态机使用，能够介于服务及其远程关联性之间。如果该电路处于闭合状态，则所有指向该关联性的调用通常将直接通过。如果某一调用失败，则故障将被计入计数。而一旦失败次数达到可配置时间区间内的阈值，该电路将被跳闸至断开。在处于断开状态时，调用将不再被发往该关联，而由此产生的结果将可自行定制(包括报告异常、返回虚假数据或者调用其它关联等等)。
该状态机会定期进入所谓“半开”状态，旨在检测关联性是否处于健康运作状态。在这种状态下，请求一般仍将继续得以通过。当请求成功通过时，该设备会重新回归闭合状态。而如果请求失败，则该设备会重新回归断开状态。除了实现状态机机制之外，Hystrix还能够提供来自各断路机制的重要遥测指标流，具体包括请求计量、响应时间直方图以及成功、失败与短路请求数量

##### Docker:
   支持在构建级生成docker镜像并上传值镜像私服，支持一键快速部署
##### Gradle:
   项目依赖管理＋定制的部署脚本
### 架构功能
   基于Header的全接口版本控制，基于HTTP的缓存，防恶意DDOS攻击的RateLimit限制访问，基于json的任意参数解析方案，基于Feign的任意客户端接入机制
### 优劣势
   相比于上一版的Dubbo＋Zookeeper，拥有更加完整的异常转移机制，同时支持任意语言的客户端接入，屏蔽了未来可能的语言差异，拥有灵活的基于git的配置文件管理同步中心，支持docker一键构建并部署，提供spring以及非spring的任意项目使用服务的客户端访问机制，唯一劣势传输速度稍低于grpc方式

## 开发规范
### api的返回值
   请求正确: 返回HttpResponse
   请求出错: 返回HttpException
### 批量查询
   将条件放入查询对象(entity)中并添加@Transient注解
### 批量添加,修改,删除
   路径添加batch,参数传递数组. 例: http://api.aixifan.com/usr/users/batch

## 业务功能
### 用户服务
   提供完全可定制的权限控制系统，能控制包括已登录用户，未登录用户，管理员等任一目标用户群体的可操作内容。
   
   测试主要包含(UI+接口)：用户管理，角色管理，权限管理，等级系统，4大部分，和完全可控的权限区分，等级优势(如：达到1级，可以上传视频等)
   
   接口地址：http://api.cloud.aixifan.com/usr/users
   
   UI地址：http://cms.cloud.aixifan.com/system/usr/users
   
   文档地址：

### 封禁服务
   提供基于用户的功能限制系统，如：某用户发布了违规内容，将予禁止在该区使用评论，弹幕功能，某用户登录失败达到一定次数，半小时内禁止登录
   
   测试包含(UI+接口)：登录封禁，手动封禁
   
   接口地址：http://api.cloud.aixifan.com/lmt/limits
   
   UI地址：http://cms.cloud.aixifan.com/system/lmt/limits
   
   文档地址：

### 地区服务
   为用户提供地区位置服务，用以用户地域统计，商城系统送货地址等
   
   测试包含(UI+接口)：用户修改地区，地区维护
   
   接口地址：http://api.cloud.aixifan.com/lmt/limits
   
   UI地址：http://cms.cloud.aixifan.com/system/lmt/limits
   
   文档地址：

### 日志服务
   为所有项目提供，可定制的操作日志记录服务
   
   测试包含(UI+接口)：日志查看，添加新的日志记录内容
   
   接口地址：http://api.cloud.aixifan.com/log/logs
   
   UI地址：http://cms.cloud.aixifan.com/system/log/logs
   
   文档地址：

### 通知服务
   提供全站用户分角色的站内通知服务
   
   测试包含(UI+接口)：发送角色通知，查看收到的通知
   
   接口地址：http://api.cloud.aixifan.com/ntc/notices
   
   UI地址：http://cms.cloud.aixifan.com/system/ntc/notices
   
   文档地址：

### 邮件服务
   提供邮件通知，邮件绑定，邮件验证等服务
   
   测试包含(接口)：发送邮件
   
   接口地址：http://api.cloud.aixifan.com/cmn/mails
   
   文档地址：

### 短信服务
   提供短信验证码，以及其它短信提醒服务
   
   测试包含(接口)：发送短信
   
   接口地址：http://api.cloud.aixifan.com/cmn/smses
   
   文档地址：

### 验证码服务
   提供可定制颜色，字体，内容，风格的验证码服务
   
   测试包含(接口)：验证码图片
   
   接口地址：http://api.cloud.aixifan.com/cmn/captchas
   
   文档地址：

### 上传服务
   提供七牛上传Token服务
   
   测试包含(接口)：返回可用于上传的Token
   
   接口地址：http://api.cloud.aixifan.com/cmn/tokens
   
   文档地址：

### CMS管理界面
   提供以上部分功能的UI操作界面
### 虚拟货币服务(计划中，未完成)
### 审核服务(计划中，未完成)
### 第三方登录(计划中，未完成)
### 意见反馈(计划中，未完成)

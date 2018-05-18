# config-server
> 配置服务，服务配置文件统一管理的配置中心。本地服务直接应用配置文件中配置，无须启动本服务。线上除manager-service, register-server, config-server外的所有服务的配置从config-sever拉取，config-server再从manager-service管理服务获取配置。服务的配置需通过choerodon-tool-config将服务配置刷入manager-service的数据库。

- 拉取配置规则。
  
  如果服务拉取配置时包含配置版本，则拉取对应的版本配置；如果不包含版本，则拉取default配置。

Choerodon的配置服务，服务配置文件统一管理的配置中心。

## Feature


## Requirements
- 本项目是一个eureka client项目，本地运行需配合register-server，线上运行需配合go-register-server。
- config-server从manager-service管理服务获取配置，需启动manager-service。
- 其他服务的配置需通过choerodon-tool-config将服务配置刷入manager-service的数据库。

## To get the code

```
git clone http://code.saas.choerodon.com.cn/hand-rdc-choerodon/config-server.git
```

## Installation and Getting Started
- 启动register-server
- 进入项目目录，执行mvn spring-boot:run或者idea中运行ConfigServerApplication运行

## Usage
- 手动打镜像

   拉取源码执行mvn clean install, 在target目录下生成app.jar，拷贝到src/main/docker目录，里面有dockerfile，执行docker build打为镜像.
- 使用已有镜像

 ```
 docker pull registry.saas.hand-china.com/hand-rdc-choerodon/config-server:0.1.0
 ```
- 打好镜像后在k8s上新建deployment运行, 并创建service。可以参考代码中的chart目录部署文件编写。

## Dependencies
- go-register-server: 注册服务
- manager-service: 管理服务
- kafka

## Reporting Issues

If you find any shortcomings or bugs, please describe them in the Issue.
    
## How to Contribute
Pull requests are welcome! Follow this link for more information on how to contribute.

## Note
- 本地服务直接应用配置文件中配置，无须启动本服务
- 线上需要和manager-service配合使用，并且服务的配置需通过choerodon-tool-config将服务配置刷入manager-service的数据库
# vue-demo
青否云 vue demo

## 官网

http://cloud.qingful.com

## 演示

https://qingful.github.io/jquery-demo/index.html
账号：13253522080
密码：mmmmmm

## 使用

1. 登录青否云
2. 创建应用
3. 数据设置。
   - 创建数据表。
     - 创建数据表user，引擎和校对默认即可。点击显示结构，添加字段phone，类型选择bigint，长度值为11，其余默认。添加字段password，类型选择text，其余默认。
     - 创建数据表todos，引擎和校对默认即可。点击显示结构，添加字段content，类型选择text，其余默认。添加字段user_id，类型选择int，其余默认。添加字段status，类型选择int，其余默认。
4. 权限设置。
   - 创建密钥，名称Authorization，密钥随便设置。
   - 创建分组，分别创建public和home分组。
   - 组权限，创建home的组权限，并选择Authorization秘钥。
   - 表权限。
     - 创建todos表权限，选择home分组，选择todos数据表，权限勾选查询、新增、更新、删除，密钥选择为空。
     - 创建user表权限，选择public分组，选择user数据表，权限勾选查询、新增，密钥选择为Authorization。
   - 字段。
     - 点击创建字段，选择public分组，user数据表，password字段，值为空，类型选择md5，传值选择是，请求链接选择为空。
     - 点击创建字段，选择home分组，todos数据表，user_id字段，值为Authorization.id。类型为空，传值选择否，请求链接选择为空。
5. 配置下`./src/config/config.js`中的appid，appkey
6. 运行`npm run dev`



## 青否云

一站式后端云服务解决方案。为H5，小程序，APP等应用，提供高效，简单，安全的后端云服务支持。



### 高效

开发效率

- 无需开发数据库增删改查，登录授权验证，短信验证码等基础功能。

人员成本

- 无需运维人员，后端仅需要设计数据库，关联，授权等功能的人员。

运维时间

- 无需搭建服务器，也无需运维，运维自动化时间节省100%。



### 简单

sdk集成

- sdk一键集成，极速部署，辅助开发文档，开发范例等快速的上手开发。

api接口

- api接口采用restful设计方案，拥有结构清晰、符合标准、易于理解、扩展方便等特性。

cdn加速

- cdn加速内置，融合主流CDN，加速传输，助力内容极速抵达用户。



### 安全

jwt授权

- JSON Web Token（JWT）是JSON风格轻量级的授权和身份认证规范，可实现无状态、分布式的Web应用授权。使用JWT在用户和服务器之间传递安全可靠的信息。

https传输

- https传输是服务器以密文的方式将对称密钥发给客户端（用公钥进行非对称加解密（TLS握手阶段）对称密钥建立受保护区），非对称加密可以很好的管理对称密钥，保证每次数据加密的对称密钥都是不相同的，通过这个对称密钥来进行后续通信的数据加解密。

sla标准

- sla可靠性不低于 99.95%，即每月服务故障时长不超过21.6分钟。并且具备完善的故障监控、自动告警、快速定位、快速恢复等一系列故障应急响应机制。
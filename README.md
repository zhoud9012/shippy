### golang GRPC 

### 参考文献 https://wuyin.io/2018/05/10/microservices-part-1-introduction-and-consignment-service/

#### 目录

```
├─shippy
│  │  README.md
│  │
│  ├─consignment-cli
│  │      cli.go
│  │      consignment.json
│  │
│  └─consignment-service
│      │  main.go
│      │
│      └─proto
│          └─consignment
│                  consignment.pb.go
│                  consignment.protols
```

#### 思路解析
1.定义protobuf 通信协议文件

2.编译protobuf 生成协议代码

3.服务端与客户端均实现协议


#### protobuf 定义service && consignment
```
(service)声明货轮服务{
    声明托运货物 rpc 方法
}
```
```
(message)声明货物{
    //货物编号
    //货物描述
    //货物重量
    //货物所属集装箱
    //承运货轮
}

(message)声明集装箱{
    //集装箱编号
    //集装箱所属客户编号
    //出发地
    //集装箱所属用户编号
}

(message)声明托运结果
{
    //托运结果是否成功
    //新托运的货物
}
```
#### 生成协议代码

1.unix

protoc -I. --go_out=plugins=grpc:$(GOPATH)/src/shippy/consignment-service/proto/consignment/consignment.proto

2.windows

protoc -I. --go_out=plugins=grpc:$env:GOPATH .\src\shippy\consignment-service\proto\consignment\consignment.proto


#### 序列化与协议文件对应关系

service：

protobuf 编译器的grpc插件 将proto序列化文件中service 中的 rpc 方法 转化成pb协议文件中的一个接口

message：

protobuf 编译器的grpc插件 将proto序列化文件中的通信数据结构message 转化成一个结构体

#### 通过go-micro 编译协议文件 不在使用grpc插件

1.linux
protoc -I. --go_out=plugins=micro:$(GOPATH)/src/shippy/consignment-service proto/consignment/consignment.proto


2.windows
protoc -I. --go_out=plugins=micro:$env:GOPATH .\src\shippy\consignment-service\proto\consignment\consignment.proto

#### vessel 服务
1.windows
protoc -I. --go_out=plugins=micro:$env:GOPATH .\src\shippy\vessel-service\proto\vessel\vessel.proto

go-mico 实现对比 gRPC

#### 服务端手动步骤
```
1.执行交叉编译
./build Linux64.bat
2.编译服务端镜像
docker build -t consignment-service.1.0.0 .
3.运行服务端容器
docker run -p 50051:50051 -e MICRO_SERVER_ADDRESS=:50051 -e MICRO_REGISTRY=mdns consignment-service.1.0.0
```

#### 客户端手动步骤
```
1.执行交叉编译
./build Linux64.bat
2.编译客户端镜像
docker build -t consignment-cli.1.0.0 .
3.运行客户端容器
docker run -e MICRO_REGISTRY=mdns  consignment-cli.1.0.0
```

### 实现服务端

0.创建main.go 文件

1.导入protoc 自动生成的包

2.生成端口常量

3.

#### 参考仓库
https://github.com/nealguo/go-micro-demo







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






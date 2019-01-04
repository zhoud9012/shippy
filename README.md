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





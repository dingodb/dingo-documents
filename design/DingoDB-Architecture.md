# 1. Architecture about DingoDB

<img width="1174" alt="image" src="https://user-images.githubusercontent.com/6895821/217449631-28ecf209-22fb-40d3-8e11-d2cb801382a2.png">

***


集群中的几个角色

- Coordinator

负责集群的元数据管理角色。其中元数据管理包含表级、集群级、用户级、Metric优化级。

- Store 

负责数据的存储角色，提供行存、列存的存储能力；同时基于StoreService接口提供基本的计算能力。

- Executor

负责接收SQL并进行SQL的解析、优化和执行。基于grpc协议对接Coordinator和Store层。

- ThinClient

SQL输入的瘦客户端。

# 2.Logical Component Layer about DingoDB

<img width="795" alt="image" src="https://user-images.githubusercontent.com/6895821/217450702-6016d5f7-3662-42c4-92aa-1c4741b05c79.png">


DingoDB的逻辑分层主要为了两层：Computer Layer 和  Storage Layer。其中Computer Layer是无状态的可以基于计算需求横向扩展；Storage Layer主要借助Raft实现多副本，提供行存储和列存储的能力。其中行存储主要借助RocksDB提供快速点查、修改的能力；列存储主要基于Merge Tree提供交互式分析的能力。


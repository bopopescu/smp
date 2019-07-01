# 服务发现

## 基于容器的服务发现如何做

服务发现的本质是名字到IP:PORT列表的映射，只不过这个映射关系是动态变化的，因为如果是静态的映射关系没必要大费周折去实现，代码写死即可。

如果基于容器来实现服务发现其实要解决的也就是动态的映射列表的变化。

### 实现方案

1. 所有服务部署前在容器配置上打上服务发现标准标签，表明服务分组，服务类型，服务依赖，服务监听端口等
2. 周期性扫描所有容器获取每个容器对应标签的配置信息
3. 对服务进行健康性探测，如果符合注册条件就调用注册中心的API进行注册
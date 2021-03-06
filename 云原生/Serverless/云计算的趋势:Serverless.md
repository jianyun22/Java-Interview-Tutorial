serverless字面意思，无服务的架构，当没有request访问或触发时，他不启动任何服务和资源，一旦触发了就会启动服务去处理任务。好处是不用关心服务是否挂了，它适合处理耗时不长的快速事务处理，当流量大的时候，它也能自动扩容去响应客户端。但是如果大量的并发一下冲过来的时候或者一下子没有流量的时候，它的自动扩容和缩容机制是否会导致更多的开销。

那Serverless解决了什么问题呢？

## 省钱、省力
算过部署服务器的开销吗？比如自己部署一套博客，常见的 Node.js MVC 架构，需购买云服务商的Linux 虚拟机、RDS 关系型数据库，做得好的话还要购买 Redis 缓存、负载均衡、CDN等。再专业一点，可能还会考虑容灾和备份，这么算下来一年最小开销都在 1w。

但你用 Serverless，成本可降到 1k 以下。Serverless 是对运维体系的极端抽象，就像 iPhone 当年颠覆诺基亚一样，它给应用开发和部署提供了一个极简模型。这种高度抽象的模型，可以让一个零运维经验的人，几分钟就部署一个 Web 应用上线，并对外提供服务。即根本不需要再学习怎么在 Linux 上装 Web 服务器，怎么配置负载均衡等等这些繁琐的偏运维方向的工作。

Serverless 可有效降低企业中中长尾应用的运营成本。
> 中长尾应用：每天大部分时间都没有流量或者有很少流量的应用。

尤其是企业在落地微服务后，一些边缘微服务被调用的概率其实很低。这时往往又很难通过人工来控制中长尾应用，因为不少应用还是被强依赖，不可直接下线。Serverless 之前，这些中长尾应用至少要独占 1 台虚拟机。现在有了 Serverless 的极速冷启动特性，企业就可以节省这部分开销。

> 微服务流行以后，所有的服务以容器化的方式运行，每个虚拟机中可以同时跑多个服务，不应该还存在中长尾应用独占虚拟机的情况吧。
另外，要支持Serverless极速冷启动，需要提前设置好启动依赖的资源限制吗？例如CPU，内存等。
其实Serverless一大特点就是缩容到0，平时没有流量时是不占用任何资源，除了硬盘。所以即使Serverless底层的容器方案，也可能是docker。但是却更加节省资源。

## 提高研发效能
SFF（Serverless For Frontend）可以让前端同学自行负责数据接口的编排，微服务 BaaS 化则让我们的后端同学更加关注领域设计。可以说，这是一个颠覆性的变化，它能够进一步放大前端工程师的价值。
外包可快速迭代，降低容错，沉淀领域解决方案。

Serverless 作为一门新兴技术，未来的想象空间很大。
- 创业公司用 FaaS 来做基础设施编排和云服务编排
- 外包公司利用 Serverless 应用架构的快速迭代能力，提升开发效率，降低出错率，还可以给自己沉淀领域的解决方案
- 风险投资方也在逐渐开始关注 Serverless 领域，毕竟这也是一个新的风口

## 解放生产力，激发创造力
前端可自由通过FaaS组合完成业务需求，大大激发前端创造力。

如果说 Node.js 语言的出现解放了一波前端工程师生产力，Node.js+Serverless 又可进一步激发前端工程师创造力。

微服务本身提出了很多理念。但微服务在服务端运维却缺少给力的支撑平台，后来我们就试着用容器集群搭建了自己的 Container Serverless。
结果证明它不但可以支撑 Node.js 微服务运维，还可以提高 Node.js 中长尾应用的资源利用率。。而放眼国内，目前还只有为数不多的大型互联网公司在重点跟进，其他人基本上只是在观望或者看热闹。

## 后端应用BaaS化


通过FaaS的后端解决方案将后端服务BaaS化，让后端工程师更加专注领域设计
serverless在实际应用上虽然说跟语言无关，但实际公司选择是node.js多，还是其他语言多？感觉更多是提到前端工程师的机会，后端作为Java开发者影响多大？
Node.js在Serverless Computing，也就是FaaS中因为JIT的特性，冷启动速度确实是优势。实践经验来说，Java或其它语言比较适合下沉，去做后端服务化，也就是BaaS。目前比较好的是FaaS+BaaS架构。

目前Serverless并不是万金油，它有它的局限性和使用场景。我们学习Serverless，应该将它作为一种工具，在适合的场景中使用。

# FAQ
- 一个完整的app后端，包括用户系统：用户信息，关注，内容系统：帖子，评论，点赞等，还有通知私信等。这样的场景适合用serverless来实现嘛，还是用传统后端开发来做
如果是新业务，可以体验Serverless技术栈。像用户信息，通知私信，这些都有很多现成的云服务提供，用FaaS很容易搭建：云服务编排。但如果是已有业务上云，那么建议还是逐步迁移吧。

- severless对运维工程师有什么机遇和挑战吗？
对运维工程师，多掌握一种事件响应的解决方案。而且FC是目前云服务里面性价比最高的服务，结合运维工程师现有的各种工具，也可以组合变化出各种高级工具。利用Serverless的思想，去设计运维架构，还可以减轻自己运维的压力。

- 感觉更适合前端工程师，后端适合吗
后端同学我觉得也适合，Serverless你可以随时随地调用一个云端函数。对前端同学来说，降低了服务端运维的门槛；对后端同学来说，则是掌握一种新的云计算服务。

- serverless 冷启动问题有没有什么好的解决方案？nodejs虽然说启动快，但是启动时间+接口耗时给人的感觉就是这个服务性能不行
云服务商都会提供给你，预热和保留容器的方案，不过会产生额外费用。

- Serverless 209 年一下子在国内火了起来，特别是鹅厂大力推 Serverless。不过 Serverless 还有很多局限性， 现在主要是用在通知系统、市场活动这类场景，整个生态还不够成熟。
Serverless混合其他云服务的架构方案。例如CaaS。

- 这serverless 咋感觉像是后端用nodejs来写，前端全栈一样，类似之前的前后端不分离，java、python换成了nodejs？
Serverless架构中，后端同学应该去写BaaS微服务。前端同学可以自己写FaaS自由编排这些BaaS微服务。

- serverless给后端带来什么好处呢？
最直接的就是后端免运维，节省人员开销和服务器开销。让后端开发和运维的门槛降低。


参考
- [阿里跨境供应链前端架构演进与 Serverless 实践](https://static001.geekbang.org/con/55/pdf/1710853715/file/%E7%BC%AA%E4%BC%A0%E6%9D%B0.pdf)
- [Serverless 前端工程化落地与实践](https://static001.geekbang.org/con/55/pdf/3151321591/file/%E7%8E%8B%E4%BF%8A%E6%9D%B0%20%20Serverless%20%E5%89%8D%E7%AB%AF%E5%B7%A5%E7%A8%8B%E5%8C%96%E8%90%BD%E5%9C%B0%E4%B8%8E%E5%AE%9E%E8%B7%B5.pdf)
- [从前端和云厂商的视角看 Serverless 与未来的开发生态](https://static001.geekbang.org/con/55/pdf/1359804153/file/%E6%9D%9C%E6%AC%A2%20%20%E4%BB%8E%E5%89%8D%E7%AB%AF%E5%92%8C%E4%BA%91%E5%8E%82%E5%95%86%E7%9A%84%E8%A7%86%E8%A7%92%E7%9C%8B%20Serverless%20%E4%B8%8E%E6%9C%AA%E6%9D%A5%E7%9A%84%E5%BC%80%E5%8F%91%E7%94%9F%E6%80%81.pdf)
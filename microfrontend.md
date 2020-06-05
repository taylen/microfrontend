## 微前端介绍和入门

### 一、什么是微前端

> Techniques, strategies and recipes for building a modern web app with multiple teams that can ship features independently.

由多个可以独立发布功能的团队构建现代Web应用程序的技术，策略和方法。

通俗解释：微前端架构是一种类似于微服务的架构，它将微服务的理念应用于浏览器端，即将 Web 应用由单一的单体应用转变为多个小型前端应用聚合为一的应用。

> 前端 + 微服务 = 微前端

#### 后端微服务化的优势
- 复杂度可控: 体积小、复杂度低，每个微服务可由一个小规模开发团队完全掌控，易于保持高可维护性和开发效率。
- 独立部署: 由于微服务具备独立的运行进程，所以每个微服务也可以独立部署。
- 技术选型灵活: 微服务架构下，技术选型是去中心化的。每个团队可以根据自身服务的需求和行业发展的现状，自由选择最适合的技术栈。
- 容错: 当某一组建发生故障时，在单一进程的传统架构下，故障很有可能在进程内扩散，形成应用全局性的不可用。
- 扩展: 单块架构应用也可以实现横向扩展，就是将整个应用完整的复制到不同的节点。

#### 前端微服务化的演变

- Monolithic Frontends
<img src="https://micro-frontends.org/ressources/diagrams/organisational/monolith-frontback-microservices.png">

- Organisation in Verticals
<img src="https://micro-frontends.org/ressources/diagrams/organisational/verticals-headline.png">

看到这个图，联想到什么？


### 二、微前端的应用场景是什么？

微前端架构旨在解决单体应用在一个相对长的时间跨度下，由于参与的人员、团队的增多、变迁，从一个普通应用演变成一个巨石应用(Frontend Monolith)后，随之而来的应用不可维护的问题。这类问题在企业级 Web 应用中尤其常见。

#### 我们何时需要前端微服务化?
- 项目技术栈老旧,相关技能的开发人员少,功能扩展吃力,重构成本高,维护成本高
- 项目过于庞大,代码编译慢,开发体差,需要一种更高维度的解耦方案
- 单一技术栈无法满足你的业务需求

#### 微前端架构核心价值
- 复杂度可控: 每一个UI业务模块由独立的前端团队开发,避免代码巨无霸,保持开发时的高速编译,保持较低的复杂度,便于维护与开发效率
- 技术选型灵活：主框架不限制接入应用的技术栈，子应用具备完全自主权
- 独立部署：子应用仓库独立，前后端可独立开发，部署完成后主框架自动完成同步更新
- 独立运行：每个子应用之间状态隔离，运行时状态不共享。单个模块发生错误,不影响全局 
- 扩展性强: 每一个服务可以独立横向扩展以满足业务伸缩性，与资源的不必要消耗

#### 微前端架构的几种实现方案
- 使用 HTTP 服务器的路由来重定向多个应用
- （主要）在不同的框架之上设计通讯、加载机制，诸如 Mooa 和 Single-SPA
- 通过组合多个独立应用、组件来构建一个单体应用
- 使用 iFrame 及自定义消息传递机制
- 使用纯 Web Components 构建应用
- 结合 Web Components 构建
  
#### 我们面临的问题与挑战
- 我们如何实现在一个页面里渲染多种技术栈?
- 不同技术栈的独立模块之间如何通讯?
- 如何通过路由渲染到正确的模块?
- 在不同技术栈之间的路由该如何正确触发?
- 项目代码别切割之后,通过何种方式合并到一起?
- 我们的每一个模块项目如何打包?
- 前端微服务化后我们该如何编写我们的代码?
- 独立团队之间该如何协作?

Mooa 是一个为 Angular 服务的微前端框架，它是一个基于 single-spa，针对 IE 10 及 IFRAME 优化的微前端解决方案。

Single-spa 一个基于JavaScript的 微前端 框架，他可以用于构建可共存的微前端应用，每个前端应用都可以用自己的框架编写，完美支持 Vue React Angular。可以实现 服务注册 事件监听 子父组件通信 等功能。 - 用于 父项目 集成子项目使用

Single-spa-vue 是提供给使用vue子项目使用的npm包。他可以快速和sigle-spa父项目集成，并提供了一些比较便携的api。 - 用于 子项目 使用

### 三、微前端的技术原理

从技术实现角度，微前端架构解决方案大概分为两类场景：
- 单实例：即同一时刻，只有一个子应用被展示，子应用具备一个完整的应用生命周期。通常基于 url 的变化来做子应用的切换。
- 多实例：同一时刻可展示多个子应用。通常使用 Web Components 方案来做子应用封装，子应用更像是一个业务组件而不是应用。

MPA 方案
- 优点在于 部署简单、各应用之间硬隔离，天生具备技术栈无关、独立开发、独立部署的特性。
- 缺点则也很明显，应用之间切换会造成浏览器重刷，由于产品域名之间相互跳转，流程体验上会存在断点。

SPA 方案
- 天生具备体验上的优势，应用直接无刷新切换，能极大的保证多产品之间流程操作串联时的流程性。
- 缺点则在于各应用技术栈之间是强耦合的。

那我们有没有可能将 MPA 和 SPA 两者的优势结合起来，构建出一个相对完善的微前端架构方案呢？

<img src="https://ucc.alicdn.com/pic/developer-ecology/0c84fbd3fd7840a590a3a6228efb6f96.png" />

Shared Stitching layer 作为主框架的核心成员，充当调度者的角色，由它来决定在不同的条件下激活不同的子应用。因此主框架的定位则仅仅是：导航路由 + 资源加载框架。




四、微前端有哪些问题？



五、微前端能给证券前端带来什么价值？


六、single-spa 和 vue-cli 的结合


参考资料：
- https://micro-frontends.org/
- https://single-spa.js.org/
- https://zhuanlan.zhihu.com/p/78362028
- https://developer.aliyun.com/article/742576
- https://github.com/phodal/mooa
- https://alili.tech/archive/ea599f7c/
- http://47.105.149.100/web/single-spa-vue-cli-wei-qian-duan-luo-di-zhi-nan-xiang-mu-ge-li-yuan-cheng-jia-zai-zi-dong-yin-ru-
- https://zh-hans.single-spa.js.org/docs/getting-started-overview
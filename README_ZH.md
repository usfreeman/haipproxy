# HAipproxy
[README](README.md) | [中文文档](README_ZH.md)

本项目所采集的IP资源都来自互联网，愿景是为大型爬虫项目提供一个**高可用低延迟的高匿IP代理池**。

# Features
- 快速抓取代理IP
- IP抓取和提取精准
- IP来源丰富
- 优良的IP校验器，并且容易根据自身需要扩展
- 支持分布式部署
- 架构设计灵活
- MIT授权协议

# Quick start

## Standalone
 - 安装Python3和Redis。有问题可以阅读[这篇文章](https://github.com/SpiderClub/weibospider/wiki/%E5%88%86%E5%B8%83%E5%BC%8F%E7%88%AC%E8%99%AB%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE)的相关部分。
 - 根据Redis的实际配置修改项目配置文件[config/settings.py](config/settings.py)中的`REDIS_HOST`、`REDIS_PASSWORD`等参数。
 - 安装[scrapy-splash](https://github.com/scrapy-plugins/scrapy-splash)，并修改配置文件[config/settings.py](config/settings.py)中的`SPLASH_URL`
 - 安装项目相关依赖
   > pip install -r requirements.txt
 - 启动*scrapy worker*，包括代理IP采集器和校验器
   > python crawler_booter.py --usage crawler

   > python crawler_booter.py --usage validator
 - 启动*调度器*，包括代理IP定时调度和校验
   > python scheduler_booter.py --usage crawler

   > python scheduler_booter.py --usage validator

   
## Dockerize
- 安装Docker

- 安装*docker-compose*
  > pip install -U docker-compose

- 修改[settings.py](config/settings.py)中的`SPLASH_URL`和`REDIS_HOST`参数

- 使用*docker-compose*启动各个应用组件
  > docker-compose up


# 注意事项
- 本项目高度依赖Redis，除了消息通信和数据存储之外，IP校验使用了Redis中的多种数据结构。如果需要替换Redis，请自己
进行度量
- 由于*GFW*的原因，某些网站需要通过科学上网才能进行访问和采集，如果用户无法访问墙外的网站，请将[rules.py](config/rules.py)
`task_queue`为` SPIDER_GFW_TASK`和`SPIDER_AJAX_GFW_TASK`的任务`enable`属性设置为0或者启动爬虫的时候指定爬虫类型为`common`和
`ajax`
  > python crawler_booter.py --usage crawler common ajax
- 相同代理IP，对于不同网站的代理效果可能大不相同。如果通用代理无法满足您的需求，您可以为特定网站编写代理IP校验器

# 如何贡献
- 欢迎给项目提新feature
- 如果发现项目某些环节有问题，欢迎提issue或者PR
- 代理IP校验和筛选的策略仍有优化的空间，欢迎大家以issue或者PR交流探讨
- 如果你发现了比较好的代理网站，欢迎分享或者直接以PR的方式分享


# 工作流程
![](static/workflow.png)


# 同类项目参考
本项目参考了Github上开源的各个爬虫代理的实现，感谢他们的付出，下面是笔者参考的所有项目，排名不分先后。

[dungproxy](https://github.com/virjar/dungproxy)

[proxyspider](https://github.com/zhangchenchen/proxyspider)

[ProxyPool](https://github.com/henson/ProxyPool)

[proxy_pool](https://github.com/jhao104/proxy_pool)

[ProxyPool](https://github.com/WiseDoge/ProxyPool)

[IPProxyTool](https://github.com/awolfly9/IPProxyTool)

[IPProxyPool](https://github.com/qiyeboy/IPProxyPool)

[proxy_list](https://github.com/gavin66/proxy_list)

[proxy_pool](https://github.com/lujqme/proxy_pool)


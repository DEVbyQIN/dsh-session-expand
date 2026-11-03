# Changelog

## 0.1.0 — 2026-11-03

首个版本：把三个会话插件打成一个 bundle。

- 组合 `dsh-session-tabs@0.1.6` + `dsh-quote-to-chat@0.2.0` + `dsh-session-md@0.1.0`，安装一次全部就位。
- 每个组件在「插件」页的组合包详情里各有一个启用/停用开关，外带组件自己的配置页入口。
- bundle 层不含插件代码，只插入三行 Loader entry；组件包保留单独安装能力。

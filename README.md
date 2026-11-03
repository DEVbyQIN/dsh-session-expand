# 会话增强包 / dsh-session-expand

一次安装，三个会话相关插件全都有；每个组件在插件页里都有**自己的开关**，想关哪个关哪个，不用卸载。

[English](README_EN.md) · MIT · 由 [dsh-session-tabs](https://github.com/DEVbyQIN/dsh-session-tabs)、[dsh-quote-to-chat](https://github.com/DEVbyQIN/dsh-quote-to-chat)、[dsh-session-md](https://github.com/DEVbyQIN/dsh-session-md) 组合而成。

## 包含的组件

| 组件 | 作用 | 版本 |
|---|---|---|
| `dsh-session-tabs` | 会话标签页：像浏览器一样在多个会话间切换，复用原生聊天视图、侧栏与工作台 | 0.1.6 |
| `dsh-quote-to-chat` | 选中回复里的任意文字 → 浮动工具条：引用到输入框、就这段开侧边线程、或直接复制 | 0.2.0 |
| `dsh-session-md` | 把一次会话导出成人读的 Markdown 或自包含 HTML（按 Turn 分组，含工具调用与思维链） | 0.1.0 |

三个组件都零运行时依赖，组合包本身也不含任何插件代码——它只是一层 bundle（DSH 的“多插件打包”机制）。

## 安装

装一次组合包，三个组件一起就位。

**桌面版（图形界面）**：左侧「插件」→「添加插件」，填包名 `dsh-session-expand`，装完点「立即启用」。

**命令行（任选一种）**：

```sh
# 桌面版自带的 CLI（profile 固定为 desktop）
"/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh" \
  plugin --profile desktop add dsh-session-expand@0.1.0

# 或任意 dsh CLI，profile 换成你自己的
dsh plugin --profile web add dsh-session-expand@0.1.0

# 从 GitHub 安装（不经过 npm）
dsh plugin --profile web add github:DEVbyQIN/dsh-session-expand#v0.1.0
```

装完在「插件」页能看到一张 **会话增强包** 卡片。

## 单独开关每个组件

「插件」页 → 点开 **会话增强包** 卡片 →「包含的组件」列表：

- 每一行右侧都有 **启用 / 停用** 开关。关掉某个组件，它的宿主半和浏览器半会立刻卸载（profile 里 HMR 生效时无需重启），其他组件不受影响；
- 组件自己带配置页的，行上还会有 **配置** 按钮，点进去就是该组件原来的设置页；
- 开关状态保存在 profile 的 `cordis.patch.yml` 里，对当前 profile 生效，重装/升级组合包不会丢。

> 注意：在「设置 → 内置插件」里的插件列表是只读清单，真正的组件开关在侧边栏「插件」页的组合包详情里。

## 不要和单独安装的组件同时用

组合包和单装插件会挂载**同一个包的两个实例**，DSH 的客户端模块系统会拒绝同名的活跃模块（还可能重复出 UI）。所以：

- 已经单独装了 `dsh-session-tabs` / `dsh-quote-to-chat` / `dsh-session-md` 的，**先卸载它们**，再装组合包；
- 反过来也一样：装了组合包就不用再单独装这三个。

想混搭、只留其中一两个，就在组合包里把不要的组件关掉即可。

## 升级与卸载

- 升级组合包 = 同时升级这三个组件的固定版本（版本表见上）。组件单独发新版后，组合包会跟着发新版本，`CHANGELOG.md` 里记录对应关系。
- 卸载组合包会移除三个组件；只想临时关掉某个组件用行开关，不要卸载。

## 兼容性

- DSH `0.2.x`（含桌面版 `0.2.1-rc.4`）；Node `^22.19.0 || >=24`。
- 组合包只是 bundle 层，不注册自己的 Loader entry，也不注入任何服务。

## 开发与自测

本仓库只有 bundle 清单（`package.json` + `cordis.patch.yml` + locale + 文档），没有代码：

```sh
node --test test/verify.mjs   # 校验组件版本钉死、patch 行、locale、发布文件清单
npm pack --dry-run            # 看会发布哪些文件
```

## License

MIT

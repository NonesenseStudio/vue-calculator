# 指南

## 简介

*vue=calculator*是基于JavaScript标准并使用[Vue框架](https://vuejs.org/guide/introduction.html#what-is-vue)开发的开源**单页应用程序**(SPA)，它可以完成基本的数学运算(+-×÷)。

## ⚠️注意

1. 此项目正处于并将长期处于萌芽阶段，并可能因作者懒得更新而随时荒废。
2. 高精度运算请使用专业计算器，此项目虽然修复了浮点数在JavaScript语言下出现0.1 + 0.2 != 0.3的**特殊情况**(详情可参阅[*Floating Point Math*](https://0.30000000000000004.com/))，但在进行更多位数的运算时仍可能会出现偏差。

## 开始

### 推荐开发环境

- IDE: [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).
- 包管理器: [pnpm](https://pnpm.io/zh/)

### 引入项目

```bash
# 克隆项目
git clone https://github.com/NonesenseStudio/vue-calculator.git
# 安装依赖
pnpm install
# 启动服务
pnpm dev
```

***

## 许可

[MIT许可证](./LICENSE)

Copyright (c) 2023 Made by [NonsenseStudio](https://github.com/NonesenseStudio)

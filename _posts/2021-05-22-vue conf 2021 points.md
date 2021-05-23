---
  layout: post
  title: vue conf 2021 points
  categories: [FE]
---

vue conf 2021里我关心的points

## Vue 3生态进展

- vue router稳定
- vuex稳定

## 开发体验改进

- 构建工具vite
- SFC语法
- IDE/TS支持

## vite

- 类似vue-cli的体验
- 基于原生ESM的热更新
- 基于esbuild的依赖预打包
- 兼容rollup的插件机制
- 内置SSR支持
- ...

## VitePress

- VuePress的所有优点
- Vite的速度
- 避免静态内容的double payload和hydration开销

## 编译阶段的优化

- script setup

```vue
<template>
	<h1>{{ msg }}</h1>
</template>

<script setup>
const msg = 'Hello World'
</script>
```

- style动态变量注入

```vue
<template>
	<h1>{{ msg }}</h1>
</template>

<script setup>
import { ref } from 'vue'
  
const msg = 'Hello World'
const color = ref('red')
</script>

<style>
  h1 {
    color: v-bind(color)
  }
</style>
```

## Vue Tools

- Vue 2/3
- Timeline面板
- 性能调试

## IDE支持计划

- Vetur -> Volar
- 官方的vue-tsc命令行类型检查
- 提供其他编辑器的LSP整合

## 2.7

- IE11支持

## 3.1和3.2

- Migration Build
- Suspense

## element 3

### headless

- Element core
- Element style (Web GL)

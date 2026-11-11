---
minutes: 1.5
preload: false
fit: false
---

# Agents can now build an entire 3D game—when backed by plans and feedback loops.

<LazyDemo
  src="./demos/saltline.html"
  openHref="./demos/saltline.html"
  previewImg="./demos/saltline-preview.svg"
  badge="FELIX RIESEBERG · CLAUDE FABLE 5.2 · 8-HOUR AUTONOMOUS RUN · 3.55 MB HTML"
  title="Saltline · Single-File Three.js FPS (Click Load to Play Locally)"
  summary="445M cached input tokens, procedural rain, drones, and physics in one static HTML file—yet comparing its raw one-shot vs. iterated build proves autonomous runs collapse without a plan and verification loops."
  height={560}
/>

<!--
大家先看今天刚火遍全网的这个例子：Anthropic 工程师 Felix Rieseberg 让模型连续自主跑了 8 个小时（消耗 4.45 亿缓存输入 token），直接生成了这个完整的单文件 3D 第一人称射击游戏 Saltline，我已经完整下载内嵌进课件了（采用了动态按需加载，不点 Load 不占显卡内存，翻页自动销毁）。为什么要放在第一页给大家看？因为我想告诉大家两件事：第一，现在的 AI 自我进化已经能做到这种程度，而且一个静态 HTML 部署成本是零；第二，Hacker News 上大家对比了它的“一枪裸跑版”和“多轮反馈修复版”——没有详细的 Plan 和严格的 Feedback Loop，跑得越久就越容易偏离目标（Goal Drifting）！
-->

::read::
Felix Rieseberg's *Saltline* (a 3.55 MB single-file Three.js game built over an 8-hour autonomous run) shows how far self-iterating agents can go—and why long runs require explicit plans and verification loops to avoid drifting.

---
title: Webassembly
date: 2024-10-28T21:41:39+08:00
lastmod: 2024-10-28T21:41:39+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# webassembly
Web Worker 结合 WebAssembly (Wasm) 是一种常见的技术组合，可以利用 WebAssembly 在 Web Worker 中执行高性能的计算密集型任务。下面是一个简单的示例，演示了如何在 Web Worker 中加载和执行 Wasm 模块：
首先，你需要编写一个用 C/C++ 或其他支持的语言编写的 Wasm 模块，比如下面这个简单的示例 example.wasm：
```wasm
(module
  (func $add (param i32 i32) (result i32)
    (i32.add (local.get 0) (local.get 1)))
  (export "add" (func $add))
)
```

接下来，你需要编写 JavaScript 代码，在主线程中创建一个 Web Worker，并在其中加载和执行这个 Wasm 模块：
```wasm
// 主线程中的代码

// 创建一个新的 Web Worker
const worker = new Worker('worker.js');

// 监听从 Worker 返回的消息
worker.onmessage = event => {
  console.log('Result:', event.data);
};

// 向 Worker 发送消息，请求执行加法运算
worker.postMessage({ type: 'add', data: [2, 3] });
```

然后，在 Web Worker 中，你需要编写代码来加载和执行 Wasm 模块，并处理主线程发送的消息：

```wasm
// worker.js 文件中的代码

// 监听主线程发送的消息
self.onmessage = event => {
  const { type, data } = event.data;

  // 加载 Wasm 模块
  fetch('example.wasm')
    .then(response => response.arrayBuffer())
    .then(buffer => WebAssembly.compile(buffer))
    .then(module => {
      // 实例化 Wasm 模块
      return WebAssembly.instantiate(module);
    })
    .then(instance => {
      // 执行 Wasm 模块中的函数，并将结果发送回主线程
      switch (type) {
        case 'add':
          const result = instance.exports.add(...data);
          self.postMessage(result);
          break;
        default:
          break;
      }
    })
    .catch(error => {
      console.error('Error:', error);
    });
};
```

这样，当主线程向 Web Worker 发送消息时，Web Worker 将加载 Wasm 模块并执行其中的函数，并将结果返回给主线程。这种方式可以在后台线程中利用 WebAssembly 执行高性能的计算任务，同时不会阻塞主线程，保持页面的响应性能。

Tags:
  wasm
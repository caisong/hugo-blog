---
title: Opetelemetry
date: 2024-06-18T21:41:16+08:00
lastmod: 2024-06-18T21:41:16+08:00
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
draft: true
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
# opetelemetry

```javascript
// auto.js
const { WebTracerProvider } = require('@opentelemetry/sdk-trace-web');
const { getWebAutoInstrumentations } = require('@opentelemetry/auto-instrumentations-web');
// const { CollectorTraceExporter } = require('@opentelemetry/exporter-collector');
// const { OTLPTraceExporter } = require('@opentelemetry/exporter-trace-otlp-http');
const { ConsoleSpanExporter } = require('@opentelemetry/sdk-trace-base')
const { SimpleSpanProcessor } = require('@opentelemetry/sdk-trace-base');
const { registerInstrumentations } = require('@opentelemetry/instrumentation');
const { ZoneContextManager } = require('@opentelemetry/context-zone');
const { B3Propagator } = require('@opentelemetry/propagator-b3');

const collectorOptions = {
    // url: '<opentelemetry-collector-url>', // url is optional and can be omitted - default is http://localhost:4318/v1/traces
    headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
            'Access-Control-Allow-Headers': 'Content-Type, Authorization'
    }, // an optional object containing custom headers to be sent with each request
    concurrencyLimit: 10, // an optional limit on pending requests
  };
  
const exporter = new ConsoleSpanExporter();
// const exporter = new OTLPTraceExporter(collectorOptions);

const provider = new WebTracerProvider();
provider.addSpanProcessor(new SimpleSpanProcessor(exporter));
provider.register({
  contextManager: new ZoneContextManager(),
  propagator: new B3Propagator(),
});

registerInstrumentations({
  instrumentations: [
    getWebAutoInstrumentations({
      // load custom configuration for xml-http-request instrumentation
      '@opentelemetry/instrumentation-xml-http-request': {
        clearTimingResources: true,
      },
    }),
  ],
});
```

* nodejs 转 web js  
```shell
npx browserify auto.js -o bundle-auto.js
```

* jaeger 接收端  
```shell
docker run --rm --name jaeger   -p 6831:6831/udp   -p 6832:6832/udp   -p 5778:5778   -p 16686:16686   -p 4317:4317   -p 4318:4318   -p 14250:14250   -p 14268:14268   -p 14269:14269 -d   jaegertracing/all-in-one
```

* 环境变量
```
export JAVA_TOOL_OPTIONS="-javaagent:/data/software/opentelemetry-javaagent.jar" OTEL_TRACES_EXPORTER=logging OTEL_METRICS_EXPORTER=logging OTEL_LOGS_EXPORTER=logging OTEL_METRIC_EXPORT_INTERVAL=150000 OTEL_PROPAGATORS=b3multi OTEL_TRACES_SAMPLER=always_off
```

**js使用`propagate b3`将`traceID`相关信息写在头文件中，java后端必须配置`OTEL_PROPAGATORS=b3multi OTEL_TRACES_SAMPLER=always_off`环境变量才能获取**

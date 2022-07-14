---
layout: default
title: Spring Error batch Unable to deserialize the execution context
parent: error
nav_order: 102201
---

BATCH_JOB_EXECUTION_CONTEXT, BATCH_STEP_EXECUTION_CONTEXT 두개 테이블의 내용이
```html
{"map":[{"entry":{"string":"seq","long":6}}]}
{"@class":"java.util.HashMap","seq":["java.lang.Long",1]}
```

위에서 아래의 내용으로 바뀜 역직렬화 보안 이슈로 인해 바뀌었기 때문에 이전 기록을 읽을때 역직렬화에 실패 한다.

spring-batch-core 4.2.2 아래로 사용하거나 테이블 로우를 전부 날려주면 된다.

## 참고링크
* https://tanzu.vmware.com/security/cve-2020-5411

```
TypeError [ERR_INVALID_ARG_TYPE]: The "fd" argument must be of type number. Received null
node:internal/validators:117 throw new ERR_INVALID_ARG_TYPE(name, 'number', value);
at process.processTicksAndRejections (node:internal/process/task_queues:77:11) { code: 'ERR_INVALID_ARG_TYPE'
...
at node_modules/warehouse/lib/database.js:14:12
...
```

出这个问题是因为版本冲突，需要降版本。

```
brew search node
brew install node@16
```
# 当导入本地模块时是否应该补全文件后缀

## CJS

cjs 依次会尝试 .js, .json, .node

## ESM

[文档](https://nodejs.org/api/esm.html#import-specifiers)明确指出 `The file extension is always necessary for these.`

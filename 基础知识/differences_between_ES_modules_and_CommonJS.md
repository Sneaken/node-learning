# Differences between ES modules and CommonJS

1. No require, exports, or module.exports

   In most cases, the ES module import can be used to load CommonJS modules.

   If needed, a require function can be constructed within an ES module using module.createRequire().

2. No `__filename` or `__dirname`

   These CommonJS variables are not available in ES modules.

   `__filename` and `__dirname` use cases can be replicated via import.meta.url.

   ```js
   // cjs
   const cjs_filename = __filename;
   const cjs_dirname = __dirname;
   
   // esm
   import { dirname } from "node:path";
   import { fileURLToPath } from "node:url";
   const esm_filename = fileURLToPath(import.meta.url);
   const esm_dirname = dirname(fileURLToPath(import.meta.url));
   ```

3. No Addon Loading

   Addons are not currently supported with ES module imports.

   They can instead be loaded with module.createRequire() or process.dlopen.

4. No require.resolve

   Relative resolution can be handled via new URL('./local', import.meta.url).

   For a complete require.resolve replacement, there is a flagged experimental import.meta.resolve API (--experimental-import-meta-resolve).

   Alternatively module.createRequire() can be used.

   ```js
   // cjs
   const cjs_react_path = require.resolve("react");

   // esm
   import { createRequire } from "node:module";
   const require = createRequire(import.meta.url);
   const esm_react_path = require.resolve("react");
   ```

5. No NODE_PATH

   NODE_PATH is not part of resolving import specifiers. Please use symlinks if this behavior is desired.

6. No require.extensions

   require.extensions is not used by import. The expectation is that loader hooks can provide this workflow in the future.

7. No require.cache

   require.cache is not used by import as the ES module loader has its own separate cache.

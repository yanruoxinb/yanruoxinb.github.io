
## `Commonjs` 和 `ES Module`的区别
Commonjs 的特性如下：
> （exports,module.exports,require）
- CommonJS 模块由 JS 运行时实现。
- CommonJs 是单个值导出，本质上导出的就是 exports 属性。
- CommonJS 是可以动态加载的，对每一个加载都存在缓存，可以有效的解决循环引用问题。
- CommonJS 模块同步加载并执行模块文件。
> `webpack` 不支持对 `CommonJS` 进行 `Tree-shaking`

> module.exports 被改变的时候，exports不会被改变，而模块导出的时候，真正导出的执行是module.exports，而不是exports

Es module 的特性如下：

- ES6 Module 静态的，不能放在块级作用域内，代码发生在编译时。
- ES6 Module 的值是动态绑定的，可以通过导出方法修改，可以直接访问修改结果。
- ES6 Module 可以导出多个属性和方法，可以单个导入导出，混合导入导出。
- ES6 模块提前加载并执行模块文件，
- ES6 Module 导入模块在严格模式下。
- ES6 Module 的特性可以很容易实现 Tree Shaking 和 Code Splitting。

## webpack 与 rollup 的区别
- webpack 不支持导出 es6 module 规范，rollup 支持导出 es6 module
- webpack 打包后代码很多冗余无法直接看，rollup 打包后的代码简洁，可读，像源码
- webpack 可以进行代码分割，静态资源处理，HRM，rollup 专注于 es module，tree-shaking更加强大的，精简

## `for in` 和 ` for of`的区别

- `for in`遍历的是数组的索引（即键名），而`for of`遍历的是数组元素值，只是数组内的元素，不包括数组的原型属性
- `for of`


